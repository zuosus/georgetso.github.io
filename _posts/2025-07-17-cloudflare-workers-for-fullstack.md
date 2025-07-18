## Why
Cloudflare workers are a powerful way to run services and websites, especially for SSG + CSR, which is a great solution for both SEO and performance. It also takes the burden off of devops and scale management, as Cloudflare handles the scaling and infrastructure. And it's free for starter projects.

## How
For API services, [Hono](http://hono.dev) is a great choice as it's born for cf workers.

For websites, [@opennextjs/cloudflare](https://opennext.js.org/cloudflare/get-started) supports both SSG and CSR with react-ts, cf R2 serves for the hosting.

For state management, cf D1 and KV are free and powerful.

## Note
The defult build and deploy comamnd on Cloudflare is `wrangler deploy`, which does not work for opennextjs projects. Change them to
```
build: pnpm opennextjs-cloudflare build
deploy: pnpm opennextjs-cloudflare deploy
```

---


Sounds a great solution to starter projects.
