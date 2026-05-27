# nabil3isamili.-github.-io
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title id="pageTitle">Boutique</title>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;0,700;1,400&family=Inter:wght@300;400;500&display=swap" rel="stylesheet">
    <style>
        :root {
            --gold: #C9A96E;
            --gold-light: #E8D5A3;
            --black: #0a0a0a;
            --dark-gray: #1a1a1a;
            --medium-gray: #2a2a2a;
            --light-gray: #888;
            --white: #f5f5f0;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--black);
            color: var(--white);
            overflow-x: hidden;
        }

        /* Video Background */
        .video-container {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            z-index: -1;
            overflow: hidden;
        }
        .video-container video {
            min-width: 100%; min-height: 100%;
            object-fit: cover;
            opacity: 0.35;
        }
        .video-overlay {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: linear-gradient(to bottom, rgba(10,10,10,0.2), rgba(10,10,10,0.85));
            z-index: -1;
        }

        /* Navigation */
        nav {
            position: fixed;
            top: 0; width: 100%;
            padding: 2rem 4rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 1000;
            background: linear-gradient(to bottom, rgba(10,10,10,0.9), transparent);
        }
        .logo {
            font-family: 'Playfair Display', serif;
            font-size: 1.8rem;
            font-weight: 700;
            letter-spacing: 4px;
            color: var(--gold);
        }
        .nav-links {
            display: flex;
            gap: 3rem;
            list-style: none;
        }
        .nav-links a {
            text-decoration: none;
            color: var(--white);
            font-size: 0.85rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            transition: color 0.3s;
            position: relative;
            cursor: pointer;
        }
        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -5px; left: 0;
            width: 0; height: 1px;
            background: var(--gold);
            transition: width 0.3s;
        }
        .nav-links a:hover { color: var(--gold); }
        .nav-links a:hover::after { width: 100%; }

        /* Settings Panel */
        .settings-btn {
            position: fixed;
            top: 1.5rem;
            right: 1.5rem;
            z-index: 1001;
            background: rgba(201, 169, 110, 0.2);
            border: 1px solid var(--gold);
            color: var(--gold);
            padding: 0.6rem 1.2rem;
            font-family: 'Inter', sans-serif;
            font-size: 0.75rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            cursor: pointer;
            transition: all 0.3s;
            backdrop-filter: blur(10px);
        }
        .settings-btn:hover {
            background: var(--gold);
            color: var(--black);
        }

        .settings-panel {
            position: fixed;
            top: 0; right: -500px;
            width: 500px;
            height: 100vh;
            background: var(--dark-gray);
            border-left: 1px solid var(--medium-gray);
            z-index: 2000;
            overflow-y: auto;
            transition: right 0.4s ease;
            padding: 2rem;
        }
        .settings-panel.open { right: 0; }
        .settings-panel h2 {
            font-family: 'Playfair Display', serif;
            font-size: 1.5rem;
            margin-bottom: 1.5rem;
            color: var(--gold);
        }
        .settings-panel .close-btn {
            position: absolute;
            top: 1.5rem; right: 1.5rem;
            background: none;
            border: none;
            color: var(--light-gray);
            font-size: 1.5rem;
            cursor: pointer;
        }
        .settings-panel .close-btn:hover { color: var(--gold); }

        .setting-group {
            margin-bottom: 1.5rem;
            padding-bottom: 1.5rem;
            border-bottom: 1px solid var(--medium-gray);
        }
        .setting-group label {
            display: block;
            font-size: 0.75rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            color: var(--light-gray);
            margin-bottom: 0.5rem;
        }
        .setting-group input,
        .setting-group textarea {
            width: 100%;
            padding: 0.8rem;
            background: var(--black);
            border: 1px solid var(--medium-gray);
            color: var(--white);
            font-family: 'Inter', sans-serif;
            font-size: 0.9rem;
            transition: border-color 0.3s;
        }
        .setting-group input:focus,
        .setting-group textarea:focus {
            outline: none;
            border-color: var(--gold);
        }
        .setting-group textarea { min-height: 80px; resize: vertical; }

        .save-settings-btn {
            width: 100%;
            padding: 1rem;
            background: var(--gold);
            border: none;
            color: var(--black);
            font-family: 'Inter', sans-serif;
            font-size: 0.85rem;
            letter-spacing: 3px;
            text-transform: uppercase;
            cursor: pointer;
            font-weight: 500;
            margin-bottom: 1rem;
            transition: all 0.3s;
        }
        .save-settings-btn:hover {
            background: var(--gold-light);
        }
        .reset-settings-btn {
            width: 100%;
            padding: 0.8rem;
            background: transparent;
            border: 1px solid var(--medium-gray);
            color: var(--light-gray);
            font-family: 'Inter', sans-serif;
            font-size: 0.8rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            cursor: pointer;
            transition: all 0.3s;
        }
        .reset-settings-btn:hover {
            border-color: #c44;
            color: #c44;
        }
        .save-status {
            text-align: center;
            font-size: 0.8rem;
            color: var(--gold);
            margin-top: 1rem;
            opacity: 0;
            transition: opacity 0.3s;
        }
        .save-status.show { opacity: 1; }

        /* Hero Section */
        .hero {
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 0 2rem;
            position: relative;
        }
        .hero-subtitle {
            font-family: 'Inter', sans-serif;
            font-size: 0.9rem;
            letter-spacing: 6px;
            text-transform: uppercase;
            color: var(--gold);
            margin-bottom: 2rem;
            opacity: 0;
            animation: fadeInUp 1s ease forwards 0.5s;
        }
        .hero-title {
            font-family: 'Playfair Display', serif;
            font-size: clamp(3rem, 8vw, 6rem);
            font-weight: 400;
            line-height: 1.1;
            margin-bottom: 2rem;
            opacity: 0;
            animation: fadeInUp 1s ease forwards 0.8s;
        }
        .hero-title em {
            font-style: italic;
            color: var(--gold-light);
        }
        .hero-desc {
            font-size: 1.1rem;
            color: var(--light-gray);
            max-width: 600px;
            line-height: 1.8;
            margin-bottom: 3rem;
            opacity: 0;
            animation: fadeInUp 1s ease forwards 1.1s;
        }
        .cta-button {
            padding: 1.2rem 3rem;
            background: transparent;
            border: 1px solid var(--gold);
            color: var(--gold);
            font-family: 'Inter', sans-serif;
            font-size: 0.9rem;
            letter-spacing: 3px;
            text-transform: uppercase;
            cursor: pointer;
            transition: all 0.4s;
            text-decoration: none;
            display: inline-block;
            opacity: 0;
            animation: fadeInUp 1s ease forwards 1.4s;
        }
        .cta-button:hover {
            background: var(--gold);
            color: var(--black);
        }
        .scroll-indicator {
            position: absolute;
            bottom: 3rem;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 0.5rem;
            opacity: 0;
            animation: fadeIn 1s ease forwards 2s;
        }
        .scroll-indicator span {
            font-size: 0.7rem;
            letter-spacing: 3px;
            text-transform: uppercase;
            color: var(--light-gray);
        }
        .scroll-line {
            width: 1px;
            height: 60px;
            background: linear-gradient(to bottom, var(--gold), transparent);
            animation: scrollPulse 2s infinite;
        }

        /* Products Section */
        .products-section {
            padding: 8rem 4rem;
            background: linear-gradient(to bottom, transparent, var(--black) 20%);
            position: relative;
        }
        .section-header {
            text-align: center;
            margin-bottom: 5rem;
        }
        .section-label {
            font-size: 0.8rem;
            letter-spacing: 4px;
            text-transform: uppercase;
            color: var(--gold);
            margin-bottom: 1rem;
        }
        .section-title {
            font-family: 'Playfair Display', serif;
            font-size: clamp(2rem, 5vw, 3.5rem);
            font-weight: 400;
        }

        /* Product Form */
        .product-form {
            max-width: 800px;
            margin: 0 auto 5rem;
            background: var(--dark-gray);
            padding: 3rem;
            border: 1px solid var(--medium-gray);
        }
        .form-group { margin-bottom: 1.5rem; }
        .form-group label {
            display: block;
            font-size: 0.8rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            color: var(--light-gray);
            margin-bottom: 0.5rem;
        }
        .form-group input,
        .form-group textarea {
            width: 100%;
            padding: 1rem;
            background: var(--black);
            border: 1px solid var(--medium-gray);
            color: var(--white);
            font-family: 'Inter', sans-serif;
            font-size: 1rem;
            transition: border-color 0.3s;
        }
        .form-group input:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: var(--gold);
        }
        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1.5rem;
        }
        .submit-btn {
            width: 100%;
            padding: 1.2rem;
            background: var(--gold);
            border: none;
            color: var(--black);
            font-family: 'Inter', sans-serif;
            font-size: 0.9rem;
            letter-spacing: 3px;
            text-transform: uppercase;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: 500;
        }
        .submit-btn:hover {
            background: var(--gold-light);
            transform: translateY(-2px);
        }

        /* Products Grid */
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
            gap: 3rem;
            max-width: 1400px;
            margin: 0 auto;
        }
        .product-card {
            background: var(--dark-gray);
            border: 1px solid var(--medium-gray);
            overflow: hidden;
            transition: all 0.4s;
            position: relative;
        }
        .product-card::before {
            content: '';
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: linear-gradient(to bottom, transparent 50%, rgba(201, 169, 110, 0.1));
            opacity: 0;
            transition: opacity 0.4s;
            pointer-events: none;
            z-index: 1;
        }
        .product-card:hover::before { opacity: 1; }
        .product-card:hover {
            transform: translateY(-10px);
            border-color: var(--gold);
        }
        .product-image {
            width: 100%;
            height: 400px;
            background: var(--medium-gray);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 4rem;
            color: var(--light-gray);
            position: relative;
            overflow: hidden;
        }
        .product-image img {
            width: 100%; height: 100%;
            object-fit: cover;
            transition: transform 0.6s;
        }
        .product-card:hover .product-image img { transform: scale(1.05); }
        .product-badge {
            position: absolute;
            top: 1.5rem; left: 1.5rem;
            background: var(--gold);
            color: var(--black);
            padding: 0.5rem 1rem;
            font-size: 0.7rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            font-weight: 500;
        }
        .product-info { padding: 2rem; }
        .product-category {
            font-size: 0.75rem;
            letter-spacing: 3px;
            text-transform: uppercase;
            color: var(--gold);
            margin-bottom: 0.5rem;
        }
        .product-name {
            font-family: 'Playfair Display', serif;
            font-size: 1.5rem;
            margin-bottom: 1rem;
        }
        .product-description {
            font-size: 0.9rem;
            color: var(--light-gray);
            line-height: 1.6;
            margin-bottom: 1.5rem;
        }
        .product-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-top: 1.5rem;
            border-top: 1px solid var(--medium-gray);
        }
        .product-price {
            font-family: 'Playfair Display', serif;
            font-size: 1.8rem;
            color: var(--gold);
        }
        .product-price span {
            font-size: 1rem;
            color: var(--light-gray);
        }
        .buy-button {
            padding: 0.8rem 2rem;
            background: transparent;
            border: 1px solid var(--gold);
            color: var(--gold);
            font-family: 'Inter', sans-serif;
            font-size: 0.8rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            cursor: pointer;
            transition: all 0.3s;
        }
        .buy-button:hover {
            background: var(--gold);
            color: var(--black);
        }
        .empty-state {
            text-align: center;
            padding: 4rem;
            color: var(--light-gray);
            grid-column: 1 / -1;
        }
        .empty-state-icon {
            font-size: 3rem;
            margin-bottom: 1rem;
            opacity: 0.5;
        }

        /* Info Section */
        .info-section {
            padding: 8rem 4rem;
            background: var(--dark-gray);
            position: relative;
        }
        .info-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 4rem;
            max-width: 1200px;
            margin: 0 auto;
        }
        .info-card {
            text-align: center;
            padding: 3rem 2rem;
            border: 1px solid var(--medium-gray);
            transition: all 0.3s;
        }
        .info-card:hover {
            border-color: var(--gold);
            transform: translateY(-5px);
        }
        .info-icon {
            font-size: 2.5rem;
            margin-bottom: 1.5rem;
            color: var(--gold);
        }
        .info-title {
            font-family: 'Playfair Display', serif;
            font-size: 1.3rem;
            margin-bottom: 1rem;
        }
        .info-text {
            font-size: 0.9rem;
            color: var(--light-gray);
            line-height: 1.7;
        }

        /* Footer */
        footer {
            padding: 4rem;
            text-align: center;
            border-top: 1px solid var(--medium-gray);
        }
        .footer-logo {
            font-family: 'Playfair Display', serif;
            font-size: 2rem;
            color: var(--gold);
            margin-bottom: 1rem;
        }
        .footer-text {
            font-size: 0.85rem;
            color: var(--light-gray);
            margin-bottom: 2rem;
        }
        .footer-links {
            display: flex;
            justify-content: center;
            gap: 2rem;
            margin-bottom: 2rem;
        }
        .footer-links a {
            color: var(--light-gray);
            text-decoration: none;
            font-size: 0.8rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            transition: color 0.3s;
        }
        .footer-links a:hover { color: var(--gold); }
        .copyright {
            font-size: 0.75rem;
            color: var(--light-gray);
            letter-spacing: 1px;
        }

        /* Animations */
        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        @keyframes scrollPulse {
            0%, 100% { opacity: 1; transform: scaleY(1); }
            50% { opacity: 0.5; transform: scaleY(0.8); }
        }

        /* Responsive */
        @media (max-width: 768px) {
            nav { padding: 1.5rem 2rem; }
            .nav-links { display: none; }
            .settings-panel { width: 100%; right: -100%; }
            .form-row { grid-template-columns: 1fr; }
            .products-grid { grid-template-columns: 1fr; }
            .info-grid { grid-template-columns: 1fr; }
            .products-section, .info-section { padding: 4rem 2rem; }
        }

        .reveal {
            opacity: 0;
            transform: translateY(50px);
            transition: all 0.8s ease;
        }
        .reveal.active {
            opacity: 1;
            transform: translateY(0);
        }
    </style>
</head>
<body>
    <!-- Background Video -->
    <div class="video-container">
        <video autoplay muted loop playsinline id="bgVideo">
            <source src="https://assets.mixkit.co/videos/preview/mixkit-luxury-clothing-store-interior-4747-large.mp4" type="video/mp4">
        </video>
    </div>
    <div class="video-overlay"></div>

    <!-- Settings Button -->
    <button class="settings-btn" id="settingsBtn">⚙ Customize</button>

    <!-- Settings Panel -->
    <div class="settings-panel" id="settingsPanel">
        <button class="close-btn" id="closeSettings">✕</button>
        <h2>Customize Website</h2>

        <div class="setting-group">
            <label>Shop Name</label>
            <input type="text" id="configShopName" placeholder="Your shop name">
        </div>
        <div class="setting-group">
            <label>Subtitle (e.g., Est. 2024 — Algeria)</label>
            <input type="text" id="configSubtitle" placeholder="Subtitle text">
        </div>
        <div class="setting-group">
            <label>Hero Title Line 1</label>
            <input type="text" id="configHeroTitle1" placeholder="First line of main title">
        </div>
        <div class="setting-group">
            <label>Hero Title Line 2 (italic)</label>
            <input type="text" id="configHeroTitle2" placeholder="Second line (italic)">
        </div>
        <div class="setting-group">
            <label>Hero Description</label>
            <textarea id="configHeroDesc" placeholder="Description paragraph"></textarea>
        </div>
        <div class="setting-group">
            <label>CTA Button Text</label>
            <input type="text" id="configCtaText" placeholder="Button text">
        </div>
        <div class="setting-group">
            <label>Collection Section Title</label>
            <input type="text" id="configCollectionTitle" placeholder="e.g., Our Collection">
        </div>
        <div class="setting-group">
            <label>Delivery Info</label>
            <textarea id="configDelivery" placeholder="Delivery fees and info"></textarea>
        </div>
        <div class="setting-group">
            <label>Quality Info</label>
            <textarea id="configQuality" placeholder="Quality promise text"></textarea>
        </div>
        <div class="setting-group">
            <label>Service Info</label>
            <textarea id="configService" placeholder="Customer service info"></textarea>
        </div>
        <div class="setting-group">
            <label>Footer Text</label>
            <textarea id="configFooter" placeholder="Footer description"></textarea>
        </div>
        <div class="setting-group">
            <label>Contact Info</label>
            <input type="text" id="configContact" placeholder="Phone / Email">
        </div>

        <button class="save-settings-btn" id="saveSettings">💾 Save Changes</button>
        <button class="reset-settings-btn" id="resetSettings">↺ Reset to Default</button>
        <div class="save-status" id="saveStatus">✓ Saved! Refresh to see changes.</div>
    </div>

    <!-- Navigation -->
    <nav>
        <div class="logo" id="navLogo">BOUTIQUE</div>
        <ul class="nav-links">
            <li><a onclick="scrollToSection('home')">Home</a></li>
            <li><a onclick="scrollToSection('collection')">Collection</a></li>
            <li><a onclick="scrollToSection('about')">About</a></li>
            <li><a onclick="scrollToSection('contact')">Contact</a></li>
        </ul>
    </nav>

    <!-- Hero Section -->
    <section class="hero" id="home">
        <p class="hero-subtitle" id="heroSubtitle">Your Premium Shop</p>
        <h1 class="hero-title">
            <span id="heroTitle1">Welcome to</span><br>
            <em id="heroTitle2">Our Boutique</em>
        </h1>
        <p class="hero-desc" id="heroDesc">
            Discover our exclusive collection of premium products. 
            Quality and elegance delivered to your doorstep.
        </p>
        <a href="#collection" class="cta-button" id="ctaButton">Explore</a>

        <div class="scroll-indicator">
            <span>Scroll</span>
            <div class="scroll-line"></div>
        </div>
    </section>

    <!-- Products Section -->
    <section class="products-section" id="collection">
        <div class="section-header reveal">
            <p class="section-label">Curated Selection</p>
            <h2 class="section-title" id="collectionTitle">Our Collection</h2>
        </div>

        <!-- Add Product Form -->
        <div class="product-form reveal">
            <div class="section-header" style="margin-bottom: 2rem;">
                <p class="section-label">Admin Panel</p>
                <h3 style="font-family: 'Playfair Display', serif; font-size: 1.5rem;">Add New Product</h3>
            </div>
            <form id="productForm">
                <div class="form-row">
                    <div class="form-group">
                        <label>Product Name *</label>
                        <input type="text" id="prodName" placeholder="e.g., Leather Handbag" required>
                    </div>
                    <div class="form-group">
                        <label>Price (DZD) *</label>
                        <input type="number" id="prodPrice" placeholder="e.g., 12500" required>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label>Category</label>
                        <input type="text" id="prodCategory" placeholder="e.g., Fashion">
                    </div>
                    <div class="form-group">
                        <label>Badge (optional)</label>
                        <input type="text" id="prodBadge" placeholder="e.g., New, Sale, Hot">
                    </div>
                </div>
                <div class="form-group">
                    <label>Description</label>
                    <textarea id="prodDesc" rows="2" placeholder="Product description..."></textarea>
                </div>
                <div class="form-group">
                    <label>Image URL (optional)</label>
                    <input type="url" id="prodImage" placeholder="https://...">
                </div>
                <button type="submit" class="submit-btn">Add Product</button>
            </form>
        </div>

        <!-- Products Grid -->
        <div class="products-grid" id="productsGrid">
            <div class="empty-state" id="emptyState">
                <div class="empty-state-icon">📦</div>
                <p>No products yet. Use the form above to add your first product.</p>
            </div>
        </div>
    </section>

    <!-- Info Section -->
    <section class="info-section" id="about">
        <div class="section-header reveal">
            <p class="section-label">Why Choose Us</p>
            <h2 class="section-title">Our Promise</h2>
        </div>

        <div class="info-grid">
            <div class="info-card reveal">
                <div class="info-icon">🚚</div>
                <h3 class="info-title">Fast Delivery</h3>
                <p class="info-text" id="deliveryText">
                    Reliable delivery across Algeria. Competitive rates and express options available.
                </p>
            </div>

            <div class="info-card reveal">
                <div class="info-icon">✨</div>
                <h3 class="info-title">Premium Quality</h3>
                <p class="info-text" id="qualityText">
                    Carefully selected products. We ensure the highest standards for our customers.
                </p>
            </div>

            <div class="info-card reveal">
                <div class="info-icon">🤝</div>
                <h3 class="info-title">Trusted Service</h3>
                <p class="info-text" id="serviceText">
                    Cash on delivery available. Easy returns and dedicated customer support.
                </p>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer id="contact">
        <div class="footer-logo" id="footerLogo">BOUTIQUE</div>
        <p class="footer-text" id="footerText">
            Your trusted shop in Algeria. Quality products, excellent service.
        </p>
        <div class="footer-links">
            <a href="#">Instagram</a>
            <a href="#">Facebook</a>
            <a href="#">WhatsApp</a>
        </div>
        <p class="copyright" id="copyright">
            © 2024 All rights reserved. <span id="contactInfo">Contact us for more info</span>
        </p>
    </footer>

    <script src="config.js"></script>
    <script>
        // Product Form Handler
        const productForm = document.getElementById('productForm');
        const productsGrid = document.getElementById('productsGrid');
        const emptyState = document.getElementById('emptyState');
        let products = JSON.parse(localStorage.getItem('boutique_products') || '[]');

        function renderProducts() {
            if (products.length === 0) {
                emptyState.style.display = 'block';
                return;
            }
            emptyState.style.display = 'none';

            // Clear existing cards (keep empty state div)
            const cards = productsGrid.querySelectorAll('.product-card');
            cards.forEach(c => c.remove());

            products.forEach((prod, index) => {
                const card = document.createElement('div');
                card.className = 'product-card reveal active';
                const emoji = ['👜','⌚','👔','👠','🎁','💎','🏺','🧿','👗','👞'][index % 10];

                card.innerHTML = `
                    <div class="product-image">
                        ${prod.image ? `<img src="${prod.image}" alt="${prod.name}" onerror="this.style.display='none'; this.parentElement.innerHTML='<span>${emoji}</span>'">` : `<span>${emoji}</span>`}
                        ${prod.badge ? `<div class="product-badge">${prod.badge}</div>` : ''}
                    </div>
                    <div class="product-info">
                        <p class="product-category">${prod.category || 'General'}</p>
                        <h3 class="product-name">${prod.name}</h3>
                        <p class="product-description">${prod.description || ''}</p>
                        <div class="product-footer">
                            <div class="product-price">${parseInt(prod.price).toLocaleString()} <span>DZD</span></div>
                            <button class="buy-button" onclick="orderProduct('${prod.name}', ${prod.price})">Order Now</button>
                        </div>
                    </div>
                `;
                productsGrid.appendChild(card);
            });
        }

        productForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const product = {
                name: document.getElementById('prodName').value,
                price: document.getElementById('prodPrice').value,
                category: document.getElementById('prodCategory').value,
                badge: document.getElementById('prodBadge').value,
                description: document.getElementById('prodDesc').value,
                image: document.getElementById('prodImage').value,
                id: Date.now()
            };
            products.unshift(product);
            localStorage.setItem('boutique_products', JSON.stringify(products));
            renderProducts();
            productForm.reset();
        });

        function orderProduct(name, price) {
            alert(`Order: ${name}\nPrice: ${price.toLocaleString()} DZD\n\nContact us to complete your order!`);
        }

        // Settings Panel
        const settingsBtn = document.getElementById('settingsBtn');
        const settingsPanel = document.getElementById('settingsPanel');
        const closeSettings = document.getElementById('closeSettings');
        const saveSettings = document.getElementById('saveSettings');
        const resetSettings = document.getElementById('resetSettings');
        const saveStatus = document.getElementById('saveStatus');

        settingsBtn.addEventListener('click', () => {
            settingsPanel.classList.add('open');
            loadSettingsIntoForm();
        });
        closeSettings.addEventListener('click', () => settingsPanel.classList.remove('open'));

        function loadSettingsIntoForm() {
            const cfg = window.siteConfig || {};
            document.getElementById('configShopName').value = cfg.shopName || '';
            document.getElementById('configSubtitle').value = cfg.subtitle || '';
            document.getElementById('configHeroTitle1').value = cfg.heroTitle1 || '';
            document.getElementById('configHeroTitle2').value = cfg.heroTitle2 || '';
            document.getElementById('configHeroDesc').value = cfg.heroDesc || '';
            document.getElementById('configCtaText').value = cfg.ctaText || '';
            document.getElementById('configCollectionTitle').value = cfg.collectionTitle || '';
            document.getElementById('configDelivery').value = cfg.delivery || '';
            document.getElementById('configQuality').value = cfg.quality || '';
            document.getElementById('configService').value = cfg.service || '';
            document.getElementById('configFooter').value = cfg.footer || '';
            document.getElementById('configContact').value = cfg.contact || '';
        }

        saveSettings.addEventListener('click', () => {
            const newConfig = {
                shopName: document.getElementById('configShopName').value,
                subtitle: document.getElementById('configSubtitle').value,
                heroTitle1: document.getElementById('configHeroTitle1').value,
                heroTitle2: document.getElementById('configHeroTitle2').value,
                heroDesc: document.getElementById('configHeroDesc').value,
                ctaText: document.getElementById('configCtaText').value,
                collectionTitle: document.getElementById('configCollectionTitle').value,
                delivery: document.getElementById('configDelivery').value,
                quality: document.getElementById('configQuality').value,
                service: document.getElementById('configService').value,
                footer: document.getElementById('configFooter').value,
                contact: document.getElementById('configContact').value
            };
            localStorage.setItem('boutique_config', JSON.stringify(newConfig));
            saveStatus.classList.add('show');
            setTimeout(() => saveStatus.classList.remove('show'), 3000);
        });

        resetSettings.addEventListener('click', () => {
            if (confirm('Reset all custom text to default?')) {
                localStorage.removeItem('boutique_config');
                location.reload();
            }
        });

        // Apply config
        function applyConfig() {
            const saved = localStorage.getItem('boutique_config');
            const cfg = saved ? JSON.parse(saved) : (window.siteConfig || {});

            if (cfg.shopName) {
                document.getElementById('navLogo').textContent = cfg.shopName;
                document.getElementById('footerLogo').textContent = cfg.shopName;
                document.getElementById('pageTitle').textContent = cfg.shopName;
            }
            if (cfg.subtitle) document.getElementById('heroSubtitle').textContent = cfg.subtitle;
            if (cfg.heroTitle1) document.getElementById('heroTitle1').textContent = cfg.heroTitle1;
            if (cfg.heroTitle2) document.getElementById('heroTitle2').textContent = cfg.heroTitle2;
            if (cfg.heroDesc) document.getElementById('heroDesc').textContent = cfg.heroDesc;
            if (cfg.ctaText) document.getElementById('ctaButton').textContent = cfg.ctaText;
            if (cfg.collectionTitle) document.getElementById('collectionTitle').textContent = cfg.collectionTitle;
            if (cfg.delivery) document.getElementById('deliveryText').textContent = cfg.delivery;
            if (cfg.quality) document.getElementById('qualityText').textContent = cfg.quality;
            if (cfg.service) document.getElementById('serviceText').textContent = cfg.service;
            if (cfg.footer) document.getElementById('footerText').textContent = cfg.footer;
            if (cfg.contact) document.getElementById('contactInfo').textContent = cfg.contact;
        }

        // Scroll
        function scrollToSection(id) {
            document.getElementById(id).scrollIntoView({ behavior: 'smooth' });
        }

        // Reveal on scroll
        const revealElements = document.querySelectorAll('.reveal');
        const revealOnScroll = () => {
            revealElements.forEach(el => {
                if (el.getBoundingClientRect().top < window.innerHeight - 100) {
                    el.classList.add('active');
                }
            });
        };
        window.addEventListener('scroll', revealOnScroll);

        // Parallax
        window.addEventListener('scroll', () => {
            document.getElementById('bgVideo')
            .style.transform = `translateY(${window.pageYOffset * 0.5}px)`;
        });

        // Init
        renderProducts();
        applyConfig();
        revealOnScroll();
    </script>
</body>
</html>
