# Petplate Next.js Components Documentation

This documentation details the usage and structure of Next.js components found in the Petplate project. It provides explanations for individual components as well as examples of how to use them within the codebase.

## Table of Contents

- [useReportJobs Component](#usereportjobs-component)
- [useFulfillment Component](#usefulfillment-component)
- [usePaymentBatch Component](#usepaymentbatch-component)
- [useAdminPage Component](#useadminpage-component)
- [useMainNavContent Component](#usemainnavcontent-component)
- [SignUp Component](#signup-component)
- [LoginPage Component](#loginpage-component)
- [ForgotPasswordPage Component](#forgotpasswordpage-component)
- [ChangePasswordPage Component](#changepasswordpage-component)
- [VerifyAccountPage Component](#verifyaccountpage-component)
- [AuthProvider Component](#authprovider-component)
- [Head Component](#head-component)
- [WebLayout Component](#weblayout-component)
- [SubscriptionDialog Component](#subscriptiondialog-component)
- [useWeightPage Component](#useweightpage-component)
- [usePlanPage Component](#useplanpage-component)
- [useActivityLevelPage Component](#useactivitylevelpage-component)
- [useFoodSensitivitiesPage Component](#usefoodsensitivitiespage-component)
- [useGenderPage Component](#usegenderpage-component)
- [useCheckoutPage Component](#usecheckoutpage-component)
- [useWaistlinePage Component](#usewaistlinepage-component)
- [useAgePage Component](#useagepage-component)
- [useRecipePage Component](#userecipepage-component)
- [useTreatsPage Component](#usetreatspage-component)
- [SubscriptionFlowPage Component](#subscriptionflowpage-component)
- [NotFoundErrorPage Component](#notfounderrorpage-component)
- [HomePage Component](#homepage-component)
- [HeadReplacement Component](#headreplacement-component)
- [Providers Component](#providers-component)
- [Singleton Page Components](#singleton-page-components)
- [Components](#components)
   - [SingleScheduleRules](#singleschedulerules)
   - [ScheduleRules](#schedulerules)
   - [EditMealPlanRecomendations](#editmealplanrecomendations)
   - [SingleMealPlanRecomendations](#singlemealplanrecomendations)
   - [SingleMealPlanRecommendations](#singlemealplanrecommendations)
   - [MealPlanRecommendations](#mealplanrecommendations)
   - [EditSchedules](#editschedules)
   - [Schedules](#schedules)
   - [EditMealPlanRecommendableProducts](#editmealplanrecommendableproducts)
   - [SingleMealPlanRecommendableProducts](#singlemealplanrecommendableproducts)
   - [MealPlanRecommendableProducts](#mealplanrecommendableproducts)
   - [Subscriptions](#subscriptions)
   - [AdminLayout and RootLayout](#adminlayout-and-rootlayout)
   - [Home](#home)
   - [Metafields](#metafields)
   - [Breeds](#breeds)
   - [BackgroundJobs](#backgroundjobs)
2. [Hooks](#hooks)
   - [useRouteSchedules](#userouteschedules)
   - [useShipmentLineItemsPreviewJob](#useshipmentlineitemspreviewjob)
   - [useBreeds](#usebreeds)
   - [useCartHandling](#usecarthandling)
   - [useFulfillmentScheduleDates](#usefulfillmentscheduledates)
   - [useIngredients](#useingredients)
   - [useReportJobs](#usereportjobs)
   - [usePaymentBatch](#usepaymentbatch)
   - [useRecipes](#userecipes)
   - [useShipmentLineItemsReportJob](#useshipmentlineitemsreportjob)
   - [lineItemMapper](#lineitemmapper)
   - [useTerms](#useterms)
   - [usePaymentMethods](#usepaymentmethods)
   - [useUniqueFulfillmentScheduleDates](#useuniquefulfillmentscheduledates)
   - [useShipmentList](#useshipmentlist)
   - [useWellnessGoals](#usewellnessgoals)
   - [usePayments](#usepayments)
3. [GraphQL Queries and Mutations](#graphql-queries-and-mutations)
4. [Utilities and Miscellaneous](#utilities-and-miscellaneous)
   - [Styled Components Registry](#styled-components-registry)
   - [Admin Filter Utilities](#admin-filter-utilities)

## useReportJobs Component

The `useReportJobs` component is a custom hook that returns a list of report jobs and a corresponding method to invoke an action on these report jobs.

### Usage

```jsx
import useReportJobs from 'src/lib/use-report-jobs';

const Page = () => {
  let reportJobs = [];
  try {
    const resp = useReportJobs();
    reportJobs = resp.reportJobs;
  } catch (err) {}

  // Render reportJobs with corresponding action button...
};
```

### Implementation

The `useReportJobs` hook uses either Apollo or SDK to query the backend for report job data and returns an array of job objects along with a method to perform operations (e.g., delete, download) on these jobs.

## useFulfillment Component

The `useFulfillment` component handles fulfillment schedule dates for shipments.

### Usage

```jsx
import useFulfillment from 'src/lib/use-fulfillment-schedule-dates';

const Page = () => {
  let fulfillmentScheduleDates = [];

  try {
    const hook = useFulfillment();
    // The `fulfillmentScheduleDates` can be used to render a schedule calendar
    fulfillmentScheduleDates = hook.fulfillmentScheduleDates;
  } catch (err) {}
  
  // Render the schedule...
};
```

### Implementation

Similar to `useReportJobs`, this hook fetches scheduling data related to shipment line items and provides methods to manipulate this data.

## usePaymentBatch Component

The `usePaymentBatch` component is used to interact with payment batch-related data.

### Usage

```jsx
import usePaymentBatch from 'src/lib/use-payment-batch';

const Page = () => {
  let paymentBatchData = [];
  let createPaymentBatch;

  try {
    const hook = usePaymentBatch();
    paymentBatchData = hook.paymentBatchData;
    createPaymentBatch = hook.createPaymentBatch;
  } catch (err) {}

  // UI logic with paymentBatchData and createPaymentBatch method...
};
```

### Implementation

The hook provides access to payment batch data, along with methods to create and manage these batches, typically interacted with in the admin side of the application for accounting and financial tracking.

## useAdminPage Component

The `useAdminPage` component is designed for fetching a single page of content by its slug from the CMS.

### Usage

```jsx
import { useAdminPage } from 'src/lib/use-admin-page';

const Page = async ({ params: { slug } }) => {
  const data = await useAdminPage(slug);

  if (!data?.docs?.[0]) {
    // Handle page not found error
  }

  // Render the page content...
};
```

### Implementation

It performs a network request to fetch a specific page's content based on a slug and returns the relevant data for rendering that page. In case the page is not found, it provides an error handling mechanism.

## useMainNavContent Component

The `useMainNavContent` component retrieves navigation data for the main navigation of the site.

### Usage

```jsx
import MainNav, { useMainNavContent } from '@petplate/ui/components/MainNav';

function WebLayout({ children }) {
  const navData = useMainNavContent();

  return (
    <MainNav navData={navData}>
      {children}
    </MainNav>
  );
}
```

### Implementation

This component fetches the navigation structure from the server and provides it to the `MainNav` component which is then responsible for rendering the main navigation based on this data.

## SignUp Component

The `SignUp` component allows users to sign up for an account.

### Usage

```jsx
import SignUp from './components/SignUp';

const SignUpPage = () => {
  // Retrieve signup data...
  return <SignUp {...data} />;
};
```

### Implementation

This component contains a form which collects user information such as email and password for account creation. Upon submission, it calls the backend API to create a new user account.

## LoginPage Component

The `LoginPage` component facilitates user login process.

### Usage

```jsx
import LoginPage from './components/Login';

export default function Login() {
  const data = // Fetch login data...
  return <LoginPage {...data} />;
}
```

### Implementation

Similar to the `SignUp` component, `LoginPage` consists of a form for login. It gathers credentials and sends them to the backend to authenticate the user, then handles the session accordingly.

## ForgotPasswordPage Component

The `ForgotPasswordPage` component allows users to request a password reset link.

### Usage

```jsx
import ForgotPasswordPage from './components/ForgotPassword';

export default function ForgotPassword() {
  const data = // Fetch data needed for password recovery...
  return <ForgotPasswordPage {...data} />;
}
```

### Implementation

Upon providing an email address, this component triggers a backend process to send a password reset link to the user’s email.

## ChangePasswordPage Component

The `ChangePasswordPage` component is used when a user wants to change their password using a token they received via email.

### Usage

```jsx
import ChangePasswordPage from './components/ChangePassword';

export default function ChangePassword() {
  // Fetch necessary data for password change...
  return <ChangePasswordPage {...data} />;
}
```

### Implementation

It renders a form where users enter their new password and submit the form alongside the token to update the password.

## VerifyAccountPage Component

The `VerifyAccountPage` component is used to handle the account verification process.

### Usage

```jsx
import VerifyAccountPage from './components/VerifyAccount';

export default function VerifyAccount() {
  const data = // Fetch account verification data...
  return <VerifyAccountPage {...data} />;
}
```

### Implementation

It interacts with backend services to verify user accounts based on a token that was sent via email.

## AuthProvider Component

The `AuthProvider` component is a context provider that wraps the application and provides authentication-related data and functions to the child components.

### Usage

```jsx
import AuthProvider from '@/lib/authProvider';

function App({ Component, pageProps }) {
  return (
    <AuthProvider>
      <Component {...pageProps} />
    </AuthProvider>
  );
}

export default App;
```

### Implementation

This component often works with authentication utilities like JWT to manage user session and state effectively across the application.

## Head Component

The `Head` component is used to modify the HTML `<head>` section on a given page.

### Usage

```jsx
import Head from '@/components/Head';

export default function SomePage() {
  return (
    <>
      <Head />
      {/* Page Content */}
    </>
  );
}
```

### Implementation

It manipulates the `<head>` of the document by adding or modifying tags such as title, meta tags, and links for SEO and page presentation on browsers.

## WebLayout Component

The `WebLayout` component is a higher-order component used to wrap pages for consistent layout.

### Usage

```jsx
import WebLayout from '@/components/WebLayout';

function HomePage() {
  return (
    <WebLayout>
      {/* Home page content... */}
    </WebLayout>
  );
}

export default HomePage;
```

### Implementation

This component controls the layout by including common UI elements such as headers, footers, and navigation bars.

## SubscriptionDialog Component

The `SubscriptionDialog` component handles the subscription dialog logic for users' subscription management.

### Usage

```jsx
import SubscriptionDialog from '@/components/subscription/SubscriptionDialog';

const ProfilePage = () => {
  return (
    <SubscriptionDialog>
      {/* Profile page content... */}
    </SubscriptionDialog>
  );
};

export default ProfilePage;
```

### Implementation

It provides an interactive dialog that allows users to manage their subscriptions like pausing, canceling, or updating their plans.

## useWeightPage Component

The `useWeightPage` component assists in managing pet weight-related data for the subscription process.

### Usage

```jsx
import useWeightPage from '@/lib/useWeightPage';

const WeightPage = () => {
  const data = useWeightPage();
  // Render weight selection and management related content...
  return <WeightComponent {...data} />;
};

export default WeightPage;
```

### Implementation

It fetches and manages pet weight data, allowing users to set or update their pet's weight during the subscription process.

## Singleton Page Components

The following components are singular in nature and represent unique pages on the Petplate platform:

- `usePlanPage`
- `useActivityLevelPage`
- `useFoodSensitivitiesPage`
- `useGenderPage`
- `useCheckoutPage`
- `useWaistlinePage`
- `useAgePage`
- `useRecipePage`
- `useTreatsPage`
- `SubscriptionFlowPage`
- `NotFoundErrorPage`
- `HomePage`
- `HeadReplacement`
- `Providers`

- # Code Documentation: Shop Administration Features

The following documentation provides thorough details on various administration features for an online shop management system implemented using React, Next.js, and related technologies. The provided code consists of various components, interfaces, services, and utilities that form the back-office functionality of an e-commerce platform.

---



---

## Components

### SingleScheduleRules

The `SingleScheduleRules` component is responsible for managing individual schedule rules based on the provided `id`. This includes fetching and displaying the schedule rule data, and providing navigation back to the main schedule rules list.

#### Usage:

```jsx
<SingleScheduleRules params={{ id: 1 }} />
```

#### Props:

- `params`: An object containing:
  - `id`: The unique identifier of the schedule rule.

---

### ScheduleRules

List out all the the schedule rules with abilitity to View, Edit or create a new one.

### EditMealPlanRecomendations

Handles the form submission for editing meal plan recommendations. It consists of several inputs and state management to handle form operations.

---

### SingleMealPlanRecomendations

A form to create new meal plan recommendations, identical in structure to editing recommendations.

---

### MealPlanRecommendations

Handles displaying a list of meal plan recommendations with the ability to sort and perform bulk operations to items. 

### EditSchedules

This functional component is used to modify the existing shipment schedule by providing a form to change details such as the shipping date, shipment list, and so on.

---

### Schedules

Display a list of schedules with interactive funcationalities including downloading reports and manage shipment.

### EditMealPlanRecommendableProducts

Allows editing of individual recommendable products by presenting a form to modify details like the product name, type, and status.

---

### SingleMealPlanRecommendableProducts

Renders a form for creating new recommendable products similar in structure and functionality to editing recommendable products.

### MealPlanRecommendableProducts

Lists all meal plan recommendable products, each with options to view or edit further details.

### Subscriptions

Provides an interface for editing particular subscriptions including their plans, meals, and add-ons.

---

### AdminLayout and RootLayout

Layout wrappers for the admin application and React root application respectively, providing a consistent structure to which individual pages can be populated.

---

### Home

A basic home component that shows a placeholder message.

---

### Metafields

A component for listing metafields and offering edit capabilities.

### Breeds

Handles the CRUD operations for breeds information on the Admin panel.

### BackgroundJobs

Provides a quick access button to the Sidekiq background jobs dashboard.

---

## Hooks

### useRouteSchedules

Fetches and returns a list of route schedules.

### useShipmentLineItemsPreviewJob

Creates a preview job for shipment line items, returning job details and helper functions.

### useBreeds

Retrieves all available dog breeds for the meal plan recommendation.

### useCartHandling (writeCart, fetchCart)

Serves cart-based operations, including the retrieval and update of cart data.

### useFulfillmentScheduleDates

Gets a list of unique fulfillment schedule dates for ordering.

### useIngredients

Fetches all available ingredients for the meal plan recipe.

### useReportJobs

Retrieves and provides access to job report details.

### usePaymentBatch

Creates a new payment batch upon function call.

### useRecipes

Retrieves a list of available recipes for meal plan.

### useShipmentLineItemsReportJob

Creates a job meant for generating shipment line items report.

### lineItemMapper

Utility for updating line items in a shopping cart based on changes or new additions.

### useTerms

Fetch and provide details of various terms, definitions or glossary related to the pet food business.

### usePaymentMethods

Handles retrieval and operations of customer payment methods.

### useUniqueFulfillmentScheduleDates

Fetches and provides unique dates available for the fulfillment schedules.

### useShipmentList

Generates a new shipment list with a specific payload.

### useWellnessGoals

Fetches and returns a list of wellness goals for pets.

### usePayments

Handles fetching payment transactions and details of individual payments.

---

## GraphQL Queries and Mutations

- Graphql queries and mutations are provided in a separate document to describe the data fetching and updating operations for various data entities like cart, breeds, ingredients, payment methods, etc.

---

## Utilities and Miscellaneous

### Styled Components Registry

Provides server-side rendering support for styled-components by attaching the stylesheet to the response.

### Admin Filter Utilities

Include utility functions to generate names for range, pattern, match, etc., for filtering operations on the administration pages. It also provides default values and options for comparison and filter components.
