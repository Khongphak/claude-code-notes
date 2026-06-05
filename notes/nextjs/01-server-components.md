# React Server Components in Next.js 15

> A practical guide to understanding React Server Components (RSC), how they work in Next.js 15 App Router, and when to use them.

## Overview

React Server Components (RSC) run exclusively on the server — they never ship JavaScript to the browser. Next.js 15 App Router makes every component a Server Component by default, which means you opt into client-side rendering only when needed. This shift dramatically reduces bundle size and enables direct access to backend resources (databases, file system, secrets) from within components.

## Server vs Client Components

| Feature | Server Component | Client Component |
|---|---|---|
| Runs on | Server only | Browser (+ server for SSR) |
| Access to browser APIs | No | Yes |
| useState / useEffect | No | Yes |
| Event handlers (onClick) | No | Yes |
| Access to DB / secrets | Yes | No |
| Reduces JS bundle | Yes | No |
| Default in App Router | Yes | No — needs `"use client"` |

## How to Mark a Client Component

Add `"use client"` at the very top of the file.

```typescript
"use client";

import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

Without `"use client"`, using `useState` will throw a build error.

## Fetching Data in Server Components

Server Components can `await` directly — no `useEffect`, no loading state boilerplate.

```typescript
// app/posts/page.tsx — Server Component (no "use client")
async function getPosts() {
  const res = await fetch("https://api.example.com/posts", {
    next: { revalidate: 60 }, // ISR: revalidate every 60s
  });
  return res.json();
}

export default async function PostsPage() {
  const posts = await getPosts();

  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}
```

## Composing Server and Client Components

Server Components can pass data **down** to Client Components as props. Client Components **cannot** import Server Components directly.

```typescript
// app/dashboard/page.tsx — Server Component
import StatsChart from "@/components/StatsChart"; // Client Component

export default async function DashboardPage() {
  const stats = await db.query("SELECT ...");

  // Pass serializable data as props — no secrets leak to the client
  return <StatsChart data={stats} />;
}
```

```typescript
// components/StatsChart.tsx — Client Component
"use client";

import { useState } from "react";

export default function StatsChart({ data }: { data: Stat[] }) {
  const [filter, setFilter] = useState("all");
  // ... interactive chart logic
}
```

> **Rule of thumb:** Push `"use client"` boundaries as far down the tree as possible. Keep data fetching and layout in Server Components; isolate interactivity into small leaf components.

## Caching Behavior (Next.js 15 Changes)

Next.js 15 made `fetch` **opt-in** for caching (previously opt-out). By default, fetches are now uncached.

```typescript
// Uncached (default in Next.js 15) — fresh data on every request
const data = await fetch("/api/data");

// Cached — stored in the Data Cache indefinitely
const data = await fetch("/api/data", { cache: "force-cache" });

// ISR — revalidate on a time interval
const data = await fetch("/api/data", { next: { revalidate: 3600 } });

// Tag-based revalidation
const data = await fetch("/api/data", { next: { tags: ["posts"] } });
```

## Common Pitfalls

- **Using hooks in Server Components** — `useState`, `useEffect`, `useRef` are client-only. Move them to a `"use client"` file.
- **Passing non-serializable props** — Functions and class instances can't cross the server→client boundary. Pass plain objects, strings, or numbers only.
- **Importing a Client Component into a Server Component that uses context** — Context is client-side. Wrap context providers at a high-level Client Component boundary.
- **Forgetting `"use client"` for event handlers** — `onClick`, `onChange`, etc. require a Client Component. The error message from Next.js is clear but easy to miss during development.
- **Over-using `"use client"`** — Marking a parent as a Client Component pulls all its children client-side too. Keep the boundary tight.

## Sources

- [Next.js Docs — Server Components](https://nextjs.org/docs/app/building-your-application/rendering/server-components)
- [Next.js Docs — Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components)
- [Next.js 15 Caching Changes](https://nextjs.org/blog/next-15#caching-semantics)
- Personal experimentation (June 2026)

## Next

- `02-server-actions.md` — Mutations and form handling with Server Actions
- `03-caching-deep-dive.md` — Full breakdown of Next.js 15 caching layers
