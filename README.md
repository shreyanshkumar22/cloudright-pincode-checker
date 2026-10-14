# CloudRight Pincode Checker

A Shopify Theme App Extension that allows customers to look up an Indian postal pincode directly from a product detail page.

## Features

- Pincode input with six-digit validation.
- Delivery-check button on the product page.
- Integration with the India Post public pincode API.
- Displays the returned district and state.
- Handles invalid input, unknown pincodes, and network/API errors.
- Responsive layout for mobile and desktop.
- Does not modify product prices, inventory, cart, or checkout.

## System Architecture

```text
Shopify Product Detail Page
          |
          v
Theme App Extension (Liquid)
          |
          v
Pincode Input + Check Button
          |
          v
Client-side Validation
          |
          v
JavaScript fetch()
          |
          v
India Post Public API
          |
          v
JSON Response Parsing
          |
          v
District + State / Error Message
```

## Technology Stack

- Shopify Theme App Extension
- Liquid
- HTML and CSS
- JavaScript (Fetch API)
- India Post public pincode API
- Shopify CLI

## API Integration

**Endpoint pattern**

`https://api.postalpincode.in/pincode/{PINCODE}`

**Method:** GET

The API response is parsed to retrieve the postal status and Post Office details. When a successful response contains postal records, the checker displays the serviceability message using the returned district and state.

**Example:** `✓ Serviceable: Delivery available to Bangalore, Karnataka`

**Important:** A valid postal record confirms the pincode's postal location; it does not guarantee that a particular seller can deliver to that location.

## Project Structure

```text
extensions/
└── pincode-checker/
    ├── assets/
    ├── blocks/
    │   ├── pincode_checker.liquid
    │   └── star_rating.liquid
    ├── locales/
    ├── snippets/
    └── shopify.extension.toml
```

## Local Setup

### Prerequisites

- Node.js
- npm
- Git
- Shopify CLI
- A Shopify development store

### Run locally

1. Clone or download this repository.
2. Open a terminal in the project root.
3. Install dependencies if required:

   `npm install`

4. Start the Shopify development environment:

   `shopify app dev`

5. Install the development app in the development store if prompted.
6. Open the theme editor and add the **Pincode Checker** app block to a product page.
7. Save the theme and test the block in the preview.

## Test Cases

| Test | Input or condition | Expected behavior |
|---|---|---|
| Valid pincode | `560001` | Displays returned district and state |
| Short input | `123` | Shows validation error |
| Unknown pincode | `999999` | Shows not-found message if the API returns no postal record |
| Network failure | Disconnect network during lookup | Shows an error message |
| Mobile layout | Narrow browser viewport | Input and button remain usable |

Actual API responses can vary; verify the behavior against the live API.

## Limitations

- Requires access to the public postal API.
- Browser requests may be affected by network restrictions or CORS.
- Postal location lookup is not a delivery-serviceability check.
- The current implementation does not use seller-specific delivery rules.

## Future Improvements

- Configurable UI settings in the Shopify theme editor.
- Improved accessibility and automated tests.
- Seller-specific serviceability checks if required by the business.

## License

For evaluation and development use. Confirm the applicable license before redistributing this project.
