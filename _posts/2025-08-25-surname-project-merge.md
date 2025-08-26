---
title: "A Day of Merging: Unifying Frontend and Backend in a Single Cloudflare Worker"
date: 2025-08-25
---

Today, August 25, 2025, marks a significant step in the development of the `surname` project, focusing on unifying our frontend (OpenNext.js) and backend (Hono.dev) into a single Cloudflare Worker. This approach streamlines deployment and maintenance, moving away from separate deployments for each service.

### The Unification Challenge: One Worker to Rule Them All

Previously, our OpenNext.js frontend and Hono.dev backend were deployed as separate Cloudflare Workers. The goal was to merge them into a single project, allowing the backend API to be accessible under a `/api/*` path relative to the frontend's host. This simplifies domain management and internal routing.

### Technical Solution: Merging Handlers

The core of this unification lies in intelligently routing requests within a single Cloudflare Worker's `fetch` handler. By leveraging the `URL` object, we can inspect the request path and direct it to the appropriate handler:

```typescript
import { createHandler } from "opennextjs";
import { Hono } from "hono";

// 1. Initialize Hono app for API routes
const api = new Hono();
api.get("/hello", (c) => c.json({ message: "Hello from API" }));
// ... add more Hono API routes here

// 2. Create Next.js handler
const nextHandler = createHandler();

export default {
  async fetch(req: Request, env: any, ctx: ExecutionContext) {
    const url = new URL(req.url);

    // If the path starts with /api, route to Hono
    if (url.pathname.startsWith("/api")) {
      return api.fetch(req, env, ctx);
    }

    // Otherwise, route to OpenNext.js
    return nextHandler(req, env, ctx);
  },
};
```

This setup ensures that requests to `/api/hello` (or any other `/api/*` path) are handled by Hono, while all other requests (e.g., `/`, `/about`, `/blog`) are served by OpenNext.js. A crucial point is that OpenNext.js can "consume" all requests, so the `/api/*` check must always precede the Next.js handler call.

### Deployment Strategy with `wrangler.jsonc`

With the handlers merged, deployment simplifies to a single Cloudflare Worker. The `wrangler.jsonc` configuration plays a vital role in defining this unified deployment:

```json
{
  "name": "my-fullstack-app",
  "main": "./dist/worker.js", // Entry point after bundling Hono and OpenNext.js
  "compatibility_date": "2025-08-25",
  "compatibility_flags": ["nodejs_compat"],

  // Example: Binding Cloudflare resources (D1, KV, R2)
  "d1_databases": {
    "DB": { "binding": "DB", "database_name": "mydb", "database_id": "xxxx-xxxx" }
  },
  "kv_namespaces": [
    { "binding": "KV", "id": "xxxx-xxxx" }
  ],
  "r2_buckets": [
    { "binding": "R2", "bucket_name": "my-bucket" }
  ],

  "dev": {
    "port": 8787
  },
  "routes": [
    {
      "pattern": "mydomain.com",
      "custom_domain": true
    }
  ],
  "vars": {
    "NODE_ENV": "production"
  }
}
```

For deployment, `wrangler deploy` is the preferred tool. While `opennextjs-cloudflare deploy` exists, it's tailored for pure Next.js deployments. For a combined Hono and OpenNext.js project, a custom build script (e.g., using `esbuild` or `vite`) to bundle both handlers into a single `worker.js` file, followed by `wrangler deploy`, offers maximum flexibility and control.

### Understanding Cloudflare Resource Bindings

A key insight during this process was clarifying the distinction between Cloudflare Dashboard resource names and `wrangler.jsonc` binding names for services like D1, KV, and R2.

*   **Dashboard Resource Name:** This is the name you see and manage in the Cloudflare console (e.g., `mydb` for a D1 database). It's primarily for internal identification and display. **Changing this name in the Dashboard does not affect your Worker code.**
*   **Binding Name:** Defined in `wrangler.jsonc` (e.g., `"binding": "DB"`). This is the actual variable name exposed to your Worker code (e.g., `env.DB`). **Your code interacts solely with this binding name.**

This means that as long as the `binding` name in `wrangler.jsonc` remains consistent, changes to the resource name in the Cloudflare Dashboard will not necessitate code modifications.

### Conclusion

Unifying our frontend and backend into a single Cloudflare Worker has significantly simplified our project architecture. By carefully managing request routing and understanding Cloudflare's deployment mechanisms and resource bindings, we've achieved a more streamlined and efficient full-stack application. This merge represents a substantial effort towards improving the project's overall structure and maintainability.