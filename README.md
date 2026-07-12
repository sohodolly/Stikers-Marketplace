# Stikers-Market

A full‑featured web application for browsing, collecting, and ordering sticker sets.  
Built with vanilla HTML, CSS, and JavaScript – no frameworks – and powered by a RESTful backend (RestDB.io). The interface includes a live product catalogue, powerful search & price filters, a persistent shopping cart (stored in `localStorage`), a dark/light theme toggle, and a dedicated admin panel for managing stickers and orders.

---

## 📸 Screenshot
![Screenshot of the interface](screenshot.jpg)  

---

## 🚀 Features

- **Product catalogue** – displays stickers as cards with name, description, price, and an image.
- **Search & filter** – filter stickers by **name** (real‑time) and by **price range** (min‑max).
- **Shopping cart / collection** – add stickers to your collection, view total price, remove items individually, or clear the cart.
- **Order placement** – fill in a simple form (name, address, phone, post office number) and submit the order directly to the backend.
- **Dark / light theme** – toggle themes with a single button; the preference is saved in `localStorage`.
- **Admin panel** – add new sticker sets (name, description, price, photo URL) and view all incoming orders with a “Mark as Completed” action.
- **Responsive layout** – works seamlessly on desktop, tablet, and mobile devices.
- **Persistent data** – cart contents and theme preference survive page reloads via `localStorage`.

---

## 🛠 Technologies

- **HTML5** – semantic markup  
- **CSS3** – custom properties (CSS variables) for theming, Flexbox & Grid, media queries, smooth transitions  
- **JavaScript (ES6)** – DOM manipulation, `fetch` API, `localStorage`, event handling, async/await  
- **External API** – [RestDB.io](https://restdb.io/) is used as a headless backend to store products and orders  
- **Font** – [Inter](https://fonts.google.com/specimen/Inter) (loaded from Google Fonts)  

---

## 📁 Project Structure
sticker-shop/
├── index.html          # Main page – catalogue + filters
├── cart.html           # Shopping cart / collection page
├── admin.html          # Admin panel – add stickers & manage orders
├── style.css           # All styles (themes, layout, components)
├── main.js             # Core logic: theme, cart, product loading, filtering, order modal
├── admin.js            # Admin-specific logic: add products, fetch & update orders
├── script.js           # (legacy, not used – can be removed)
└── README.md           # This file

---

## ⚙️ Installation & Usage

1. **Clone or download** all files into a single folder.
2. Make sure you have an internet connection (the app loads fonts and API data from external sources).
3. Open `index.html` in any modern browser (Chrome, Firefox, Edge, Safari).
4. Browse the sticker collection, use the **search** and **price range** filters, and add stickers to your collection.
5. Go to `cart.html` to view your collection, adjust quantities (remove items), and proceed to checkout.
6. Visit `admin.html` to add new sticker sets and manage incoming orders.

> **Note:** The app expects the RestDB API endpoints to be available. The API key is hardcoded in `main.js` and `admin.js` – you may replace it with your own key if you wish to use your own database.

---

## 🔧 How It Works

### Product Data & Filtering
- Products are fetched from `https://market-6d33.restdb.io/rest/products` using a GET request.
- The `applyFilters()` function reads the search input and price fields, filters the product list, and re‑renders the catalogue.
- Filtering is triggered both by clicking the **Apply** button and automatically on every input change (for a smooth live search experience).

### Cart & LocalStorage
- The cart is stored in `localStorage` under the key `'cart'`.
- Functions `getCart()`, `saveCart()`, `addToCart()`, `removeFromCart()`, and `clearCart()` manage the data.
- The cart count in the header updates automatically.

### Order Placement
- On the cart page, clicking **Оформить заказ** opens a modal with a summary of selected stickers.
- The user fills in personal details; the form submits a POST request to `/orders` containing the cart items and customer info.
- On success, the cart is cleared and the user is notified.

### Admin Panel
- The admin page loads all orders from `/orders` and displays them as cards.
- Each order shows the customer details, a list of ordered stickers with prices, and a total.
- Clicking **Mark as Completed** sends a PUT request to update the order status.
- The “Add sticker” form sends a POST request to `/products` to create a new sticker set.

### Theme Switching
- The theme toggle adds/removes the class `dark-theme` on the `<body>`.
- CSS variables (custom properties) change values accordingly, affecting background, text, borders, and accent colours.
- The chosen theme is saved in `localStorage` and restored on page load.

---

## 🧪 Testing

No extra dependencies are needed. Simply open the HTML files in a browser and interact with the UI.  
All data operations (fetch, POST, PUT) are made to the RestDB API, so a working internet connection is required.

---

## 📝 Notes

- The `script.js` file is not used in the current version and can be safely deleted.
- The API key and endpoint URLs are hardcoded in the JavaScript files – for production, consider moving them to environment variables or a config file.
- The admin panel assumes the order objects contain a `products` array. The frontend sends the cart array as `products` when placing an order.
- Status colours for orders (“Pending” / “Completed”) are styled with CSS classes (`pending` / `completed`).

---

**Author:** [Your Name]  
**Contact:** [your email or link]
