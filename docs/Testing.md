## Testing Strategy

We followed a **test-driven development (TDD)-inspired approach**, using the **Red–Green–Refactor cycle**:

1. **Red (Write Failing Tests):**  
   Before writing code, we created `.todo` entries in our test files to outline the behaviours we wanted to see  
   _(e.g., “scoreboard should update when a goal event is received”)._

2. **Green (Implement Logic):**  
   We then implemented the UI or logic until the test passed.

3. **Refactor:**  
   Once the tests were passing, we cleaned up and refactored the codebase while making sure all functionality remained intact.

This process helped us stay focused on **user intent** and ensured that **every feature had test coverage from the beginning**.

---

## Tools and Frameworks Used

- **Jest:** Our main testing framework, used for running unit and integration tests.
- **React Testing Library:** Simulated user interactions such as clicking buttons, navigating between pages, or checking if live match updates appear correctly.
- **jsdom:** Provided a virtual DOM so we could test React components outside of a real browser.
- **Axios mocking:** Allowed us to test API calls without relying on live football data, by simulating responses like goals, substitutions, or match start events.
- **Google OAuth mocking:** Simulated the login process for users signing in with Google.

---

## Testing Approach

We structured our testing to make sure that both **critical features** and **edge cases** were covered:

- **Authentication flows:** Verified that users could log in with Google, stay logged in during a session, and log out successfully.
- **Live feed updates:** Ensured that match scores, goal events, and substitutions updated correctly when mock API data was returned.
- **Component rendering:** Checked that pages such as the live matches screen, match details, and team information rendered correctly and responded to user actions.
- **Error handling:** Tested how the app responded to missing or invalid API data  
  _(e.g., if the API failed, a “data unavailable” message appeared instead of crashing)._
- **Navigation:** Verified routing worked properly by simulating transitions between pages with React Router.

---

## Test Design

We designed our tests at different levels to provide **good coverage**:

- **Unit tests:** Focused on individual components like the scoreboard, event list, or navigation bar.
- **Integration tests:** Covered multiple components working together, for example ensuring that the live feed page correctly updated both the scoreboard and event list when new match data arrived.
- **Async flow tests:** Simulated API calls (using Axios mocks) to test that data fetched from the backend or external APIs updated the UI correctly.

---
