# GarmentOMS BD

CSE-327 Software Engineering project: a garment order management system with grade-based export and a local surplus shop.
I may be doing the full project by myself. Deadline: **December 15, 2026**.

## Stack

- Back end: C++17 with MySQL
- Front end: HTML, CSS, JavaScript (plain, no framework)
- Build: CMake

## Project structure (organized by feature, not by type)

Each module keeps its C++ files and its web pages together, like my earlier project AgriSphere.

```
/
├── CLAUDE.md, README.md, .gitignore, CMakeLists.txt, main.cpp
├── docs/                 proposal PDF, ER/class/sequence diagrams
├── database/             schema.sql, seed.sql
├── core/                 shared code: DB connection, config, email sender, hashing, utils
└── modules/
    ├── auth/             login, register, email verification
    ├── dashboard/        main dashboard
    ├── orders/           order management
    ├── grading/          grade-based export vs. local routing
    └── shop/             surplus shop
        each module has: *Controller, *Service, *Repository (.h/.cpp) + web/ (html, css, js)
```

## Architecture rules

- Layering inside a module: Controller -> Service -> Repository -> MySQL. Never skip a layer.
- Controllers only handle HTTP and call services. Business logic lives in services. SQL lives only in repositories.
- Shared code goes in `core/`. Do not copy helpers between modules.
- The server serves only the `web/` folders to the browser, never the `.cpp` or `.h` files.
- Never commit secrets. Real config is git-ignored; commit `config.example.json` only.

## Design patterns (use 6, maximum 8; course minimum is 6)

Add each pattern when building the feature that needs it. Keep pattern classes clearly named so they are easy to point out in the demo.

| Pattern   | Where              | Purpose                                            |
| --------- | ------------------ | -------------------------------------------------- |
| Singleton | `core/`            | single database connection                         |
| Factory   | `modules/auth/`    | create users by role (admin, staff, customer)      |
| Builder   | `modules/orders/`  | build an order with many optional fields           |
| State     | `modules/orders/`  | order status lifecycle                             |
| Strategy  | `modules/grading/` | grade-based routing and pricing (export vs. local) |
| Observer  | `core/`            | notifications, e.g. email on order status change   |

Optional extras if time allows: Facade, Decorator (discounts/pricing add-ons).

## Roadmap

- **Nov 20-22, Setup and proposal:** folders, CMake, "hello" endpoint, MySQL connection (Singleton). Finish proposal (functional/non-functional requirements, system architecture).
- **Nov 23-27, auth + database:** `schema.sql`, seed data, register, login, email verification, roles (Factory), first dashboard page.
- **Nov 28-Dec 3, orders:** products, buyers, create/view/update orders, status flow (Builder, State), dashboard summaries.
- **Dec 4-9, grading + shop:** grade assignment, export vs. local routing (Strategy), surplus shop, purchase flow, email notifications (Observer).
- **Dec 10-11, polish:** validation, error messages, UI cleanup, reports. **Feature freeze Dec 11.**
- **Dec 12-15, finish:** testing, bug fixes, update docs/proposal, rehearse demo. Also the buffer if something slips.

## Working rules

- Build one vertical slice at a time: table -> back end -> page, working end to end before moving on.
- Keep changes small and compile often. Commit after each working piece and push daily.
- Work in a local folder and push to GitHub regularly (at least daily). Keep a `.gitignore` for build files and secrets.
- If behind schedule, cut extras (reports, UI polish), never the core features, the 6 patterns or testing.
- Prefer simple, readable code over clever code. Comment where a design pattern is used.

## Proposal status

Done: description, end users, ER, class and sequence diagrams.
In progress: functional/non-functional requirements, system architecture.

## My responsibility

Possibly the entire project: back end, front end, database, design patterns and proposal.

## Currently

Phase 0: project setup and proposal. (Update this line at the start of each phase.)

## Repo

https://github.com/RatulHassan18182/Cse327-GarmentsOMS-with-Grade-Based-Export-and-Local-Sales
