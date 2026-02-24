# SingleWallet Frontend

The frontend for **Single Wallet**, a banking app that lets users connect and manage all their bank accounts in one place. Built with **Angular** and communicates with a Spring Boot backend via REST APIs.

---

## Tech Stack

- **Framework:** Angular (standalone components, 2025)
- **Language:** TypeScript
- **Styling:** CSS with global CSS variables
- **Routing:** Angular Router with route guards
- **HTTP:** Angular HttpClient (proxied to Spring Boot on port 8080)

---

## Getting Started

### Prerequisites
- Node.js v18+
- Angular CLI: `npm install -g @angular/cli`

### Installation
```bash
# From the root of the repository
cd frontend
npm install
```

### Running the App
```bash
ng serve
```

The app will be running at `http://localhost:4200`.  
Make sure the Spring Boot backend is also running at `http://localhost:8080`.

---

## Folder Structure

```
frontend/
└── src/
    └── app/
        ├── components/         # Reusable UI pieces used across multiple pages
        │   └── navbar/         # Top navigation bar
        │
        ├── guards/             # Route guards (protect pages that require login)
        │   └── auth.guard.ts   # Redirects to login if user is not authenticated
        │
        ├── pages/              # Full page components (one per route)
        │   ├── login/          # Login screen - entry point of the app
        │   ├── dashboard/      # Main dashboard after logging in
        │   └── accounts/       # View and manage connected bank accounts
        │
        ├── services/           # Handles all API calls to the backend
        │   ├── auth.service.ts     # Login, logout, token management
        │   └── accounts.service.ts # Fetching and managing bank accounts
        │
        ├── app.routes.ts       # All route definitions live here
        ├── app.config.ts       # App-wide configuration (router, HTTP client)
        ├── app.html            # Root template - just contains <router-outlet />
        └── app.ts              # Root component
```

---

## Routing

| Path | Component | Protected? |
|---|---|---|
| `/` | Redirects to `/login` | No |
| `/login` | LoginComponent | No |
| `/dashboard` | DashboardComponent | Yes (requires login) |
| `/accounts` | AccountsComponent | Yes (requires login) |

Protected routes use `authGuard` - if a user tries to visit `/dashboard` without being logged in, they get redirected to `/login` automatically.

---

## Global Styles

All global styles live in `src/styles.css`. This includes:

- **Google Fonts import** (Roboto)
- **CSS variables** for the color palette, change colors here and they update everywhere:

```css
:root {
  --primary: #1a73e8;
  --primary-dark: #1558b0;
  --background: #f0f4f8;
  --white: #ffffff;
  --text: #333333;
  --text-light: #666666;
  --border: #dddddd;
}
```

Component-specific styles go in that component's own `.css` file (e.g. `login.css` for login-only styles).

---

## Connecting to the Backend

The proxy is configured in `proxy.conf.json`. Any request made to `/api/...` from the frontend automatically gets forwarded to the Spring Boot backend at `http://localhost:8080`.

Example: a call to `/api/accounts` in Angular hits `http://localhost:8080/api/accounts` on the backend.

All API calls should go through the **services** folder, never call the backend directly from a component.

---

## How to Add a New Page

Follow these steps every time you need to add a new page to the app.

**Step 1 - Generate the component:**
```bash
ng generate component pages/your-page-name
```
This creates 4 files inside `src/app/pages/your-page-name/`:
- `your-page-name.ts` - the logic
- `your-page-name.html` - the template
- `your-page-name.css` - the styles
- `your-page-name.spec.ts` - the test file (can ignore for now)

**Step 2 - Add the route in `app.routes.ts`:**
```ts
import { YourPageNameComponent } from './pages/your-page-name/your-page-name';

export const routes: Routes = [
  // ...existing routes...
  { path: 'your-page-name', component: YourPageNameComponent }
];
```

If the page should require the user to be logged in, add `canActivate: [authGuard]`:
```ts
{ path: 'your-page-name', component: YourPageNameComponent, canActivate: [authGuard] }
```

**Step 3 - Navigate to it from another page:**

In any `.ts` file, inject the router and navigate:
```ts
import { Router } from '@angular/router';

constructor(private router: Router) {}

goToPage() {
  this.router.navigate(['/your-page-name']);
}
```

Or in any `.html` file, use `routerLink`:
```html
<a routerLink="/your-page-name">Go to page</a>
<button (click)="goToPage()">Go to page</button>
```

---

## How to Add a New Reusable Component

Reusable components are things like buttons, cards, or modals that are used across multiple pages. They go in the `components/` folder instead of `pages/`.

```bash
ng generate component components/your-component-name
```

Then use it inside any page's HTML like this:
```html
<app-your-component-name />
```

The `app-` prefix is added automatically by Angular based on the selector in the component's `.ts` file.

---

## How to Add a New Service

Services handle all communication with the backend. Every new feature that needs data from the backend should have its own service.

**Step 1 - Generate the service:**
```bash
ng generate service services/your-service-name
```

**Step 2 - Write the API call in the service file:**
```ts
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';

@Injectable({ providedIn: 'root' })
export class YourServiceNameService {

  constructor(private http: HttpClient) {}

  getData() {
    return this.http.get('/api/your-endpoint');
  }

  postData(body: any) {
    return this.http.post('/api/your-endpoint', body);
  }
}
```

**Step 3 - Use the service in a component:**
```ts
import { YourServiceNameService } from '../../services/your-service-name.service';

export class SomePageComponent {
  constructor(private yourService: YourServiceNameService) {}

  ngOnInit() {
    this.yourService.getData().subscribe(data => {
      console.log(data);
    });
  }
}
```

---

## Naming Conventions

Keeping names consistent makes it easier for the whole team to read each other's code.

| What | Convention | Example |
|---|---|---|
| Component files | kebab-case | `bank-card.ts` |
| Component classes | PascalCase | `BankCardComponent` |
| Service files | kebab-case | `auth.service.ts` |
| Service classes | PascalCase + Service | `AuthService` |
| Variables & functions | camelCase | `getUserBalance()` |
| CSS classes | kebab-case | `.account-card` |
| Route paths | kebab-case | `/bank-accounts` |

---

## Team Workflow (Git)

To avoid stepping on each other's code, follow this branch strategy:

```bash
# Always pull the latest before starting work
git pull origin main

# Create your own branch for the feature you're working on
git checkout -b feature/your-feature-name

# When done, push your branch
git push origin feature/your-feature-name

# Then open a Pull Request on GitHub to merge into main
```

**Branch naming examples:**
- `feature/login-page`
- `feature/dashboard-ui`
- `feature/accounts-list`
- `fix/login-button-bug`

Never push directly to `main`. Always go through a Pull Request so your teammate can review it first.

---

## Common Angular CLI Commands

| Command | What it does |
|---|---|
| `ng serve` | Starts the dev server at localhost:4200 |
| `ng generate component pages/name` | Creates a new page |
| `ng generate component components/name` | Creates a new reusable component |
| `ng generate service services/name` | Creates a new service |
| `ng generate guard guards/name` | Creates a new route guard |
| `ng build` | Builds the app for production |

---

## Frontend Team

This frontend was built by the frontend team as part of the **CS 4398 semester project**.  
Backend is handled separately under `/src` using Spring Boot (Java).