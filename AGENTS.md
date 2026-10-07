# obsidian-symlink-manager Agent Rules

Key documents in the `specifications-vault` folder include:
* `03_Requirements` – Functional & non-functional requirements, use cases, activity diagrams, and the software requirement specification.
* `04_Architecture` – Technical architecture, system architecture, architectural decisions, and behavioral modeling.

> **Instruction for AI Agents:** When answering architectural questions or writing code, reference the appropriate spec files inside `obsidian-symlink-manager/specifications-vault/` and ensure full consistency with defined conventions.

---

## Core Capabilities to Implement
1. **Symlink Inspection & Management:**
   - Detect and list all plugins, CSS snippets, and themes across registered vaults.
   - Differentiate between native files, valid symlinks, and broken symlinks.
   - Provide actions to create, repoint, and safely unlink items.
2. **Global / Origin Vault Configuration:**
   - Allow setting a single "source of truth" vault where canonical configurations reside.
   - Sync configurations from origin to target vaults.
3. **Vault Bootstrapping & Creation:**
   - Step-by-step Raycast Form to scaffold a new vault and selectively choose which origin components to symlink.
4. **Safety & Validation:**
   - Prevent circular symlinks or linking inside non-Obsidian directories.
   - Offer dry-run checks and graceful handling of missing origin targets.

---

## Tech Stack & Standards
* **Framework:** Raycast API (`@raycast/api`, `@raycast/utils`)
* **Runtime:** Node.js (via Raycast runtime)
* **Language:** TypeScript (`strict: true`)
* **File Operations:** Node `fs/promises` (`lstat`, `readlink`, `symlink`, `unlink`) with POSIX/Windows cross-platform path handling (`path`).

---

## Development Workflow & Commands
* `npm install` – Install dependencies
* `npm run dev` – Start Raycast extension development mode
* `npm run build` – Build extension bundle
* `npm run lint` – Run ESLint and Prettier checks

---

## Agent Instructions & Rules
* **Always verify against specifications:** Do not invent file structures or settings keys without consulting `obsidian-symlink-manager/specifications-vault/`.
* **Safe Filesystem Changes:** Always verify `lstat().isSymbolicLink()` before invoking `unlink()`. Never recursively delete files without explicit confirmation prompts (`showHUD` / `confirmAlert`).
* **Keep Raycast UI Responsive:** Perform heavy I/O scans asynchronously using Raycast's `usePromise` or background workers.
