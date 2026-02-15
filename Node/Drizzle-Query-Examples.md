# Drizzle ORM Query Examples

> _Trainer Reference Guide - Comprehensive query examples for the Call Of Duty project_

---

This guide provides detailed Drizzle ORM query patterns with explanations, use cases, and best practices. This is a reference document for trainers and mentors.

[[_TOC_]]

---

## Prerequisites

Make sure you have the following imports in your file:

```typescript
import { eq, and, sql, arrayContains } from 'drizzle-orm';
import { db } from './db'; // your database connection
import { soldiers, duties, dutySoldiers } from './schema'; // your schema
```

---

## Basic Queries

### Select All Records

```typescript
// Get all soldiers
const allSoldiers = await db.select().from(soldiers);

// Get all duties
const allDuties = await db.select().from(duties);
```

### Filter with Where Clause

```typescript
// Find a soldier by ID
const soldier = await db
  .select()
  .from(soldiers)
  .where(eq(soldiers.id, '0112358'));

// Find duties with specific status
const scheduledDuties = await db
  .select()
  .from(duties)
  .where(eq(duties.status, 'scheduled'));
```

---

## Array Operations

### Array Contains (PostgreSQL Arrays)

```typescript
// Find soldiers by limitations (array contains)
const soldiersWithLimitations = await db
  .select()
  .from(soldiers)
  .where(arrayContains(soldiers.limitations, ['food', 'standing']));
```

**Use case**: Find all soldiers who have both 'food' and 'standing' limitations.

---

## Geospatial Queries (PostGIS)

### Find Nearby Locations

```typescript
// Find duties within 1000 meters of a point (PostGIS)
const nearbyDuties = await db
  .select()
  .from(duties)
  .where(
    sql`ST_DWithin(
      ${duties.location}::geography, 
      ST_SetSRID(ST_MakePoint(34.7818, 32.0853), 4326)::geography, 
      1000
    )`
  );
```

**Use case**: Find all duties within 1km radius of Tel Aviv coordinates (34.7818°E, 32.0853°N).

**Parameters**:
- `34.7818` - Longitude
- `32.0853` - Latitude
- `1000` - Distance in meters
- `4326` - SRID (coordinate system for WGS 84)

---

## Aggregations and Joins

### Justice Board - Complex Join with Aggregation

```typescript
// Justice Board aggregation
const justiceBoard = await db
  .select({
    soldierId: soldiers.id,
    name: soldiers.name,
    score: sql<number>`COALESCE(SUM(${duties.value}), 0)`.as('score'),
  })
  .from(soldiers)
  .leftJoin(dutySoldiers, eq(soldiers.id, dutySoldiers.soldierId))
  .leftJoin(duties, and(
    eq(dutySoldiers.dutyId, duties.id),
    eq(duties.status, 'scheduled')
  ))
  .groupBy(soldiers.id, soldiers.name)
  .orderBy(sql`score DESC`);
```

**Use case**: Calculate total duty points for each soldier, ordered by highest score.

**Key features**:
- `leftJoin` - Include all soldiers even if they have no duties
- `COALESCE(SUM(...), 0)` - Return 0 instead of NULL for soldiers with no duties
- `groupBy` - Aggregate by soldier
- Only count duties with status 'scheduled'

---

## Insert Operations

### Insert into Junction Table

```typescript
// Insert with relations (scheduling a duty)
await db.insert(dutySoldiers).values({
  dutyId: 123,
  soldierId: '0112358',
});
```

**Use case**: Assign a soldier to a duty (many-to-many relationship).

### Insert with Auto-generated Fields

```typescript
// Insert a new soldier
const [newSoldier] = await db.insert(soldiers).values({
  id: '0112358',
  name: 'John Doe',
  rankValue: 3,
  rankName: 'lieutenant',
  limitations: ['food'],
}).returning();
```

**Use case**: Create a new soldier and get the inserted record back.

---

## Update Operations

### Simple Update

```typescript
// Update duty status
await db.update(duties)
  .set({ status: 'scheduled' })
  .where(eq(duties.id, 123));
```

### Update with JSONB Manipulation

```typescript
// Update status history (JSONB append)
await db.update(duties)
  .set({
    status: 'scheduled',
    statusHistory: sql`${duties.statusHistory} || ${JSON.stringify([{ status: 'scheduled', date: new Date() }])}::jsonb`,
  })
  .where(eq(duties.id, 123));
```

**Use case**: Update duty status and append to status history array in one operation.

**Key features**:
- `||` operator - JSONB concatenation (append to array)
- `::jsonb` - Cast JSON string to JSONB type
- Atomic operation - no race conditions

---

## Delete Operations

```typescript
// Delete a soldier
await db.delete(soldiers)
  .where(eq(soldiers.id, '0112358'));

// Delete a duty
await db.delete(duties)
  .where(eq(duties.id, 123));
```

**Note**: The `onDelete: 'cascade'` option in the schema will automatically remove related records in `dutySoldiers` junction table.

---

## Advanced Patterns

### Multiple Conditions with AND

```typescript
// Find duties within time range and specific status
const activeDuties = await db
  .select()
  .from(duties)
  .where(and(
    eq(duties.status, 'scheduled'),
    sql`${duties.startTime} <= NOW()`,
    sql`${duties.endTime} >= NOW()`
  ));
```

### Subqueries

```typescript
// Find soldiers who have no scheduled duties
const availableSoldiers = await db
  .select()
  .from(soldiers)
  .where(
    sql`NOT EXISTS (
      SELECT 1 FROM ${dutySoldiers}
      JOIN ${duties} ON ${dutySoldiers.dutyId} = ${duties.id}
      WHERE ${dutySoldiers.soldierId} = ${soldiers.id}
      AND ${duties.status} = 'scheduled'
      AND ${duties.startTime} <= NOW()
      AND ${duties.endTime} >= NOW()
    )`
  );
```

**Use case**: Find soldiers who are not currently on duty.

---

## Transaction Example

```typescript
// Schedule a duty with transaction
await db.transaction(async (tx) => {
  // Update duty status
  await tx.update(duties)
    .set({
      status: 'scheduled',
      statusHistory: sql`${duties.statusHistory} || ${JSON.stringify([{ status: 'scheduled', date: new Date() }])}::jsonb`,
    })
    .where(eq(duties.id, dutyId));

  // Assign soldiers
  await tx.insert(dutySoldiers).values(
    soldierIds.map(soldierId => ({ dutyId, soldierId }))
  );
});
```

**Use case**: Ensure both duty update and soldier assignment succeed or fail together.

---

## Performance Tips

1. **Use indexes** - Already defined in the schema for common queries
2. **Select only needed columns** - Use `.select({ id: soldiers.id, name: soldiers.name })`
3. **Batch inserts** - Pass array to `.values()` for multiple records
4. **Use transactions** - For operations that must succeed/fail together
5. **Prepare statements** - Drizzle automatically prepares parameterized queries

---

## Common Patterns

### Search by Name (Case-Insensitive)

```typescript
const searchResults = await db
  .select()
  .from(soldiers)
  .where(sql`LOWER(${soldiers.name}) LIKE LOWER(${'%' + searchQuery + '%'})`);
```

### Pagination

```typescript
const page = 1;
const pageSize = 10;

const results = await db
  .select()
  .from(soldiers)
  .limit(pageSize)
  .offset((page - 1) * pageSize);
```

### Count Records

```typescript
const [{ count }] = await db
  .select({ count: sql<number>`COUNT(*)` })
  .from(soldiers);
```

---

## Related Resources

- [Drizzle ORM Documentation](https://orm.drizzle.team/)
- [Drizzle PostgreSQL Column Types](https://orm.drizzle.team/docs/column-types/pg)
- [PostGIS Documentation](https://postgis.net/docs/)
- [PostgreSQL Array Functions](https://www.postgresql.org/docs/current/functions-array.html)
- [PostgreSQL JSON Functions](https://www.postgresql.org/docs/current/functions-json.html)
