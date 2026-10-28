# User Stories (INVEST) – ScholarStack

This repository tracks the user stories for the **ScholarStack (NextAppStore)** platform.

---

## INVEST Framework Overview

| Criteria | Principle | Guiding Question |
|:---|:---|:---|
| **I** – Independent | Self-contained | Can this story be developed and delivered without hard dependencies on incomplete stories? |
| **N** – Negotiable | Focus on What & Why | Does the story describe the required capability without locking into rigid implementation details prematurely? |
| **V** – Valuable | Clear User Benefit | Does this story deliver clear, perceptible value to the user role (BWL Lecturer)? |
| **E** – Estimable | Sizable Effort | Is the requirement specific enough for the engineering team to estimate the effort reliably? |
| **S** – Small | Sprint-Sized | Is the scope focused enough to fit comfortably within a single development iteration? |
| **T** – Testable | Objective Verification | Are there concrete, verifiable acceptance criteria to prove the requirement is fulfilled? |

---

## Story Overview

| ID | Title | Role | Implementation Status | Related Tickets |
|---|---|---|---|---|
| **BWL1** | Information before installation | BWL Lecturer | ✅ Implemented & Verified | Backend: [#15](https://github.com/NextAppStore/backend/issues/15), PR [#27](https://github.com/NextAppStore/backend/pull/27)<br>Frontend: [#12](https://github.com/NextAppStore/frontend/issues/12), PR [#34](https://github.com/NextAppStore/frontend/pull/34) |
| **BWL2** | Start preconfigured environment with few clicks | BWL Lecturer | ✅ Implemented & Verified | Frontend: [#11](https://github.com/NextAppStore/frontend/issues/11), PR [#24](https://github.com/NextAppStore/frontend/pull/24), PR [#31](https://github.com/NextAppStore/frontend/pull/31), PR [#45](https://github.com/NextAppStore/frontend/pull/45) |
| **BWL3** | Recommendations and assistance for configuration | BWL Lecturer | ✅ Implemented & Verified | Frontend: [#10](https://github.com/NextAppStore/frontend/issues/10), PR [#16](https://github.com/NextAppStore/frontend/pull/16), PR [#35](https://github.com/NextAppStore/frontend/pull/35) |
| **BWL5** | Provide files | BWL Lecturer | 🟡 In Progress | Issue [#2](https://github.com/NextAppStore/user-stories/issues/2), Backend: [#17](https://github.com/NextAppStore/backend/issues/17) |
| **BWL6** | Use without technical knowledge | BWL Lecturer | 🟡 In Progress | Issue [#1](https://github.com/NextAppStore/user-stories/issues/1), Backend: [#10](https://github.com/NextAppStore/backend/issues/10), Frontend: [#61](https://github.com/NextAppStore/frontend/issues/61) |
| **ADMIN1** | Integration into self-service | Administrator | 🟡 In Progress | Issue [#3](https://github.com/NextAppStore/user-stories/issues/3) |

---

## BWL1: Information before installation

### User Story
> **As** BWL lecturer,  
> **I want** to see detailed information and requirements of an app or VM before installation,  
> **so that** I can judge whether it is suitable for my course without unnecessary setup effort.

### Acceptance Criterias
- [ ] Lecturer can view an app details page (`/apps/{id}`) from the catalog before initiating any deployment.
- [ ] The app details page displays a comprehensive description, software stack, VM topology, and minimum hardware requirements (flavor, RAM, vCPU).
- [ ] Current version information, author, release date, and release notes/changelog are clearly visible.
- [ ] Empty or unprovided metadata fields are gracefully handled without UI glitches.

### INVEST Assessment
* **Independent:** Yes. Can be developed and maintained as a read-only metadata presentation without modifying the deployment workflow.
* **Negotiable:** Yes. Layout presentation and optional fields remain flexible.
* **Valuable:** Yes. Prevents lecturers from spending time provisioning unsuitable applications.
* **Estimable:** Yes. Well-defined schema extensions (`vm_topology`, `requirements`, `recommended_for`) and UI views.
* **Small:** Yes. Fits into a single development iteration.
* **Testable:** Yes. Objectively verifiable by inspecting the `/apps/{id}` route for apps with and without populated metadata.

### Implementation References & Sub-Issues
* **Backend:**
  * Issue: [NextAppStore/backend#15](https://github.com/NextAppStore/backend/issues/15) (*B1 — Extend app metadata: `vm_topology`, `requirements`, `recommended_for`*)
  * Pull Request: [NextAppStore/backend#27](https://github.com/NextAppStore/backend/pull/27) (*Feat/extend app metadata*, merged)
* **Frontend:**
  * Issue: [NextAppStore/frontend#12](https://github.com/NextAppStore/frontend/issues/12) (*F3 — Extend the app form + detail page with metadata*)
  * Pull Request: [NextAppStore/frontend#34](https://github.com/NextAppStore/frontend/pull/34) (*feat(apps): edit and show app metadata*, merged)
  * View: `src/views/AppsDetailView.vue`
  * Tests: `tests/unit/views/AppsDetailView.spec.ts`

---

## BWL2: Start preconfigured environment with few clicks

### User Story
> **As** BWL lecturer,  
> **I want** to start a preconfigured learning environment with just a few clicks,  
> **so that** I can begin teaching immediately without configuration overhead.

### Acceptance Criterias
- [ ] Each app card in the catalog offers a visible "Quick Deploy" / "Schnell-Deploy" action (`data-testid="app-quick-deploy"`).
- [ ] Clicking Quick Deploy opens a lightweight modal (`QuickDeployModal`) to select the target course or "Only for me" (single user).
- [ ] All variables and settings are automatically populated with author defaults, skipping the multi-step configuration wizard directly to the review step.
- [ ] Complete deployment trigger is achievable within 2 to 3 clicks from the catalog.
- [ ] If an app requires mandatory inputs without default values, the system safely falls back to the full wizard with an explanatory hint.

### INVEST Assessment
* **Independent:** Yes. Acts as an express shortcut leveraging existing deployment orchestration.
* **Negotiable:** Yes. Modal styling and course selection mechanisms can be adapted to user feedback.
* **Valuable:** Yes. Eliminates configuration friction in live classroom environments.
* **Estimable:** Yes. Clear scope: modal component, store action shortcut, and route redirection.
* **Small:** Yes. Focused feature well-suited for a single sprint.
* **Testable:** Yes. Quantifiable click count (max 3 clicks), verification of pre-filled defaults, and automated unit/E2E tests.

### Implementation References & Sub-Issues
* **Frontend:**
  * Issue: [NextAppStore/frontend#11](https://github.com/NextAppStore/frontend/issues/11) (*F2 — Express deploy shortcut from the app tile*)
  * Pull Request: [NextAppStore/frontend#24](https://github.com/NextAppStore/frontend/pull/24) (*feat(deployment): Schnell-Deploy von der App-Kachel*, merged)
  * PR [NextAppStore/frontend#31](https://github.com/NextAppStore/frontend/pull/31) & PR [NextAppStore/frontend#45](https://github.com/NextAppStore/frontend/pull/45)
  * Components: `src/views/AppsView.vue`, `src/components/QuickDeployModal.vue`
  * Tests: `tests/unit/components/QuickDeployModal.spec.ts`, `tests/unit/views/AppsDetailView.spec.ts`

---

## BWL3: Recommendations and assistance for configuration

### User Story
> **As** BWL lecturer,  
> **I want** recommendations and contextual help for configurations,  
> **so that** I can choose the right settings for my use case without deep OpenStack knowledge (e.g. tooltips, prefilled defaults, 'Recommended' badges).

### Acceptance Criterias
- [ ] Configuration fields with author defaults are prefilled on initial load.
- [ ] Recommended choices in dropdowns (e.g., flavors, networks) are marked with a distinct "Recommended" badge (`data-testid="picker-recommended"`) and sorted to the top.
- [ ] Contextual help or tooltips explain technical parameters in non-technical language.
- [ ] Optional settings with working defaults are collapsed by default behind an "Advanced settings" section to keep the standard view clutter-free.
- [ ] The "Recommended" badge dynamically disappears if the user modifies the prefilled default.

### INVEST Assessment
* **Independent:** Yes. Confined to the variable configuration UI step without backend API breaking changes.
* **Negotiable:** Yes. Visual badge styles, tooltip wording, and collapse triggers are adaptable.
* **Valuable:** Yes. Prevents non-technical users from encountering resource misconfigurations (e.g. wrong network or insufficient flavor).
* **Estimable:** Yes. Standard UI component enhancements (badges, accordion, tooltips).
* **Small:** Yes. Fits into a single sprint.
* **Testable:** Yes. Verifiable through automated DOM assertions for badges, default values, and collapsible section toggles.

### Implementation References & Sub-Issues
* **Frontend:**
  * Issue: [NextAppStore/frontend#10](https://github.com/NextAppStore/frontend/issues/10) (*F1 — "Standard"/"Advanced" mode in the variable step + "Recommended" badges*)
  * Pull Request: [NextAppStore/frontend#16](https://github.com/NextAppStore/frontend/pull/16) (*feat: collapse defaulted variables behind 'Advanced' toggle*, merged)
  * Pull Request: [NextAppStore/frontend#35](https://github.com/NextAppStore/frontend/pull/35) (*feat(variables): merge packer and terraform variables*, merged)
  * Components: `src/views/NewDeploymentVariableView.vue`, `src/components/OpenStackResourcePicker.vue`, `src/components/VariableInput.vue`
  * Tests: `tests/unit/components/OpenStackResourcePicker.spec.ts`, `tests/unit/views/NewDeploymentVariableView.spec.ts`

---

## Live System Verification

The implementation of BWL1, BWL2, and BWL3 has been verified end-to-end on the live deployed system (`https://appstore.s242808-at-student-dhbw-mannheim-de.users.dhbw.site/`):
* **BWL1 Verified:** Full Markdown description, hardware requirements, author metadata, commit hashes, and version selectors rendered on app detail pages.
* **BWL2 Verified:** Quick Deploy button operational across catalog app cards; modal opens with course options; default values populated; wizard skipped to review.
* **BWL3 Verified:** Default parameters collapsed behind *"Erweiterte Einstellungen (6)"* with *"Alles vorkonfiguriert, hier ist keine Eingabe nötig"*; all defaults marked with visible `EMPFOHLEN` badges.
