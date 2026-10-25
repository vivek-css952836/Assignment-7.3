<!DOCTYPE html>
<html lang="en" class="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Assignment 7.3 — Responsive Product Listing</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#f0f7ff',
                            100: '#e0effe',
                            500: '#3b82f6',
                            600: '#2563eb',
                            700: '#1d4ed8',
                        }
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Inter Font -->
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            transition: background-color 0.3s ease, color 0.3s ease;
        }
        
        /* Flexbox requirements demonstration styles */
        .product-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 1.5rem; /* Requirement 4: spacing using gap */
        }

        .product-card {
            /* Requirement 5: Experimenting with flex-grow, flex-shrink, and flex-basis */
            flex: 1 1 280px;
            max-width: 100%;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .product-card:hover {
            transform: translateY(-4px);
        }

        /* Glassmorphism utility */
        .glass-panel {
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 dark:bg-slate-950 dark:text-slate-100 min-h-screen flex flex-col">

    <!-- Header / Navbar -->
    <header class="sticky top-0 z-40 w-full border-b border-slate-200 dark:border-slate-800 bg-white/80 dark:bg-slate-900/80 glass-panel">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between gap-4">
            
            <!-- Brand Logo -->
            <div class="flex items-center gap-2">
                <div class="bg-blue-600 text-white p-2 rounded-xl flex items-center justify-center shadow-lg shadow-blue-500/30">
                    <i class="fa-solid fa-boxes-stacked text-lg"></i>
                </div>
                <div>
                    <h1 class="font-bold text-lg leading-tight tracking-tight">FlexStore</h1>
                    <p class="text-[10px] text-slate-500 dark:text-slate-400 font-mono hidden sm:block">Assignment 7.3 Showcase</p>
                </div>
            </div>

            <!-- Search Bar -->
            <div class="flex-1 max-w-md mx-2 sm:mx-6">
                <div class="relative">
                    <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400 text-sm"></i>
                    <input type="text" id="searchInput" placeholder="Search products..." 
                           class="w-full pl-10 pr-4 py-2 text-sm bg-slate-100 dark:bg-slate-800 border-0 rounded-full focus:ring-2 focus:ring-blue-500 outline-none transition">
                </div>
            </div>

            <!-- Actions & Theme Toggle -->
            <div class="flex items-center gap-3">
                <!-- Viewport Indicator Badge -->
                <div class="hidden md:flex items-center gap-1.5 px-3 py-1 rounded-full text-xs font-mono bg-blue-50 text-blue-700 dark:bg-blue-950/80 dark:text-blue-300 border border-blue-200 dark:border-blue-800">
                    <i class="fa-solid fa-display text-[11px]"></i>
                    <span id="viewportWidth">Screen: Desktop</span>
                </div>

                <!-- Dark Mode Toggle -->
                <button id="themeToggle" title="Toggle Theme" aria-label="Toggle Theme"
                        class="p-2.5 rounded-full text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 transition">
                    <i class="fa-solid fa-moon text-base dark:hidden"></i>
                    <i class="fa-solid fa-sun text-base hidden dark:inline"></i>
                </button>

                <!-- Shopping Cart Icon -->
                <div class="relative">
                    <button class="p-2.5 rounded-full text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 transition">
                        <i class="fa-solid fa-cart-shopping text-base"></i>
                        <span id="cartBadge" class="absolute top-1 right-1 bg-blue-600 text-white text-[10px] font-bold w-4 h-4 rounded-full flex items-center justify-center opacity-0 transition-opacity">0</span>
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- Main Content Area -->
    <main class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8">

        <!-- Assignment Information Banner -->
        <section class="mb-8 p-6 rounded-2xl bg-gradient-to-r from-blue-600 to-indigo-700 text-white shadow-xl relative overflow-hidden">
            <div class="absolute -right-10 -bottom-10 opacity-10 text-9xl">
                <i class="fa-solid fa-cubes"></i>
            </div>
            <div class="relative z-10">
                <span class="inline-block px-3 py-1 bg-white/20 backdrop-blur-md rounded-full text-xs font-medium tracking-wide mb-2 uppercase">CSS Flexbox Layout</span>
                <h2 class="text-2xl sm:text-3xl font-extrabold tracking-tight">Assignment 7.3: Responsive Product Grid</h2>
                <p class="mt-2 text-blue-100 text-sm sm:text-base max-w-2xl">
                    Demonstrating dynamic wrapping with <code class="bg-black/20 px-1.5 py-0.5 rounded font-mono text-xs">display: flex</code>, 
                    <code class="bg-black/20 px-1.5 py-0.5 rounded font-mono text-xs">flex-wrap: wrap</code>, and item sizing 
                    <code class="bg-black/20 px-1.5 py-0.5 rounded font-mono text-xs">flex: 1 1 280px</code>. Resize your browser window to test responsiveness!
                </p>
            </div>
        </section>

        <!-- Category / Filter Control Bar -->
        <div class="flex flex-wrap items-center justify-between gap-4 mb-6">
            <div class="flex flex-wrap items-center gap-2" id="categoryFilters">
                <button class="filter-btn active px-4 py-2 rounded-xl text-sm font-medium bg-blue-600 text-white shadow-md shadow-blue-500/20 transition" data-category="all">All Items</button>
                <button class="filter-btn px-4 py-2 rounded-xl text-sm font-medium bg-white dark:bg-slate-900 text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 border border-slate-200 dark:border-slate-800 transition" data-category="audio">Audio</button>
                <button class="filter-btn px-4 py-2 rounded-xl text-sm font-medium bg-white dark:bg-slate-900 text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 border border-slate-200 dark:border-slate-800 transition" data-category="wearables">Wearables</button>
                <button class="filter-btn px-4 py-2 rounded-xl text-sm font-medium bg-white dark:bg-slate-900 text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 border border-slate-200 dark:border-slate-800 transition" data-category="computing">Computing</button>
                <button class="filter-btn px-4 py-2 rounded-xl text-sm font-medium bg-white dark:bg-slate-900 text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 border border-slate-200 dark:border-slate-800 transition" data-category="accessories">Accessories</button>
            </div>
            
            <div class="text-xs text-slate-500 dark:text-slate-400 font-medium">
                Showing <span id="itemCount" class="font-bold text-slate-800 dark:text-slate-200">8</span> products
            </div>
        </div>

        <!-- Product Cards Container (Requirements 1, 3, 4, 6) -->
        <div id="productGrid" class="product-grid">
            <!-- Dynamic JavaScript Product Cards rendered here -->
        </div>

    </main>

    <!-- Footer -->
    <footer class="mt-auto border-t border-slate-200 dark:border-slate-800 bg-white dark:bg-slate-900 py-6">
        <div class="max-w-7xl mx-auto px-4 text-center text-xs text-slate-500 dark:text-slate-400 space-y-2">
            <p><strong>Assignment 7.3: Responsive Product Listing</strong> — Built with HTML, CSS (Flexbox), JavaScript & Tailwind CSS.</p>
            <p class="font-mono">Flexbox Specs: <code class="bg-slate-100 dark:bg-slate-800 px-1 py-0.5 rounded">display: flex</code> | <code class="bg-slate-100 dark:bg-slate-800 px-1 py-0.5 rounded">flex-wrap: wrap</code> | <code class="bg-slate-100 dark:bg-slate-800 px-1 py-0.5 rounded">gap: 1.5rem</code></p>
        </div>
    </footer>

    <!-- Toast Notification Container -->
    <div id="toastContainer" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>

    <!-- JavaScript Logic -->
    <script>
        // Data Array: 8 detailed product items (Exceeding requirement of 6)
        const products = [
            {
                id: 1,
                name: "Wireless ANC Headphones",
                category: "audio",
                price: 199.99,
                rating: 4.8,
                reviews: 142,
                image: "https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=600&auto=format&fit=crop&q=80",
                description: "High-fidelity sound with active noise cancellation and 35-hour battery life."
            },
            {
                id: 2,
                name: "Smart Watch Ultra",
                category: "wearables",
                price: 299.50,
                rating: 4.9,
                reviews: 89,
                image: "https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=600&auto=format&fit=crop&q=80",
                description: "Advanced health tracking, cellular connectivity, and rugged titanium case."
            },
            {
                id: 3,
                name: "Minimalist Mechanical Keyboard",
                category: "computing",
                price: 129.00,
                rating: 4.7,
                reviews: 215,
                image: "https://images.unsplash.com/photo-1587829741301-dc798b83add3?w=600&auto=format&fit=crop&q=80",
                description: "Custom tactile switches with RGB backlighting and wireless Bluetooth mode."
            },
            {
                id: 4,
                name: "Precision Ergonomic Mouse",
                category: "computing",
                price: 79.99,
                rating: 4.6,
                reviews: 76,
                image: "https://images.unsplash.com/photo-1615663245857-ac93bb7c39e7?w=600&auto=format&fit=crop&q=80",
                description: "Seamless multi-device switching with ultra-fast scroll wheel and wrist support."
            },
            {
                id: 5,
                name: "Portable Bluetooth Speaker",
                category: "audio",
                price: 89.95,
                rating: 4.5,
                reviews: 198,
                image: "https://images.unsplash.com/photo-1608043152269-423dbba4e7e1?w=600&auto=format&fit=crop&q=80",
                description: "360-degree deep bass acoustics with IPX7 waterproof housing for outdoors."
            },
            {
                id: 6,
                name: "Premium Leather Desk Pad",
                category: "accessories",
                price: 45.00,
                rating: 4.9,
                reviews: 310,
                image: "https://images.unsplash.com/photo-1544816155-12df9643f363?w=600&auto=format&fit=crop&q=80",
                description: "Waterproof synthetic leather desk mat protecting surfaces with a smooth feel."
            },
            {
                id: 7,
                name: "MagSafe Wireless Power Bank",
                category: "accessories",
                price: 59.99,
                rating: 4.4,
                reviews: 64,
                image: "https://images.unsplash.com/photo-1609592424109-dd9892f1b177?w=600&auto=format&fit=crop&q=80",
                description: "10,000mAh magnetic portable charger featuring fast 15W wireless output."
            },
            {
                id: 8,
                name: "Noise-Isolating Earbuds",
                category: "audio",
                price: 119.99,
                rating: 4.7,
                reviews: 153,
                image: "https://images.unsplash.com/photo-1590658268037-6bf12165a8df?w=600&auto=format&fit=crop&q=80",
                description: "Compact true wireless earbuds with crisp studio audio and quick charging case."
            }
        ];

        let cartCount = 0;
        let activeCategory = 'all';
        let searchQuery = '';

        // DOM Elements
        const productGrid = document.getElementById('productGrid');
        const searchInput = document.getElementById('searchInput');
        const categoryFilters = document.getElementById('categoryFilters');
        const itemCount = document.getElementById('itemCount');
        const themeToggle = document.getElementById('themeToggle');
        const viewportWidth = document.getElementById('viewportWidth');
        const cartBadge = document.getElementById('cartBadge');

        // Render Product Cards
        function renderProducts() {
            productGrid.innerHTML = '';
            
            const filteredProducts = products.filter(product => {
                const matchesCategory = activeCategory === 'all' || product.category === activeCategory;
                const matchesSearch = product.name.toLowerCase().includes(searchQuery.toLowerCase()) || 
                                      product.description.toLowerCase().includes(searchQuery.toLowerCase());
                return matchesCategory && matchesSearch;
            });

            itemCount.textContent = filteredProducts.length;

            if (filteredProducts.length === 0) {
                productGrid.innerHTML = `
                    <div class="w-full text-center py-16 bg-white dark:bg-slate-900 rounded-2xl border border-dashed border-slate-300 dark:border-slate-800">
                        <i class="fa-solid fa-box-open text-4xl text-slate-400 mb-3"></i>
                        <h3 class="font-semibold text-lg text-slate-700 dark:text-slate-300">No products found</h3>
                        <p class="text-sm text-slate-500">Try adjusting your search or filter options.</p>
                    </div>
                `;
                return;
            }

            filteredProducts.forEach(product => {
                const card = document.createElement('article');
                card.className = 'product-card bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-2xl overflow-hidden shadow-sm hover:shadow-xl flex flex-col';
                
                // Card HTML structure meeting Step 2: Image, Name, Price, Button
                card.innerHTML = `
                    <div class="relative aspect-video sm:aspect-square overflow-hidden bg-slate-100 dark:bg-slate-800">
                        <img src="${product.image}" alt="${product.name}" 
                             loading="lazy"
                             onerror="this.src='https://placehold.co/600x400/e2e8f0/475569?text=Product+Image'"
                             class="w-full h-full object-cover transition-transform duration-500 hover:scale-105">
                        <span class="absolute top-3 right-3 bg-white/90 dark:bg-slate-900/90 backdrop-blur-md px-2.5 py-1 rounded-full text-xs font-semibold shadow-sm flex items-center gap-1 text-amber-500">
                            <i class="fa-solid fa-star text-[10px]"></i> ${product.rating}
                        </span>
                    </div>

                    <div class="p-5 flex flex-col flex-1 justify-between">
                        <div>
                            <span class="text-[11px] font-bold tracking-wider text-blue-600 dark:text-blue-400 uppercase">${product.category}</span>
                            <h3 class="font-bold text-base sm:text-lg text-slate-900 dark:text-white mt-1 leading-snug">${product.name}</h3>
                            <p class="text-xs text-slate-500 dark:text-slate-400 mt-2 line-clamp-2 leading-relaxed">${product.description}</p>
                        </div>

                        <div class="mt-5 pt-4 border-t border-slate-100 dark:border-slate-800/80 flex items-center justify-between gap-2">
                            <div>
                                <span class="text-[10px] text-slate-400 block font-medium">Price</span>
                                <span class="text-lg sm:text-xl font-extrabold text-slate-900 dark:text-white">$${product.price.toFixed(2)}</span>
                            </div>
                            
                            <!-- Interactive Button -->
                            <button onclick="addToCart('${product.name}')" 
                                    class="px-4 py-2 bg-blue-600 hover:bg-blue-700 active:scale-95 text-white font-medium text-xs sm:text-sm rounded-xl shadow-md shadow-blue-500/20 flex items-center gap-2 transition-all">
                                <i class="fa-solid fa-cart-plus"></i>
                                Add to Cart
                            </button>
                        </div>
                    </div>
                `;
                productGrid.appendChild(card);
            });
        }

        // Add to Cart Toast Notification
        function addToCart(productName) {
            cartCount++;
            cartBadge.textContent = cartCount;
            cartBadge.classList.remove('opacity-0');

            // Create Toast
            const toast = document.createElement('div');
            toast.className = 'pointer-events-auto bg-slate-900 dark:bg-white text-white dark:text-slate-900 px-4 py-3 rounded-xl shadow-2xl flex items-center gap-3 transform translate-y-4 opacity-0 transition-all duration-300 text-xs sm:text-sm font-medium';
            toast.innerHTML = `
                <i class="fa-solid fa-circle-check text-emerald-400 dark:text-emerald-600 text-base"></i>
                <span>Added <strong>${productName}</strong> to cart!</span>
            `;

            const toastContainer = document.getElementById('toastContainer');
            toastContainer.appendChild(toast);

            // Animate In
            requestAnimationFrame(() => {
                toast.classList.remove('translate-y-4', 'opacity-0');
            });

            // Remove Toast
            setTimeout(() => {
                toast.classList.add('translate-y-4', 'opacity-0');
                setTimeout(() => toast.remove(), 300);
            }, 3000);
        }

        // Search Listener
        searchInput.addEventListener('input', (e) => {
            searchQuery = e.target.value;
            renderProducts();
        });

        // Category Filter Listener
        categoryFilters.addEventListener('click', (e) => {
            const btn = e.target.closest('.filter-btn');
            if (!btn) return;

            document.querySelectorAll('.filter-btn').forEach(b => {
                b.classList.remove('bg-blue-600', 'text-white', 'shadow-md', 'shadow-blue-500/20');
                b.classList.add('bg-white', 'dark:bg-slate-900', 'text-slate-600', 'dark:text-slate-300', 'hover:bg-slate-100', 'dark:hover:bg-slate-800');
            });

            btn.classList.remove('bg-white', 'dark:bg-slate-900', 'text-slate-600', 'dark:text-slate-300', 'hover:bg-slate-100', 'dark:hover:bg-slate-800');
            btn.classList.add('bg-blue-600', 'text-white', 'shadow-md', 'shadow-blue-500/20');

            activeCategory = btn.dataset.category;
            renderProducts();
        });

        // Dark Mode Toggle Logic
        themeToggle.addEventListener('click', () => {
            document.documentElement.classList.toggle('dark');
        });

        // Viewport Size Responsive Indicator
        function updateViewportIndicator() {
            const width = window.innerWidth;
            let label = 'Desktop';
            if (width < 640) label = `Mobile (${width}px)`;
            else if (width < 1024) label = `Tablet (${width}px)`;
            else label = `Desktop (${width}px)`;

            viewportWidth.textContent = `Viewport: ${label}`;
        }

        window.addEventListener('resize', updateViewportIndicator);

        // Initial Initialization
        window.onload = function() {
            renderProducts();
            updateViewportIndicator();
        };
    </script>
</body>
</html>