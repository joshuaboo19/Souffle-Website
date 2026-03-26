<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Fluff Lab | Artisanal Soufflé Pancakes</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Lato:wght@300;400;700&family=Playfair+Display:wght@600;800&display=swap" rel="stylesheet">
    <style>
        /* --- CSS VARIABLES & RESET --- */
        :root {
            --cream: #FFF8F0;
            --pink: #FFD6D6;
            --gold: #FFD700;
            --brown: #3E1C00;
            --white: #FFFFFF;
            --shadow: 0 10px 30px rgba(62, 28, 0, 0.1);
            --transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }
        html { scroll-behavior: smooth; }
        body { 
            font-family: 'Lato', sans-serif; 
            background-color: var(--cream); 
            color: var(--brown); 
            line-height: 1.6;
            overflow-x: hidden;
        }
        h1, h2, h3 { font-family: 'Playfair Display', serif; }
        ul { list-style: none; }
        a { text-decoration: none; color: inherit; }
        img { max-width: 100%; display: block; border-radius: 8px; }

        /* --- UTILITIES --- */
        .container { max-width: 1200px; margin: 0 auto; padding: 0 20px; }
        .btn {
            display: inline-block;
            padding: 14px 30px;
            border-radius: 50px;
            font-weight: 700;
            cursor: pointer;
            transition: var(--transition);
            border: none;
            text-align: center;
        }
        .btn-primary { background: var(--brown); color: var(--cream); }
        .btn-primary:hover { transform: translateY(-3px); background: #5a2a00; }
        .btn-outline { border: 2px solid var(--brown); color: var(--brown); }
        .btn-outline:hover { background: var(--brown); color: var(--cream); }
        
        .section-padding { padding: 100px 0; }
        .text-center { text-align: center; }
        
        /* Animation State */
        .fade-in { opacity: 0; transform: translateY(30px); transition: 0.8s ease-out; }
        .fade-in.visible { opacity: 1; transform: translateY(0); }

        /* --- NAVIGATION --- */
        nav {
            position: fixed; top: 0; width: 100%; z-index: 1000;
            background: rgba(255, 248, 240, 0.95);
            backdrop-filter: blur(10px);
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            padding: 15px 0;
        }
        nav .container { display: flex; justify-content: space-between; align-items: center; }
        .logo { font-family: 'Playfair Display', serif; font-size: 1.5rem; font-weight: 800; }
        .nav-links { display: flex; gap: 30px; align-items: center; }
        .hamburger { display: none; cursor: pointer; font-size: 1.5rem; }

        /* --- HERO --- */
        .hero {
            height: 100vh;
            background: linear-gradient(rgba(0,0,0,0.3), rgba(0,0,0,0.3)), 
                        url('https://images.unsplash.com/photo-1575853121743-60c24f0a7502?auto=format&fit=crop&q=80&w=1600') center/cover no-repeat;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--white);
            text-align: center;
        }
        .hero h1 { font-size: clamp(2.5rem, 8vw, 5rem); margin-bottom: 20px; }
        .hero p { font-size: 1.2rem; margin-bottom: 30px; max-width: 600px; margin-inline: auto; }
        .hero-btns { display: flex; gap: 15px; justify-content: center; }

        /* --- URGENCY BANNER --- */
        .urgency-banner {
            background: var(--gold);
            padding: 10px 0;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        /* --- USP SECTION --- */
        .usp-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 40px; margin-top: 50px; }
        .usp-card {
            background: var(--white);
            padding: 40px;
            border-radius: 20px;
            box-shadow: var(--shadow);
            transition: var(--transition);
        }
        .usp-card:hover { transform: translateY(-10px); }
        .usp-icon { font-size: 3rem; margin-bottom: 20px; }

        /* --- MENU SECTION --- */
        .menu-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 30px; margin-top: 50px; }
        .menu-card {
            background: var(--white);
            border-radius: 20px;
            overflow: hidden;
            box-shadow: var(--shadow);
        }
        .menu-img { height: 250px; overflow: hidden; }
        .menu-img img { width: 100%; height: 100%; object-fit: cover; transition: 0.5s; }
        .menu-card:hover img { transform: scale(1.1); }
        .menu-content { padding: 25px; }
        .menu-price { font-weight: 700; color: var(--brown); font-size: 1.2rem; margin: 10px 0; }
        .add-cart { width: 100%; margin-top: 15px; }

        /* --- PROCESS SECTION --- */
        .process-steps { display: flex; justify-content: space-around; flex-wrap: wrap; gap: 20px; margin-top: 50px; }
        .step { flex: 1; min-width: 250px; position: relative; }
        .step-num { 
            width: 50px; height: 50px; background: var(--pink); border-radius: 50%; 
            display: flex; align-items: center; justify-content: center; 
            font-weight: 800; margin: 0 auto 20px;
        }

        /* --- COUNTDOWN --- */
        .countdown-wrap { background: var(--pink); border-radius: 20px; padding: 50px; margin-top: 50px; }
        #timer { font-size: 3rem; font-weight: 800; display: flex; justify-content: center; gap: 20px; }
        .time-part { display: flex; flex-direction: column; }
        .time-label { font-size: 0.8rem; text-transform: uppercase; }

        /* --- ACCORDION --- */
        .faq-item { background: var(--white); margin-bottom: 10px; border-radius: 10px; overflow: hidden; }
        .faq-header { padding: 20px; cursor: pointer; display: flex; justify-content: space-between; font-weight: 700; }
        .faq-body { padding: 0 20px; max-height: 0; overflow: hidden; transition: 0.3s ease-out; }

        /* --- MODAL --- */
        .modal {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.7); display: none; align-items: center; justify-content: center; z-index: 2000;
        }
        .modal-content {
            background: var(--cream); padding: 40px; border-radius: 20px; max-width: 500px; 
            text-align: center; position: relative; margin: 20px;
        }
        .close-modal { position: absolute; top: 15px; right: 20px; font-size: 1.5rem; cursor: pointer; }

        /* --- RESPONSIVE --- */
        @media (max-width: 768px) {
            .nav-links { display: none; position: absolute; top: 100%; left: 0; width: 100%; background: var(--cream); flex-direction: column; padding: 20px; }
            .nav-links.active { display: flex; }
            .hamburger { display: block; }
            .hero h1 { font-size: 3rem; }
            #timer { font-size: 2rem; }
        }
    </style>
</head>
<body>

    <nav>
        <div class="container">
            <a href="#" class="logo">THE FLUFF LAB</a>
            <div class="hamburger" onclick="toggleMenu()">☰</div>
            <ul class="nav-links">
                <li><a href="#why-us">About</a></li>
                <li><a href="#menu">Menu</a></li>
                <li><a href="#process">The Craft</a></li>
                <li><a href="#faq">FAQ</a></li>
                <li><a href="#menu" class="btn btn-primary">Order Now</a></li>
            </ul>
        </div>
    </nav>

    <section class="hero">
        <div class="container fade-in">
            <p style="text-transform: uppercase; letter-spacing: 3px; font-weight: 700;">Artisanal & Hand-Whisked</p>
            <h1>Cloud-Like Perfection</h1>
            <p>Experience the legendary wobble of Japan’s softest soufflé pancakes, made fresh to order with premium organic ingredients.</p>
            <div class="hero-btns">
                <a href="#menu" class="btn btn-primary">View Menu</a>
                <a href="#process" class="btn btn-outline" style="border-color: white; color: white;">See How It's Made</a>
            </div>
        </div>
    </section>

    <div class="urgency-banner text-center">
        ⚠️ Only 30 portions made daily! High demand today.
    </div>

    <section id="why-us" class="section-padding container">
        <div class="text-center fade-in">
            <h2>Why Our Pancakes?</h2>
            <p>The secret is in the whisking and the warmth.</p>
        </div>
        <div class="usp-grid">
            <div class="usp-card text-center fade-in">
                <div class="usp-icon">☁️</div>
                <h3>Ethereal Texture</h3>
                <p>Triple-sifted flour and perfectly peaked egg whites create a texture that melts the moment it hits your tongue.</p>
            </div>
            <div class="usp-card text-center fade-in">
                <div class="usp-icon">🍓</div>
                <h3>Fresh Ingredients</h3>
                <p>We use farm-fresh organic eggs, Hokkaido milk, and seasonal fruits sourced from local farmers.</p>
            </div>
            <div class="usp-card text-center fade-in">
                <div class="usp-icon">⏳</div>
                <h3>Small Batches</h3>
                <p>We never rush perfection. Our slow-cooking process takes 20 minutes to ensure every pancake is a masterpiece.</p>
            </div>
        </div>
    </section>

    <section id="menu" class="section-padding" style="background: #fff;">
        <div class="container">
            <div class="text-center fade-in">
                <span style="color: #ff8e8e; font-weight: 700;">OUR CLASSICS</span>
                <h2>Signature Creations</h2>
            </div>
            <div class="menu-grid">
                <div class="menu-card fade-in">
                    <div class="menu-img"><img src="https://images.unsplash.com/photo-1567620905732-2d1ec7bb7445?auto=format&fit=crop&q=80&w=600" alt="Classic Fluff"></div>
                    <div class="menu-content">
                        <h3>Original Cloud</h3>
                        <p>Three stacks served with whipped honeycomb butter and pure Grade A maple syrup.</p>
                        <p class="menu-price">$14.50</p>
                        <button class="btn btn-outline add-cart">Add to Order</button>
                    </div>
                </div>
                <div class="menu-card fade-in">
                    <div class="menu-img"><img src="https://images.unsplash.com/photo-1528207776546-365bb710ee93?auto=format&fit=crop&q=80&w=600" alt="Berry Bliss"></div>
                    <div class="menu-content">
                        <h3>Berry Bliss</h3>
                        <p>Topped with fresh raspberries, blueberries, and our signature vanilla bean cream.</p>
                        <p class="menu-price">$16.50</p>
                        <button class="btn btn-outline add-cart">Add to Order</button>
                    </div>
                </div>
                <div class="menu-card fade-in">
                    <div class="menu-img"><img src="https://images.unsplash.com/photo-1554520735-0ad66a951bb6?auto=format&fit=crop&q=80&w=600" alt="Matcha Zen"></div>
                    <div class="menu-content">
                        <h3>Uji Matcha</h3>
                        <p>Premium Uji matcha dust, red bean paste, and mochi pearls for a serene indulgence.</p>
                        <p class="menu-price">$17.00</p>
                        <button class="btn btn-outline add-cart">Add to Order</button>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section id="process" class="section-padding container text-center">
        <div class="fade-in">
            <h2>The 20-Minute Masterpiece</h2>
            <p>Patience is the main ingredient.</p>
        </div>
        <div class="process-steps">
            <div class="step fade-in">
                <div class="step-num">1</div>
                <h3>The Whisk</h3>
                <p>We whip organic egg whites until they form stiff, glossy peaks for maximum airiness.</p>
            </div>
            <div class="step fade-in">
                <div class="step-num">2</div>
                <h3>The Steam</h3>
                <p>Pancakes are cooked slowly under a lid with a dash of water to create a steaming effect.</p>
            </div>
            <div class="step fade-in">
                <div class="step-num">3</div>
                <h3>The Garnish</h3>
                <p>Hand-crafted toppings are added seconds before the plate reaches your table.</p>
            </div>
        </div>
    </section>

    <section class="section-padding container">
        <div class="countdown-wrap text-center fade-in">
            <h3>Next Fresh Batch In:</h3>
            <div id="timer">
                <div class="time-part"><span id="hours">00</span><span class="time-label">Hrs</span></div>
                <div class="time-part"><span id="minutes">00</span><span class="time-label">Min</span></div>
                <div class="time-part"><span id="seconds">00</span><span class="time-label">Sec</span></div>
            </div>
            <p style="margin-top: 20px;">We reset our grills daily at 10:00 AM.</p>
        </div>
    </section>

    <section class="section-padding" style="background: var(--white);">
        <div class="container text-center fade-in">
            <h2>What Our Fluff-Lovers Say</h2>
            <div class="usp-grid">
                <div class="usp-card">
                    <p>"The wobble is real. It's like eating a sweet, warm cloud. Best breakfast in the city!"</p>
                    <div style="color: var(--gold); margin-top: 15px;">★★★★★</div>
                    <p><strong>- Sarah J.</strong></p>
                </div>
                <div class="usp-card">
                    <p>"Worth the wait! You can really taste the quality of the ingredients."</p>
                    <div style="color: var(--gold); margin-top: 15px;">★★★★★</div>
                    <p><strong>- Mark R.</strong></p>
                </div>
            </div>
            <div style="margin-top: 40px; font-weight: 700;">500+ Happy Customers Daily | 4.9 ★ Average Rating</div>
        </div>
    </section>

    <section id="faq" class="section-padding container">
        <h2 class="text-center" style="margin-bottom: 40px;">Frequently Asked Questions</h2>
        <div style="max-width: 800px; margin: 0 auto;">
            <div class="faq-item">
                <div class="faq-header" onclick="toggleFaq(this)">How long is the wait? <span>+</span></div>
                <div class="faq-body"><p>Every pancake is made from scratch. Please allow 15–20 minutes for your order to reach peak fluffiness.</p></div>
            </div>
            <div class="faq-item">
                <div class="faq-header" onclick="toggleFaq(this)">Do you offer gluten-free options? <span>+</span></div>
                <div class="faq-body"><p>Currently, our soufflé technique requires wheat flour for structure. We are working on a GF recipe!</p></div>
            </div>
            <div class="faq-item">
                <div class="faq-header" onclick="toggleFaq(this)">Can I take them to-go? <span>+</span></div>
                <div class="faq-body"><p>Yes, but we recommend eating them within 15 minutes to enjoy the airy texture before they settle.</p></div>
            </div>
        </div>
    </section>

    <footer class="section-padding" style="background: var(--brown); color: var(--cream);">
        <div class="container text-center">
            <h2 style="font-size: 2rem; margin-bottom: 20px;">THE FLUFF LAB</h2>
            <p>123 Sweet Street, Dessert District, NY 10001</p>
            <p>Mon-Sun: 10:00 AM - 8:00 PM</p>
            <div style="margin: 20px 0; font-size: 1.5rem; display: flex; justify-content: center; gap: 20px;">
                <span></span> <span></span> <span></span>
            </div>
            <p>&copy; 2026 The Fluff Lab. All rights reserved.</p>
        </div>
    </footer>

    <div class="modal" id="discountModal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeModal()">&times;</span>
            <div style="font-size: 3rem;">🎁</div>
            <h2>Sweeten the Deal!</h2>
            <p>Join our Fluff Club and get <strong>10% OFF</strong> your first order.</p>
            <input type="email" placeholder="Enter your email" style="width: 100%; padding: 12px; margin: 20px 0; border: 1px solid #ccc; border-radius: 5px;">
            <button class="btn btn-primary" style="width: 100%;">Claim My Discount</button>
        </div>
    </div>

    <script>
        // --- MOBILE MENU ---
        function toggleMenu() {
            document.querySelector('.nav-links').classList.toggle('active');
        }

        // --- COUNTDOWN TIMER ---
        function updateTimer() {
            const now = new Date();
            let target = new Date();
            target.setHours(10, 0, 0, 0);

            // If it's already past 10am today, set target for 10am tomorrow
            if (now > target) {
                target.setDate(target.getDate() + 1);
            }

            const diff = target - now;
            const h = Math.floor(diff / (1000 * 60 * 60));
            const m = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
            const s = Math.floor((diff % (1000 * 60)) / 1000);

            document.getElementById('hours').innerText = h.toString().padStart(2, '0');
            document.getElementById('minutes').innerText = m.toString().padStart(2, '0');
            document.getElementById('seconds').innerText = s.toString().padStart(2, '0');
        }
        setInterval(updateTimer, 1000);
        updateTimer();

        // --- FAQ ACCORDION ---
        function toggleFaq(header) {
            const body = header.nextElementSibling;
            const span = header.querySelector('span');
            if (body.style.maxHeight) {
                body.style.maxHeight = null;
                body.style.paddingBottom = "0";
                span.innerText = "+";
            } else {
                body.style.maxHeight = "200px";
                body.style.paddingBottom = "20px";
                span.innerText = "-";
            }
        }

        // --- FADE-IN ON SCROLL ---
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('visible');
                }
            });
        }, { threshold: 0.1 });

        document.querySelectorAll('.fade-in').forEach(el => observer.observe(el));

        // --- EMAIL MODAL ---
        setTimeout(() => {
            if(!localStorage.getItem('modalShown')) {
                document.getElementById('discountModal').style.display = 'flex';
            }
        }, 5000);

        function closeModal() {
            document.getElementById('discountModal').style.display = 'none';
            localStorage.setItem('modalShown', 'true');
        }

        // Close modal if clicking outside content
        window.onclick = function(event) {
            const modal = document.getElementById('discountModal');
            if (event.target == modal) closeModal();
        }
    </script>
</body>
</html>
