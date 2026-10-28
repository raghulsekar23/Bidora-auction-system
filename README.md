# Bidora — Live Auction Marketplace (Review Build)

A responsive, interactive online-auction demo with a marketplace-style UI, live bidding, seller accounts, local product image uploads, smart keyword search, watchlist, and optional Razorpay test checkout.

## Requirements
- Node.js 22 or newer (Node 24 is suitable)
- Internet during `npm install` (for packages and hosted fonts/product photography)
- Docker is not required

## Run on Windows
1. Extract this ZIP into a new folder, for example `C:\Demo\Bidora-Live-Auction`.
2. Open PowerShell in that folder.
3. Run:

   ```powershell
   npm install
   $env:PORT=8090
   npm start
   ```

4. Keep that terminal open and browse to `http://localhost:8090`.
5. If you need to check the server, open `http://localhost:8090/api/health`.

## Try the main features
- Browse sample listings across Electronics, Fashion, Home & Living, Art & Collectibles, Sports & Hobbies, and Toys & Games. The electronics catalog includes illustrative model-named mobile listings such as Samsung Galaxy A55 5G, Apple iPhone 13, Redmi Note 13 5G, Vivo T3x 5G, and Realme Narzo 70 Pro 5G, with example configurations and starting prices.
- Search for `mobile`, `phone`, `smartphone`, `Samsung`, `iPhone`, `Redmi`, `Vivo`, or `Realme` to find relevant demo listings. Smart Find expands common synonyms locally. Product names, prices, and specs are illustrative demo data, not verified current offers or inventory from retailers in Tamil Nadu. For genuine live inventory, connect a licensed retailer/marketplace API or ingest verified seller listings.
- Create an account and choose **Seller** to publish an item. The listing form accepts a local image upload (JPG, PNG, WEBP, GIF up to 5 MB), previews it, and stores it in `public/uploads`.
- Create another account as a buyer to bid. Bid events are broadcast live over Socket.IO.
- Save products with the heart icon. The watchlist is stored in the browser's local storage.
- Auctions close at their end time and the highest valid bidder becomes the winner.

## Demo Buy Now payment
The product detail dialog has a **Buy now · Demo checkout** option for active listings. It records a clearly labelled `demo_paid` transaction in the local SQLite database and displays a demo receipt. This is intentionally simulated: it does not contact a payment provider and does not charge money. Never present demo receipts as real payment confirmation.

## Payment setup
Razorpay auction-winner checkout is optional and disabled until you add Razorpay TEST credentials. It is separate from the simulated Buy Now flow. Payment cannot be enabled remotely without your merchant credentials, and Razorpay auction-winner checkout is available only to the winning bidder after an auction ends. To enable it:
1. Copy `.env.example` to `.env`.
2. Add your Razorpay **TEST** key ID and key secret from your Razorpay dashboard.
3. Restart the server.

Only use test mode for review. A payment requires an auction to end with the signed-in user as the winner. The app verifies the Razorpay signature server-side. Never commit real payment secrets or use this review build for production payments.

## Storage and limitations
- SQLite data lives in `data/auction.sqlite`; uploaded images live in `public/uploads`.
- Sample products use externally hosted Unsplash images; an internet connection is needed for those images and Google Fonts.
- Smart Find is local keyword expansion, not an external AI model. Product results are the listings in this demo database, not a live feed from online retailers.
- This is a local review/demo application, not a production-ready marketplace. The seeded mobile listings are mock listings; live inventory from all over Tamil Nadu requires a permitted live data provider or real sellers registering and posting products. Production use needs deployment, secure secret management, image moderation/storage, stronger transaction concurrency controls, audit logging, order/shipping/refund workflows, privacy/legal review, and payment webhook reconciliation.

## Useful commands
```powershell
npm run check
npm start
```
