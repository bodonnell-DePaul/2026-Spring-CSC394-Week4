# Vertical Slice Demo Guidelines

## CSC 394 · Software Projects · DePaul University

---

## What Is a Vertical Slice?

A **vertical slice** is a single, narrow feature implemented through **every layer** of your application — from the UI, through the API, down to the database and back. It proves your architecture works end-to-end by delivering one real piece of user-facing functionality.

```
┌─────────────────────────┐
│   Frontend              │  ← User sees and interacts with the feature
│   (UI framework)        │
└───────────┬─────────────┘
            │ HTTP / JSON
┌───────────▼─────────────┐
│   Backend / API         │  ← Server handles the request
│   (routes + logic)      │
└───────────┬─────────────┘
            │ ORM / queries
┌───────────▼─────────────┐
│   Database              │  ← Data is persisted and retrieved
│   (tables / collections)│
└─────────────────────────┘
```

> **Think of it as a toothpick through a layer cake** — thin, but touching every layer.

---

## Why It Matters

| Without a Vertical Slice | With a Vertical Slice |
|---|---|
| "The frontend is done but the API isn't ready" | One feature works completely |
| Integration bugs surface late | Integration is proven early |
| Hard to demo anything real | You can demo a working feature |
| Team members work in silos | Team sees how layers connect |

---

## Guidelines for Your Vertical Slice Demo

### 1. Pick One Real User Story

Choose a single, specific feature from your backlog. It should be something a real user would actually do.

- ✅ **Good:** "A user can create a new task and see it appear on their board"
- ✅ **Good:** "A user can register an account and log in"
- ❌ **Bad:** "The homepage looks nice" (no backend, no data)
- ❌ **Bad:** "All CRUD operations for every entity" (too wide, not a slice)

### 2. Touch Every Layer

Your slice **must** flow through all three tiers. Verify each:

- [ ] **Frontend** — A UI component or page where the user initiates the action (form, button, page)
- [ ] **API** — At least one backend route/endpoint that handles the request with real logic
- [ ] **Database** — At least one data model or table defined *(recommended but not required — hardcoded/mock data is acceptable)*
- [ ] **Round trip** — Data flows from UI → API → (DB or hardcoded source) → API → UI (the user sees the result)

### 3. Data Can Be Mock or Hardcoded — Database-Backed Is Recommended

Any of these approaches are **perfectly acceptable** for the demo:

| Approach | Acceptable? | Notes |
|---|---|---|
| Hardcoded data in the API | ✅ Yes | Fastest way to unblock the frontend |
| Mock/seed data returned from an endpoint | ✅ Yes | Shows the API contract is defined |
| Data read/written from your database via an ORM or query layer | ⭐ Recommended | Proves your persistence layer works end-to-end |

The key requirement is that your **frontend calls your real API** — where the API gets its data is up to you. That said, pulling from the database earns the most confidence that your architecture actually works, so aim for it if you can.

### 4. Keep It Narrow but Complete

Resist the urge to build wide. A vertical slice is about **depth**, not breadth.

| Narrow & Complete ✅ | Wide & Incomplete ❌ |
|---|---|
| Create a task (one form, one endpoint, one table) | Stubbed-out pages for tasks, users, settings, dashboard |
| Login flow with auth token stored and sent on requests | Login page UI with no actual authentication |
| Display a list fetched from the API with loading/error states | Five different list pages that all return `[]` |

### 5. Handle the Unhappy Path (at least minimally)

Show that your app doesn't break when something goes wrong:

- What happens if a required field is empty?
- What does the user see if the API returns an error?
- Does your form show validation feedback?

You don't need to handle every edge case, but **at least one error scenario** should be gracefully handled.

### 6. Prove Your Architecture Diagram Is Real

Your architecture diagram from Week 4 should match what's actually running. During the demo:

- Show that the components in your diagram actually exist in code
- Show data flowing between them as the diagram describes
- If your diagram includes auth, show auth actually working (even if only login/logout)

### 7. Environment and Setup

Your teammates (and the instructor) should be able to run your project:

- [ ] `README.md` has clear setup instructions (install, migrate, seed, run)
- [ ] `.env.example` exists with all required variables (no real secrets committed)
- [ ] Installing dependencies and starting the app is straightforward (document the commands)
- [ ] Database setup/migrations can be applied cleanly (if using a database)

### 8. Work as a Team, Integrate Early

- Use **feature branches** and **pull requests** — don't all commit to `main`
- Merge and test the integrated slice **before** the demo, not during
- If one person builds the API and another builds the UI, integrate at least 2 days before the demo
- Run through the demo as a team at least once before presenting

---

## Demo Day Checklist

Use this as a final check before you present:

- [ ] The app starts without errors
- [ ] You can walk through the feature from the user's perspective (click → result)
- [ ] Data persists — refresh the page and it's still there
- [ ] At least one error/validation scenario is handled
- [ ] The code is in your team's GitHub repo on `main` (or a clearly marked branch)
- [ ] Every team member can explain what their layer does
- [ ] No secrets or passwords are committed to the repo
- [ ] Setup instructions in the README actually work

---

## What We're Looking For

| Criteria | What "Good" Looks Like |
|---|---|
| **End-to-end completeness** | One feature works from UI through the API and back |
| **Real integration** | Frontend calls a real API endpoint (data source can be mock, hardcoded, or DB) |
| **Code in repo** | Working code is pushed, not just on someone's laptop |
| **Team collaboration** | Evidence of PRs, branches, and shared work |
| **Basic error handling** | App doesn't crash on bad input |
| **Clarity** | Team can explain their architecture and how the slice flows through it |

---

## Common Pitfalls to Avoid

1. **"Demo on my machine"** — If it only runs on one laptop, it's not ready. Use your repo.
2. **All frontend, no backend** — Beautiful UI with fake data isn't a vertical slice.
3. **All backend, no frontend** — A working API with no UI to demo isn't a vertical slice either.
4. **Last-minute integration** — Merging everything the night before guarantees bugs during the demo.
5. **Scope creep** — Three half-finished features are worse than one finished feature.
6. **No API at all** — If your frontend never talks to an API (even one returning hardcoded data), the layers aren't connected.

---

> **Remember:** The goal of the vertical slice demo is not to show a finished product. It's to prove that your team can build one working feature through every layer of your application. Nail one slice, and the rest is repetition.
