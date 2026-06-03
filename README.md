<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Don Ramón - Sucursal Takorito</title>
    <style>
        /* --- VARIABLES Y PALETA DÍA DE MUERTOS (LUCES TENUES) --- */
        :root {
            --bg-dark: #0d0d0d;
            --surface-dark: #161616;
            --cempasuchil: #ff9f00;
            --rosa-mexicano: #ff007f;
            --morado-calavera: #9d4edd;
            --papel-picado-cyan: #00f5d4;
            --text-light: #f8f9fa;
            --glow-neon: 0 0 12px;
        }

        /* --- ESTILOS GENERALES --- */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            scroll-behavior: smooth;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-light);
            line-height: 1.6;
            overflow-x: hidden;
        }

        /* Fondo de velas atenuadas (Efecto atmósfera) */
        body::before {
            content: '';
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: radial-gradient(circle at 20% 30%, rgba(255,159,0,0.05) 0%, transparent 40%),
                        radial-gradient(circle at 80% 70%, rgba(255,0,127,0.05) 0%, transparent 40%);
            z-index: -1;
            pointer-events: none;
        }

        .container {
            width: 90%;
            max-width: 1200px;
            margin: 0 auto;
        }

        /* --- HEADER Y NAVEGACIÓN --- */
        header {
            background-color: rgba(13, 13, 13, 0.95);
            border-bottom: 3px dashed var(--rosa-mexicano);
            position: sticky;
            top: 0;
            z-index: 1000;
            box-shadow: 0 4px 20px rgba(0,0,0,0.8);
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1.2rem 0;
        }

        .logo-container {
            display: flex;
            flex-direction: column;
        }

        .logo-main {
            font-size: 1.8rem;
            font-weight: 900;
            color: var(--cempasuchil);
            text-shadow: var(--glow-neon) var(--cempasuchil);
            letter-spacing: 2px;
        }

        .logo-sub {
            font-size: 0.9rem;
            color: var(--papel-picado-cyan);
            text-shadow: var(--glow-neon) var(--papel-picado-cyan);
            font-weight: bold;
            text-transform: uppercase;
        }

        nav ul {
            display: flex;
            list-style: none;
            gap: 2rem;
        }

        nav a {
            color: var(--text-light);
            text-decoration: none;
            font-weight: 600;
            text-transform: uppercase;
            font-size: 0.9rem;
            transition: all 0.3s ease;
        }

        nav a:hover {
            color: var(--rosa-mexicano);
            text-shadow: var(--glow-neon) var(--rosa-mexicano);
        }

        /* --- HERO SECTION --- */
        #hero {
            padding: 6rem 0;
            text-align: center;
            background: linear-gradient(rgba(0,0,0,0.6), rgba(13,13,13,1)), url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" viewBox="0 0 60 60"><path d="M30 0 L60 30 L30 60 L0 30 Z" fill="none" stroke="rgba(157,78,221,0.1)" stroke-width="1"/></svg>');
        }

        .hero-title {
            font-size: 3.5rem;
            color: var(--text-light);
            text-shadow: 0 0 20px var(--morado-calavera);
            margin-bottom: 1rem;
        }

        .hero-tagline {
            font-size: 1.3rem;
            color: var(--cempasuchil);
            margin-bottom: 2rem;
        }

        /* Estado Sucursal Dinámico */
        .status-badge {
            display: inline-block;
            padding: 0.5rem 1.5rem;
            border-radius: 50px;
            font-weight: bold;
            font-size: 0.9rem;
            border: 1px solid transparent;
        }
        .open-badge {
            background-color: rgba(0, 245, 212, 0.1);
            color: var(--papel-picado-cyan);
            border-color: var(--papel-picado-cyan);
            box-shadow: var(--glow-neon) rgba(0, 245, 212, 0.3);
        }
        .closed-badge {
            background-color: rgba(255, 0, 127, 0.1);
            color: var(--rosa-mexicano);
            border-color: var(--rosa-mexicano);
            box-shadow: var(--glow-neon) rgba(255, 0, 127, 0.3);
        }

        /* --- SECCIÓN DINÁMICA: MENÚ --- */
        #menu-section {
            padding: 5rem 0;
        }

        .section-title {
            text-align: center;
            font-size: 2.2rem;
            margin-bottom: 3rem;
            text-transform: uppercase;
        }
        .title-donramon { color: var(--cempasuchil); text-shadow: var(--glow-neon) var(--cempasuchil); }
        .title-takorito { color: var(--papel-picado-cyan); text-shadow: var(--glow-neon) var(--papel-picado-cyan); }

        .filter-container {
            display: flex;
            justify-content: center;
            gap: 1rem;
            margin-bottom: 3rem;
            flex-wrap: wrap;
        }

        .filter-btn {
            background: transparent;
            border: 2px solid var(--morado-calavera);
            color: var(--text-light);
            padding: 0.6rem 1.5rem;
            cursor: pointer;
            border-radius: 4px;
            font-weight: bold;
            transition: all 0.3s ease;
        }

        .filter-btn.active, .filter-btn:hover {
            background-color: var(--morado-calavera);
            box-shadow: var(--glow-neon) var(--morado-calavera);
        }

        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
        }

        .menu-item {
            background-color: var(--surface-dark);
            border: 1px solid rgba(255,255,255,0.05);
            border-radius: 8px;
            padding: 1.5rem;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .menu-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(157, 78, 221, 0.2);
            border-color: var(--morado-calavera);
        }

        .menu-item-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 0.8rem;
        }

        .menu-item-title {
            font-size: 1.2rem;
            color: var(--cempasuchil);
        }

        .menu-item-price {
            color: var(--papel-picado-cyan);
            font-weight: bold;
        }

        /* --- SECCIÓN UBICACIÓN --- */
        #ubicacion {
            padding: 5rem 0;
            background-color: #111;
            border-top: 1px solid rgba(255,255,255,0.05);
        }

        .ubicacion-wrapper {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 3rem;
            align-items: center;
        }

        @media (max-width: 768px) {
            .ubicacion-wrapper { grid-template-columns: 1fr; }
            nav ul { display: none; } /* Simplificación móvil */
        }

        .map-container {
            width: 100%;
            height: 350px;
            background-color: var(--surface-dark);
            border: 2px solid var(--papel-picado-cyan);
            box-shadow: var(--glow-neon) rgba(0, 245, 212, 0.2);
            border-radius: 8px;
            overflow: hidden;
        }

        .map-container iframe {
            width: 100%;
            height: 100%;
            border: 0;
            filter: grayscale(1) invert(0.9) contrast(1.2); /* Filtro tenue/oscuro */
        }

        .info-card {
            padding: 2rem;
            background-color: var(--surface-dark);
            border-left: 4px solid var(--rosa-mexicano);
            border-radius: 0 8px 8px 0;
        }

        .info-card h3 {
            color: var(--rosa-mexicano);
            margin-bottom: 1rem;
            font-size: 1.5rem;
        }

        .info-card p {
            margin-bottom: 0.8rem;
        }

        /* --- SECCIÓN CONTACTO --- */
        #contacto {
            padding: 5rem 0;
        }

        .form-container {
            max-width: 600px;
            margin: 0 auto;
            background-color: var(--surface-dark);
            padding: 2.5rem;
            border-radius: 8px;
            border: 1px solid var(--morado-calavera);
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            color: var(--cempasuchil);
            font-weight: 600;
            font-size: 0.9rem;
        }

        .form-group input, .form-group textarea {
            width: 100%;
            padding: 0.8rem;
            background-color: var(--bg-dark);
            border: 1px solid rgba(255,255,255,0.1);
            color: var(--text-light);
            border-radius: 4px;
            transition: all 0.3s ease;
        }

        .form-group input:focus, .form-group textarea:focus {
            outline: none;
            border-color: var(--rosa-mexicano);
            box-shadow: var(--glow-neon) rgba(255, 0, 127, 0.3);
        }

        .submit-btn {
            width: 100%;
            background: linear-gradient(45deg, var(--rosa-mexicano), var(--morado-calavera));
            color: var(--text-light);
            border: none;
            padding: 1rem;
            font-size: 1rem;
            font-weight: bold;
            text-transform: uppercase;
            cursor: pointer;
            border-radius: 4px;
            box-shadow: var(--glow-neon) rgba(255, 0, 127, 0.2);
            transition: transform 0.2s ease, opacity 0.3s ease;
        }

        .submit-btn:hover {
            opacity: 0.9;
            transform: scale(1.01);
        }

        /* --- FOOTER --- */
        footer {
            background-color: var(--bg-dark);
            text-align: center;
            padding: 2rem 0;
            border-top: 1px solid rgba(255,255,255,0.05);
            font-size: 0.9rem;
            color: #666;
        }
    </style>
</head>
<body>

    <header>
        <div class="container nav">
            <div class="logo-container">
                <span class="logo-main">DON RAMÓN</span>
                <span class="logo-sub">Takorito</span>
            </div>
            <nav>
                <ul>
                    <li><a href="#hero">Inicio</a></li>
                    <li><a href="#menu-section">Menú</a></li>
                    <li><a href="#ubicacion">Ubicación</a></li>
                    <li><a href="#contacto">Contacto</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <section id="hero">
        <div class="container">
            <h1 class="hero-title">Tradición Hecha Taco</h1>
            <p class="hero-tagline">Celebrando los sabores de nuestra tierra en un ambiente místico.</p>
            <div id="store-status" class="status-badge">Verificando horario...</div>
        </div>
    </section>

    <section id="menu-section">
        <div class="container">
            <h2 class="section-title title-donramon">Nuestro Altar del Sabor</h2>
            
            <div class="filter-container">
                <button class="filter-btn active" data-category="all">Ver Todo</button>
                <button class="filter-btn" data-category="tacos">Tacos</button>
                <button class="filter-btn" data-category="bebidas">Bebidas tradicionales</button>
                <button class="filter-btn" data-category="postres">Postres del más allá</button>
            </div>

            <div class="menu-grid" id="menu-container">
                </div>
        </div>
    </section>

    <section id="ubicacion">
        <div class="container">
            <h2 class="section-title title-takorito">Encuéntranos</h2>
            <div class="ubicacion-wrapper">
                <div class="map-container">
                    <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3762.6615926524316!2d-99.1633044!3d19.4270451!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x0!2zMTnCsDI1JzM3LjQiTiA5OcKwMDknNDcuOSJX!5e0!3m2!1ses-419!2smx!4v1625000000000!5m2!1ses-419!2smx" allowfullscreen="" loading="lazy"></iframe>
                </div>
                <div class="info-card">
                    <h3>Sucursal Takorito</h3>
                    <p><strong>Dirección:</strong> Av. Paseo de la Reforma 222, Juárez, Cuauhtémoc, CDMX, México.</p>
                    <p><strong>Horarios:</strong> Lunes a Domingo - 14:00 hrs a 23:00 hrs</p>
                    <p style="color: var(--cempasuchil); margin-top: 1rem; font-weight: bold;">¡Te esperamos para iluminar la noche!</p>
                </div>
            </div>
        </div>
    </section>

    <section id="contacto">
        <div class="container">
            <h2 class="section-title title-donramon">Escríbenos al Más Allá</h2>
            <div class="form-container">
                <form id="contact-form">
                    <div class="form-group">
                        <label for="name">Nombre o Calaverita</label>
                        <input type="text" id="name" required placeholder="Tu nombre">
                    </div>
                    <div class="form-group">
                        <label for="email">Correo Electrónico</label>
                        <input type="email" id="email" required placeholder="tu@correo.com">
                    </div>
                    <div class="form-group">
                        <label for="message">Mensaje / Pedido</label>
                        <textarea id="message" rows="5" required placeholder="¿Qué le depara el destino a tu paladar?"></textarea>
                    </div>
                    <button type="submit" class="submit-btn">Enviar Mensaje</button>
                </form>
            </div>
        </div>
    </section>

    <footer>
        <div class="container">
            <p>&copy; 2026 DON RAMÓN - SUCURSAL TAKORITO. Todos los derechos reservados.</p>
            <p style="font-size: 0.8rem; margin-top: 0.5rem; color: var(--morado-calavera)">Hecho con respeto a nuestras tradiciones.</p>
        </div>
    </footer>

    <script>
        // Data del Menú (Simulación de base de datos dinámica)
        const menuData = [
            { id: 1, title: "Tacos al Pastor 'Catrina'", price: "$95", category: "tacos", desc: "Con piña iluminada y jardín fresco." },
            { id: 2, title: "Tacos de Barbacoa del Inframundo", price: "$110", category: "tacos", desc: "Carne suave cocida lentamente en penca de maguey." },
            { id: 3, title: "Agua de Cempasúchil y Naranja", price: "$45", category: "bebidas", desc: "Infusión mística de temporada, refrescante y dulce." },
            { id: 4, title: "Mezcal Ancestral Curado", price: "$85", category: "bebidas", desc: "Acompañado de sal de gusano y rodajas de naranja." },
            { id: 5, title: "Pan de Muerto con Nata", price: "$60", category: "postres", desc: "Espolvoreado con azúcar rosa tradicional mexicana." },
            { id: 6, title: "Calaverita de Azúcar Flameada", price: "$50", category: "postres", desc: "Chocolate oaxaqueño con toque de licor." }
        ];

        // Inicialización y renderizado del menú
        const menuContainer = document.getElementById('menu-container');
        const filterButtons = document.querySelectorAll('.filter-btn');

        function displayMenuItems(category) {
            let filteredMenu = menuData;
            if (category !== 'all') {
                filteredMenu = menuData.filter(item => item.category === category);
            }

            const menuHTML = filteredMenu.map(item => `
                <div class="menu-item">
                    <div class="menu-item-header">
                        <h3 class="menu-item-title">${item.title}</h3>
                        <span class="menu-item-price">${item.price}</span>
                    </div>
                    <p style="font-size: 0.9rem; color: #aaa;">${item.desc}</p>
                </div>
            `).join('');

            menuContainer.innerHTML = menuHTML;
        }

        // Eventos para filtros del menú
        filterButtons.forEach(btn => {
            btn.addEventListener('click', (e) => {
                filterButtons.forEach(b => b.classList.remove('active'));
                e.target.classList.add('active');
                displayMenuItems(e.target.dataset.category);
            });
        });

        // Verificación Dinámica de Horario Abierto/Cerrado (14:00 a 23:00)
        function checkStoreStatus() {
            const statusBadge = document.getElementById('store-status');
            const currentHour = new Date().getHours();
            
            if (currentHour >= 14 && currentHour < 23) {
                statusBadge.textContent = "● SUCURSAL TAKORITO ABIERTA - PASA A ILUMINAR TU HAMBRE";
                statusBadge.className = "status-badge open-badge";
            } else {
                statusBadge.textContent = "● SUCURSAL CERRADA - LOS ESPÍRITUS ESTÁN DESCANSANDO (ABRIMOS A LAS 2:00 PM)";
                statusBadge.className = "status-badge closed-badge";
            }
        }

        // Gestión interactiva del Formulario de Contacto
        document.getElementById('contact-form').addEventListener('submit', (e) => {
            e.preventDefault();
            const name = document.getElementById('name').value;
            alert(`¡Gracias por tu mensaje, ${name}! Los espíritus de Don Ramón han llevado tus palabras a la cocina de Takorito.`);
            e.target.reset();
        });

        // Carga inicial
        window.addEventListener('DOMContentLoaded', () => {
            displayMenuItems('all');
            checkStoreStatus();
        });
    </script>
</body>
</html>
