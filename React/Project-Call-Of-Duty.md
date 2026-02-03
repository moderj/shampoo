# Call Of Duty - Frontend Interface

> _Estimation time: 10-14 Days_

---

In the Node.js path, you built the backend for the "Call of Duty" system. Now, you will build the Frontend interface for it. This is a "Full Stack" moment!

You will build a Single Page Application (SPA) using React that interacts with your existing API.

![Call of Duty Frontend](<https://cdn.vox-cdn.com/thumbor/cnh3fYY5kgmjuF3O4uR9JKj3avY=/0x0:960x540/1220x813/filters:focal(404x194:556x346):format(webp)/cdn.vox-cdn.com/uploads/chorus_image/image/70538810/025d6f6199fb817e05158e20b9640808_CODVG_Reveal_Standard_Keyart_Textless_Bnet_Shop_Product_Browsing_Card_960x540.0.jpeg>)

**_Learning objectives:_**

At the end of this module, you'll be able to:

- Build a complex SPA with **React Router** and **Material UI**.
- Manage server state using **Fetch/React Query** and forms with **React Hook Form**.
- Handle large datasets efficiently using **Virtualization** and **TanStack Table**.
- Visualize geospatial data using **OpenLayers**.
- Manage global client state using **Jotai**.

---

_Send me back [home](home)_ or up to [React Overview](React/React)

[[_TOC_]]

---

## Instructions

### Pre-requirements

- Completed [React Foundations](React/Foundations)
- Completed [React Deep Dive](React/Deep-Dive)
- Your [Node/Call-Of-Duty](Node/Call-Of-Duty) API running locally (or a mock API).

### General Guidelines

- Use **Functional Components** and **Hooks** only.
- Use **TypeScript** (Strongly Recommended) or JavaScript.
- UX matters. Handle loading states and error states gracefully.
- Component composition is key. Avoid "God Components" (components with 500+ lines).

### Recommended Technologies

- **Build Tool**: [Vite](https://vitejs.dev/)
- **UI Framework**: [Material UI (MUI)](https://mui.com/)
- **Routing**: [React Router](https://reactrouter.com/)
- **Forms**: [React Hook Form](https://react-hook-form.com/)
- **Data Fetching**: [TanStack Query](https://tanstack.com/query/latest)
- **Tables**: [TanStack Table](https://tanstack.com/table/latest)
- **State Management**: [Jotai](https://jotai.org/)
- **Maps**: [OpenLayers](https://openlayers.org/)

## Data Models (Frontend)

Define these TypeScript interfaces to mirror your backend data:

**Soldier**

```typescript
interface Soldier {
  _id: string;
  name: string;
  rank: {
    name: string;
    value: number;
  };
  limitations: string[];
  createdAt: string;
  updatedAt: string;
}
```

**Duty**

```typescript
interface Duty {
  _id: string;
  name: string;
  description: string;
  location: {
    type: "Point";
    coordinates: [number, number]; // [longitude, latitude]
  };
  startTime: string;
  endTime: string;
  minRank?: number;
  maxRank?: number;
  constraints: string[];
  soldiersRequired: number;
  value: number;
  soldiers: string[]; // Array of Soldier IDs
  status: "unscheduled" | "scheduled" | "canceled";
}
```

## Task 1 - Setup & Architecture

> _Estimation time: 1 Day_

1. **Initialize the Project**:
   - Create a new React project using Vite + TypeScript.
   - Use the `create-vite` template: `npm create vite@latest call-of-duty-web -- --template react-ts`.
   - Install Material UI (MUI) and configure the basics (`CssBaseline`, `ThemeProvider`).

2. **Navigation Structure**:
   - Install React Router.
   - Create a `Navbar` component that is present on all pages.
   - Create the following routes:
     - `/` (Home/Dashboard)
     - `/soldiers` (Soldiers Card View)
     - `/duties` (Duties Card View)
     - `/admin` (Table View)

3. **Layout**:
   - Create a global `Layout` component (using `Outlet`) that wraps your application.
   - Ensure the app is responsive (looks good on mobile and desktop).

## Task 2 - The Card Views (Soldiers & Duties)

> _Estimation time: 3-4 Days_

In this task, you will create the main "Card Views" for viewing and managing entities.

### Soldiers Page (`/soldiers`)

1. **Fetch & Display**:
   - Fetch the list of soldiers from your API.
   - Display them in a CSS Grid / Flexbox layout using MUI `Card` components.
   - Each card should show: Name, Rank, ID, and Limitations.

2. **Search & Filter**:
   - Add a search bar to filter soldiers by **Name**.
   - (Optional) Implement server-side filtering via query params (e.g., `?name=david`).

3. **Create Soldier (Forms)**:
   - Create a "Add Soldier" button that opens a Dialog (Modal).
   - Inside the dialog, build a form using **React Hook Form**.
   - Fields: Name, Rank (Select), ID, Limitations.
   - Validation: Name is required (3-50 chars), ID must be valid.
   - On submit: Send a POST request to your API and update the UI.

4. **Delete**:
   - Add a "Delete" button to each card.
   - On click, show a confirmation dialog.
   - On confirm, delete the soldier via API and remove from the list.

### Duties Page (`/duties`)

1. **Replicate**:
   - Implement the same "Card View" logic for Duties.
   - Display: Name, Description, Location (lat/long text for now), Status badge.
   - Implement Add/Delete functionality similar to Soldiers.

## Task 3 - The Admin Dashboard (Table View)

> _Estimation time: 3-4 Days_

Sometimes cards are not enough. We need a dense, high-performance view for managing large datasets.

1. **TanStack Table**:
   - Install `@tanstack/react-table`.
   - Create a reusable `DataTable` component.

2. **Features**:
   - **Sorting**: Allow clicking on column headers to sort (ASC/DESC).
   - **Pagination**: Display 10/20/50 rows per page. Connect this to your API's pagination if available, or do client-side pagination.
   - **Row Actions**: Add "Edit" and "Delete" buttons to each row.

3. **Virtualization**:
   - Assume we might have thousands of soldiers.
   - Implement **Row Virtualization** (using `@tanstack/react-virtual`) to render only the visible rows within the table body.

4. **Implementation**:
   - Use this table on the `/admin` route to show a unified list of Soldiers or Duties (use Tabs to switch between views).

## Task 4 - Tactical Map (Advanced)

> _Estimation time: 3 Days_

Duties have locations (Geometries). Let's visualize them.

1. **OpenLayers Integration**:
   - Install `ol` (OpenLayers).
   - Create a `Map` component that renders a map.

2. **Plot Duties**:
   - Fetch duties that have location data.
   - Add a "Vector Layer" to the map with markers (Features) for each duty.
   - Clicking a marker should show a popup (Overlay) with the Duty's name and description.

3. **Interaction**:
   - Add a button to the Duty Card: "Show on Map".
   - Clicking it should navigate to the Map page (or open a map modal) and animate ("fly to") the view to that specific duty's coordinates.

## Task 5 - State Management Refactor

> _Estimation time: 2 Days_

By now, you might have used `useContext` or "Prop Drilling" to manage global state (like the current list of soldiers, or UI themes).

**The Challenge:**

1. Identify global state in your app (e.g., Theme Mode, specific cached lists if not using Query).
2. **Refactor**: Replace React Context for these items with **Jotai**.
3. Create atoms for your state (e.g., `themeAtom`).
4. Ensure your app still works exactly the same, but with cleaner state logic.

## Task 6 - Make it Professional (Optional)

> _Estimation time: 2 Days_

1. **Error Boundaries**:
   - Wrap your main routes in an Error Boundary to catch crashes gracefully and show a "Something went wrong" UI.

2. **Loading Skeletons**:
   - Instead of a spinning loader, use MUI `Skeleton` components to show a placeholder UI (shaped like cards or table rows) while data is fetching.

3. **Toast Notifications**:
   - Add a "Toast" (Snackbar) notification system (e.g., `notistack` or custom MUI Snackbar).
   - Show a success message when a Soldier/Duty is created or deleted.
   - Show an error message if an API call fails.

4. **404 Page**:
   - Create a custom "Not Found" page for unknown routes.

## Next Steps

You have built a full-stack application! This is a massive achievement.

- Check out [React Testing](React/Testing-Javascript) to learn how to test your components.
- Explore [Production Build](https://vitejs.dev/guide/build.html) optimization.
