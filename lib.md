# Documentation for PetPlate Subscription Service Code

Welcome to the documentation for the PetPlate Subscription Service codebase. This document will guide you through the various functions, constants, GraphQL queries/mutations, React hooks, and utility functions present in the code. The goal is to provide a comprehensive source of information for new team members to understand and work with the existing code effectively.

---

## Table of Contents

- [Utility Functions](#utility-functions)
  - [calcFromName](#calcfromname)
  - [calcToName](#calctoname)
  - [calcPatternName](#calcpatternname)
  - [calcMatchName](#calcmatchname)
- [Constants](#constants)
  - [COMPARISON_OPTIONS](#comparison_options)
  - [QUERY_OPTIONS](#query_options)
  - [DEFAULT_VALUES](#default_values)
- [Interfaces](#interfaces)
  - [Line](#line-interface)
  - [FetchCartResponse](#fetchcartresponse-interface)
- [GraphQL Queries and Mutations](#graphql-queries-and-mutations)
  - [Queries](#queries)
  - [Mutations](#mutations)
- [React Components and Hooks](#react-components-and-hooks)
  - [StyledComponentsRegistry](#styledcomponentsregistry)
  - [useBreeds](#usebreeds)
  - [useContinueHandler](#usecontinuehandler)
  - [useFulfillmentScheduleDates](#usefulfillmentscheduledates)
  - [… (Other Hooks)](#other-hooks)
- [Utility and Helper Functions](#utility-and-helper-functions)
  - [Session Cart Helpers](#session-cart-helpers)
  - [Error Handling](#error-handling)
  - [Cookie Helpers](#cookie-helpers)
  - [Scroll Utilities](#scroll-utilities)
  - [SDK Helpers](#sdk-helpers)
  - [Search Helpers](#search-helpers)
  - [Scroll Block](#scroll-block)

---

## Utility Functions

### calcFromName

```typescript
export const calcFromName = (name: string) => `${name}From`;
```

- Description: Generates a new string by appending `'From'` to the input string.
- Parameters:
  - `name`: A string value to transform.
- Returns: A new string with `'From'` concatenation.

### calcToName

```typescript
export const calcToName = (name: string) => `${name}To`;
```

- Description: Generates a new string by appending `'To'` to the input string.
- Parameters:
  - `name`: A string value to transform.
- Returns: A new string with `'To'` concatenation.

### calcPatternName

```typescript
export const calcPatternName = (name: string) => `${name}Pattern`;
```

- Description: Generates a new string by appending `'Pattern'` to the input string.
- Parameters:
  - `name`: A string value to transform.
- Returns: A new string with `'Pattern'` concatenation.

### calcMatchName

```typescript
export const calcMatchName = (name: string) => `${name}Match`;
```

- Description: Generates a new string by appending `'Match'` to the input string.
- Parameters:
  - `name`: A string value to transform.
- Returns: A new string with `'Match'` concatenation.

---

## Constants

### COMPARISON_OPTIONS

```typescript
export const COMPARISON_OPTIONS = [
  { label: 'Equals', value: 'equals' },
  { label: 'Greater Than', value: 'greaterThan' },
  { label: 'Less Than', value: 'lessThan' }
];
```

- Description: An array of objects representing different comparison options, each with a `label` for display and a `value` for internal logic.

### QUERY_OPTIONS

```typescript
export const QUERY_OPTIONS = [
  { label: 'Contains', value: 'contains' },
  { label: 'Equals', value: 'equals' },
  { label: 'Starts With', value: 'startsWith' },
  { label: 'Ends With', value: 'endsWith' }
];
```

- Description: An array of objects representing different query options, each with a `label` for display and a `value` for internal logic.

### DEFAULT_VALUES

```typescript
export const DEFAULT_VALUES = {
  empty: '',
  query: QUERY_OPTIONS[0].value,
  comparison: COMPARISON_OPTIONS[0].value,
  sort: ['']
};
```

- Description: An object containing default values for various fields used in querying and filtering data.

---

## Interfaces

### Line Interface

```typescript
interface Line {
  type: string;
  sku: string;
}
```

- Description: An interface representing a line item with a type and stock keeping unit (SKU).

### FetchCartResponse Interface

```typescript
interface FetchCartResponse {
  data: {
    fetchCart: { lineItemsData: Line[] };
  };
}
```

- Description: An interface representing the expected response structure for a fetchCart request, which includes line items data.

---

## GraphQL Queries and Mutations

GraphQL queries and mutations are defined as template strings and executed using the Apollo Client's `useQuery` and `useMutation` hooks, respectively.

### Queries

`FETCH_CART`, `FETCH_UNIQUE_FULFILLMENT_SCHEDULE_DATES`, `FETCH_FULFILLMENT_SCHEDULE_DATES`, `FETCH_CARTS`, `FETCH_REPORT_JOBS`, `QUERY_GQL_BREEDS`, `QUERY_GQL_INGREDIENTS`, `QUERY_GQL_WELLNESS_GOALS`, `QUERY_GQL_RECIPES`, `QUERY_GQL_PAYMENTS`, `QUERY_GQL_PAYMENT`, `QUERY_GQL_TERMS`, `QUERY_GQL_TERM`, `QUERY_GQL_PAYMENT_METHODS`, `QUERY_GQL_PAYMENT_METHOD`, `QUERY_GQL_ROUTE_SCHEDULES`, `QUERY_GQL_ZIP_CODES`, and `QUERY_GQL_ZIP_CODE`.

### Mutations

`WRITE_CART`, `CREATE_PAYMENT_BATCH`, `CREATE_SHIPMENT_LIST`, `CREATE_SHIPMENT_LINE_ITEMS_PREVIEW_JOB`, and `CREATE_SHIPMENT_LINE_ITEMS_REPORT_JOB`.

---

## React Components and Hooks

### StyledComponentsRegistry

```tsx
export default function StyledComponentsRegistry({ children }: { children: React.ReactNode }) {
  // implementation
}
```

- Description: A component that manages the inclusion of server-side rendered styles for styled-components, enabling them to be rehydrated on the client.
- Parameters:
  - `children`: React nodes to be wrapped within the `StyleSheetManager`.
- Usage: Intended for use with Next.js's Server Component API (`'use client'`) to handle server-inserted HTML through `useServerInsertedHTML` hook.

### useBreeds

```tsx
export default function useBreeds() {
  const { data } = useQuery(QUERY_GQL_BREEDS);
  return { breeds: data?.fetchBreeds || [] };
}
```

- Description: A custom React hook to fetch breeds using the GraphQL `QUERY_GQL_BREEDS` query.
- Returns: An object containing `breeds`, which is an array of breed data or an empty array if no data is available.

### useContinueHandler

```tsx
export default function useContinueHandler() {
  // implementation
  return goToNext;
}
```

- Description: A custom React hook to handle the navigation for a multi-step subscription process. 
- Returns: A `goToNext` function to navigate to the next step based on the current path.

### useFulfillmentScheduleDates

```tsx
export default function useFulfillmentScheduleDates() {
  const { data } = useQuery(FETCH_FULFILLMENT_SCHEDULE_DATES);
  return {
    fulfillmentScheduleDates: data?.fetchFulfillmentScheduleDates || []
  };
}
```

- Description: A custom React hook to fetch fulfillment schedule dates using the GraphQL `FETCH_FULFILLMENT_SCHEDULE_DATES` query.
- Returns: An object containing `fulfillmentScheduleDates`, which is an array of dates or an empty array if no data is available.

[... (Other Hooks)](#other-hooks)

- Description: There are other custom hooks similar to `useBreeds` and `useFulfillmentScheduleDates` that are designed to fetch or mutate data using predefined GraphQL operations.
- Examples: `useIngredients`, `usePaymentBatch`, `usePaymentMethods`, `usePayments`, `useRecipes`, `useReportJobs`, `useRouteSchedules`, `useShipmentLineItemsPreviewJob`, `useShipmentLineItemsReportJob`, `useShipmentList`, `useTerms`, `useUniqueFulfillmentScheduleDates`, `useWellnessGoals`, `useZipCodes`.

---

## Utility and Helper Functions

### Session Cart Helpers

- `findOrCreateCart`: Function to retrieve the current session cart or redirect to the cart initialization endpoint.
- `getSessionCart`: Asynchronous function to get the current session cart from cookies.
- `PetPlateCart`: Type alias for a non-null or undefined return type of `findOrCreateCart`.

### Error Handling

- `handleMutationError`: Function to handle errors that occur during GraphQL mutations and set form errors accordingly.
- `GraphQLErrorResponse`: Type definition for responses containing GraphQL errors.

### Cookie Helpers

- `readCookie`: Isomorphic method to retrieve cookie values in both client and server environment.
- `CART_COOKIE_NAME`: Constant for the cookie name containing the cart ID.

### Scroll Utilities

- `scrollTo`: Function to smoothly scroll an element or window to the specified position and optionally execute a callback once the scroll is complete.

### SDK Helpers

- `sdk`: An instance of the GraphQL Client with predefined operations from `getSdk`.
- `AUTH_HEADER_NAME`, `persistCreds`, `retrieveCreds`: Constants and functions related to handling user authentication and credentials.

### Search Helpers

- `useSearchIndex`: A custom hook that provides handlers for sorting, filtering, and pagination in list views.

### Scroll Block

```tsx
export default function useScrollBlock(condition: boolean) {
  // implementation
}
```

- Description: A utility hook to conditionally block and unblock page scrolling based on the provided `condition`.
- Parameters:
  - `condition`: A boolean indicating whether the page scroll should be blocked.

---

## GraphQL Queries and Mutations (Detailed)

### Queries

Each query defined is a string literal wrapped in a `gql` template tag provided by 'Apollo Client'. The query is usually named after its functionality, e.g. `FETCH_CART` fetches cart-related data. Below are the detailed explanations of the GraphQL queries/hooks exported in the codebase:

- `FETCH_CART`: Fetches details of a specific shopping cart including line items data.
- `FETCH_UNIQUE_FULFILLMENT_SCHEDULE_DATES`: Retrieves a list of unique fulfillment schedule dates.
- `FETCH_FULFILLMENT_SCHEDULE_DATES`: Acquires a list of fulfillment schedule dates with details like delivery date, shipping day, status, and zip code.
- `FETCH_CARTS`: Retrieves a list of shopping carts, used for administrative or user profile layouts.
- `FETCH_REPORT_JOBS`: Fetches a list of reporting jobs for backend processing.
- `QUERY_GQL_BREEDS`: Gets a list of animal breeds (specific to PetPlate services).
- `QUERY_GQL_INGREDIENTS`: Retrieves details on various food ingredients available.
- `QUERY_GQL_WELLNESS_GOALS`: Fetches wellness goals that can be set within the PetPlate service.
- `QUERY_GQL_RECIPES`: Acquires recipes information.
- `QUERY_GQL_PAYMENTS`: Lists payments.
- `QUERY_GQL_PAYMENT`: Provides detailed information on a specific payment.
- `QUERY_GQL_TERMS`: Fetches terms and conditions.
- `QUERY_GQL_TERM`: Retrieves a specific term by ID.
- `QUERY_GQL_PAYMENT_METHODS`: Gets a list of payment methods.
- `QUERY_GQL_PAYMENT_METHOD`: Fetches a specific payment method by ID.
- `QUERY_GQL_ROUTE_SCHEDULES`: Retrieves route schedules, likely used for delivery planning.
- `QUERY_GQL_ZIP_CODES`: Gets a list of zip codes, potentially for delivery areas.
- `QUERY_GQL_ZIP_CODE`: Fetches a specific zip code by ID.

### Mutations

Similar to queries, mutations are also wrapped in a `gql` template tag. They are designed to execute actions that modify data on the backend. Here are the details:

- `WRITE_CART`: Mutation to create or update a shopping cart.
- `CREATE_PAYMENT_BATCH`: Generates a new payment batch for processing transactions.
- `CREATE_SHIPMENT_LIST`: Creates a shipment list likely used for coordinating deliveries.
- `CREATE_SHIPMENT_LINE_ITEMS_PREVIEW_JOB`: Initiates a job to preview shipment line items, perhaps for administrative confirmation before processing.
- `CREATE_SHIPMENT_LINE_ITEMS_REPORT_JOB`: Starts a reporting job for shipment line items, probably for backend processing and auditing.

