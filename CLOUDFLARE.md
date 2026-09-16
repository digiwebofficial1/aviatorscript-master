# Cloudflare Workers deployment

This repository contains the original AviatorScript Java/JVM implementation plus a Cloudflare Workers compatibility layer.

The Java engine itself cannot execute directly inside the Workers V8 runtime. The Worker therefore uses the Cloudflare-safe JavaScript interpreter in `worker/interpreter.js` for the supported language subset.

## Deploy

```bash
npm install
npm test
npx wrangler deploy
```

## API

`GET /api/health`

`POST /api/eval`

Example body:

```json
{
  "expression": "price * quantity > 100",
  "env": { "price": 25, "quantity": 5 }
}
```

The evaluator is sandboxed and does not expose Java reflection, arbitrary class loading, JVM bytecode generation, Java I/O, or unrestricted Java method invocation.

## Important compatibility note

The Cloudflare interpreter is not a drop-in replacement for every JVM-specific AviatorScript 5.4.4 feature. Keep the original Java implementation as the reference implementation when adding language compatibility.
