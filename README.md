# ShopAI - AI-Powered Product Q&A for Shopify

ShopAI is a Shopify Theme App Extension that adds an "Ask Me Anything" search bar to your product pages. Customers can ask questions about the product, and the app uses the OpenAI API to provide answers based on the product's description and details.

## Features

*   **"Ask Me Anything" Search Bar:** Allows customers to ask natural language questions about products directly on the product page.
*   **OpenAI Integration:** Leverages OpenAI's language models to understand questions and generate relevant answers based on product context.
*   **Seamless Theme Integration:** Adds a new section available in the Shopify Theme Editor for easy placement and configuration.
*   **Customizable UI:** Modern search bar design with gradient effects, easily styleable via Liquid and CSS.

## Technology Stack

*   **Frontend:** Remix, React, TypeScript, Tailwind CSS
*   **Backend:** Remix (Resource Routes for API endpoint)
*   **Shopify:** Shopify CLI, Theme App Extensions, Liquid
*   **AI:** OpenAI API (gpt-3.5-turbo)
*   **Database:** Prisma with SQLite (for session storage)

## Prerequisites

*   Node.js (v18.20, v20.10, or >=21.0.0)
*   npm or yarn
*   Shopify CLI
*   A Shopify Partner Account and a development store
*   An OpenAI API Key

## Setup and Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/alexandermazza/Shop-AI.git
    cd ShopAI
    ```

2.  **Install dependencies:**
    Navigate into the app directory and install packages:
    ```bash
    cd shop-ai
    npm install
    ```

3.  **Environment Variables:**
    *   Create a `.env` file in the `shop-ai` directory: `shop-ai/.env`
    *   Add your Shopify App API Key/Secret and your OpenAI API Key:
        ```dotenv
        SHOPIFY_API_KEY=your_shopify_api_key
        SHOPIFY_API_SECRET=your_shopify_api_secret
        OPENAI_API_KEY=your_openai_api_key
        # SCOPES can be adjusted as needed, e.g., SCOPES=write_products,read_products
        SCOPES=write_products
        # SHOPIFY_APP_URL will likely be provided by the dev server (Cloudflare tunnel)
        # SHOPIFY_APP_URL=https://your-tunnel-url.trycloudflare.com
        ```
    *   *Note:* The `.env` file is already in `.gitignore` to prevent accidental commits.

4.  **Run the Development Server:**
    Make sure you are in the `shop-ai` directory.
    ```bash
    cd /Users/alexmazza/Documents/projects/ShopAI/shop-ai # Or navigate if not already there
    shopify app dev
    ```
    Follow the prompts from the Shopify CLI (select partner org, development store, etc.). This will start the Remix server and the Shopify tunnel.

## Usage

1.  **Add the Section:** In your Shopify development store's Theme Editor, navigate to a product page. Click "Add section" and search for "Ask Me Anything" (or the name configured in `shopify.extension.toml`). Add the section to your desired location.
2.  **Ask Questions:** View the product page on your storefront. Use the "Ask Me Anything" search bar to ask questions about the product. The response from OpenAI, based on the product details, will appear below the search bar.

## Troubleshooting

*   **Extension Not Appearing:** Ensure `extension_points = ["section"]` is present in `shop-ai/extensions/shop-ai/shopify.extension.toml`. Make sure the block file (`ask-me-anything.liquid`) is directly inside the `blocks` directory. Restart `shopify app dev` and hard-refresh the Theme Editor.
*   **OpenAI API Key Error:** Double-check that the `OPENAI_API_KEY` is correctly set in the `shop-ai/.env` file and that the backend route (`resource-openai.tsx`) is loading it correctly.
*   **500 Internal Server Error / Rate Limiting:** These errors from Shopify's API during `shopify app dev` might be temporary Shopify issues or due to making too many requests. Try waiting, restarting the dev server, re-authenticating (`shopify auth logout` then run `shopify app dev` again), or updating the Shopify CLI (`npm update -g @shopify/cli @shopify/theme`). Check `https://www.shopifystatus.com/`.
*   **404 Errors for API Route:** Ensure the API route file (`shop-ai/app/routes/resource-openai.tsx`) exists and is correctly configured as a resource route (no default export). Check the `fetch` URL in the frontend JavaScript (`ask-me-anything.js`).

## Changelog

See [changelog.md](changelog.md) for a detailed history of changes. 