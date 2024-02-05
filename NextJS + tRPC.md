---
tags:
  - Server-Components
  - RSC
  - tRPC
  - NextJS
---
## React Server Components + tRPC Compatibility

I have run into an issue were the conventional method of using tRPC server side, the tRPC caller, causes the app to hang indefinitely.

```typescript
const trpc = appRouter.createCaller(await createContext());
export default trpc;
```
> *reference: [stack overflow](https://stackoverflow.com/a/77279538)*

Even with the settings to allow top level await, I think that NextJS does not like this.

I have run into a few other options including an experimental `createServerAction` option found [here](https://github.com/trpc/examples-next-app-dir/blob/main/src/server/trpc.ts).

```typescript
import { experimental_createServerActionHandler } from '@trpc/next/app-dir/server';

// ...

export const createAction = experimental_createServerActionHandler(t, {
  async createContext() {
    const session = await auth();

    return {
      session,
      headers: {
        // Pass the cookie header to the API
        cookies: headers().get('cookie') ?? '',
      },
    };
  },
});
```
