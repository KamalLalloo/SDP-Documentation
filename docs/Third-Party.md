# Third-Party Code Documentation

Our project makes use of several third-party libraries and frameworks to speed up development and provide reliable functionality. Below we document the main ones, how we used them, and why they were chosen.

---

## Frontend Core

### React (v19.1.0) & React-DOM (v19.1.0)

We used **React** as the main frontend framework for building our web app. It allowed us to create reusable components such as scoreboards, live match cards, and navigation elements.  
**React-DOM** is used for rendering our components in the browser.

We chose React because it is widely supported, integrates well with TypeScript, and makes it easier to handle dynamic updates like live football scores.

---

### React Router DOM (v7.7.1)

This library is used for routing between pages in the app. For example, it handles navigation between the live matches view and the match detail pages.

We chose it because it is the standard routing solution for React projects.

---

### Axios (v1.11.0)

**Axios** is our HTTP client for making requests to football APIs and our backend server.

We used it instead of the native `fetch` API because it has simpler syntax, better error handling, and built-in support for interceptors.

---

### @supabase/supabase-js (v2.53.0)

This SDK connects our frontend to **Supabase**, which we use for authentication and storing user data. For example, it manages login sessions and user preferences such as favorite teams.

We picked Supabase because it saves us time setting up a full backend from scratch.

---

### @react-oauth/google (v0.12.2)

This package provides **Google login functionality**. We use it to let users sign in easily using their Google accounts.

We chose it because it’s reliable and avoids the need to implement OAuth flows manually.

---

### Framer Motion (v12.23.12)

Used for adding **smooth animations** to the app, such as transitions when navigating between screens or when live match updates appear.

It improves the overall user experience with minimal extra effort.

---

### Lucide-React (v0.539.0) & React-Icons (v5.5.0)

These libraries provide access to ready-to-use **icons**.

We use them in the UI to display things like football icons, arrows, and navigation elements. They save time compared to designing custom icons.

---

### Dotenv (v17.2.1)

**Dotenv** is used to load environment variables into the app, such as API keys.

This prevents us from hardcoding sensitive information into the source code.

---

## Styling and Design

### Tailwind CSS (v3.4.17)

**Tailwind CSS** is used as the main styling framework for the frontend.  
It allows us to build responsive layouts quickly using utility classes, ensuring consistent design without writing large amounts of custom CSS.

We chose Tailwind because it integrates smoothly with React and Vite, and speeds up UI development.

---

### PostCSS (v8.5.6) & Autoprefixer (v10.4.21)

These tools process and optimize CSS at build time.  
**PostCSS** enables plugin-based transformations, while **Autoprefixer** automatically adds vendor prefixes for better browser compatibility.

---

### Fontsource (v5.x)

We use **@fontsource/inter** and **@fontsource-variable/bricolage-grotesque** to load and manage fonts locally.

This ensures consistent typography without relying on external CDNs.

---

## 3D and Visualization

### Three.js (v0.180.0)

**Three.js** provides 3D rendering capabilities in the browser.  
We use it for interactive visual elements, such as match graphics or animated components.

---

### @react-three/fiber (v9.3.0) & @react-three/drei (v10.7.6)

These libraries make it easier to use **Three.js** with React.  
**@react-three/fiber** provides a React renderer for Three.js, and **@react-three/drei** adds useful helpers and components (like cameras, lights, and controls).

They allow us to build complex 3D experiences declaratively within our React components.

---

## Utilities

### PapaParse (v5.5.3)

**PapaParse** is used to parse and export CSV data.  
It allows us to handle structured football data (like match statistics) efficiently in the frontend.

---

## Backend Core

### Express (v5.1.0)

**Express** is the main framework we used for the backend server. It handles routes and endpoints for our API, such as fetching football data or serving user profiles.

We chose Express because it’s lightweight, flexible, and widely used.

---

### Supabase (v2.53.0)

The same Supabase SDK is also used on the backend to connect to the database and manage authentication.

This gives us **consistency between the client and server** sides.

---

### Cors (v2.8.5)

This package enables **cross-origin requests**, allowing our React frontend (running on a different port) to communicate with the backend safely.

---

### Dotenv (v17.2.1)

Like on the frontend, **dotenv** is also used on the backend to manage environment variables, such as database URLs and API keys.

---

### yargs (v18.0.0)

**Yargs** is used in backend scripts to handle command-line arguments.  
It simplifies running tasks such as data ingestion or scheduled jobs via custom CLI commands.

---

## Testing and Quality Assurance

### Jest (v30.1.2)

**Jest** is the main testing framework we use.  
It helps us run **unit and integration tests** across both frontend and backend.

---

### React Testing Library (v16.3.0)

This library is used to **test React components**.  
Instead of testing the code directly, it simulates how a user would interact with the app—for example, checking that the scoreboard updates when new match data arrives.

---

### Additional Testing Tools

- **@testing-library/jest-dom** – adds custom DOM matchers for Jest (e.g., `toBeInTheDocument()`).
- **jest-environment-jsdom** – provides a browser-like testing environment.
- **supertest (v6.3.4)** – used in the backend to test Express routes and APIs.

---

## Development Tools

### Vite (v7.0.4)

**Vite** is our build tool and development server for the frontend.  
It gives us **fast reloads during development** and builds the app efficiently for production.

---

### TypeScript (v5.x)

**TypeScript** is used across both the frontend and backend to add **static typing**.  
This helps catch bugs early and makes the code easier to maintain.

---

### ESLint (v9.34.0) & TypeScript-ESLint (v8.41.0)

We use **ESLint** with TypeScript support to enforce coding standards and maintain code quality.  
Custom linting rules help ensure consistent syntax and style across the codebase.

---

### Tailwind & PostCSS Integration

Our development setup includes **Tailwind CSS**, **PostCSS**, and **Autoprefixer** for styling.  
These are managed through Vite’s plugin system and the `postcss.config.js` file.

---

### Nodemon (v3.1.10)

**Nodemon** is used in the backend during development.  
It automatically restarts the server when code changes, saving time.

---

### ts-node (v10.9.2)

**ts-node** allows us to run TypeScript files directly without compiling them first, making backend development quicker.

---

## Version Consistency

We use the **Supabase SDK** on both frontend and backend.  
The backend currently runs on `v2.56.1` while the frontend uses `v2.53.0`.  
Future updates will align these versions for consistency.

---

## Summary

We documented these third-party tools because they are the **core parts of our project**.  
Each one either supports a major feature (like live data fetching, routing, or authentication) or improves development and testing.

Using these libraries allowed us to focus more on building the actual football live feed app rather than reinventing common functionality.
