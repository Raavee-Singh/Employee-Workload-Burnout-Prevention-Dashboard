# Equipoise test report

## Results

| Area | Result | Verification |
|---|---|---|
| Frontend production build | PASS | `npm run build` completed successfully after the final UI changes. |
| Backend package and unit tests | PASS | `mvn clean package` succeeded on Java 25; 3 workload-logic tests passed. |
| Authentication and API reads | PASS | Demo login succeeded; 14 authenticated read endpoints returned HTTP 200. |
| Backend write flows | PASS | Capacity allocation create/delete, alert-rule threshold crossing, settings threshold updates, and task reassignment were verified. |
| Seed data | PASS | Startup data includes 15 employees, 50 tasks, and 6 projects. |
| Route smoke test | PASS | Login, overview, team, employee detail, rebalancer, planner, burnout, alerts, reports, projects, settings, and 404 routes loaded. |
| Mobile layout | PASS | At a 390px viewport, Overview and Alerts had no horizontal overflow. |
| Interactive flows | PASS | Login, leave scheduling, alert mark-all-read and rule creation, report date-range selection, threshold editing and saving, and rebalancer drag/apply/refresh persistence were exercised. |
| Rebalancer suggestion | PASS | Accepting the suggestion persisted the task reassignment. |
| Dead UI markers | PASS | No `href="#"`, empty click handler, `console.log`, or TODO/FIXME marker was found under `frontend/src`. |
| Exhaustive manual coverage | PARTIAL | Representative primary actions were exercised, but every control, filter, modal, export, and visual detail was not individually clicked or compared against every design screenshot. |

## Details

- The drag-and-drop test moved a task from Asha Patel to James Okafor. Capacity/status previews updated immediately; applying and refreshing preserved the assignment in the API.
- Changing the overloaded threshold to 140% changed Marcus Reed's 130% workload status from critical to overloaded, confirming server-side recalculation.
- The frontend emitted two non-blocking React Router v7 future-flag warnings. No post-login application error was observed.
- Maven's initial clean attempt could not delete OneDrive's generated `backend/target` reparse-point tree. Removing only that ignored build-output directory allowed the clean package and tests to complete successfully.
