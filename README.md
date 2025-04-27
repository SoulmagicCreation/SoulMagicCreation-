<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🌟 KREATIVER SHOP - [Dein Name]</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <link href="style.css" rel="stylesheet">
    <!-- Google Analytics -->
    <script async src="https://www.googletagmanager.com/gtag/js?id=G-DEINE-ID"></script>
    <script>
        window.dataLayer = window.dataLayer || [];
        function gtag(){dataLayer.push(arguments);}
        gtag('js', new Date());
        gtag('config', 'G-DEINE-ID');
    </script>
</head>
<body class="bg-gradient-to-r from-purple-100 to-blue-100">
    <!-- 3D-Header mit Parallax-Effekt -->
    <header class="parallax-header h-96 relative overflow-hidden">
        <div class="absolute inset-0 bg-black/50"></div>
        <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 text-center">
            <h1 class="text-6xl font-bold text-white mb-4 animate-pulse">🛍️ Dein Shop</h1>
            <p class="text-xl text-white">Willkommen in der Zukunft des Einkaufens!</p>
        </div>
    </header>

    <!-- Admin-Bearbeitungsleiste (Nur sichtbar mit Passwort) -->
    <div id="adminPanel" class="hidden fixed top-0 right-0 bg-white p-4 shadow-lg z-50">
        <input type="password" id="adminPass" placeholder="Admin-Passwort" class="border p-2">
        <button onclick="loginAdmin()" class="bg-blue-500 text-white p-2">Login</button>
        <div id="editor" class="hidden mt-4">
            <input type="text" id="productName" placeholder="Produktname" class="border p-2 block mb-2">
            <input type="number" id="productPrice" placeholder="Preis" class="border p-2 block mb-2">
            <button onclick="addProduct()" class="bg-green-500 text-white p-2">Produkt hinzufügen</button>
        </div>
    </div>

    <!-- Produktgalerie (Automatisch befüllt) -->
    <main class="max-w-6xl mx-auto py-12 px-4">
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8" id="products">
            <!-- Produkte werden via JS geladen -->
        </div>
    </main>

    <!-- Zahlungsfooter -->
    <footer class="bg-black text-white py-8">
        <div class="max-w-6xl mx-auto px-4">
            <div class="flex flex-wrap gap-8 justify-center">
                <img src="https://www.paypalobjects.com/webstatic/mktg/Logo/pp-logo-100px.png" alt="PayPal" class="h-12">
                <img src="https://stripe.com/img/v3/home/twitter.png" alt="Stripe" class="h-12">
            </div>
        </div>
    </footer>

    <script src="script.js"></script>
</body>
</html>
/* Kustom Design */
.parallax-header {
    background: url('https://images.unsplash.com/photo-1607082352121-fa243f3dde32?auto=format&fit=crop&w=1920') fixed;
    background-size: cover;
}

@keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-20px); }
}

.product-card {
    transition: transform 0.3s, box-shadow 0.3s;
    background: rgba(255, 255, 255, 0.9);
    backdrop-filter: blur(10px);
}

.product-card:hover {
    transform: scale(1.05);
    box-shadow: 0 10px 30px rgba(0,0,0,0.1);
}
// 🔑 ADMIN-LOGIN (Passwort: "admin123")
let isAdmin = false;

// 🛒 Produkt-Daten (Du kannst diese bearbeiten!)
let products = [
    { 
        name: "Magisches T-Shirt",
        price: 29.99,
        image: "https://via.placeholder.com/400x300",
        category: "Kleidung",
        video: "https://youtu.be/Beispielvideo"
    }
];

// 🎬 Lade Produkte automatisch
function loadProducts() {
    const container = document.getElementById('products');
    container.innerHTML = products.map(product => `
        <div class="product-card rounded-lg overflow-hidden shadow-lg p-6">
            <div class="relative">
                ${product.video ? `
                    <iframe 
                        src="${product.video}" 
                        class="w-full h-48"
                        allowfullscreen
                    ></iframe>
                ` : `
                    <img 
                        src="${product.image}" 
                        alt="${product.name}"
                        class="w-full h-48 object-cover"
                    >
                `}
            </div>
            <h3 class="text-xl font-bold mt-4">${product.name}</h3>
            <p class="text-2xl text-purple-600 my-2">€${product.price}</p>
            <button class="w-full bg-purple-500 text-white py-2 rounded hover:bg-purple-600">
                Kaufen
            </button>
        </div>
    `).join('');
}

// 🔒 Admin-Funktionen
function loginAdmin() {
    const password = document.getElementById('adminPass').value;
    if (password === "admin123") {
        isAdmin = true;
        document.getElementById('editor').classList.remove('hidden');
        alert("Admin-Modus aktiviert! 🛠️");
    }
}

function addProduct() {
    if (!isAdmin) return;
    const newProduct = {
        name: document.getElementById('productName').value,
        price: parseFloat(document.getElementById('productPrice').value),
        image: "https://via.placeholder.com/400x300"
    };
    products.push(newProduct);
    loadProducts();
}

// Start
document.addEventListener('DOMContentLoaded', loadProducts);
