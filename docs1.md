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
