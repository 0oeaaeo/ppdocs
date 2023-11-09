# GraphQL Schema Documentation

This document provides a comprehensive description of the GraphQL schema used in our system, including types, queries, and mutations. It's designed to help new developers get quickly up-to-speed with the functionality available through the API.

## Scalar Types

- `Boolean`: Represents `true` or `false` values.
- `Int`: Represents non-fractional signed whole numeric values.
- `Float`: Represents signed double-precision fractional values as specified by IEEE 754.
- `ID`: Represents a unique identifier that is often used to refetch an object or as a key for a cache. `ID` type is serialized in the same way as a `String`.
- `ISO8601Date`: An ISO 8601-encoded date.
- `ISO8601DateTime`: An ISO 8601-encoded datetime.
- `JSON`: Represents untyped JSON.
- `String`: Represents textual data.

## Enums

Enums are special scalar types that restrict a set of allowed values. They are used to describe fields that can only take one of a predefined set of options.

### `BoxVariantOrder`

Determines the ordering of `BoxVariant` items when listed.

- `NAME_ASC`
- `NAME_DESC`
- `PRICE_ASC`
- `PRICE_DESC`

### `BoxVariantPlanTypeEnum`

Defines the plan type for a `BoxVariant`.

- `bundle`
- `custom`
- `full`
- `retail`
- `space_saver`
- `topper`
- `welcome`

### `BreedOrder`

Determines the ordering of `Breed` items when listed.

- `NAME_ASC`
- `NAME_DESC`
- `RECENTLY_CREATED`
- `RECENTLY_MODIFIED`

### `FulfillmentScheduleRuleOrder`

Determines the ordering of `FulfillmentScheduleRule` items when listed.

- `END_DATE_ASC`
- `END_DATE_DESC`
- `START_DATE_ASC`
- `START_DATE_DESC`

### `IngredientOrder`

Determines the ordering of `Ingredient` items when listed.

- `NAME_ASC`
- `NAME_DESC`

### `MealOrder`

Determines the ordering of `Meal` items when listed.

- `RECENTLY_CREATED`
- `RECENTLY_MODIFIED`

### `PaymentMethodOrder`

Determines the ordering of `PaymentMethod` items when listed.

- `RECENTLY_CREATED`
- `RECENTLY_MODIFIED`

### `PetOrder`

Determines the ordering of `Pet` items when listed.

- `PET_NAME_ASC`
- `PET_NAME_DESC`
- `RECENTLY_CREATED`

### `PetPlateProductOrder`

Determines the ordering of `PetPlateProduct` items when listed.

- `RECENTLY_CREATED`
- `RECENTLY_MODIFIED`

### `PetPlateLineItemTypeEnum`

Defines the type of line item for `PetPlateLineItem`.

- `addons`
- `bundles`
- `dishes`
- `plans`
- `products`

### `RecipeOrder`

Determines the ordering of `Recipe` items when listed.

- `NAME_ASC`
- `NAME_DESC`

### `ReportJobOrder`

Determines the ordering of `ReportJob` items when listed.

- `RECENTLY_CREATED`
- `RECENTLY_MODIFIED`

### `RouteScheduleOrder`

Determines the ordering of `RouteSchedule` items when listed.

- `RECENTLY_CREATED`
- `RECENTLY_MODIFIED`
- `RECENTLY_MODIFIED_`
- `SCHEDULING_START_DATE_ASC`
- `SCHEDULING_START_DATE_DESC`
- `SHIPPING_START_DATE_ASC`
- `SHIPPING_START_DATE_DESC`

### `SizeClassOrder`

Determines the ordering of `SizeClass` items when listed.

- `RECENTLY_CREATED`
- `RECENTLY_MODIFIED`

### `TermOrder`

Determines the ordering of `Term` items when listed.

- `RECENTLY_CREATED`
- `RECENTLY_MODIFIED`

### `WellnessGoalOrder`

Determines the ordering of `WellnessGoal` items when listed.

- `NAME_ASC`
- `NAME_DESC`

### `ZipCodeOrder`

Determines the ordering of `ZipCode` items when listed.

- `ZIP_CODE_ASC`
- `ZIP_CODE_DESC`

## Objects

### `BoxVariant`

Describes a variation of a product box offered to customers, which may include different sizes or combinations of meals.

#### Fields

- `active`: (`Boolean`) Indicates whether the box variant is currently offered.
- `activeFrom`: (`ISO8601Date`) The date from which the box variant is active.
- `activeUntil`: (`ISO8601Date`) The date until which the box variant is active.
- `addonUnits`: (`Int!`) The number of additional units that can be added (Required).
- `boxId`: (`Int`) A unique identifier for the box tied to a particular variant.
- `calorieGroup`: (`Int`) The calorie grouping associated with this variant.
- `category`: (`String!`) A category marking for the variant (Required).
- `defaultFrequency`: (`Int`) The default frequency at which this variant may be delivered.
- `deletedAt`: (`ISO8601Date`) The date the box variant was marked for deletion.
- `displayOrder`: (`Int`) An integer representing the display order in lists.
- `id`: (`ID!`) The unique identifier for a `BoxVariant` (Required).
- `mealsPerDay`: (`Int!`) The number of meals provided per day (Required).
- `name`: (`String!`) The name of the box variant (Required).
- `planType`: (`BoxVariantPlanTypeEnum`) The type of plan associated with the box variant.
- `price`: (`Float`) The price of the box variant.
- `sellingPlanId`: (`String`) An ID representing the selling plan.
- `shopifyId`: (`String`) The ID associated with a Shopify entry.
- `sku`: (`String`) Stock Keeping Unit to identify the box variant.

### `BoxVariantConnection`

A connection type that includes a list of `BoxVariant` nodes and supports pagination.

#### Fields

- `edges`: List of edges housing `BoxVariantEdge` elements.
- `nodes`: List of `BoxVariant` nodes.
- `pageInfo`: (`PPPageInfo!`) Information related to pagination (Required). 

### `BoxVariantEdge`

An edge in the connection related to `BoxVariant`.

#### Fields

- `cursor`: (`String!`) A pagination cursor string (Required).
- `node`: The `BoxVariant` at the end of the edge.

### `Breed`

Defines the properties of a dog breed.

#### Fields

- `active`: (`Boolean!`) Indicates whether the breed is active in the system (Required).
- `activityLevel`: (`String`) Describes the general activity level of the breed.
- `createdAt`: (`ISO8601DateTime!`) The timestamp when the breed was created (Required).
- `id`: (`ID!`) The unique identifier for a breed (Required).
- `mixedBreed`: (`Boolean!`) Flag indicating if the breed is a mixed breed (Required).
- `name`: (`String!`) The name of the breed (Required).
- `sizeClass`: (`String`) The classification of the breed's size.
- `slug`: (`String!`) A URL-friendly string identifying the breed (Required).
- `updatedAt`: (`ISO8601DateTime!`) The timestamp when the breed was last updated (Required).

### `BreedConnection`

A connection type for listing breeds with pagination support.

#### Fields

- `edges`: List of edges housing `BreedEdge` elements.
- `nodes`: List of `Breed` nodes.
- `pageInfo`: Pagination information using `PPPageInfo`.

### `Ingredient`

Represents an ingredient that can be used in meals.

#### Fields

- `active`: (`Boolean!`) Indicates whether the ingredient is active in the system (Required).
- `id`: (`ID!`) The unique identifier for an ingredient (Required).
- `name`: (`String!`) The name of the ingredient (Required).
- `slug`: (`String!`) A URL-friendly string identifying the ingredient (Required).

### `IngredientConnection`

A connection type for listing ingredients with pagination support.

#### Fields

- `edges`: List of edges housing `IngredientEdge` elements.
- `nodes`: List of `Ingredient` nodes.
- `pageInfo`: Pagination information using `PPPageInfo`.

### `Meal`

Describes a specific meal or dish, including nutritional analysis and ordering information.

#### Fields

- `active`: (`Boolean`) If true, the meal is available for ordering.
- `analysis`: (`JSON`) A JSON object providing detailed nutritional information.
- `category`: (`Int`) A category identifier for the type of meal.
- `clusterAvailable`: (`Boolean`) A flag indicating if the meal is available in the cluster.
- `createdAt`: (`ISO8601DateTime!`) Creation timestamp (Required).
- `description`: (`String`) Descriptive text about the meal.
- `displayOrder`: (`Int`) The order in which the meal should be displayed.
- `emergencyOutOfStock`: (`Boolean`) A flag indicating emergency stock status.
- `id`: (`ID!`) Unique identifier (Required).
- `ingredients`: (`String`) Ingredients used in the meal.
- `lineItemName`: (`String`) The name used for order line items.
- `metadata`: (`JSON`) Additional JSON metadata associated with the meal.
- `name`: (`String`) The meal's display name.
- `outOfStock`: (`Boolean`) A flag indicating if a meal is out of stock.
- `outOfStockMessage`: (`String`) Custom message to display when a meal is out of stock.
- `pageUrl`: (`String`) The URL of the meal's product page.
- `price`: (`Float`) The price of the meal.
- `priceCategory`: (`String`) Categorization of the price (e.g., premium).
- `productCategory`: (`String`) Categorization of the product.
- `productType`: (`String`) The product type, such as meal, add-on, etc.
- `recipeId`: (`Int`) An identifier linking the meal with its recipe.
- `shopifyId`: (`String`) An identifier used by Shopify.
- `shortName`: (`String`) A short, descriptive name for the meal.
- `sku`: (`String`) Stock keeping unit for the meal.
- `slug`: (`String`) A URL-friendly string identifying the meal.
- `surchargeAmount`: (`Float!`) Any additional charge for the meal (Required).
- `updatedAt`: (`ISO8601DateTime!`) Timestamp of the last update (Required).
- `weightInOunces`: (`Float`) The weight of the meal in ounces.

### `MealConnection`

A connection type for listing meals with pagination support.

#### Fields

- `edges`: List of edges housing `MealEdge` elements.
- `nodes`: List of `Meal` nodes.
- `pageInfo`: Pagination information using `PPPageInfo`.

### `MealPlan`

Describes the detailed plan for feeding a specific pet, including meal amount and frequency.

#### Fields

- `containers`: (`Int`) The number of meal containers provided.
- `feedingGuideline`: An associated `FeedingGuideline` entry.
- `feedingPortion`: (`Float`) The amount of food per feeding.
- `servingsPerDay`: (`Int`) The number of servings the pet should receive each day.

### `PaymentMethod`

Describes a payment method associated with a user account.

#### Fields

- `apiCardId`: (`String`) ID of the payment card from the payment API.
- `apiCustomerId`: (`String`) Customer ID from the payment API.
- `cardFingerprint`: (`String`) A token used to identify the card.
- `cardLast4`: (`String`) The last four digits of the payment card.
- `cardMonth`: (`Int`) The expiration month of the payment card.
- `cardYear`: (`Int`) The expiration year of the payment card.
- `createdAt`: (`ISO8601DateTime!`) The creation timestamp (Required).
- `id`: (`ID!`) Unique identifier (Required).
- `metadata`: (`JSON`) Additional JSON metadata associated with the payment method.
- `migratedFromId`: (`Int`) ID of the previous system if the payment method was migrated.
- `paymentGatewayProvider`: (`String`) The name of the payment gateway provider.
- `state`: (`String`) The state of the payment method.
- `updatedAt`: (`ISO8601DateTime!`) Timestamp of the last update (Required).
- `userId`: (`Int`) ID of the user whom the payment method belongs to.

### `PaymentMethodConnection`

A connection type for listing payment methods with pagination support.

#### Fields

- `edges`: List of edges housing `PaymentMethodEdge` elements.
- `nodes`: List of `PaymentMethod` nodes.
- `pageInfo`: Pagination information using `PPPageInfo`.

### `Pet`

Describes a pet belonging to a user, including personal information and dietary needs.

#### Fields

- `activityLevel`: (`String`) The pet's activity level.
- `birthDate`: (`ISO8601Date`) The pet's birthdate.
- `breedType`: (`String!`) The primary breed type (Required).
- `completedBirthDate`: (`Int`) Flag indicating completion of the birth date field.
- `createdAt`: (`ISO8601DateTime!`) Creation timestamp (Required).
- `gender`: (`String`) The pet's gender.
- `hasFoodSensitivities`: (`Boolean`) If the pet has food sensitivities.
- `hasWellnessGoals`: (`Boolean`) If the pet has wellness goals.
- `id`: (`ID!`) Unique identifier (Required).
- `idealWeight`: (`Int`) The pet's ideal weight.
- `petName`: (`String`) The pet's name.
- `primaryBreedId`: (`Int`) The ID of the primary breed.
- `secondaryBreedId`: (`Int`) The ID of the secondary breed, if any.
- `servingSizeInOunces`: (`Int`) The recommended serving size in ounces.
- `spayedNeutered`: (`Boolean`) If the pet is spayed or neutered.
- `updatedAt`: (`ISO8601DateTime!`) Timestamp of the last update (Required).
- `user`: (`User!`) The associated user who owns the pet (Accessor field).
- `userId`: (`Int`) The ID of the user who owns the pet.
- `waistline`: (`String`) Description of the pet's waistline.
- `weight`: (`Int`) The pet's current weight.

### `PetConnection`

A connection type for listing pets with pagination support.

#### Fields

- `edges`: List of edges housing `PetEdge` elements.
- `nodes`: List of `Pet` nodes.
- `pageInfo`: Pagination information using `PPPageInfo`.

### `PetPlateCart`

Defines properties related to a shopping cart, including selected options and calculated recommendations for pet nutrition.

#### Fields

- `activityLevel`: (`String`) The pet's activity level.
- `attributions`: (`JSON`) Attribution data associated with the cart.
- `birthDate`: (`ISO8601Date`) The pet's birth date.
- `breedType`: (`String!`) The pet's primary breed type (Required).
- `checkoutUrl`: (`String`) URL to the checkout page.
- `completedBirthDate`: (`Int`) Indicates whether the pet's birth date is complete.
- `completedPlans`: (`Boolean`) Indicates whether the plan selection is complete.
- `completedSupplements`: (`Boolean`) Indicates whether the supplements selection is complete.
- `completedTreats`: (`Boolean`) Indicates whether the treats selection is complete.
- `contactEmail`: (`String`) The contact email for the cart.
- `contactName`: (`String`) The contact name for the cart.
- `contactPhoneNumber`: (`String`) The contact phone number for the cart.
- `couponsData`: (`JSON`) Data about any coupons applied to the cart.
- `createdAt`: (`ISO8601DateTime!`) Creation timestamp (Required).
- `gender`: (`String`) The pet's gender.
- `hasFoodSensitivities`: (`Boolean`) If the pet has food sensitivities.
- `hasWellnessGoals`: (`Boolean`) If the pet has wellness goals.
- `id`: (`ID!`) Unique identifier (Required).
- `idealWeight`: (`Int`) The pet's ideal weight.
- `lineItemsData`: (`JSON`) Data representing line items in the cart.
- `oversized`: (`Boolean`) Indicates if the order is oversized.
- `pet`: (`Pet!`) The associated pet (Accessor field).
- `petId`: (`Int`) The ID of the associated pet.
- `petName`: (`String`) The pet's name.
- `petPlateLineItems`: Access to related `PetPlateLineItem` elements.
- `plan`: (`BoxVariant`) The box variant selected for the cart.
- `planId`: (`Int`) The ID of the selected plan.
- `primaryBreedId`: (`Int`) The ID of the pet's primary breed.
- `recipeIds`: (`[ID!]`) An array of IDs representing selected recipes.
- `recipes`: (`RecipeConnection!`) Connection to list associated recipes.
- `recommendedCaloriesPerDay`: (`Int`) Recommended number of calories for the pet to consume each day.
- `recommendedServingSize`: (`Float`) The recommended serving size determined for the pet.
- `secondaryBreedId`: (`Int`) The ID of the pet's secondary breed, if any.
- `selectedBreedOptions`: (`[Option]`) Selected options for breed.
- `selectedRecipeOptions`: (`[Option]`) Selected options for recipes.
- `selectedWellnessGoalOptions`: (`[Option]`) Selected options for wellness goals.
- `servingSizeInOunces`: (`Int`) The serving size in ounces.
- `shopifyId`: (`String`) The cart's Shopify ID.
- `spayedNeutered`: (`Boolean`) Indicates if the pet is spayed or neutered.
- `subscriptionId`: (`Int`) The ID of the associated subscription.
- `updatedAt`: (`ISO8601DateTime!`) Timestamp of the last update (Required).
- `user`: (`User!`) The associated user who owns the cart (Accessor field).
- `userId`: (`Int`) The ID of the user who owns the cart.
- `waistline`: (`String`) Description of the pet's waistline.
- `weight`: (`Int`) The pet's current weight.
- `wellnessGoalIds`: (`[ID!]`) An array of IDs representing selected wellness goals.
- `wellnessGoals`: (`WellnessGoalConnection!`) Connection to list associated wellness goals.

### `PetPlateCartConnection`

A connection type for listing shopping carts with pagination support.

#### Fields

- `edges`: List of edges housing `PetPlateCartEdge` elements.
- `nodes`: List of `PetPlateCart` nodes.
- `pageInfo`: Pagination information using `PPPageInfo`.

### `PetPlateProduct`

Defines a product available for purchase, such as a meal, an add-on, or a plan.

#### Fields

- `active`: (`Boolean`) Indicates if the product is currently available for purchase.
- `analysis`: (`JSON`) Nutritional analysis for the product.
- `category`: (`Int`) The product category identifier.
- `clusterAvailable`: (`Boolean`) Indicates if the product is available in a cluster.
- `createdAt`: (`ISO8601DateTime!`) The
