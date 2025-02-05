---
title: Frontend React
---

## React and Material UI
 React Github repos - https://github.com/enaqx/awesomereact?tab=readme-ov-file

React Docs old - https://legacy.reactjs.org/docs/getting-started.html
React Docs new - https://react.dev/reference/react

Go over the following react concepts:
1. Components
2. Hooks – and useState and useEffect specific
3. refs and useRef hook
4. Context
5. Fragments
6. Refs and Frorward refs
7. Error Boundaries
8. JSX
9. High Order Components
10. JSX
11. Memorization – useMemo and useCallback
12. Custom Hooks
13. React query

Important video, watch till 3:30: https://www.youtube.com/watch?v=CFRhGnuXG-4

Important article about useEffect in react! https://overreacted.io/acomplete-guide-to-useeffect/

Important article about rendering in react!!
https://www.developerway.com/posts/react-re-renders-guide#part7


## Global State Management
Read about jotai library for handling global state management inside your
application. 

Read https://jotai.org/docs Check out the core and Utilities
section.

## Call Of Duty Frontend Project

Write a Soldiers list application with Next js and MUI 6 which
corresponds to the backend schemas and implementation of
Soldiers.
(Note this is a Frontend exercise, there is no connection to a
server/db for now)

Minimum Requirements:
- One main page of the soldiers list.
- Input form to add new soldiers with an add button
- Add edit icon and form to update the Soldiers properties
- Delete Soldiers from the soldiers list
- Add option to filter and search Soldiers in the list.

## 1. Main Soldiers List Page
**Header:** Displays the title "Soldiers List".

**Toolbar:**
- Search Box: Allows searching by soldier name or other properties.
- Filter Dropdown: Options to filter soldiers based on rank, age, or

other attributes. (filter by select)
- Soldiers List Display:
- Each soldier entry in the list is displayed as a card or row with the following details:

1. Name
2. id
3. Rank
4. Limitations

**Actions**:
- Edit Icon: Opens an edit form to update the soldier's
properties.
- Delete Icon: Removes the soldier from the list.


## 2. Input Form to Add New Soldiers
- Located either at the top of the list or accessible via an Add Button.
- Implement the form using formik
- Fields:
1. Name (Text input)
2. Rank name and value (Dropdown with predefined options like Private, Sergeant, Captain, etc.)
3. Limitations aka ptorim
4. Add Button: Validates and adds a new soldier to the list.

## 3. Edit Soldier Properties
- Accessed by clicking the Edit Icon for a soldier.
- Modal or Inline Form: Pre-filled with the current properties of the
selected soldier.

1. Name
2. Rank – name and value
3. Limitations

- Save Button: Updates the soldier's information in the list.

## 4. Delete Soldiers
- Clicking the Delete Icon shows a confirmation dialog:
- "Are you sure you want to delete this soldier?"  Options: Yes / Cancel


## 5. Search and Filter Functionality
- Search Box: Filters the list dynamically as the user types.
- Filter Dropdown: Filters based on categories like rank or age range

## 6. Connect Frontend To The Backend
- Next js API: use Next js api request to get the soldiers data from the
server
- Create the proper custom hooks: use react query for the fetching
Soldiers data from the server (useSoldiers)

## Bonus Sections
## **Navigation Bar**
- Implement a navigation bar using Next js Routing to switch between the
following tabs:
- Home (Soldiers List): Displays the main soldiers list and OpenLayers
map.
- Admin: Contains the admin-specific table for soldiers.

**Admin Tab:** Use material-react-table for a fully interactive table:
Features:
1. Table Setup:
 - Columns: Name, Rank, Age, Location, Edit, Delete.
 - Sortable Columns: Name, Rank, Age.
 - Searchable/Filterable: Add a global search box above the table for filtering by any column.

2. Add Soldier Option:
- A button above the table opens a form modal for adding a new soldier.
- Same input fields as in the main tab (Name, Rank, Age, Location).

3. Edit and Delete Cells:
Edit Cell:
- Contains an Edit Icon that triggers a modal to update the
soldier's details.
- Delete Cell: Contains a Delete Icon with a confirmation prompt before
removal.

## Map Feature
**Soldiers Base layer:**

Integrate OpenLayers to display Soldiers by their base locations:
We will add a new optional "Base” property which is coordinate location of long, lat to the soldier
schema.

- Display a map centered on a default location.
- Add base as optional property to the soldier entity that is a coordinate of long, lat (inside the forms).
- Add the Soldiers base layer to the map 

