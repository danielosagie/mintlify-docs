# sssync Backend Development & Documentation Preview

This guide covers setting up the **sssync NestJS backend** for local development and how to preview the **Mintlify API documentation** locally.

## Part 1: sssync Backend Development (Node.js/NestJS)

Follow these instructions to get the main backend application running on your local machine.

### Prerequisites

-   **Node.js**: Latest LTS version recommended (check `.nvmrc` or `package.json` -> `engines`). Use `nvm` to manage versions.
    ```bash
    nvm install 18 # Or specified version
    nvm use 18
    ```
-   **npm** or **yarn**: Use the one corresponding to the project's lock file (`package-lock.json` for npm, `yarn.lock` for yarn).
-   **Git**: For cloning.
-   **Supabase Account/CLI (Recommended)**: For database and auth. [Supabase CLI](https://supabase.com/docs/guides/cli) is useful for local development.

### 1. Clone the Repository

```bash
git clone <your-sssync-backend-repo-url>
cd sssync-bknd # Or your backend project's root directory
```

### 2. Install Dependencies

<CodeGroup>
```bash npm
npm install
```
```bash yarn
yarn install
```
</CodeGroup>

### 3. Environment Configuration (`.env`)

Create a `.env` file in the project root (e.g., `sssync-bknd/.env`). Copy from `.env.example` if it exists.

Key variables:
```env
# Application
NODE_ENV=development
PORT=3001

# Supabase
SUPABASE_URL=your_supabase_project_url
SUPABASE_KEY=your_supabase_service_role_key
SUPABASE_JWT_SECRET=your_supabase_jwt_secret

# Security
ENCRYPTION_SECRET_KEY=generate_a_strong_32_byte_secret_key

# Platform APIs (use sandbox/dev keys)
SHOPIFY_API_KEY=...
SHOPIFY_API_SECRET=...
SHOPIFY_APP_URL=http://localhost:3001 # Or ngrok URL
# ... other platform keys (Square, Clover)

# Optional: Redis for BullMQ
# REDIS_HOST=localhost
# REDIS_PORT=6379
```
**Important:** Never commit `.env` with actual secrets. Use `ngrok` for webhook testing if developing locally.

### 4. Running the Backend (Development Mode)

<CodeGroup>
```bash npm
npm run start:dev
```
```bash yarn
yarn start:dev
```
</CodeGroup>
This starts the NestJS server with hot-reloading, typically on `http://localhost:3001`.

### 5. Key `package.json` Scripts

-   `build`: Compile TypeScript to JavaScript (`dist` folder).
-   `start`: Run compiled app (for production).
-   `lint`: Check code style with ESLint.
-   `test`: Run unit tests (Jest).
-   `test:e2e`: Run end-to-end tests.

### 6. Database (Supabase)

Ensure your Supabase instance (cloud or local CLI) is set up with the required schema. Use migrations in `supabase/migrations` if available.

```bash
# Example Supabase CLI commands
# supabase login
# supabase link --project-ref <your-project-ref>
# supabase start # For local dev stack
# supabase db reset # Apply local migrations
```

---

## Part 2: Previewing API Documentation (Mintlify)

These instructions are for previewing the documentation site itself, which is built using Mintlify.

### Mintlify Setup

1.  **Install Mintlify CLI**: If you don't have it, install it globally.
    ```bash
    npm i -g mintlify
    ```

2.  **Navigate to Docs Folder**: Change to the directory containing your Mintlify documentation (e.g., `mintlify-docs` or the root of this docs project if `docs.json` is there).
    ```bash
    cd mintlify-docs # Or the correct path to your docs
    ```

3.  **Run Mintlify Development Server**:
    ```bash
    mintlify dev
    ```
    This command starts a local server, usually on `http://localhost:3000`, allowing you to see your documentation changes live.

### Publishing Documentation Changes

-   Install the Mintlify GitHub App to automatically propagate changes from your repository to your deployed documentation site.
-   Changes pushed to the default branch will be deployed to production automatically.

### Troubleshooting Mintlify

-   **`mintlify dev` isn't running**: Try running `mintlify install` in your docs folder. This will re-install dependencies for the documentation viewer.
-   **Page loads as a 404**: Make sure you are running `mintlify dev` in the folder that contains your `docs.json` file.

This combined guide should help you develop the sssync backend and preview its documentation effectively.
