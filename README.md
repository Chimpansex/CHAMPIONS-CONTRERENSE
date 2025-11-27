<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Reglamento Oficial | La Champions Contrerense</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&display=swap');
        
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f5f5f4; /* Stone-100: Warm neutral */
            color: #1c1917; /* Stone-900 */
        }

        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 400px;
        }

        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }

        .tab-active {
            border-bottom: 3px solid #059669; /* Emerald-600 */
            color: #059669;
            font-weight: 600;
        }

        .tab-inactive {
            border-bottom: 3px solid transparent;
            color: #78716c; /* Stone-500 */
        }
        
        .card-shadow {
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }

        .interactive-btn {
            transition: all 0.2s ease;
        }
        .interactive-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
        }
    </style>
    <!-- Chosen Palette: Warm Neutrals (Stone) with Emerald Green Accents for a professional sports feel. -->
    <!-- Application Structure Plan: 
         1. Hero Section: Sets the formal tone and objective.
         2. Dashboard "Game Stats": Visualizes the numerical constraints (Time, Points, Players) for quick reference.
         3. Interactive Rulebook (Tabs): Splits content into logical operational domains (General, Discipline, Organization) to avoid text walls.
         4. Simulation Tools: Interactive calculators for "Points" and "Fair Play Scenarios" to make abstract rules concrete.
         This structure moves from high-level visual understanding to detailed textual reference, and finally to practical application.
    -->
    <!-- Visualization & Content Choices:
         - Time Breakdown (Doughnut Chart): Shows 20/10/20 split clearly. Goal: Inform.
         - Point System (Bar Chart): Compares Win vs Draw vs Loss visually. Goal: Compare.
         - Mixed Team Composition (DOM visual): Uses icons to show the 5/6 split. Goal: Inform.
         - Simulator (Inputs): Allows users to input outcomes to understand the table mechanics. Goal: Change/Learn.
         - Justification: Charts used for numeric data to break up text; Tabs used to organize the 7 chapters logically. 
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
</head>
<body class="bg-stone-50 min-h-screen flex flex-col">

    <!-- Header Section -->
    <header class="bg-white border-b border-stone-200 sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center gap-2">
                <span class="text-2xl">⚽</span>
                <h1 class="text-xl font-bold tracking-tight text-stone-900">La Champions Contrerense <span class="text-emerald-600 text-sm font-normal uppercase tracking-wider ml-2 hidden sm:inline">Reglamento Oficial</span></h1>
            </div>
            <nav class="flex space-x-4">
                <button onclick="scrollToSection('dashboard')" class="text-sm font-medium text-stone-600 hover:text-emerald-600 transition-colors">Resumen</button>
                <button onclick="scrollToSection('rules')" class="text-sm font-medium text-stone-600 hover:text-emerald-600 transition-colors">Normativa</button>
                <button onclick="scrollToSection('simulator')" class="text-sm font-medium text-stone-600 hover:text-emerald-600 transition-colors">Simulador</button>
            </nav>
        </div>
    </header>

    <main class="flex-grow">
        
        <!-- Intro Section -->
        <section class="max-w-4xl mx-auto px-4 py-10 text-center">
            <h2 class="text-3xl font-extrabold text-stone-800 mb-4">Objetivo del Reglamento</h2>
            <p class="text-lg text-stone-600 leading-relaxed max-w-2xl mx-auto">
                Establecer un marco normativo claro, justo y profesional para la práctica del fútbol mixto amateur y escolar. 
                Este documento busca garantizar el <span class="font-semibold text-emerald-700">Fair Play</span>, la integridad física de los participantes y el correcto desarrollo de la competición.
            </p>
        </section>

        <!-- Dashboard Section: Visual Data -->
        <section id="dashboard" class="bg-white py-12 border-y border-stone-200">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="mb-8">
                    <h3 class="text-2xl font-bold text-stone-800">Especificaciones Técnicas</h3>
                    <p class="text-stone-500 mt-2">Visualización rápida de los tiempos de juego, sistema de puntuación y composición de equipos.</p>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                    
                    <!-- Chart 1: Time Distribution -->
                    <div class="bg-stone-50 p-6 rounded-xl border border-stone-200 card-shadow">
                        <h4 class="font-semibold text-stone-700 mb-4 text-center">⏱️ Duración del Encuentro</h4>
                        <div class="chart-container">
                            <canvas id="timeChart"></canvas>
                        </div>
                        <p class="text-xs text-center text-stone-500 mt-4">Total evento: 50 minutos</p>
                    </div>

                    <!-- Chart 2: Point System -->
                    <div class="bg-stone-50 p-6 rounded-xl border border-stone-200 card-shadow">
                        <h4 class="font-semibold text-stone-700 mb-4 text-center">🏆 Sistema de Puntos</h4>
                        <div class="chart-container">
                            <canvas id="pointsChart"></canvas>
                        </div>
                        <p class="text-xs text-center text-stone-500 mt-4">Criterio clave para clasificación</p>
                    </div>

                    <!-- Visual: Team Composition -->
                    <div class="bg-stone-50 p-6 rounded-xl border border-stone-200 card-shadow flex flex-col">
                        <h4 class="font-semibold text-stone-700 mb-4 text-center">👥 Alineación Mixta (11 vs 11)</h4>
                        <div class="flex-grow flex flex-col justify-center items-center space-y-4">
                            <div class="w-full bg-white p-4 rounded-lg border border-stone-200">
                                <div class="flex justify-between items-center mb-2">
                                    <span class="text-sm font-bold text-emerald-700">Mínimo Mujeres</span>
                                    <span class="text-2xl font-bold">5</span>
                                </div>
                                <div class="w-full bg-stone-200 h-2 rounded-full overflow-hidden">
                                    <div class="bg-emerald-500 h-full" style="width: 45%"></div>
                                </div>
                            </div>
                            <div class="w-full bg-white p-4 rounded-lg border border-stone-200">
                                <div class="flex justify-between items-center mb-2">
                                    <span class="text-sm font-bold text-stone-600">Máximo Hombres</span>
                                    <span class="text-2xl font-bold">6</span>
                                </div>
                                <div class="w-full bg-stone-200 h-2 rounded-full overflow-hidden">
                                    <div class="bg-stone-500 h-full" style="width: 55%"></div>
                                </div>
                            </div>
                            <div class="text-center mt-2 p-2 bg-red-50 border border-red-100 rounded text-red-800 text-sm">
                                🚫 <strong>Prohibido:</strong> Barridas o juego brusco.
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Interactive Rules Section -->
        <section id="rules" class="max-w-5xl mx-auto px-4 py-16">
            <div class="mb-10 text-center">
                <h3 class="text-2xl font-bold text-stone-800">Reglamento Detallado</h3>
                <p class="text-stone-500 mt-2">Navegue por las pestañas para conocer los artículos específicos de cada capítulo.</p>
            </div>

            <!-- Tab Navigation -->
            <div class="flex flex-wrap justify-center border-b border-stone-200 mb-8 overflow-x-auto">
                <button onclick="switchTab('general')" id="tab-general" class="tab-active px-6 py-3 text-sm font-medium focus:outline-none interactive-btn">General y Juego</button>
                <button onclick="switchTab('puntuacion')" id="tab-puntuacion" class="tab-inactive px-6 py-3 text-sm font-medium focus:outline-none interactive-btn">Puntuación</button>
                <button onclick="switchTab('disciplina')" id="tab-disciplina" class="tab-inactive px-6 py-3 text-sm font-medium focus:outline-none interactive-btn">Disciplinario</button>
                <button onclick="switchTab('organizacion')" id="tab-organizacion" class="tab-inactive px-6 py-3 text-sm font-medium focus:outline-none interactive-btn">Organización</button>
            </div>

            <!-- Tab Content Area -->
            <div id="content-area" class="bg-white p-8 rounded-2xl border border-stone-200 shadow-sm min-h-[400px]">
                <!-- Dynamic Content injected via JS -->
            </div>
        </section>

        <!-- Simulator Tool -->
        <section id="simulator" class="bg-stone-900 text-stone-100 py-16">
            <div class="max-w-4xl mx-auto px-4">
                <div class="mb-8">
                    <h3 class="text-2xl font-bold text-white">🧮 Calculadora de Torneo</h3>
                    <p class="text-stone-400 mt-2">Simule los resultados de su equipo para proyectar su puntaje final según el Artículo 3 del reglamento.</p>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
                    <div class="bg-stone-800 p-4 rounded-lg">
                        <label class="block text-xs font-bold text-emerald-400 uppercase tracking-wide mb-2">Partidos Ganados (3 pts)</label>
                        <input type="number" id="input-wins" min="0" value="0" oninput="updateCalculator()" class="w-full bg-stone-700 border border-stone-600 text-white rounded p-3 focus:ring-2 focus:ring-emerald-500 focus:outline-none text-2xl font-mono">
                    </div>
                    <div class="bg-stone-800 p-4 rounded-lg">
                        <label class="block text-xs font-bold text-yellow-400 uppercase tracking-wide mb-2">Partidos Empatados (1 pt)</label>
                        <input type="number" id="input-draws" min="0" value="0" oninput="updateCalculator()" class="w-full bg-stone-700 border border-stone-600 text-white rounded p-3 focus:ring-2 focus:ring-yellow-500 focus:outline-none text-2xl font-mono">
                    </div>
                    <div class="bg-stone-800 p-4 rounded-lg">
                        <label class="block text-xs font-bold text-red-400 uppercase tracking-wide mb-2">Partidos Perdidos (0 pts)</label>
                        <input type="number" id="input-losses" min="0" value="0" oninput="updateCalculator()" class="w-full bg-stone-700 border border-stone-600 text-white rounded p-3 focus:ring-2 focus:ring-red-500 focus:outline-none text-2xl font-mono">
                    </div>
                </div>

                <div class="bg-stone-800 p-6 rounded-xl border border-stone-700 flex flex-col md:flex-row justify-between items-center">
                    <div class="mb-4 md:mb-0">
                        <h4 class="text-lg font-semibold">Proyección de Puntos</h4>
                        <p class="text-sm text-stone-400">Total acumulado en tabla general</p>
                    </div>
                    <div class="text-5xl font-bold text-emerald-400 font-mono" id="total-points">0</div>
                </div>
                
                <div class="mt-6 grid grid-cols-1 md:grid-cols-2 gap-4">
                     <div class="bg-stone-800 p-4 rounded border-l-4 border-yellow-500">
                        <h5 class="font-bold text-sm mb-1">⚠️ Criterio de Desempate 1</h5>
                        <p class="text-xs text-stone-400">En caso de igualdad de puntos, el primer criterio es la <strong>Diferencia de Goles</strong> (Goles a Favor - Goles en Contra).</p>
                    </div>
                     <div class="bg-stone-800 p-4 rounded border-l-4 border-blue-500">
                        <h5 class="font-bold text-sm mb-1">ℹ️ Nota Importante</h5>
                        <p class="text-xs text-stone-400">No presentarse (W.O.) resulta en 0 puntos y un marcador adverso (generalmente 0-2 o 0-3 según comité).</p>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <footer class="bg-white border-t border-stone-200 mt-auto py-8">
        <div class="max-w-7xl mx-auto px-4 text-center">
            <p class="text-stone-500 text-sm">© 2024 La Champions Contrerense. Todos los derechos reservados.</p>
            <p class="text-stone-400 text-xs mt-2">Documento oficial para uso interno de torneos escolares y amateurs.</p>
        </div>
    </footer>

    <!-- Logic Script -->
    <script>
        // Data Store for Rules Content
        const rulesContent = {
            general: `
                <div class="space-y-6 animate-fade-in">
                    <div class="border-l-4 border-emerald-500 pl-4">
                        <h4 class="text-lg font-bold text-stone-800">Capítulo 1: Del Terreno y Duración</h4>
                        <ul class="list-disc list-inside mt-2 text-stone-600 space-y-2">
                            <li><strong>Artículo 1.1:</strong> El torneo se jugará en modalidad Fútbol 11.</li>
                            <li><strong>Artículo 1.2:</strong> Los partidos constarán de <span class="bg-emerald-100 text-emerald-800 px-1 rounded">2 tiempos de 20 minutos</span>.</li>
                            <li><strong>Artículo 1.3:</strong> Se otorgará un descanso obligatorio de 10 minutos entre tiempos.</li>
                        </ul>
                    </div>
                    <div class="border-l-4 border-blue-500 pl-4">
                        <h4 class="text-lg font-bold text-stone-800">Capítulo 2: De los Equipos y Jugadores</h4>
                        <ul class="list-disc list-inside mt-2 text-stone-600 space-y-2">
                            <li><strong>Artículo 2.1:</strong> El torneo es de categoría <strong>Mixta</strong>.</li>
                            <li><strong>Artículo 2.2:</strong> Cada equipo debe mantener en cancha un mínimo de <span class="font-bold">5 mujeres</span> durante todo el encuentro.</li>
                            <li><strong>Artículo 2.3:</strong> El incumplimiento del Artículo 2.2 resultará en la pérdida del partido por default.</li>
                            <li><strong>Artículo 2.4:</strong> Todos los jugadores deben estar debidamente inscritos y acreditarse antes del inicio.</li>
                        </ul>
                    </div>
                    <div class="border-l-4 border-red-500 pl-4">
                        <h4 class="text-lg font-bold text-stone-800">Capítulo 3: Seguridad y Juego Limpio</h4>
                        <p class="mt-2 text-stone-600 mb-2">Para proteger la integridad de los participantes escolares y amateurs:</p>
                        <ul class="list-disc list-inside text-stone-600 space-y-2">
                            <li><strong>Artículo 3.1:</strong> Quedan estrictamente <span class="text-red-600 font-bold">PROHIBIDAS las barridas</span> (deslizamientos al suelo para disputar el balón).</li>
                            <li><strong>Artículo 3.2:</strong> Cualquier barrida será sancionada con Tiro Libre Directo y Amonestación (Tarjeta Amarilla) o Expulsión (Roja) según la intensidad.</li>
                        </ul>
                    </div>
                </div>
            `,
            puntuacion: `
                 <div class="space-y-6 animate-fade-in">
                    <div class="bg-stone-50 p-6 rounded-lg border border-stone-200">
                        <h4 class="text-lg font-bold text-stone-800 mb-4">Capítulo 4: Sistema de Puntuación</h4>
                        <table class="w-full text-left border-collapse">
                            <thead>
                                <tr class="text-sm text-stone-500 border-b border-stone-300">
                                    <th class="py-2">Resultado</th>
                                    <th class="py-2">Puntos Otorgados</th>
                                </tr>
                            </thead>
                            <tbody class="text-stone-700">
                                <tr class="border-b border-stone-100">
                                    <td class="py-3 font-semibold text-emerald-600">Victoria</td>
                                    <td class="py-3">3 Puntos</td>
                                </tr>
                                <tr class="border-b border-stone-100">
                                    <td class="py-3 font-semibold text-yellow-600">Empate</td>
                                    <td class="py-3">1 Punto</td>
                                </tr>
                                <tr>
                                    <td class="py-3 font-semibold text-red-600">Derrota</td>
                                    <td class="py-3">0 Puntos</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                    
                    <div class="border-l-4 border-stone-500 pl-4">
                        <h4 class="text-lg font-bold text-stone-800">Capítulo 5: Clasificación y Desempates</h4>
                        <p class="mt-2 text-stone-600">En caso de empate en puntos en la tabla general, se aplicarán los siguientes criterios en orden:</p>
                        <ol class="list-decimal list-inside mt-2 text-stone-600 space-y-1">
                            <li>Diferencia de Goles (Goles Favor - Goles Contra).</li>
                            <li>Mayor cantidad de Goles a Favor.</li>
                            <li>Resultado directo entre los equipos empatados.</li>
                            <li>Fair Play (Menor acumulación de tarjetas).</li>
                            <li>Sorteo.</li>
                        </ol>
                    </div>
                </div>
            `,
            disciplina: `
                 <div class="space-y-6 animate-fade-in">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="bg-yellow-50 p-5 rounded-lg border border-yellow-200">
                            <h4 class="text-lg font-bold text-yellow-800 flex items-center gap-2"><span class="text-2xl">🟨</span> Tarjeta Amarilla</h4>
                            <p class="text-sm text-yellow-900 mt-2">Amonestación por conducta antideportiva, infracciones reiteradas o barridas imprudentes.</p>
                            <div class="mt-3 text-xs font-semibold text-yellow-800 uppercase tracking-wide">Acumulación</div>
                            <p class="text-sm text-yellow-900">2 Amarillas en el mismo partido = Expulsión (Roja).</p>
                        </div>
                        <div class="bg-red-50 p-5 rounded-lg border border-red-200">
                            <h4 class="text-lg font-bold text-red-800 flex items-center gap-2"><span class="text-2xl">🟥</span> Tarjeta Roja</h4>
                            <p class="text-sm text-red-900 mt-2">Expulsión inmediata por agresión, insultos graves o juego brusco grave (barrida con fuerza excesiva).</p>
                            <div class="mt-3 text-xs font-semibold text-red-800 uppercase tracking-wide">Consecuencia</div>
                            <p class="text-sm text-red-900">Suspensión mínima de 1 partido. El equipo juega con uno menos.</p>
                        </div>
                    </div>
                    <div class="bg-white p-4 border border-stone-200 rounded">
                        <h4 class="font-bold text-stone-800">Capítulo 6: Conducta (Fair Play)</h4>
                        <p class="text-stone-600 mt-2 text-sm">El respeto hacia árbitros, rivales y público es obligatorio. Cualquier agresión física o verbal grave resultará en la expulsión del torneo del jugador o del equipo completo, según determine el comité.</p>
                    </div>
                </div>
            `,
            organizacion: `
                 <div class="space-y-6 animate-fade-in">
                    <div class="border-l-4 border-purple-500 pl-4">
                        <h4 class="text-lg font-bold text-stone-800">Capítulo 7: Logística</h4>
                        <ul class="list-disc list-inside mt-2 text-stone-600 space-y-2">
                            <li><strong>Puntualidad:</strong> Tolerancia máxima de 10 minutos. Pasado este tiempo, se decreta W.O. (Walkover).</li>
                            <li><strong>Credenciales:</strong> Obligatorio presentar credencial o identificación oficial antes del partido.</li>
                            <li><strong>Uniformes:</strong> Camisetas del mismo color y numeradas. Uso obligatorio de espinilleras.</li>
                        </ul>
                    </div>
                    <div class="border-l-4 border-purple-500 pl-4">
                        <h4 class="text-lg font-bold text-stone-800">Capítulo 8: Sustituciones</h4>
                        <ul class="list-disc list-inside mt-2 text-stone-600 space-y-2">
                            <li>Cambios ilimitados (rotativos).</li>
                            <li>Deben realizarse por la línea central y con autorización del árbitro.</li>
                            <li>Al realizar cambios, siempre se debe mantener el mínimo de 5 mujeres en cancha.</li>
                        </ul>
                    </div>
                </div>
            `
        };

        // Navigation Logic
        function switchTab(tabId) {
            // Reset styles
            ['general', 'puntuacion', 'disciplina', 'organizacion'].forEach(id => {
                const btn = document.getElementById(`tab-${id}`);
                btn.classList.remove('tab-active');
                btn.classList.add('tab-inactive');
            });

            // Set active style
            const activeBtn = document.getElementById(`tab-${tabId}`);
            activeBtn.classList.remove('tab-inactive');
            activeBtn.classList.add('tab-active');

            // Update content with Fade effect
            const contentDiv = document.getElementById('content-area');
            contentDiv.style.opacity = '0';
            setTimeout(() => {
                contentDiv.innerHTML = rulesContent[tabId];
                contentDiv.style.opacity = '1';
            }, 200);
        }

        function scrollToSection(id) {
            document.getElementById(id).scrollIntoView({ behavior: 'smooth' });
        }

        // Calculator Logic
        function updateCalculator() {
            const wins = parseInt(document.getElementById('input-wins').value) || 0;
            const draws = parseInt(document.getElementById('input-draws').value) || 0;
            const losses = parseInt(document.getElementById('input-losses').value) || 0; // Losses affect nothing but are good for tracking

            const total = (wins * 3) + (draws * 1);
            
            const display = document.getElementById('total-points');
            
            // Simple animation
            display.style.transform = "scale(1.2)";
            setTimeout(() => display.style.transform = "scale(1)", 200);
            
            display.textContent = total;
        }

        // Initialize Charts and Default Tab
        document.addEventListener('DOMContentLoaded', () => {
            // Load default tab
            const contentDiv = document.getElementById('content-area');
            contentDiv.innerHTML = rulesContent['general'];
            contentDiv.style.transition = 'opacity 0.3s ease-in-out';

            // Chart 1: Time
            const ctxTime = document.getElementById('timeChart').getContext('2d');
            new Chart(ctxTime, {
                type: 'doughnut',
                data: {
                    labels: ['1er Tiempo', 'Descanso', '2do Tiempo'],
                    datasets: [{
                        data: [20, 10, 20],
                        backgroundColor: ['#10b981', '#fbbf24', '#059669'], // Emerald-500, Amber-400, Emerald-600
                        borderWidth: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { position: 'bottom' },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return context.label + ': ' + context.raw + ' min';
                                }
                            }
                        }
                    }
                }
            });

            // Chart 2: Points
            const ctxPoints = document.getElementById('pointsChart').getContext('2d');
            new Chart(ctxPoints, {
                type: 'bar',
                data: {
                    labels: ['Victoria', 'Empate', 'Derrota'],
                    datasets: [{
                        label: 'Puntos Otorgados',
                        data: [3, 1, 0],
                        backgroundColor: ['#10b981', '#f59e0b', '#ef4444'], // Green, Amber, Red
                        borderRadius: 5
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: { stepSize: 1 }
                        }
                    },
                    plugins: {
                        legend: { display: false }
                    }
                }
            });
        });

    </script>
</body>
</html>
