const express = require("express");
const path = require("path");

const app = express();
const PORT = process.env.PORT || 3000;

app.use(express.static(path.join(__dirname, "public")));
app.use(express.json());

// Home route
app.get("/", (req, res) => {
  res.sendFile(path.join(__dirname, "public", "index.html"));
});

// Products API
app.get("/api/products", (req, res) => {
  const products = [
    { id: 1, name: "Classic Black Tee", price: 12000, image: "https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?w=500&h=500&fit=crop", category: "featured" },
    { id: 2, name: "Urban White Hoodie", price: 22000, image: "https://images.unsplash.com/photo-1556821552-7f41c5d440db?w=500&h=500&fit=crop", category: "featured" },
    { id: 3, name: "Street Cargo Pants", price: 18000, image: "https://images.unsplash.com/photo-1542272604-787c62d465d1?w=500&h=500&fit=crop", category: "featured" },
    { id: 4, name: "Minimalist Black Jacket", price: 35000, image: "https://images.unsplash.com/photo-1551028719-00167b16ebc5?w=500&h=500&fit=crop", category: "arrivals" },
    { id: 5, name: "Premium White Shirt", price: 15000, image: "https://images.unsplash.com/photo-1596755094514-f87e34085b2c?w=500&h=500&fit=crop", category: "arrivals" },
    { id: 6, name: "Elegant Black Dress", price: 28000, image: "https://images.unsplash.com/photo-1595777707802-41d339d60280?w=500&h=500&fit=crop", category: "arrivals" }
  ];

  res.json(products);
});

// Contact API
app.post("/api/contact", (req, res) => {
  const { name, email, message } = req.body;

  if (name && email && message) {
    console.log("Contact:", { name, email, message });
    res.json({ success: true, message: "Thank you! We will respond soon." });
  } else {
    res.status(400).json({ error: "All fields required" });
  }
});

app.listen(PORT, () => {
  console.log(`🚀 Running on http://localhost:${PORT}`);
});