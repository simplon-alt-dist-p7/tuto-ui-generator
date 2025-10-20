# UI Generation Prompt Template

Template réutilisable pour générer prompts écrans optimisés V0/Bolt/Lovable.

## Variables à remplir

Avant d'utiliser template, définir:

- `[PROJECT_NAME]`: Nom projet
- `[PROJECT_PURPOSE]`: Objectif projet (1 phrase)
- `[USER_ROLES]`: Rôles utilisateurs (ex: Admin, User, Guest)
- `[SCREEN_NAME]`: Nom écran (ex: Login Page, Dashboard)
- `[SCREEN_CONTEXT]`: Pourquoi écran existe, problème résolu (2-3 lignes)
- `[BUILD_DESCRIPTION]`: Que doit faire écran (1 phrase action)
- `[COMPONENTS_LIST]`: Liste composants shadcn avec rôle précis
- `[INTERACTIONS_LIST]`: Actions utilisateur → résultats système
- `[LAYOUT_STRUCTURE]`: Grid/Flex, spacing, responsive
- `[DATA_DISPLAY]`: Données affichées à l'écran
- `[DATA_COLLECT]`: Données collectées via formulaires

---

## Template Prompt Écran

```markdown
# [SCREEN_NAME]

Context: [PROJECT_NAME] - [PROJECT_PURPOSE]. [SCREEN_CONTEXT]

Build: [BUILD_DESCRIPTION]

Components (shadcn/ui defaults):
[COMPONENTS_LIST]
- Component: Role + position in layout
- Component: Role + position in layout
- Component: Role + position in layout

Interactions:
[INTERACTIONS_LIST]
- When [user action]: [system response with details]
- When [user action]: [system response with details]
- When [user action]: [system response with details]

Layout Structure:
[LAYOUT_STRUCTURE]
- Grid/Flex configuration with spacing values
- Component arrangement details
- Responsive behavior (mobile/tablet/desktop)

Data:
- Displays: [DATA_DISPLAY]
- Collects: [DATA_COLLECT]
```

---

## Exemple rempli: Login Page

```markdown
# Login Page

Context: TaskFlow project management app. Only registered users can access tasks dashboard. Failed login shows clear error messages for wrong credentials or unverified accounts.

Build: Simple login form with email/password authentication and error handling.

Components (shadcn/ui defaults):
- Card: Login form container, centered on page
- Input: Email field with type="email" validation
- Input: Password field with type="password", min 8 chars
- Checkbox: "Remember me" option below password
- Button: Primary "Sign In" submit button, full-width
- Alert: Error message for invalid credentials or unverified email
- Link: "Forgot password?" text link below form
- Link: "Don't have an account? Sign up" below forgot password

Interactions:
- When user enters valid email/password and clicks "Sign In": Redirect to /dashboard, session created with 7-day expiry
- When credentials are incorrect: Alert shows "Invalid email or password", input borders turn red
- When account not verified: Alert shows "Please verify your email before logging in", with resend verification link
- When "Remember me" checked: Session persists 30 days instead of 7
- When user clicks "Forgot password?": Redirect to /reset-password

Layout Structure:
- Centered Card (max-w-sm) with padding p-6 on white background
- Vertical stack of inputs with gap-4 spacing
- Button full-width below inputs
- Links centered below button with text-sm, gap-2
- Alert appears above Card when error occurs
- Mobile: Card takes 90% width with mx-auto

Data:
- Displays: Empty email/password fields initially
- Collects: email (string), password (string), remember_me (boolean)
```

---

## Exemple rempli: Dashboard

```markdown
# Dashboard (User)

Context: TaskFlow project management app. Logged-in users need quick overview of active tasks, deadlines, and team activity. Dashboard provides stats cards and shortcuts to core actions.

Build: Dashboard with stats overview cards and action buttons for quick navigation.

Components (shadcn/ui defaults):
- Card: "Overview" container with 4 stat cards inside
- Card: Stat card "Active Tasks" showing number with icon
- Card: Stat card "Completed Today" showing number with icon
- Card: Stat card "Overdue" showing number with warning icon
- Card: Stat card "Team Members" showing number with icon
- Button: Primary "Create Task" large button with plus icon
- Button: Secondary "View All Tasks" button
- Button: Secondary "Team Activity" button
- Table: Recent tasks table (5 rows) showing task name, assignee, due date, status
- Badge: Status badge per task row (To Do, In Progress, Done)
- Separator: Horizontal divider between stats and recent tasks

Interactions:
- When page loads: Fetch user stats (active tasks count, completed today count, overdue count, team size) and display in stat cards
- When user clicks "Create Task": Open dialog modal with task creation form
- When user clicks "View All Tasks": Redirect to /tasks with all user's tasks
- When user clicks "Team Activity": Redirect to /activity feed
- When user clicks task row in table: Redirect to /tasks/[id] detail view
- When stat card shows overdue > 0: Card border turns red, shows warning icon

Layout Structure:
- Grid 4 columns (lg:grid-cols-4, md:grid-cols-2, sm:grid-cols-1) for stat cards
- Cards have padding p-6, gap-6 between cards, shadow-sm
- Separator with margin my-8
- Flex row gap-4 for action buttons, justify-start
- Table full-width below buttons with striped rows (bg-muted/50 on even rows)
- Mobile: Stack buttons vertically, table scrolls horizontally

Data:
- Displays: Active tasks count, completed today count, overdue count, team members count, recent 5 tasks (name, assignee, due_date, status)
- Collects: None (read-only dashboard)
```

---

## Checklist validation prompt

Avant envoyer à V0/Bolt:

- [ ] Context explique pourquoi écran existe (pas juste "page login")
- [ ] Build = 1 phrase action claire
- [ ] Components listés avec rôle précis + position
- [ ] Interactions décrivent flows complets (action → résultat détaillé)
- [ ] Layout structure donne valeurs spacing (gap-4, p-6, max-w-sm)
- [ ] Responsive mentionné (mobile/tablet/desktop)
- [ ] Data display/collect explicites

---

## Composants shadcn/ui disponibles

Liste référence composants à utiliser:

**Forms:**
- Input (text, email, password, number, date)
- Textarea
- Select (dropdown)
- Checkbox
- Radio Group
- Switch
- Slider

**Layout:**
- Card
- Separator
- Tabs
- Accordion
- Collapsible

**Feedback:**
- Alert
- Toast
- Badge
- Progress
- Skeleton

**Overlays:**
- Dialog (modal)
- Sheet (side drawer)
- Popover
- Tooltip
- Dropdown Menu

**Navigation:**
- Breadcrumb
- Pagination
- Command (search palette)

**Data Display:**
- Table
- Avatar
- Calendar
- Chart (via Recharts)

**Actions:**
- Button (primary, secondary, destructive, outline, ghost)
- Link

**Docs complètes:** https://ui.shadcn.com/docs/components

---

## Exemples projects types

### SaaS Dashboard
Écrans essentiels: Login, Dashboard, Settings, Billing, Team Management

### E-commerce
Écrans essentiels: Product Listing, Product Detail, Cart, Checkout, Order Confirmation

### Social App
Écrans essentiels: Feed, Profile, Post Creation, Notifications, Messages

### Admin Panel
Écrans essentiels: User Management Table, Analytics Dashboard, Settings, Audit Logs

---

## Tips génération

**DO:**
- ✅ Décrire flows utilisateur complets (action → validation → résultat)
- ✅ Préciser états (loading, error, empty state, success)
- ✅ Indiquer données exactes affichées (pas juste "user info")
- ✅ Donner valeurs spacing Tailwind (gap-4, p-6, max-w-md)

**DON'T:**
- ❌ Demander couleurs custom dans wireframe
- ❌ Rester vague ("une belle interface moderne")
- ❌ Oublier responsive mobile
- ❌ Ignorer états erreur/validation
