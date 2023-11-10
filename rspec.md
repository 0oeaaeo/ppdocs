# Rails Project SPEC Documentation

Welcome to the Rails project SPEC documentation. This document will help you understand the purpose and functionality of each RSpec test in the SPEC folder of the project.

## Table of Contents

- [General Information](#general-information)
- [Model Specs](#model-specs)
  - [Box Variant Model](#box-variant-model)
  - [Box Model](#box-model)
  - [Breed Model](#breed-model)
  - [Product Model](#product-model)
  - [Packaging Model](#packaging-model)
  - [Product Variant Model](#product-variant-model)
  - [Pet Model](#pet-model)
  - [Cart Model](#cart-model)
  - [Role Model](#role-model)
- [Module Specs](#module-specs)
  - [GraphQL Module](#graphql-module)
- [Request Specs](#request-specs)
  - [Ingredients Request](#ingredients-request)
  - [Box Variants Request](#box-variants-request)
  - [Boxes Request](#boxes-request)
  - [Breeds Request](#breeds-request)
  - [Zip Codes Request](#zip-codes-request)
  - [Terms Request](#terms-request)
  - [Recipes Request](#recipes-request)
  - [Size Classes Request](#size-classes-request)
  - [Pets Request](#pets-request)
  - [Carts Request](#carts-request)
  - [Route Schedules Request](#route-schedules-request)
  - [Fulfillment Schedule Rules Request](#fulfillment-schedule-rules-request)
  - [Report Jobs Request](#report-jobs-request)
  - [Wellness Goals Request](#wellness-goals-request)
  - [Payment Methods Request](#payment-methods-request)
  - [Users Request](#users-request)
- [FactoryBot Definitions](#factorybot-definitions)
  - [Breeds Factory](#breeds-factory)
  - [Product Variant Factory](#product-variant-factory)
  - [Ingredient Factory](#ingredient-factory)
  - [Meal Line Item Factory](#meal-line-item-factory)
  - [And many more...](#and-many-more)
- [Job Specs](#job-specs)
  - [CustomerPaymentMethodsCreateJob](#customerpaymentmethodscreatejob)
- [Controller Specs](#controller-specs)
  - [WebhookController](#webhookcontroller)
- [View Specs](#view-specs)
  - [Selling Plan View](#selling-plan-view)
  - [Subscription Contracts View](#subscription-contracts-view)
- [Supporting Files](#supporting-files)
  - [rails_helper.rb](#railshelperrb)
  - [WebhookHelper](#webhookhelper)

---

## General Information

This documentation covers tests written in the `RSpec` framework for a Rails application. RSpec is a testing tool for Ruby programmers, used to test the behavior of Ruby and Rails applications. In the context of this project, RSpec is utilized to ensure the models, requests, jobs, and other components of the Rails application are working as expected.

## Model Specs

### Box Variant Model

The file `box_variant_spec.rb` contains tests for the `BoxVariant` model. These tests are currently pending, indicating that examples need to be added or requirements further defined before it becomes actionable.

### Box Model

The `box_spec.rb` test file checks the behavior of the `Box` model. As with the Box Variant model, the test examples are pending.

### Breed Model

For `Breed`, the `breed_spec.rb` checks that the model operates correctly. The tests are marked as pending.

### Product Model

`Product` model tests in `product_spec.rb` are also pending and need further elaboration or examples.

### Packaging Model

In `packaging_spec.rb`, tests for the `Packaging` model are pending.

### Product Variant Model

Tests for `ProductVariant` are covered under `product_variant_spec.rb` and are marked as pending.

### Pet Model

The `Pet` model tests in `pet_spec.rb` follow the same pending status as the others above.

### Cart Model

For `Cart`, the `cart_spec.rb` also has pending tests for future development.

### Role Model

The `Role` model is tested in `role_spec.rb` with a pending status.

## Module Specs

### GraphQL Module

The `GQ` module is tested under `gq_spec.rb`. This module makes custom GraphQL calls, processes the response, and handles errors in return data.

## Request Specs

### Ingredients Request

In `ingredients_request_spec.rb`, the behavior for querying and creating ingredients via GraphQL is tested.

### Box Variants Request

The file `box_variants_request_spec.rb` contains tests for querying and creating box variant records.

### Boxes Request

The `boxes_request_spec.rb` tests GraphQL queries for listing and creating box records. It uses a conditional exclusion symbol `xit` for skipped tests.

### Breeds Request

Request tests for breeds are found in `breeds_request_spec.rb`. These handle GraphQL queries for both retrieval and creation.

### Zip Codes Request

In `zip_codes_request_spec.rb`, the tests cover GraphQL operations for managing zip codes.

### Terms Request

The `terms_request_spec.rb` contains tests for retrieving and creating terms.

### Recipes Request

`recipes_request_spec.rb` focuses on testing GraphQL queries related to recipe records.

### Size Classes Request

Size class management is tested in `size_classes_request_spec.rb` for listing and creating operations.

### Pets Request

The file `pets_request_spec.rb` contains tests for pet-related GraphQL queries.

### Carts Request

Functionalities for handling carts via GraphQL are tested in `carts_request_spec.rb`.

### Route Schedules Request

The `route_schedules_request_spec.rb` file handles tests for queries on route schedules.

### Fulfillment Schedule Rules Request

GraphQL queries for fulfillment schedules are tested in `fulfillment_schedule_rules_request_spec.rb`.

### Report Jobs Request

The behavior for listing and creating job reports is covered by tests in `report_jobs_request_spec.rb`.

### Wellness Goals Request

Tests in `wellness_goals_request_spec.rb` focus on managing wellness goals through GraphQL queries.

### Payment Methods Request

The file `payment_methods_request_spec.rb` covers tests for payment method queries.

### Users Request

The behavior for user-related queries is tested in `users_request_spec.rb`.

## FactoryBot Definitions

### Breeds Factory

The `breeds_factory.rb` file defines a setup for creating breeds with various traits.

### Product Variant Factory

The `product_variant_factory.rb` helps create different product variants with various attributes.

### Ingredient Factory

The `ingredient_factory.rb` provides a template for creating ingredients.

### Meal Line Item Factory

In `meal_line_item_factory.rb`, a factory for meal line items is defined.

### And many more...

Many other factory files are included, such as `meal_factory.rb`, `size_class_factory.rb`, `wellness_goal_factory.rb`, etc.

## Job Specs

### CustomerPaymentMethodsCreateJob

The `customer_payment_methods_create_job_spec.rb` file contains pending tests for payment method creation jobs.

## Controller Specs

### WebhookController

Tests for webhook reception and handling are pending in `webhook_controller_spec.rb`.

## View Specs

### Selling Plan View

The `selling_plan_view_spec.rb` is a placeholder for view tests related to selling plans.

### Subscription Contracts View

Similarly, `subscription_contracts_view_spec.rb` will test the rendering of subscription contracts views.

## Supporting Files

### rails_helper.rb

`rails_helper.rb` includes settings and configuration needed to run RSpec tests effectively.

### WebhookHelper

`webhook_helper_spec.rb` defines a test suite for webhook-related helper methods.

---

For the complete definitions and specifics of each factory, job, view, and controller test, please review each individual `.rb` file in the `spec/` directory. This organized and comprehensive documentation will be a valuable resource for the new team to understand the current test states and areas requiring attention.
