import { array, boolean, object, string } from "valibot";
export const ComponentLazyLoadImportSchema = object({
  componentName: string(),
  importSource: string(),
  importedBy: string(),
  rendered: boolean()
});
export const ComponentLazyLoadDataSchema = object({
  id: string(),
  route: string(),
  state: object({
    pageLoaded: boolean(),
    hasReported: boolean(),
    directImports: array(ComponentLazyLoadImportSchema)
  })
});
