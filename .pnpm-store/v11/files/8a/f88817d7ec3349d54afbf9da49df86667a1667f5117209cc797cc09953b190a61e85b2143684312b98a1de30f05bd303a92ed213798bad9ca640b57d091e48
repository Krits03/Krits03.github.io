import { schemaAutoImports } from '../imports.mjs';

const schemaOrgAutoImports = [
  {
    from: "@unhead/schema-org/vue",
    imports: schemaAutoImports
  }
];
const schemaOrgComponents = [
  "SchemaOrgArticle",
  "SchemaOrgBreadcrumb",
  "SchemaOrgComment",
  "SchemaOrgDiscussionForumPosting",
  "SchemaOrgEmployerAggregateRating",
  "SchemaOrgEvent",
  "SchemaOrgFoodEstablishment",
  "SchemaOrgHowTo",
  "SchemaOrgImage",
  "SchemaOrgJobPosting",
  "SchemaOrgLocalBusiness",
  "SchemaOrgMathSolver",
  "SchemaOrgOrganization",
  "SchemaOrgPerson",
  "SchemaOrgProduct",
  "SchemaOrgQuestion",
  "SchemaOrgQuiz",
  "SchemaOrgRecipe",
  "SchemaOrgReview",
  "SchemaOrgVideo",
  "SchemaOrgVacationRental",
  "SchemaOrgWebPage",
  "SchemaOrgWebSite",
  "SchemaOrgMovie",
  "SchemaOrgCourse",
  "SchemaOrgItemList",
  "SchemaOrgBook",
  "SchemaOrgSoftwareApp"
];
function SchemaOrgResolver(options = {}) {
  const { prefix = "" } = options;
  return {
    type: "component",
    resolve: (name) => {
      if (name.startsWith(prefix)) {
        const componentName = name.substring(prefix.length);
        if (schemaOrgComponents.includes(componentName)) {
          return {
            name: componentName,
            from: "@unhead/schema-org/vue"
          };
        }
      }
    }
  };
}

export { SchemaOrgResolver, schemaOrgAutoImports, schemaOrgComponents };
