## References 
* https://github.com/trpc/trpc/issues/3297#issuecomment-1644237475
	* has a snippet using a `createPage` helper.
	* uses zod to type Page params and search params
	* Create a util that does this and another to do something similar with `createAction` that injects `trpc` 
```typescript 
export default createPage(
  z.object({ params: Params.findMany, searchParams: SearchParams.findMany }),
  async ({ params, searchParams }) => {
    const { server } = getResourceFromUri(params.uri);
    const initialData = await server.api.findMany({});
                                  // ^ this is our createCaller() instance 

    return (
      <ResourceTable initialData={initialData} searchParams={searchParams} />
    );
  },
);
```