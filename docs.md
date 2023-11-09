# Documentation

## Overview

The given codebase implements classes for a system managing various entities related to retail operations, such as payments, shipping, user management, and reports, among others. Below is the detailed documentation organized by models and modules, describing purpose, relationships, validations, scopes, and other functionalities.

### Models

#### `PaymentBatch`

The `PaymentBatch` model represents a group of payment transactions processed together. It holds information about the state of the batch, start and end times, due date, and associated shipping dates.

- Associations:
  - `has_many :payment_batch_entries`, which are individual entries representing payment transactions within the batch.

- States: It uses a state machine with states `:created`, `:processing`, `:finished`, `:error`.

#### `ReportJob`

The `ReportJob` model handles background processing for generating reports. It tracks the progress, duration, completion status, and potential errors during report generation.

- Associations:
  - `belongs_to :user`, indicating which user requested the report.
  
- States: States include `:enqueued`, `:started`, `:completed`, `:failed`.

#### `Subscription`

This model represents a user's subscription plan for product delivery. It maintains state, plan frequency, meal counts, scheduled shipping dates, and associated payments.

- Associations: 
  - `belongs_to :payment_method`
  - `belongs_to :pet`
  - `belongs_to :current_plan`, which is a `BoxVariant` representing the current subscription plan.
  
- States: The states are `:cart`, `:active`, `:paused`, `:canceled`.

#### `Pet`

The `Pet` model holds detailed information about a customer's pet including breed, birth date, weight, and serving size.

- Associations:
  - `belongs_to :primary_breed`, `belongs_to :secondary_breed`: Associations to `Breed` model to capture breed information.
  - `has_many :pet_sensitivities`: Associations to `Ingredient` through sensitivities.
  
- Validations: It includes validations for presence and uniqueness of various attributes e.g., primary_breed_id, etc.

#### `PaymentMethod`

The `PaymentMethod` contains data related to a user's payment method like card details, API data, and state (active or inactive).

- Associations:
  - `belongs_to :owner`, the user owning this payment method.
  - `has_many :payments` representing payments made using this payment method.
  
- States: Includes `:primary`, `:active`, `:inactive`, `:risky`.

#### `BoxVariant` & `MealVariant`

Models representing different product offerings and their variants. 

- Associations: `BoxVariant` has many `MealVariant`, and vice versa.
- Validations: Each has validations for attributes like price, ID, and SKU.

#### `User`

This model extends the `Devise` gem for user authentication and implements roles and permissions.

- Associations:
  - `has_and_belongs_to_many :roles`, representing the roles assigned to the user for authorization purposes.
  - `has_many :pets`, `has_many :shipping_addresses`, `has_many :payment_methods`: Associations to other domain entities.

### Modules

#### `Importable`

A concern for facilitating import processes, providing a scoped and consistent way of defining import-related attributes.

#### `IdentityMap`

A utility module that allows fetching records with minimized redundant database queries, improving performance for operations like bulk inserts or updates.

#### `IsSku`

A shared concern across product-related models implements a mechanism to handle SKU generation and uniqueness.

#### `ActAsProductVariant`

This concern is included in product variant models to encapsulate the shared logic for handling product variant data, statuses, etc.

#### `HasLogEvents`

A module for models that should log changes or state transitions, facilitating audit trails.

#### `ActAsProduct`

Provides shared business logic for product related models. It encapsulates common functionalities, like validation, state transitions, and listing options.

#### `Facade`

For constructing an object's representation in a simplified format, often used to aggregate and transform data for external APIs or front-end views.

#### `AsJsonWithAliases`

Allows models to represent themselves as JSON with support for alias attributes, providing a consistent JSON structure even if database column names change.

### Scopes

The code provides several predefined scopes for querying collections of records based on certain criteria, such as `.active`, `.with_payment_batch_entry_counts`, `.serviced`, `.started`, `.completed`, etc.

### Validations

Models include validations to ensure data integrity and business rules are enforced. Some examples are uniqueness of SKUs, existence of associated records, and custom validations for business-specific constraints.

### Misc

In addition to models and modules, the codebase employs some design patterns and practices that are worth noting:

- Use of `friendly_id` for human-readable URLs.
- State machines for managing the lifecycle of entities like `PaymentBatch` or `Subscription`.
- Batch-loading for performance optimization in data retrieval.
- Integrations with external services via API wrappers.

---

## Additional Notes

- This documentation aims to provide a high-level overview, but it might not cover all the intricate details nor all the interconnected relationships between models.
- The use of concerns and modules promotes DRY (Don't Repeat Yourself) principles and encapsulation, making it clear that certain functionalities are shared across different models.
- Since this is a high-level description, it does not cover method-level documentation for the code. Each method within models should have individual documentation explaining its purpose, parameters, return values, and any side effects.
- The documentation assumes familiarity with `ActiveRecord` models and Rails conventions regarding validations, associations, and callbacks.


# Fulfillments & Subscriptions Module Documentation

The provided code includes various modules, classes, and jobs related to managing fulfillments and subscriptions for an e-commerce platform, specifically for pet-related products. The code seems to be written in Ruby and is likely part of a larger Ruby on Rails application.

## Modules and Classes Summary

- **Fulfillments**: Related to shipping, handling, and delivery of products.
- **Types**: Defines various base and complex data types and sets.
- **Nift**: Integrates with Nift services, likely for marketing or referral purposes.
- **Customers**: Deals with user profile data and operations such as updating addresses or pausing subscriptions.
- **Pets**: Related to pet information management in user profiles.
- **CommandsV1**: Contains commands for processing various operations like order placements or subscription updates.
- **Products**: Concerned with product details, particularly related to serving suggestions and quantity calculations.
- **Invoices**: Responsible for generating invoice information/documents.
- **Vercel**: Involves interaction with Vercel deployments, possibly related to continuous integration/deployment tasks.
- **Dates**: Provides utility functions for handling dates.
- **Compressor**: Pertains to file compression and extraction.
- **HerokuReviewApp**: Specific to managing Heroku review apps, potentially used as part of the deployment process.

## Detailed Documentation

Below is the detailed documentation for key functions and classes found in the codebase. Note that actual functionality may differ, and this documentation assumes the intent based on code analysis.

### Fulfillments Module

#### `ShipmentProcessJob`
Runs as a background job, creating and processing a shipping list for products. These are enqueued in a Sidekiq queue, ensuring jobs run in the background and do not block the main application process.

```ruby
module Fulfillments
  module Jobs
    class ShipmentProcessJob
      # ...
    end
  end
end
```

#### `CommandBase`
Serves as the base class for command-style service objects used to encapsulate business logic related to operations like pausing or unpausing subscriptions.

```ruby
module CommandsV1
  class CommandBase
    # ...
  end
end
```

### Types Module

#### `BaseSet`
Defines a generic set collection that can hold items of a specific type.

```ruby
module Types
  class BaseSet
    # ...
  end
end
```

### Nift Module

#### `Client`
Handles communication with the Nift service, primarily around creating orders associated with Nift campaigns or referral programs.

```ruby
module Nift
  class Client < BaseClient
    # ...
  end
end
```

### Customers Module

#### `Profile`
Contains information relating to a customer's profile.

```ruby
module Customers
  class Profile < Types::ValueObject
    # ...
  end
end
```

#### `Listener`
Responds to events such as changes in user profiles or other customer-related activities.

```ruby
module Customers
  class Listener
    # ...
  end
end
```

### Pets Module

#### `FeedingGuideline`
Calculates feeding guidelines based on pet attributes like weight, activity, and the amount of food provided.

```ruby
module Pets
  class FeedingGuideline
    # ...
  end
end
```

### CommandsV1 Module

#### `PauseSubscription`
Handles the business logic and operations associated with pausing a pet subscription.

```ruby
module CommandsV1
  class PauseSubscription < CommandBase
    # ...
  end
end
```

### Products Module

#### `ServingRecommendation`
Determines recommended serving quantities for various pet products, potentially useful when suggesting appropriate quantities for pet treats.

```ruby
module Products
  class ServingRecommendation < Types::ValueObject
    # ...
  end
end
```

### Invoices Module

#### `PdfGenerator`
Generates PDF invoices that can be shared with customers or used for accounting purposes.

```ruby
module Invoices
  class PdfGenerator
    # ...
  end
end
```

### Vercel Module

#### `Client`
Interfaces with the Vercel platform, perhaps for deploying the application or managing the runtime environment.

### Various Utility Functions

- **Dates**: Provides tools to convert dates to/from specific encodings.
- **Compressor**: Facilitates compression and decompression of files, possibly for data exchange or storage purposes.

### HerokuReviewApp

Ensures proper configuration and environment setting for review apps deployed on the Heroku platform, which are ephemeral environments used for testing and validating changes before production.

## Conclusion

This extensive documentation provides an overview of various modules and classes within the application, offering insight into how they contribute to the general functionality regarding fulfillment processes, customer management, and interaction with external services and utility functions.

### Usage

To make use of the functions provided by these modules, instantiate the corresponding classes or call the methods as needed, passing appropriate parameters as defined by their contracts or method signatures. Ensure background jobs are enqueued and processed by the Sidekiq server for asynchronous execution. Utilize the utility classes and methods to handle typical tasks like date manipulation and file compression.

**Note**: Keep the context and mission of the overarching application in mind while integrating these modules and always refer to actual business requirements and intended application behavior.


# Subscriptions Module Documentation

This documentation covers the `Subscriptions` module, which consists of several classes and methods to handle various aspects of subscription management within a system. This module is part of a larger application presumably dealing with customer subscriptions, meal plans, diet recommendations, etc.

## Classes and Modules

### Subscriptions::Listener

`Subscriptions::Listener` is a listener class that includes `Wisper::Publisher` to subscribe to certain events related to subscription processes. It is responsible for handling events like successful order charge or failed charge and thereby initiating particular actions like incrementing renewal counts or pausing subscriptions.

**Methods:**

- `initialize(subscription)`: Constructor that takes a `subscription` object and registers listeners for specific events.

**Events Handled:**

- `order_charged_successfully(charge_id)`: Increments the renewal count and broadcasts a successful renewal event.
- `order_charge_failed(charge, error_message, exception)`: Handles subscription renewals that failed to process which can potentially lead to subscription pausing depending on the failure count.

### Subscriptions::Statistics

`Subscriptions::Statistics` module calculates statistics for subscriptions based on their states by a given date.

**Methods:**
 
- `stats_by_date(end_date)`: Calculates and returns subscription statistics for a given `end_date`.
  
### Subscriptions::ChangeMealsStockImporter

`Subscriptions::ChangeMealsStockImporter` is responsible for updating subscription meal line items based on stock availability from a CSV file input.

**Methods:**

- `initialize(csv_path)`: Constructor taking a path to the CSV file.
- `validate`: Validates the CSV file content.
- `call`: Processes the CSV file and updates subscriptions accordingly.
- `print_results`: Outputs the results to the log.

### Subscriptions::LineItem
`Subscriptions::LineItem` is a value object representing a line item in a subscription order. It includes attributes such as SKU, quantity, price, type, and if it's recurring.

### Subscriptions::LineItemSet
`Subscriptions::LineItemSet` is a collection of `Subscriptions::LineItem` objects and includes methods for deserialization, initialization, and getting a subset of recurring items.

### Subscriptions::Commands::ChangePhoto
Handles the command to update a pet's photo within a subscription.

### Subscriptions::Commands::RemovePhoto
Handles the command to remove a pet's photo from a subscription.

### Subscriptions::Commands::IgnoreNewPlanRecommendations
Handles the command to ignore new plan recommendations in a subscription.

### Subscriptions::Commands::ChangePlan
Handles the command to change a subscription plan based on provided SKU and admin mode flag.

### Subscriptions::Commands::HideSubscription
Handles the command to set a subscription as hidden or unhidden.

### Subscriptions::Jobs::UpdateDailySubscriptionStatsJob
A background job that updates subscription statistics on a daily basis.

### Subscriptions::LineItemMapper
Responsible for mapping subscription line items to different categories, such as meals or addons.

### Subscriptions::LegacyMapper
Includes various class methods to aid in old-to-new system migrations involving fulfillment schedules and billing information.

### Subscriptions::Models::LineItemsAttribute
ActiveRecord type extension to assist in the serialization/deserialization process of `LineItemSet` objects.

### Subscriptions::AutomaticRescheduler
A service to automatically reschedule subscription dates if the last order's shipping date is too close to the next scheduled date.

### Subscriptions::Commands::ChangePhoto
Handles the operation of changing the photo in a subscription based on the subscription number and provided photo data.

### Subscriptions::Commands::RemovePhoto
Manages the removal of photos in a subscription based on the given subscription number.

### Subscriptions::Commands::IgnoreNewPlanRecommendations
Updates the subscription to ignore new plan recommendations based on the subscription number and a flag indicating whether to ignore or not.

### Subscriptions::Commands::ChangePlan
Allows changes to a subscription's plan by specifying the subscription number, selected plan SKU, and whether it's in admin mode or not.

### Subscriptions::Commands::HideSubscription
Enables or disables visibility of a subscription by providing the subscription number and a flag to hide or unhide the subscription.

### Subscriptions::Jobs::UpdateDailySubscriptionStatsJob
Performs daily updates of subscription statistics.

## Usage

Each class and module offers functionalities that intertwine to form a cohesive subscription management system. This system performs tasks such as updating meal plans depending on stock availability, handling subscription photo assets, reacting to subscription changes, and maintaining subscription health through statistics and automatic rescheduling.

When using this module, one should be aware of the specific roles and responsibilities of each class and method to effectively integrate them into the larger application context.

# PetPlate Billing and Webhook Handling Documentation

This documentation aims to provide a comprehensive guide on the implementation and functionalities of the PetPlate billing system and webhook handling. The codebase is organized into multiple modules that cater to different aspects of the billing processes and webhook events.

## Billing

### Payment Gateway

The `PaymentGateway` module is responsible for abstracting the payment gateway logic. It allows the system to interact with various payment service providers like Stripe, Shopify Payments, Merchant Ware and so on.

#### Payment Gateway Providers

- **Stripe**: Integration with Stripe's payment services.
- **ShopifyPayment**: Handles Shopify's payment functionalities.
- **MerchantWare**: Integration with MerchantWare's processing services.
- **PetPay**: A custom, mocked-up payment provider used for testing.

The gateways provide unified interfaces to create charges, create refunds, and manage payment methods.

##### Charge

Handles the creation of a transaction charge. Must implement `capture` method for actual charge processing.

##### Refund

Handles refund processing for a transaction. Must implement a method to actually process refund with the corresponding payment gateway.

##### Payment Method

Handles the customer payment methods details, such as creating and updating payment information.

#### Operators

Operators are responsible for handling specific actions such as charging the customer's card (`ChargeOperator`), creating payment intents (`PaymentIntentOperator`), and general operations (`Operator`).

#### Errors

Custom error classes for handling gateway specific errors such as `CardError` and `RiskyCardError`.

### Jobs

`Billing::Jobs` namespace contains several background jobs to handle asynchronous tasks in the billing process.

#### PaymentBatchJob

This job is responsible for creating payment batches which help process multiple orders related to upcoming shipments. It handles the orchestration of order creation, charging, updating subscriptions, and more.

#### RefundInvoiceJob

Handles the creation of invoices associated with refunds asynchronously.

#### SyncStripeCustomerJob

This job synchronizes customer information with Stripe's records.

#### StripeWebhookJob

Processes Stripe events received through webhooks.

## Webhooks

The `Webhooks` module manages the incoming webhook events from different third-party services like Shopify.

### Shopify Webhook Handlers

Each Shopify event (e.g., `shop/update`, `app/uninstalled`, `orders/create`, `subscription_contracts/create`, etc.) is handled by a corresponding job. The jobs will process the event data and perform necessary actions such as creating records, updating data, or complex operations like syncing customers and orders.

#### OrdersCreateJob

Processes the `orders/create` event from Shopify. It handles saving order information and associating the order with the correct subscription and customer entities.

## ActiveJob Queue

The system utilizes ActiveJob for asynchronous job execution. Each webhook event and billing job is processed in the background with the help of ActiveJob.

#### Sidekiq Configuration

The codebase is configured with Sidekiq for queue backend. Jobs are enqueued with unique options and other settings to ensure efficient processing. Sidekiq batches are also used to group related jobs.

#### Retry Mechanisms

For robustness, the jobs have retry mechanisms in place, ensuring that transient issues do not lead to failures in processing events and transactions.

#### Scheduling

Some jobs are scheduled to run at regular intervals, such as `RegenerateInstagramToken` and `SyncAllStripeCustomersJob`. This ensures up-to-date records and functioning integrations.

## Note Attributes Parsing

Webhooks often include custom note attributes that need to be parsed to associate event data with internal entity IDs, such as customer or order IDs.

## Error Handling

The jobs and commands include error handling to ensure exceptions are logged, and in some cases, retried with appropriate intervals.

## Development and Testing

For local development and testing, certain jobs and operations can be faked or mocked, such as in `PetPay` or based on environment variables that indicate the non-production environment. This is essential for safe development without affecting real customers or transactions.

## Integration Points

The billing system integrates with several services:

- Shopify: For cart, order, subscription, and customer management.
- Stripe: For managing charges, payment methods, and handling payment processing.
- MerchantWare: As an additional payment processing solution.
- Instagram: For refreshing media tokens periodically.

Each of these integrations has its own set of handlers, jobs, and processes to maintain data synchronization and process business logic.

## Monitoring and Logging

The jobs are set to log significant events and errors to ensure traceability and tracking of the billing system's performance and issues.

## Conclusion

The PetPlate billing system and webhook handling involves a complex interplay of jobs, commands, and services to deal with payment processing, handling third-party events, and ensuring data consistency. This documentation gives an overview of the system's architecture and functionality, ensuring the maintainability and extensibility of the system.
