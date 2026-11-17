<!DOCTYPE html>
<html lang="id" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>UMKM Nexus - Enterprise Pro Dashboard & Katalog</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: { 50: '#eef2ff', 500: '#6366f1', 600: '#4f46e5', 700: '#4338ca' }
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; }
        .glass-card { background: rgba(255, 255, 255, 0.05); backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.1); }
        .dark .glass-card { background: rgba(15, 23, 42, 0.7); border: 1px solid rgba(255, 255, 255, 0.05); }
    </style>
</head>
<body class="bg-slate-50 dark:bg-slate-950 text-slate-800 dark:text-slate-100 min-h-screen transition-colors duration-300">

    <!-- TOP NAVIGATION BAR -->
    <header class="sticky top-0 z-50 backdrop-blur-md bg-white/70 dark:bg-slate-900/70 border-b border-slate-200 dark:border-slate-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-indigo-600 to-violet-500 flex items-center justify-center text-white font-bold text-xl shadow-lg shadow-indigo-500/30">
                    <i class="fa-solid fa-store"></i>
                </div>
                <div>
                    <span class="text-lg font-bold tracking-tight bg-gradient-to-r from-indigo-500 to-violet-500 bg-clip-text text-transparent">UMKM Nexus</span>
                    <span class="hidden sm:inline-block ml-2 text-xs px-2 py-0.5 rounded-full bg-indigo-500/10 text-indigo-500 font-semibold border border-indigo-500/20">v2.5 Pro</span>
                </div>
            </div>

            <!-- Search & Actions -->
            <div class="flex items-center space-x-4">
                <div class="relative hidden md:block w-64">
                    <span class="absolute inset-y-0 left-0 flex items-center pl-3 text-slate-400"><i class="fa-solid fa-search"></i></span>
                    <input type="text" id="searchInput" onkeyup="filterProducts()" placeholder="Cari kuliner lezat..." class="w-full pl-10 pr-4 py-2 text-sm bg-slate-100 dark:bg-slate-800/50 border border-slate-200 dark:border-slate-700 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-500 transition">
                </div>

                <!-- Dark Mode Toggle -->
                <button onclick="toggleDarkMode()" class="w-10 h-10 rounded-xl bg-slate-100 dark:bg-slate-800 flex items-center justify-center text-slate-600 dark:text-slate-300 hover:bg-slate-200 dark:hover:bg-slate-700 transition">
                    <i id="themeIcon" class="fa-solid fa-moon"></i>
                </button>

                <!-- Cart Button -->
                <button onclick="toggleCartModal()" class="relative w-10 h-10 rounded-xl bg-indigo-600 text-white flex items-center justify-center hover:bg-indigo-700 transition shadow-md shadow-indigo-600/20">
                    <i class="fa-solid fa-cart-shopping"></i>
                    <span id="cartBadge" class="absolute -top-1 -right-1 w-5 h-5 rounded-full bg-rose-500 text-white text-xs flex items-center justify-center font-bold">0</span>
                </button>
            </div>
        </div>
    </header>

    <!-- HERO SECTION -->
    <section class="relative overflow-hidden py-16 lg:py-24 border-b border-slate-200 dark:border-slate-800">
        <div class="absolute inset-0 bg-gradient-to-tr from-indigo-500/10 via-transparent to-violet-500/10 pointer-events-none"></div>
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10 text-center">
            <span class="px-3 py-1 rounded-full text-xs font-semibold bg-indigo-500/10 text-indigo-500 border border-indigo-500/20 inline-block mb-4">🚀 Pusat Kuliner & Jajanan Nusantara Terkurasi</span>
            <h1 class="text-4xl sm:text-6xl font-extrabold tracking-tight mb-6">
                Katalog Digital UMKM <span class="bg-gradient-to-r from-indigo-500 to-violet-500 bg-clip-text text-transparent">Masa Kini</span>
            </h1>
            <p class="max-w-2xl mx-auto text-slate-600 dark:text-slate-400 text-base sm:text-lg mb-8">
                Platform mandiri berkinerja tinggi untuk memamerkan produk kuliner lokal pilihan langsung ke genggaman pelanggan via QR Code & Web App.
            </p>
            <div class="flex flex-wrap justify-center gap-4">
                <a href="#katalog" class="px-6 py-3 rounded-xl bg-indigo-600 text-white font-semibold hover:bg-indigo-700 transition shadow-lg shadow-indigo-600/30">Jelajahi Menu <i class="fa-solid fa-arrow-down ml-2"></i></a>
                <button onclick="openQrModal()" class="px-6 py-3 rounded-xl bg-slate-200 dark:bg-slate-800 font-semibold hover:bg-slate-300 dark:hover:bg-slate-700 transition"><i class="fa-solid fa-qrcode mr-2 text-indigo-500"></i> Buat QR Code Toko</button>
            </div>
        </div>
    </section>

    <!-- STATS DASHBOARD BAR -->
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 -mt-8 relative z-20 mb-12">
        <div class="grid grid-cols-1 sm:grid-cols-3 gap-6">
            <div class="glass-card p-6 rounded-2xl shadow-xl flex items-center space-x-4">
                <div class="w-12 h-12 rounded-xl bg-emerald-500/10 text-emerald-500 flex items-center justify-center text-xl font-bold"><i class="fa-solid fa-utensils"></i></div>
                <div>
                    <p class="text-sm text-slate-500 dark:text-slate-400 font-medium">Total Produk Aktif</p>
                    <h3 class="text-2xl font-bold">6 Varian</h3>
                </div>
            </div>
            <div class="glass-card p-6 rounded-2xl shadow-xl flex items-center space-x-4">
                <div class="w-12 h-12 rounded-xl bg-indigo-500/10 text-indigo-500 flex items-center justify-center text-xl font-bold"><i class="fa-solid fa-store"></i></div>
                <div>
                    <p class="text-sm text-slate-500 dark:text-slate-400 font-medium">Mitra UMKM Terdaftar</p>
                    <h3 class="text-2xl font-bold">1 Lokal Utama</h3>
                </div>
            </div>
            <div class="glass-card p-6 rounded-2xl shadow-xl flex items-center space-x-4">
                <div class="w-12 h-12 rounded-xl bg-amber-500/10 text-amber-500 flex items-center justify-center text-xl font-bold"><i class="fa-solid fa-star"></i></div>
                <div>
                    <p class="text-sm text-slate-500 dark:text-slate-400 font-medium">Rating Kepuasan</p>
                    <h3 class="text-2xl font-bold">4.9 / 5.0</h3>
                </div>
            </div>
        </div>
    </div>

    <!-- MAIN CATALOG SECTION -->
    <main id="katalog" class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pb-20">
        <div class="flex flex-col md:flex-row md:items-center justify-between mb-8 gap-4">
            <div>
                <h2 class="text-2xl font-bold tracking-tight">Daftar Produk Kuliner</h2>
                <p class="text-sm text-slate-500 dark:text-slate-400">Pilih menu favorit Anda dan langsung pesan lewat WhatsApp.</p>
            </div>
            <!-- Category Filters -->
            <div class="flex flex-wrap gap-2" id="categoryFilters">
                <button onclick="filterCategory('all')" class="px-4 py-2 rounded-xl text-sm font-semibold bg-indigo-600 text-white transition category-btn" data-cat="all">Semua</button>
                <button onclick="filterCategory('makanan')" class="px-4 py-2 rounded-xl text-sm font-semibold bg-slate-200 dark:bg-slate-800 hover:bg-slate-300 dark:hover:bg-slate-700 transition category-btn" data-cat="makanan">Makanan Berat</button>
                <button onclick="filterCategory('camilan')" class="px-4 py-2 rounded-xl text-sm font-semibold bg-slate-200 dark:bg-slate-800 hover:bg-slate-300 dark:hover:bg-slate-700 transition category-btn" data-cat="camilan">Camilan</button>
                <button onclick="filterCategory('minuman')" class="px-4 py-2 rounded-xl text-sm font-semibold bg-slate-200 dark:bg-slate-800 hover:bg-slate-300 dark:hover:bg-slate-700 transition category-btn" data-cat="minuman">Minuman</button>
            </div>
        </div>

        <!-- PRODUCT GRID -->
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8" id="productGrid">
            <!-- Rendered via JavaScript for high dynamic vibe -->
        </div>
    </main>

    <!-- CART MODAL DRAWER -->
    <div id="cartModal" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm hidden flex justify-end">
        <div class="w-full max-w-md bg-white dark:bg-slate-900 h-full p-6 flex flex-col shadow-2xl transition-transform">
            <div class="flex items-center justify-between pb-4 border-b border-slate-200 dark:border-slate-800">
                <h3 class="text-lg font-bold flex items-center"><i class="fa-solid fa-cart-shopping mr-2 text-indigo-500"></i> Keranjang Belanja</h3>
                <button onclick="toggleCartModal()" class="w-8 h-8 rounded-lg bg-slate-100 dark:bg-slate-800 flex items-center justify-center hover:bg-slate-200 dark:hover:bg-slate-700"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <div id="cartItemsContainer" class="flex-1 overflow-y-auto py-4 space-y-4">
                <!-- Cart list dynamic -->
            </div>
            <div class="pt-4 border-t border-slate-200 dark:border-slate-800">
                <div class="flex justify-between mb-4 font-bold text-lg">
                    <span>Total:</span>
                    <span id="cartTotalPrice" class="text-indigo-500">Rp 0</span>
                </div>
                <button onclick="checkoutWhatsApp()" class="w-full py-3 rounded-xl bg-emerald-600 text-white font-semibold hover:bg-emerald-700 transition shadow-lg shadow-emerald-600/30 flex items-center justify-center">
                    <i class="fa-brands fa-whatsapp mr-2 text-xl"></i> Pesan via WhatsApp Sekarang
                </button>
            </div>
        </div>
    </div>

    <!-- QR CODE GENERATOR MODAL -->
    <div id="qrModal" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm hidden flex items-center justify-center p-4">
        <div class="w-full max-w-md bg-white dark:bg-slate-900 rounded-2xl p-6 shadow-2xl border border-slate-200 dark:border-slate-800 text-center">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-lg font-bold"><i class="fa-solid fa-qrcode mr-2 text-indigo-500"></i> QR Code Web Katalog</h3>
                <button onclick="openQrModal()" class="w-8 h-8 rounded-lg bg-slate-100 dark:bg-slate-800 flex items-center justify-center"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <p class="text-sm text-slate-500 dark:text-slate-400 mb-6">Pindai kode QR di bawah untuk membuka katalog langsung dari perangkat seluler Anda.</p>
            <div class="bg-white p-4 inline-block rounded-xl shadow-inner mb-6 border border-slate-200">
                <img id="qrImageDisplay" src="" alt="QR Code" class="w-48 h-48 mx-auto object-contain">
            </div>
            <p id="currentUrlText" class="text-xs font-mono bg-slate-100 dark:bg-slate-800 p-2 rounded-lg break-all text-slate-500 mb-4"></p>
            <button onclick="openQrModal()" class="w-full py-2.5 rounded-xl bg-indigo-600 text-white font-semibold hover:bg-indigo-700 transition">Tutup</button>
        </div>
    </div>

    <!-- FOOTER -->
    <footer class="border-t border-slate-200 dark:border-slate-800 bg-white/50 dark:bg-slate-950/50 py-8">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center text-sm text-slate-500 dark:text-slate-400">
            <p>&copy; 2026 UMKM Nexus Enterprise. Dibangun dengan penuh semangat dan arsitektur Vibe Coding.</p>
        </div>
    </footer>

    <!-- JAVASCRIPT LOGIC EXPERT LAYER -->
    <script>
        // Database Produk Katalog UMKM
        const products = [
            { id: 1, name: "Kue Lumpur Tradisional", category: "camilan", price: 15000, desc: "Kue basah tradisional bertekstur lembut dengan taburan kismis manis di atasnya.", image: "images/kue-lumpur.jpg" },
            { id: 2, name: "Es Cendol Durian", category: "minuman", price: 20000, desc: "Minuman segar es cendol dipadu dengan daging buah durian asli pilihan.", image: "images/es-cendol.jpg" },
            { id: 3, name: "Keripik Singkong Balado", category: "camilan", price: 12000, desc: "Keripik singkong renyah dengan bumbu balado pedas manis khas rumahan.", image: "images/keripik-singkong.jpg" },
            { id: 4, name: "Pempek Palembang Asli", category: "makanan", price: 25000, desc: "Pempek ikan tenggiri asli lengkap dengan cuko hitam pedas mantap.", image: "images/pempek.jpg" },
            { id: 5, name: "Kopi Tubruk Nusantara", category: "minuman", price: 10000, desc: "Kopi hitam murni pilihan biji kopi terbaik dari dataran tinggi lokal.", image: "images/kopi-tubruk.jpg" },
            { id: 6, name: "Risoles Mayo Spesial", category: "camilan", price: 8000, desc: "Risoles isi ragout ayam padat berbalut mayones creamy dan telur.", image: "images/risoles.jpg" }
        ];

        let cart = [];
        let currentCategory = 'all';

        // Render Products to Grid
        function renderProducts(filteredList = products) {
            const grid = document.getElementById('productGrid');
            grid.innerHTML = '';
            
            if(filteredList.length === 0) {
                grid.innerHTML = `<div class="col-span-full text-center py-12 text-slate-400"><i class="fa-solid fa-box-open text-4xl mb-3"></i><p>Tidak ada produk yang ditemukan.</p></div>`;
                return;
            }

            filteredList.forEach(p => {
                grid.innerHTML += `
                    <div class="glass-card rounded-2xl overflow-hidden shadow-xl hover:-translate-y-1 transition duration-300 flex flex-col justify-between">
                        <div>
                            <div class="h-48 overflow-hidden relative bg-slate-200 dark:bg-slate-800">
                                <img src="${p.image}" alt="${p.name}" class="w-full h-full object-cover hover:scale-105 transition duration-500" onerror="this.src='https://images.unsplash.com/photo-1546069901-ba9599a7e63c?auto=format&fit=crop&w=600&q=80'">
                                <span class="absolute top-3 right-3 px-3 py-1 rounded-full text-xs font-bold uppercase tracking-wider bg-slate-900/70 text-white backdrop-blur-md">${p.category}</span>
                            </div>
                            <div class="p-6">
                                <h3 class="text-lg font-bold mb-2">${p.name}</h3>
                                <p class="text-sm text-slate-500 dark:text-slate-400 mb-4 line-clamp-2">${p.desc}</p>
                            </div>
                        </div>
                        <div class="p-6 pt-0 flex items-center justify-between">
                            <span class="text-lg font-extrabold text-indigo-500">Rp ${p.price.toLocaleString('id-ID')}</span>
                            <button onclick="addToCart(${p.id})" class="px-4 py-2 rounded-xl bg-indigo-600 text-white text-sm font-semibold hover:bg-indigo-700 transition shadow-md shadow-indigo-600/20"><i class="fa-solid fa-cart-plus mr-1"></i> Beli</button>
                        </div>
                    </div>
                `;
            });
        }

        // Filter Category
        function filterCategory(cat) {
            currentCategory = cat;
            document.querySelectorAll('.category-btn').forEach(btn => {
                if(btn.dataset.cat === cat) {
                    btn.className = "px-4 py-2 rounded-xl text-sm font-semibold bg-indigo-600 text-white transition category-btn shadow-md shadow-indigo-600/20";
                } else {
                    btn.className = "px-4 py-2 rounded-xl text-sm font-semibold bg-slate-200 dark:bg-slate-800 hover:bg-slate-300 dark:hover:bg-slate-700 transition category-btn";
                }
            });

            if(cat === 'all') {
                renderProducts(products);
            } else {
                const filtered = products.filter(p => p.category === cat);
                renderProducts(filtered);
            }
        }

        // Live Search Filter
        function filterProducts() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const filtered = products.filter(p => p.name.toLowerCase().includes(query) || p.desc.toLowerCase().includes(query));
            renderProducts(filtered);
        }

        // Cart Management
        function addToCart(id) {
            const product = products.find(p => p.id === id);
            const existing = cart.find(item => item.id === id);
            if(existing) {
                existing.qty++;
            } else {
                cart.push({ ...product, qty: 1 });
            }
            updateCartUI();
            toggleCartModal();
        }

        function updateCartUI() {
            const badge = document.getElementById('cartBadge');
            const container = document.getElementById('cartItemsContainer');
            const totalElement = document.getElementById('cartTotalPrice');

            const totalQty = cart.reduce((sum, item) => sum + item.qty, 0);
            badge.innerText = totalQty;

            container.innerHTML = '';
            if(cart.length === 0) {
                container.innerHTML = `<div class="text-center text-slate-400 py-12"><i class="fa-solid fa-basket-shopping text-3xl mb-2"></i><p>Keranjang masih kosong.</p></div>`;
                totalElement.innerText = 'Rp 0';
                return;
            }

            let totalPrice = 0;
            cart.forEach((item, index) => {
                totalPrice += item.price * item.qty;
                container.innerHTML += `
                    <div class="flex items-center justify-between p-3 rounded-xl bg-slate-100 dark:bg-slate-800/50">
                        <div class="flex-1">
                            <h4 class="text-sm font-bold">${item.name}</h4>
                            <p class="text-xs text-slate-500">Rp ${item.price.toLocaleString('id-ID')} x ${item.qty}</p>
                        </div>
                        <div class="flex items-center space-x-2">
                            <button onclick="changeQty(${index}, -1)" class="w-7 h-7 rounded-lg bg-slate-200 dark:bg-slate-700 flex items-center justify-center font-bold">-</button>
                            <span class="text-sm font-bold w-5 text-center">${item.qty}</span>
                            <button onclick="changeQty(${index}, 1)" class="w-7 h-7 rounded-lg bg-slate-200 dark:bg-slate-700 flex items-center justify-center font-bold">+</button>
                        </div>
                    </div>
                `;
            });

            totalElement.innerText = `Rp ${totalPrice.toLocaleString('id-ID')}`;
        }

        function changeQty(index, amount) {
            cart[index].qty += amount;
            if(cart[index].qty <= 0) {
                cart.splice(index, 1);
            }
            updateCartUI();
        }

        function toggleCartModal() {
            const modal = document.getElementById('cartModal');
            modal.classList.toggle('hidden');
        }

        // WhatsApp Checkout Integration
        function checkoutWhatsApp() {
            if(cart.length === 0) {
                alert('Keranjang belanja Anda masih kosong!');
                return;
            }

            let text = "Halo Kak, saya ingin memesan produk kul berikut:\n\n";
            let total = 0;
            cart.forEach((item, i) => {
                text += `${i+1}. ${item.name} (${item.qty}x) - Rp ${(item.price * item.qty).toLocaleString('id-ID')}\n`;
                total += item.price * item.qty;
            });
            text += `\n*Total Keseluruhan: Rp ${total.toLocaleString('id-ID')}*\n\nMohon informasi ketersediaan dan proses pengirimannya. Terima kasih!`;

            const encoded = encodeURIComponent(text);
            window.open(`https://wa.me/6281234567890?text=${encoded}`, '_blank');
        }

        // QR Code Modal Toggle & Generator
        function openQrModal() {
            const modal = document.getElementById('qrModal');
            modal.classList.toggle('hidden');
            const currentUrl = window.location.href;
            document.getElementById('currentUrlText').innerText = currentUrl;
            document.getElementById('qrImageDisplay').src = `https://api.qrserver.com/v1/create-qr-code/?size=250x250&data=${encodeURIComponent(currentUrl)}`;
        }

        // Dark Mode Toggle
        function toggleDarkMode() {
            const html = document.documentElement;
            const icon = document.getElementById('themeIcon');
            html.classList.toggle('dark');
            if(html.classList.contains('dark')) {
                icon.className = "fa-solid fa-sun";
            } else {
                icon.className = "fa-solid fa-moon";
            }
        }

        // Initial Load
        window.onload = () => {
            renderProducts();
        };
    </script>
</body>
</html>
