## Manual Processes Overview

- **Recovering Payment Batches**: Addressing unexpected failures in payment batches.
- **Manual Sync of Subscription Contracts**: Occurs when an application leak fails to sync a subscription contract on reactivation or resuming a subscription.
  - Leak likely resolved in the last release, but uncertainty remains.
  - An easy script is available for manual syncing.
- **List of Complex Processes and Open Issues**: Areas requiring significant investigation or knowledge transfer.
  - Yapo and invoicing issues, tech debt.
  - Native view order creation issues with validating user inputs.
  - Subscription coupon logic bugs.
  - Shopify integration improvements.
  - Integration with Chewy and handling third-party services.

## Subscription Workflow and Troubleshooting

### Subscription Contract Synchronization

During reactivation of a subscription:

1. The subscription state changes in the database.
2. A new Shopify subscription contract is created and synced.
3. Coupons are individually synced due to Shopify error handling.
4. Troubleshooting involves Shopify's own administrative interface for source-truth data and refund functionalities.

### Webhooks and Order Creation

- Orders are created through Shopify's webhook payload, converting the webhook into an order and subscription in Pet Plate's system.
- Errors or sync issues with webhooks must be manually reconciled through an auditing script.

### Testing and Debugging Tools

For debugging purposes, tools such as RapidAPI are used for performing GraphQL requests, which help validate queries and mutations both in the Rails app and Shopify API.

## Shopify Integration Specifics

- Most front-end GraphQL calls target the Rails API, with Shopify's Storefront API accessible for unauthenticated requests (e.g., fetching products).
- Account changes that involve payment methods must communicate with Shopify's Admin API using a custom Ruby client (`ShopifyAPI` gem).

## GraphQL and API Interaction

- **Queries and mutations** in the Next.js app are primarily targeting Rails API.
- **GraphQL Storefront API**: Used sparingly within the Pet Plate app; public-facing and covers non-sensitive data.
- **Admin API**: Contains sensitive data such as payment methods, orders, and subscription contracts.

## Technical Concerns

- **Refunds**: Must be performed in Shopify's native interface.
- **Order Changes**: Recommended to be made in Pet Plate's app view to ensure proper syncing with Shopify.
- **Webhook Limitations**: Currently, only supports one-way syncing from the Pet Plate app to Shopify.

## Front-end Integration

- **Hydrogen**: Shopify's framework used in next.js app.
- **Internal UI Components**: Some components are static and need updates within the codebase, e.g., product images.
- **API Client**: The custom API client (`ShopifyAPI` gem in Rails) handles back-end Shopify API calls.

### React/Hydrogen Hooks

- Utilized within the subscription workflow for integrating the Shopify cart.
- Improves handling checkout processes in the front-end.

## Access and Permissions

- Limited access to view orders and products within Shopify's admin interface; team members need permissions from lead personnel.

## Development Practices

- **PR Process**: Squash merges for cleaner commit history.
- **Syncing with Shopify**: Primarily handled during order creation or updates within the app, not directly through Shopify.

## Unresolved Questions and Future Work

- Two-way syncing between the Pet Plate and Shopify database remains a challenge.
- Potential need for real-time error capturing and troubleshooting mechanisms; currently, inconsistency in reproducing issues.
