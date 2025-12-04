<!DOCTYPE html>
<html lang="es" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Plataforma de Gestión Estratégica en Neuroimagen - RA3 Tecnología Médica. Universidad Señor de Sipán.">
    <meta name="author" content="Becerra, Chimoven, Delgado, Quintana">
    <meta name="theme-color" content="#0ea5e9">
    <title>NEURO-GESTIÓN | Plataforma Integral RA3</title>
    
    <!-- ==============================================
         1. INFRAESTRUCTURA Y LIBRERÍAS (CÓDIGO BASE)
    =============================================== -->
    
    <!-- Tipografía Clínica: 'Lato' para lectura densa y 'Oswald' para títulos de impacto -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,300&family=Oswald:wght@200;300;400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- Iconos Médicos Pro (FontAwesome) -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Animaciones al Scroll (AOS) -->
    <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
    <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>

    <!-- Visualización de Datos (Chart.js) -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <!-- Efectos Especiales (Confetti) -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

    <!-- Framework de Diseño (Tailwind CSS) -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Configuración del Tema "Hospital Futuro" -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Lato', 'sans-serif'],
                        header: ['Oswald', 'sans-serif'],
                    },
                    colors: {
                        // Paleta Clínica de Alto Contraste para Pantallas Diurnas
                        clinic: {
                            50: '#F8FAFC',  /* Blanco Hueso - Fondo Principal */
                            100: '#EFF6FF', /* Azul Hielo - Paneles Secundarios */
                            200: '#DBEAFE', /* Bordes Suaves */
                            300: '#BFDBFE',
                            400: '#60A5FA',
                            500: '#3B82F6', /* Azul Principal */
                            600: '#2563EB', /* Azul Acción */
                            700: '#1D4ED8',
                            800: '#1E40AF',
                            900: '#0F172A', /* Texto Profundo */
                        },
                        brand: {
                            primary: '#0077B6',   /* Azul Radiología */
                            secondary: '#00B4D8', /* Cian Diagnóstico */
                            accent: '#90E0EF',    /* Luz de Pantalla */
                            dark: '#03045E',      /* Contraste */
                        },
                        state: {
                            success: '#10B981', /* Verde Éxito */
                            warning: '#F59E0B', /* Ámbar Alerta */
                            danger: '#EF4444',  /* Rojo Peligro */
                            info: '#3B82F6',    /* Azul Info */
                        }
                    },
                    boxShadow: {
                        'soft': '0 4px 20px -2px rgba(0, 0, 0, 0.05)',
                        'hover': '0 20px 40px -5px rgba(0, 119, 182, 0.15)',
                        'card': '0 2px 10px rgba(0,0,0,0.03)',
                        'inner-glow': 'inset 0 2px 10px 0 rgba(255, 255, 255, 0.5)',
                        '3d': '0 10px 0 #e2e8f0',
                    },
                    backgroundImage: {
                        'grid-paper': "url('data:image/svg+xml,%3Csvg width=\"40\" height=\"40\" viewBox=\"0 0 40 40\" xmlns=\"http://www.w3.org/2000/svg\"%3E%3Cg fill=\"%230077b6\" fill-opacity=\"0.05\" fill-rule=\"evenodd\"%3E%3Cpath d=\"M0 40L40 0H20L0 20M40 40V20L20 40\"/%3E%3C/g%3E%3C/svg%3E')",
                    }
                }
            }
        }
    </script>

    <style>
        /* --- ESTILOS DE INGENIERÍA WEB --- */
        body {
            background-color: #F8FAFC;
            color: #0F172A;
            -webkit-font-smoothing: antialiased;
            overflow-x: hidden;
        }

        /* Tipografía Avanzada */
        h1, h2, h3, h4 { letter-spacing: 0.02em; }
        .text-justify-medical { text-align: justify; text-justify: inter-word; line-height: 1.8; }

        /* NAVEGACIÓN INTELIGENTE */
        .nav-fixed {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(16px);
            border-bottom: 1px solid rgba(0, 119, 182, 0.1);
            transition: all 0.3s ease;
        }
        .nav-link {
            position: relative;
            font-size: 0.75rem;
            font-weight: 700;
            color: #475569;
            text-transform: uppercase;
            letter-spacing: 0.05em;
            padding: 10px 0;
            transition: color 0.2s;
        }
        .nav-link:hover, .nav-link.active { color: #0077B6; }
        .nav-link::after {
            content: '';
            position: absolute;
            bottom: -4px; left: 0;
            width: 0; height: 3px;
            background: #0077B6;
            transition: width 0.3s ease;
        }
        .nav-link:hover::after, .nav-link.active::after { width: 100%; }

        /* TARJETAS DE INFORMACIÓN (CARDS) */
        .info-card {
            background: #FFFFFF;
            border: 1px solid #E2E8F0;
            border-radius: 16px;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.02);
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            overflow: hidden;
            display: flex;
            flex-direction: column;
            position: relative;
        }
        .info-card::before {
            content: '';
            position: absolute;
            top: 0; left: 0; width: 4px; height: 100%;
            background: #00B4D8;
            opacity: 0;
            transition: opacity 0.3s;
        }
        .info-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 20px 30px -10px rgba(0, 180, 216, 0.15);
            border-color: #90E0EF;
        }
        .info-card:hover::before { opacity: 1; }

        /* --- VISOR DICOM LINEAL (CORRECCIÓN APLICADA) --- */
        .dicom-viewer {
            position: relative;
            width: 100%;
            height: 600px;
            background: #000;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: inset 0 0 50px rgba(0,0,0,0.8);
            border: 6px solid #E2E8F0;
            cursor: ns-resize; /* Cursor vertical para indicar barrido */
        }
        .dicom-layer {
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background-size: cover;
            background-position: center;
        }
        /* Capa 1: Anatomía Base (T1 Simple - Oscuro) */
        .layer-anatomy {
            background-image: url('https://www.researchgate.net/publication/382934155/figure/fig1/AS:11431281272576084@1724156501766/Cranial-navigation-with-brainlab-cranial-navigation-10-The-primary-panel-A-displays.tif');
            filter: grayscale(100%) contrast(1.1) brightness(0.6);
            z-index: 1;
        }
        /* Capa 2: Patología Revelada (T1 Contraste - Color) */
        .layer-pathology {
            background-image: url('https://www.researchgate.net/publication/382934155/figure/fig1/AS:11431281272576084@1724156501766/Cranial-navigation-with-brainlab-cranial-navigation-10-The-primary-panel-A-displays.tif');
            filter: contrast(1.4) brightness(1.3) hue-rotate(15deg); 
            z-index: 2;
            /* La máscara se controla vía JS con clip-path: polygon */
            clip-path: polygon(0 0, 100% 0, 100% 0%, 0 0%); 
            transition: clip-path 0.05s linear; 
        }
        /* Barra de Escaneo Lineal */
        .scan-bar {
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 3px;
            background: #06B6D4; /* Cian Radiológico */
            box-shadow: 0 0 15px #06B6D4, 0 0 30px #06B6D4;
            z-index: 10;
            pointer-events: none;
        }
        
        /* INTERFAZ DE NUTRICIÓN (JUEGO) */
        .food-item {
            cursor: pointer;
            transition: transform 0.2s;
        }
        .food-item:hover { transform: scale(1.1); }
        .lunchbox-slot {
            border: 2px dashed #CBD5E1;
            border-radius: 12px;
            min-height: 100px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: #F8FAFC;
            transition: all 0.3s;
        }
        .lunchbox-slot.active { border-color: #10B981; background: #ECFDF5; }

        /* Biografías Expandibles */
        .bio-expand {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.8s ease, opacity 0.5s ease;
            opacity: 0;
        }
        .bio-expand.open { max-height: 1000px; opacity: 1; }

        /* Video Frame */
        .video-responsive {
            position: relative;
            padding-bottom: 56.25%;
            height: 0;
            overflow: hidden;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.2);
            border: 1px solid #E2E8F0;
        }
        .video-responsive iframe { position: absolute; top: 0; left: 0; width: 100%; height: 100%; }

        /* Scrollbar Personalizado */
        ::-webkit-scrollbar { width: 10px; }
        ::-webkit-scrollbar-track { background: #F1F5F9; }
        ::-webkit-scrollbar-thumb { background: #94A3B8; border-radius: 5px; border: 2px solid #F1F5F9; }
        ::-webkit-scrollbar-thumb:hover { background: #2563EB; }
    </style>
</head>
<body class="font-sans antialiased text-clinic-900 bg-white">

    <!-- ==============================================
         1. NAVEGACIÓN COMPLETA
    =============================================== -->
    <header class="fixed w-full top-0 z-[100] nav-fixed">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-20">
                <!-- Branding -->
                <div class="flex items-center gap-3 cursor-pointer" onclick="window.scrollTo(0,0)">
                    <div class="w-10 h-10 bg-brand-primary text-white rounded-lg flex items-center justify-center text-xl shadow-lg">
                        <i class="fas fa-brain-circuit"></i>
                    </div>
                    <div class="flex flex-col">
                        <h1 class="font-header font-bold text-xl leading-none text-clinic-900 tracking-tight">NEURO<span class="text-brand-secondary">GESTIÓN</span></h1>
                        <span class="text-[10px] font-bold uppercase tracking-[0.25em] text-clinic-500">RA3 • 2025</span>
                    </div>
                </div>

                <!-- Menú de Navegación -->
                <nav class="hidden xl:flex space-x-6">
                    <a href="#inicio" class="nav-link active">Inicio</a>
                    <a href="#diagnostico" class="nav-link">Diagnóstico</a>
                    <a href="#fundamentacion" class="nav-link">Informe</a>
                    <a href="#scanner" class="nav-link text-brand-secondary"><i class="fas fa-desktop mr-1"></i> DICOM Web</a>
                    <a href="#portafolio" class="nav-link">Actividades</a>
                    <a href="#recomendaciones" class="nav-link">Consejos</a>
                    <a href="#nutricion" class="nav-link text-state-success"><i class="fas fa-apple-alt mr-1"></i> Nutrición</a>
                    <a href="#equipo" class="nav-link">Equipo</a>
                </nav>

                <!-- Botones Acción -->
                <div class="flex items-center gap-3">
                    <button onclick="toggleBot()" class="flex items-center gap-2 px-5 py-2.5 bg-brand-dark text-white rounded-full text-xs font-bold uppercase tracking-wide hover:bg-black transition shadow-lg hover:shadow-xl hover:-translate-y-0.5">
                        <i class="fas fa-robot text-brand-accent"></i> Asistente
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- ==============================================
         2. HERO SECTION: PRESENTACIÓN DE ALTO IMPACTO
    =============================================== -->
    <section id="inicio" class="relative pt-32 pb-24 overflow-hidden bg-gradient-to-b from-clinic-50 to-white">
        <!-- Decoración -->
        <div class="absolute inset-0 bg-grid-paper opacity-10 pointer-events-none"></div>
        <div class="absolute top-0 right-0 w-[600px] h-[600px] bg-brand-secondary/5 rounded-full blur-3xl -translate-y-1/2 translate-x-1/4"></div>

        <div class="max-w-7xl mx-auto px-4 relative z-10">
            <div class="text-center mb-16">
                <div data-aos="fade-down" class="inline-flex items-center gap-2 px-4 py-1.5 rounded-full bg-white border border-brand-secondary/30 shadow-sm mb-6">
                    <span class="w-2 h-2 rounded-full bg-state-success animate-pulse"></span>
                    <span class="text-xs font-bold text-clinic-500 uppercase tracking-widest">Proyecto Académico Final</span>
                </div>
                
                <h1 data-aos="fade-up" class="text-5xl md:text-7xl font-header font-black text-clinic-900 mb-6 leading-tight">
                    PROGRAMA ESTRATÉGICO <br>
                    <span class="text-transparent bg-clip-text bg-gradient-to-r from-brand-primary to-brand-secondary">NEUROIMAGEN ONCOLÓGICA</span>
                </h1>
                
                <p data-aos="fade-up" data-aos-delay="100" class="text-xl text-clinic-600 max-w-4xl mx-auto font-light leading-relaxed">
                    Una propuesta integral para la detección temprana de tumores del Sistema Nervioso Central en la región <strong>Lambayeque</strong>, fusionando tecnología médica, gestión eficiente y neurociencia aplicada.
                </p>
            </div>

            <!-- Módulo de Video -->
            <div data-aos="zoom-in" data-aos-delay="200" class="max-w-5xl mx-auto mb-20">
                <div class="bg-white p-2 rounded-3xl shadow-hover border border-clinic-200 relative group">
                    <div class="absolute -inset-1 bg-gradient-to-r from-brand-primary to-brand-secondary rounded-[24px] blur opacity-25 group-hover:opacity-50 transition duration-1000"></div>
                    <div class="video-responsive bg-clinic-900 relative z-10">
                        <iframe src="https://www.youtube.com/embed/0yQtTuMdm-s?rel=0" title="Presentación del Proyecto" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
                    </div>
                    <div class="flex justify-between items-center px-6 py-4 relative z-10 bg-white rounded-b-2xl">
                        <div>
                            <h4 class="font-bold text-clinic-800 text-sm">Sustentación Oficial RA3</h4>
                            <p class="text-xs text-clinic-500">Duración: 4:00 min • Calidad HD</p>
                        </div>
                        <a href="#fundamentacion" class="text-xs font-bold text-brand-primary hover:underline uppercase tracking-wide transition">
                            Leer Documentación <i class="fas fa-file-medical ml-1"></i>
                        </a>
                    </div>
                </div>
            </div>

            <!-- Dashboard de Métricas (KPIs) -->
            <div class="grid grid-cols-2 md:grid-cols-4 gap-6 max-w-6xl mx-auto border-t border-clinic-200 pt-12">
                <div class="text-center group cursor-default">
                    <div class="text-4xl font-header font-bold text-brand-primary mb-1 group-hover:scale-110 transition-transform">300k+</div>
                    <div class="text-[10px] font-bold text-clinic-400 uppercase tracking-widest">Casos Globales/Año</div>
                </div>
                <div class="text-center group cursor-default">
                    <div class="text-4xl font-header font-bold text-state-danger mb-1 group-hover:scale-110 transition-transform">64%</div>
                    <div class="text-[10px] font-bold text-clinic-400 uppercase tracking-widest">Diagnóstico Tardío</div>
                </div>
                <div class="text-center group cursor-default">
                    <div class="text-4xl font-header font-bold text-state-warning mb-1 group-hover:scale-110 transition-transform">>60d</div>
                    <div class="text-[10px] font-bold text-clinic-400 uppercase tracking-widest">Espera Promedio</div>
                </div>
                <div class="text-center group cursor-default">
                    <div class="text-4xl font-header font-bold text-state-success mb-1 group-hover:scale-110 transition-transform">ODS 3</div>
                    <div class="text-[10px] font-bold text-clinic-400 uppercase tracking-widest">Salud y Bienestar</div>
                </div>
            </div>
        </div>
    </section>

    <!-- ==============================================
         3. REALIDAD PROBLEMÁTICA (DATA DRIVEN)
    =============================================== -->
    <section id="diagnostico" class="py-24 bg-white relative">
        <div class="max-w-7xl mx-auto px-4">
            
            <div class="grid lg:grid-cols-2 gap-16 items-start">
                <!-- Columna Texto -->
                <div data-aos="fade-right">
                    <div class="inline-block px-3 py-1 bg-state-danger/10 text-state-danger rounded font-bold text-xs uppercase tracking-widest mb-4 border border-state-danger/20">
                        <i class="fas fa-exclamation-triangle mr-2"></i> Diagnóstico Situacional
                    </div>
                    <h2 class="text-4xl font-header font-bold text-clinic-900 mb-6">El "Desierto Diagnóstico" en Lambayeque</h2>
                    
                    <div class="text-justify-medical text-clinic-600 space-y-6 text-sm md:text-base">
                        <p>
                            La región enfrenta una <strong>"paradoja tecnológica"</strong>. Aunque existen equipos de Resonancia Magnética en el Hospital Regional, la falta de gestión del ciclo de vida genera ineficiencia. Los pacientes sufren de <strong>"Scanxiety"</strong> (ansiedad por el escáner) ante la incertidumbre de citas lejanas.
                        </p>
                        <p>
                            La centralización en Chiclayo obliga a pacientes de zonas altoandinas (Incahuasi, Cañaris) a realizar viajes costosos, enfrentando barreras geográficas y lingüísticas. Esto resulta en diagnósticos en estadios avanzados (III y IV) donde las opciones terapéuticas son limitadas.
                        </p>
                        
                        <div class="bg-clinic-50 p-6 rounded-xl border-l-4 border-state-danger mt-6 shadow-sm">
                            <h4 class="font-bold text-clinic-800 mb-3 text-sm uppercase border-b border-clinic-200 pb-2">Evidencia Cuantitativa (MINSA/SUSALUD):</h4>
                            <ul class="space-y-3 text-sm">
                                <li class="flex items-start gap-3">
                                    <i class="fas fa-times-circle text-state-danger mt-1"></i>
                                    <span><strong>Escasez:</strong> Solo hay un resonador operativo por cada 10,000 pacientes oncológicos.</span>
                                </li>
                                <li class="flex items-start gap-3">
                                    <i class="fas fa-clock text-state-danger mt-1"></i>
                                    <span><strong>Retraso:</strong> Tiempo de espera > 60 días en el sector público.</span>
                                </li>
                                <li class="flex items-start gap-3">
                                    <i class="fas fa-user-md text-state-danger mt-1"></i>
                                    <span><strong>Brecha Humana:</strong> Déficit crítico de tecnólogos subespecialistas.</span>
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>

                <!-- Columna Gráfica -->
                <div data-aos="fade-left" class="sticky top-28">
                    <div class="bg-white p-8 rounded-3xl shadow-hover border border-clinic-200">
                        <div class="text-center mb-6">
                            <h3 class="font-bold text-clinic-800 text-lg">Brecha de Acceso Regional</h3>
                            <p class="text-xs text-clinic-400 uppercase tracking-widest">Comparativa 2024-2025</p>
                        </div>
                        <!-- Canvas para Chart.js -->
                        <div class="h-64">
                            <canvas id="chartRealidad"></canvas>
                        </div>
                        <div class="mt-6 grid grid-cols-2 gap-4">
                            <div class="p-3 bg-red-50 rounded-lg text-center border border-red-100">
                                <span class="block text-2xl font-black text-state-danger">64%</span>
                                <span class="text-[10px] font-bold text-clinic-500 uppercase">Detección Tardía</span>
                            </div>
                            <div class="p-3 bg-orange-50 rounded-lg text-center border border-orange-100">
                                <span class="block text-2xl font-black text-state-warning">40%</span>
                                <span class="text-[10px] font-bold text-clinic-500 uppercase">Tasa Downtime</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- ==============================================
         4. HERRAMIENTA: VISOR DICOM LINEAL (CORRECCIÓN APLICADA)
    =============================================== -->
    <section id="scanner" class="py-24 bg-clinic-900 text-white relative overflow-hidden">
        <div class="absolute inset-0 bg-grid-paper opacity-10 pointer-events-none"></div>
        <div class="max-w-6xl mx-auto px-4 relative z-10">
            <div class="text-center mb-12">
                <span class="text-brand-accent font-mono text-xs tracking-[0.2em] uppercase mb-2 block">Módulo de Entrenamiento Clínico</span>
                <h2 class="text-3xl md:text-4xl font-header font-bold text-white mb-4">VISOR DICOM: BARRIDO LINEAL</h2>
                <p class="text-clinic-400 max-w-2xl mx-auto text-sm">
                    <strong>Instrucciones:</strong> Desliza el cursor verticalmente sobre la imagen para simular el barrido del escáner y revelar la patología oculta en el cerebro (Lóbulo Frontal).
                </p>
            </div>

            <!-- CONTENEDOR DEL ESCÁNER -->
            <div class="dicom-viewer group" id="dicomViewer" onmousemove="updateDicomScan(event)">
                
                <!-- Capa 1: Anatomía (Imagen Base - Oscura/T1 Simple) -->
                <div class="dicom-layer layer-anatomy"></div>
                
                <!-- Capa 2: Patología (Imagen Revelada - Contraste) -->
                <div class="dicom-layer layer-pathology" id="dicomReveal"></div>

                <!-- Barra de Escaneo (Línea Vertical) -->
                <div class="scan-bar" id="scanBar"></div>

                <!-- HUD (Head-Up Display) -->
                <div class="absolute top-4 left-4 font-mono text-xs text-brand-accent space-y-1 pointer-events-none select-none z-20 bg-black/50 p-2 rounded border border-clinic-700">
                    <p>PT: Anonymous | ID: 849302</p>
                    <p>SEQ: T1_W_SE / T1_Gad_Enhance</p>
                    <p>SLICE: <span id="slicePos">0</span> mm</p>
                    <p>WW: 400 WL: 40</p>
                </div>

                <!-- Grid Overlay -->
                <div class="scan-overlay-grid"></div>

                <!-- Alerta Diagnóstica (Feedback) -->
                <div id="tumorAlert" class="absolute bottom-10 left-1/2 -translate-x-1/2 bg-state-danger text-white px-6 py-2 rounded-full font-bold text-sm uppercase tracking-widest shadow-lg hidden z-30 animate-pulse border-2 border-white">
                    <i class="fas fa-radiation-alt mr-2"></i> Anomalía Detectada
                </div>
            </div>

            <div class="flex justify-center gap-4 mt-8">
                <button onclick="resetDicom()" class="px-6 py-2 border border-clinic-600 text-clinic-400 text-xs font-bold uppercase rounded hover:text-white hover:border-white transition">
                    Reiniciar Secuencia
                </button>
                <button onclick="alert('Imagen capturada y enviada al PACS. Iniciando protocolo de neurocirugía.')" class="px-6 py-2 bg-brand-primary text-white text-xs font-bold uppercase rounded hover:bg-brand-secondary transition shadow-lg shadow-brand-primary/30">
                    <i class="fas fa-camera mr-2"></i> Capturar Imagen
                </button>
            </div>
        </div>
    </section>

    <!-- ==============================================
         5. INFORME TÉCNICO COMPLETO (TABS)
    =============================================== -->
    <section id="fundamentacion" class="py-24 bg-clinic-50 border-y border-clinic-200">
        <div class="max-w-7xl mx-auto px-4">
            
            <!-- Navegación de Pestañas -->
            <div class="flex flex-wrap justify-center gap-2 mb-12 bg-white p-2 rounded-full shadow-sm w-fit mx-auto border border-clinic-200">
                <button onclick="openTab('objs', this)" class="px-6 py-2 rounded-full text-xs font-bold uppercase tracking-wide transition bg-brand-primary text-white shadow-md">Objetivos</button>
                <button onclick="openTab('just', this)" class="px-6 py-2 rounded-full text-xs font-bold uppercase tracking-wide transition text-clinic-600 hover:bg-clinic-100">Justificación</button>
                <button onclick="openTab('metod', this)" class="px-6 py-2 rounded-full text-xs font-bold uppercase tracking-wide transition text-clinic-600 hover:bg-clinic-100">Metodología</button>
                <button onclick="openTab('result', this)" class="px-6 py-2 rounded-full text-xs font-bold uppercase tracking-wide transition text-clinic-600 hover:bg-clinic-100">Resultados</button>
                <button onclick="openTab('refl', this)" class="px-6 py-2 rounded-full text-xs font-bold uppercase tracking-wide transition text-clinic-600 hover:bg-clinic-100">Reflexión</button>
            </div>

            <!-- Contenido Dinámico -->
            <div class="bg-white p-10 md:p-16 rounded-3xl shadow-medical border border-clinic-100 min-h-[500px]">
                
                <!-- 1. OBJETIVOS -->
                <div id="tab-objs" class="tab-content active">
                    <div class="bg-gradient-to-r from-brand-primary to-brand-secondary text-white p-10 rounded-2xl mb-10 shadow-lg">
                        <h3 class="font-header font-bold text-2xl mb-4 border-b border-white/20 pb-4 inline-block">OBJETIVO GENERAL</h3>
                        <p class="text-lg font-light leading-relaxed">
                            "Determinar un programa estratégico de diagnóstico por imágenes que fortalezca la detección temprana de lesiones tumorales cerebrales en la región Lambayeque, optimizando recursos tecnológicos y humanos."
                        </p>
                    </div>
                    <div class="grid md:grid-cols-3 gap-8">
                        <div class="info-card p-8">
                            <span class="text-4xl font-bold text-clinic-200 mb-4 block">01</span>
                            <h4 class="font-bold text-clinic-800 text-lg mb-2">Fundamentar</h4>
                            <p class="text-sm text-clinic-600">Establecer bases teóricas sobre gestión tecnológica avanzada y neurociencia aplicada a la oncología.</p>
                        </div>
                        <div class="info-card p-8">
                            <span class="text-4xl font-bold text-clinic-200 mb-4 block">02</span>
                            <h4 class="font-bold text-clinic-800 text-lg mb-2">Diagnosticar</h4>
                            <p class="text-sm text-clinic-600">Evaluar infraestructura, brechas de talento y tiempos de espera críticos en los servicios.</p>
                        </div>
                        <div class="info-card p-8">
                            <span class="text-4xl font-bold text-clinic-200 mb-4 block">03</span>
                            <h4 class="font-bold text-clinic-800 text-lg mb-2">Diseñar</h4>
                            <p class="text-sm text-clinic-600">Crear un programa integral con protocolos estandarizados y plan de mantenimiento (GCEB).</p>
                        </div>
                    </div>
                </div>

                <!-- 2. JUSTIFICACIÓN -->
                <div id="tab-just" class="tab-content">
                    <h3 class="font-bold text-clinic-900 text-2xl mb-8">Justificación e Importancia</h3>
                    <div class="grid md:grid-cols-2 gap-12">
                        <div class="prose text-clinic-600 text-justify-medical">
                            <p>
                                En neuro-oncología, el axioma es absoluto: <strong>"el tiempo es cerebro"</strong>. Cada semana de retraso reduce significativamente la ventana terapéutica y la supervivencia global. Este programa busca transformar el modelo de una "medicina de la espera" a una "medicina de la oportunidad".
                            </p>
                            <div class="mt-6 p-6 bg-green-50 rounded-2xl border-l-4 border-state-success">
                                <h5 class="font-bold text-green-800 mb-2 flex items-center gap-2"><i class="fas fa-leaf"></i> Aporte Ecológico</h5>
                                <p class="text-sm text-green-700">Descentralizar reduce traslados masivos a Lima, disminuyendo significativamente la huella de carbono del transporte médico.</p>
                            </div>
                        </div>
                        <div class="space-y-6">
                            <div class="p-6 bg-blue-50 rounded-2xl border-l-4 border-state-info">
                                <h5 class="font-bold text-blue-800 mb-2 flex items-center gap-2"><i class="fas fa-users"></i> Aporte Social</h5>
                                <p class="text-sm text-blue-700">Reivindica el derecho a la salud equitativa, eliminando barreras financieras para los más pobres (ODS 3 y 10).</p>
                            </div>
                            <div class="p-6 bg-purple-50 rounded-2xl border-l-4 border-purple-500">
                                <h5 class="font-bold text-purple-800 mb-2 flex items-center gap-2"><i class="fas fa-user-md"></i> Aporte Profesional</h5>
                                <p class="text-sm text-purple-700">Revaloriza al Tecnólogo Médico como pieza científica clave, fomentando la especialización en física médica y neuroanatomía.</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- 3. METODOLOGÍA -->
                <div id="tab-metod" class="tab-content">
                    <h3 class="font-bold text-clinic-900 text-2xl mb-8">Estrategia Metodológica</h3>
                    <div class="grid md:grid-cols-2 gap-12">
                        <div>
                            <h4 class="font-bold text-clinic-800 mb-4">Métodos Teóricos</h4>
                            <ul class="space-y-4">
                                <li class="flex items-start gap-4 p-4 rounded-xl hover:bg-clinic-50 transition border border-transparent hover:border-clinic-100">
                                    <div class="w-8 h-8 rounded-full bg-clinic-100 flex items-center justify-center text-clinic-600"><i class="fas fa-check"></i></div>
                                    <p class="text-sm text-clinic-600"><strong>Analítico-Sintético:</strong> Descomponer la realidad del servicio de radiología en sus componentes (RRHH, Equipos).</p>
                                </li>
                                <li class="flex items-start gap-4 p-4 rounded-xl hover:bg-clinic-50 transition border border-transparent hover:border-clinic-100">
                                    <div class="w-8 h-8 rounded-full bg-clinic-100 flex items-center justify-center text-clinic-600"><i class="fas fa-network-wired"></i></div>
                                    <p class="text-sm text-clinic-600"><strong>Enfoque Sistémico:</strong> Entender el diagnóstico como un subsistema crítico, interactuando con oncología y neurocirugía.</p>
                                </li>
                            </ul>
                        </div>
                        <div class="bg-clinic-50 p-8 rounded-2xl border border-clinic-200">
                            <h4 class="font-bold text-clinic-800 mb-4 text-center">Fuentes de Datos</h4>
                            <div class="flex flex-wrap gap-2 justify-center mb-6">
                                <span class="bg-white px-3 py-1 rounded shadow-sm text-xs font-bold text-clinic-600">GLOBOCAN 2024</span>
                                <span class="bg-white px-3 py-1 rounded shadow-sm text-xs font-bold text-clinic-600">MINSA</span>
                                <span class="bg-white px-3 py-1 rounded shadow-sm text-xs font-bold text-clinic-600">SUSALUD</span>
                                <span class="bg-white px-3 py-1 rounded shadow-sm text-xs font-bold text-clinic-600">PubMed</span>
                            </div>
                            <h4 class="font-bold text-clinic-800 mb-4 text-center">Instrumentos</h4>
                            <ul class="text-xs text-clinic-500 space-y-2 text-center">
                                <li>• Encuesta de Capacidad y Satisfacción (ECSN)</li>
                                <li>• Matriz de KPIs (Tiempo de Espera, Uptime)</li>
                                <li>• Auditoría Técnica de Imágenes DICOM</li>
                            </ul>
                        </div>
                    </div>
                </div>

                <!-- 4. RESULTADOS -->
                <div id="tab-result" class="tab-content">
                    <h3 class="font-bold text-clinic-900 text-2xl mb-8">Impacto Proyectado</h3>
                    <div class="grid md:grid-cols-2 gap-8">
                        <div class="info-card p-6 border-l-4 border-l-state-success">
                            <h4 class="font-bold text-clinic-800 mb-2">Reducción de Brechas</h4>
                            <p class="text-sm text-clinic-600 text-justify">Se espera disminuir el Tiempo Mediano de Espera (TME) de >60 días a <15 días, alineando la atención regional con estándares internacionales.</p>
                        </div>
                        <div class="info-card p-6 border-l-4 border-l-brand-primary">
                            <h4 class="font-bold text-clinic-800 mb-2">Neurociencia Aplicada</h4>
                            <p class="text-sm text-clinic-600 text-justify">La integración de técnicas avanzadas (tractografía) permitirá planificar cirugías que preserven las redes neuronales, mejorando la calidad de vida.</p>
                        </div>
                        <div class="info-card p-6 border-l-4 border-l-state-warning">
                            <h4 class="font-bold text-clinic-800 mb-2">Eficiencia de Recursos</h4>
                            <p class="text-sm text-clinic-600 text-justify">La gestión del ciclo de vida (GCEB) aumentará el "uptime" de los equipos al 95%, reduciendo las cancelaciones de citas.</p>
                        </div>
                        <div class="info-card p-6 border-l-4 border-l-state-info">
                            <h4 class="font-bold text-clinic-800 mb-2">Equidad Social</h4>
                            <p class="text-sm text-clinic-600 text-justify">Al descentralizar el diagnóstico, se eliminan barreras geográficas para pacientes de zonas rurales, democratizando la salud de alta complejidad.</p>
                        </div>
                    </div>
                </div>

                <!-- 5. REFLEXIÓN -->
                <div id="tab-refl" class="tab-content">
                    <div class="prose max-w-none text-clinic-600 text-justify-medical">
                        <div class="bg-clinic-100 p-8 rounded-2xl border border-clinic-200 mb-8">
                            <p class="text-lg italic font-medium text-clinic-800">
                                "El proceso de elaboración de este informe nos ha permitido comprender que la 'brecha tecnológica' no se resuelve simplemente comprando más máquinas, sino gestionando inteligentemente las que se tienen y capacitando al talento humano que las opera."
                            </p>
                        </div>
                        <div class="grid md:grid-cols-2 gap-8">
                            <div>
                                <h4 class="font-bold text-clinic-900 mb-2">Rol Profesional</h4>
                                <p class="text-sm">El Tecnólogo Médico es garante de la calidad diagnóstica. Nuestra especialización en física médica nos empodera para ser líderes en la implementación de técnicas que salvan vidas.</p>
                            </div>
                            <div>
                                <h4 class="font-bold text-clinic-900 mb-2">Ética Neurocientífica</h4>
                                <p class="text-sm">La conexión con la ética es fundamental. La neurociencia nos revela la complejidad de la identidad humana, imponiendo el deber ético de la <strong>"no maleficencia"</strong>: combatir la ineficiencia que causa daño irreversible.</p>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </section>

    <!-- ==============================================
         6. PORTAFOLIO 10 ACTIVIDADES (TARJETAS GRANDES)
    =============================================== -->
    <section id="portafolio" class="py-24 bg-white border-t border-clinic-200">
        <div class="max-w-7xl mx-auto px-4">
            <div class="text-center mb-16">
                <span class="text-clinic-600 font-bold uppercase tracking-widest text-xs mb-3 block">Intervención Comunitaria</span>
                <h2 class="text-4xl font-header font-black text-clinic-900 mb-6">10 ESTRATEGIAS MAESTRAS</h2>
                <p class="text-clinic-500 max-w-3xl mx-auto">
                    Propuestas de intervención comunitaria basadas en los determinantes sociales de la salud y la neurociencia. Haz clic para ver el detalle completo.
                </p>
            </div>

            <div class="grid md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8" id="activitiesGrid">
                <!-- JS inyectará las tarjetas aquí -->
            </div>
        </div>
    </section>

    <!-- ==============================================
         7. SECCIÓN DE RECOMENDACIONES (NUEVA)
    =============================================== -->
    <section id="recomendaciones" class="py-24 bg-clinic-50 border-t border-clinic-200">
        <div class="max-w-7xl mx-auto px-4">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-header font-bold text-clinic-900">10 Recomendaciones Clave</h2>
                <p class="text-clinic-600">Guía práctica para la gestión eficiente y humanizada en neuroimagen.</p>
            </div>
            
            <div class="grid md:grid-cols-2 gap-6">
                <!-- 1-5 -->
                <div class="space-y-4">
                    <div class="bg-white p-4 rounded-xl shadow-sm border-l-4 border-l-brand-primary">
                        <h4 class="font-bold text-sm text-clinic-800">1. Gestión de Uptime</h4>
                        <p class="text-xs text-clinic-600">Implementar contratos de mantenimiento preventivo para asegurar la operatividad de los equipos.</p>
                    </div>
                    <div class="bg-white p-4 rounded-xl shadow-sm border-l-4 border-l-state-success">
                        <h4 class="font-bold text-sm text-clinic-800">2. Humanización</h4>
                        <p class="text-xs text-clinic-600">Capacitar al personal en "Soft Skills" para reducir el estrés del paciente (Scanxiety).</p>
                    </div>
                    <div class="bg-white p-4 rounded-xl shadow-sm border-l-4 border-l-brand-secondary">
                        <h4 class="font-bold text-sm text-clinic-800">3. Protocolos Rápidos</h4>
                        <p class="text-xs text-clinic-600">Estandarizar secuencias rápidas (Fast-MRI) para pacientes pediátricos o claustrofóbicos.</p>
                    </div>
                    <div class="bg-white p-4 rounded-xl shadow-sm border-l-4 border-l-state-warning">
                        <h4 class="font-bold text-sm text-clinic-800">4. Descentralización</h4>
                        <p class="text-xs text-clinic-600">Crear redes de tele-radiología para que las imágenes tomadas en provincias sean leídas por especialistas.</p>
                    </div>
                    <div class="bg-white p-4 rounded-xl shadow-sm border-l-4 border-l-state-danger">
                        <h4 class="font-bold text-sm text-clinic-800">5. Signos de Alarma</h4>
                        <p class="text-xs text-clinic-600">Educar a la atención primaria para derivar inmediatamente ante "Red Flags" (Vómitos, Cefalea nocturna).</p>
                    </div>
                </div>
                <!-- 6-10 -->
                <div class="space-y-4">
                    <div class="bg-white p-4 rounded-xl shadow-sm border-l-4 border-l-brand-primary">
                        <h4 class="font-bold text-sm text-clinic-800">6. Neuro-Protección</h4>
                        <p class="text-xs text-clinic-600">Promover estilos de vida (sueño, ejercicio) que aumenten la reserva cognitiva de la población.</p>
                    </div>
                    <div class="bg-white p-4 rounded-xl shadow-sm border-l-4 border-l-state-success">
                        <h4 class="font-bold text-sm text-clinic-800">7. Seguridad Radiológica</h4>
                        <p class="text-xs text-clinic-600">Cumplir estrictamente con los criterios de seguridad en RM (Zona IV) para evitar accidentes con ferromagnéticos.</p>
                    </div>
                    <div class="bg-white p-4 rounded-xl shadow-sm border-l-4 border-l-brand-secondary">
                        <h4 class="font-bold text-sm text-clinic-800">8. Interdisciplina</h4>
                        <p class="text-xs text-clinic-600">Fomentar comités de tumores (Tumor Board) donde radiólogos, tecnólogos y cirujanos discutan los casos.</p>
                    </div>
                    <div class="bg-white p-4 rounded-xl shadow-sm border-l-4 border-l-state-warning">
                        <h4 class="font-bold text-sm text-clinic-800">9. Capacitación Continua</h4>
                        <p class="text-xs text-clinic-600">El personal debe actualizarse anualmente en nuevas secuencias (DTI, PWI) y software de post-proceso.</p>
                    </div>
                    <div class="bg-white p-4 rounded-xl shadow-sm border-l-4 border-l-state-danger">
                        <h4 class="font-bold text-sm text-clinic-800">10. Auditoría de Calidad</h4>
                        <p class="text-xs text-clinic-600">Realizar revisiones mensuales de la calidad de imagen para detectar fallas técnicas a tiempo.</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- ==============================================
         8. JUEGO NEURO-NUTRICIÓN (INTERACTIVO)
    =============================================== -->
    <section id="nutricion" class="py-24 bg-white border-t border-clinic-200">
        <div class="max-w-4xl mx-auto px-4 text-center">
            <h2 class="text-3xl font-header font-bold text-clinic-900 mb-4">Arma tu Lonchera Cerebral</h2>
            <p class="text-clinic-600 mb-8">Selecciona los alimentos que protegen la mielina y potencian la función cognitiva. ¡Evita los neurotóxicos!</p>
            
            <div class="bg-clinic-50 p-8 rounded-3xl border border-clinic-200 shadow-inner">
                <div class="flex flex-wrap justify-center gap-6 mb-8" id="foodContainer">
                    <div class="food-item text-center" onclick="selectFood(this, true, 'Pescado')">
                        <div class="w-16 h-16 bg-white rounded-full flex items-center justify-center text-3xl shadow-sm border border-clinic-100">🐟</div>
                        <p class="text-xs mt-2 font-bold text-clinic-600">Pescado</p>
                    </div>
                    <div class="food-item text-center" onclick="selectFood(this, false, 'Gaseosa')">
                        <div class="w-16 h-16 bg-white rounded-full flex items-center justify-center text-3xl shadow-sm border border-clinic-100">🥤</div>
                        <p class="text-xs mt-2 font-bold text-clinic-600">Gaseosa</p>
                    </div>
                    <div class="food-item text-center" onclick="selectFood(this, true, 'Nueces')">
                        <div class="w-16 h-16 bg-white rounded-full flex items-center justify-center text-3xl shadow-sm border border-clinic-100">🥜</div>
                        <p class="text-xs mt-2 font-bold text-clinic-600">Nueces</p>
                    </div>
                    <div class="food-item text-center" onclick="selectFood(this, true, 'Arándanos')">
                        <div class="w-16 h-16 bg-white rounded-full flex items-center justify-center text-3xl shadow-sm border border-clinic-100">🫐</div>
                        <p class="text-xs mt-2 font-bold text-clinic-600">Arándanos</p>
                    </div>
                    <div class="food-item text-center" onclick="selectFood(this, false, 'Frituras')">
                        <div class="w-16 h-16 bg-white rounded-full flex items-center justify-center text-3xl shadow-sm border border-clinic-100">🍟</div>
                        <p class="text-xs mt-2 font-bold text-clinic-600">Frituras</p>
                    </div>
                </div>

                <div class="grid grid-cols-3 gap-4 max-w-lg mx-auto">
                    <div class="lunchbox-slot" id="slot1"></div>
                    <div class="lunchbox-slot" id="slot2"></div>
                    <div class="lunchbox-slot" id="slot3"></div>
                </div>
                
                <p id="nutriFeedback" class="mt-6 font-bold text-sm h-6"></p>
                <button onclick="resetGame()" class="mt-4 px-6 py-2 bg-clinic-600 text-white rounded-full text-xs font-bold uppercase hover:bg-clinic-700 transition">Reiniciar Lonchera</button>
            </div>
        </div>
    </section>

   <!-- ==============================================
     9. EQUIPO DE INVESTIGACIÓN (CORREGIDO)
=============================================== -->
<section id="equipo" class="py-24 bg-clinic-50 border-t border-clinic-200">
  <div class="max-w-7xl mx-auto px-4 text-center">
    <h2 class="text-3xl font-header font-bold text-clinic-900 mb-6">EQUIPO DE INVESTIGACIÓN</h2>

    <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-8">

      <!-- 1. ISAAC DELGADO -->
      <article class="card-person bg-white p-8 rounded-2xl shadow-medical border border-clinic-100 hover:-translate-y-2 transition duration-300">
        <div class="w-32 h-32 mx-auto rounded-full overflow-hidden border-4 border-brand-accent mb-6 shadow-lg">
          <img src="https://i.postimg.cc/s2Jwx8kZ/34fdb936-f9b8-458e-b04c-bc36f97d812e.jpg" alt="Isaac Delgado" class="w-full h-full object-cover">
        </div>
        <h3 class="font-bold text-lg text-clinic-900">Isaac Delgado Fernández</h3>
        <p class="text-xs text-brand-secondary font-bold uppercase tracking-widest mb-4">Analista DSS</p>
        <button onclick="toggleBio('bio1')" class="text-xs text-clinic-400 hover:text-brand-secondary uppercase font-bold underline">Ver Biografía</button>

        <div id="bio1" class="bio-expand mt-4 text-xs text-clinic-500 text-justify bg-clinic-50 p-4 rounded-lg">
          <p>
            Soy Isaac Delgado Fernández, estudiante de Tecnología Médica con especialidad en Radiología en la Universidad Señor de Sipán. Actualmente curso el cuarto ciclo, donde continúo fortaleciendo mis conocimientos en diagnóstico por imágenes. Me considero una persona tranquila, dedicada y con valores sólidos. En mis tiempos libres disfruto salir con mi familia, pescar y practicar deporte, actividades que me mantienen activo y en equilibrio. Mi objetivo es desarrollarme profesionalmente para brindar un servicio de calidad y contribuir al bienestar de los pacientes desde el área de la salud.
          </p>
        </div>
      </article>

      <!-- 2. GERARDO BECERRA -->
      <article class="card-person bg-white p-8 rounded-2xl shadow-medical border border-clinic-100 hover:-translate-y-2 transition duration-300">
        <div class="w-32 h-32 mx-auto rounded-full overflow-hidden border-4 border-brand-primary mb-6 shadow-lg">
          <img src="https://i.postimg.cc/N0xpFV3m/cda23891-a71e-4fef-9bcc-686c8e294174.jpg" alt="Gerardo Becerra" class="w-full h-full object-cover">
        </div>
        <h3 class="font-bold text-lg text-clinic-900">Gerardo Becerra Fernández</h3>
        <p class="text-xs text-brand-primary font-bold uppercase tracking-widest mb-4">Investigador</p>
        <button onclick="toggleBio('bio2')" class="text-xs text-clinic-400 hover:text-brand-primary uppercase font-bold underline">Ver Biografía</button>

        <div id="bio2" class="bio-expand mt-4 text-xs text-clinic-500 text-justify bg-clinic-50 p-4 rounded-lg">
          <p>
            Mi nombre es Gerardo Becerra Fernández, tengo 26 años y resido en Chiclayo. Estudio Tecnología Médica con especialidad en Radiología en la Universidad Señor de Sipán, actualmente en el cuarto ciclo. Me apasiona el diagnóstico por imágenes y la aplicación de la tecnología en el ámbito de la salud. Me considero perseverante, responsable y con un fuerte deseo de superación. En mis momentos libres disfruto jugar básquet y conectarme con la naturaleza. Aspiro a convertirme en un tecnólogo médico ético, competente y comprometido con la calidad del cuidado al paciente.
          </p>
        </div>
      </article>

      <!-- 3. MASHORY CIELO -->
      <article class="card-person bg-white p-8 rounded-2xl shadow-medical border border-clinic-100 hover:-translate-y-2 transition duration-300">
        <div class="w-32 h-32 mx-auto rounded-full overflow-hidden border-4 border-state-success mb-6 shadow-lg">
          <img src="https://i.postimg.cc/jjhZ29py/61ef48f3-1b9d-41db-8690-0b4adb3d000e.jpg" alt="Mashory Cielo" class="w-full h-full object-cover">
        </div>
        <h3 class="font-bold text-lg text-clinic-900">Mashory Cielo Chimoven Quispe</h3>
        <p class="text-xs text-state-success font-bold uppercase tracking-widest mb-4">Neuro-Desarrollo</p>
        <button onclick="toggleBio('bio3')" class="text-xs text-clinic-400 hover:text-state-success uppercase font-bold underline">Ver Biografía</button>

        <div id="bio3" class="bio-expand mt-4 text-xs text-clinic-500 text-justify bg-clinic-50 p-4 rounded-lg">
          <p>
            Soy Mashory Cielo Chimoven Quispe, estudiante de Tecnología Médica con especialidad en Radiología en la Universidad Señor de Sipán. Actualmente curso el cuarto ciclo y me encuentro enfocada en desarrollar habilidades sólidas en técnicas radiológicas. Me motiva aprender continuamente, pues considero que esta área es fundamental para el diagnóstico oportuno de diversas patologías. Me esfuerzo por mantener un desempeño responsable y ético, buscando siempre mejorar. Aspiro a convertirme en una tecnóloga médica preparada y comprometida con brindar atención de calidad y contribuir al bienestar de la comunidad.
          </p>
        </div>
      </article>

      <!-- 4. FRANK QUINTANA -->
      <article class="card-person bg-white p-8 rounded-2xl shadow-medical border border-clinic-100 hover:-translate-y-2 transition duration-300">
        <div class="w-32 h-32 mx-auto rounded-full overflow-hidden border-4 border-state-warning mb-6 shadow-lg">
          <img src="https://i.postimg.cc/s2Jwx8kS/3f1bb54e-c46c-4a1c-a904-17a5447d472e.jpg" alt="Frank Quintana" class="w-full h-full object-cover">
        </div>
        <h3 class="font-bold text-lg text-clinic-900">Frank Yomar Quintana Carranza</h3>
        <p class="text-xs text-state-warning font-bold uppercase tracking-widest mb-4">Coordinador</p>
        <button onclick="toggleBio('bio4')" class="text-xs text-clinic-400 hover:text-state-warning uppercase font-bold underline">Ver Biografía</button>

        <div id="bio4" class="bio-expand mt-4 text-xs text-clinic-500 text-justify bg-clinic-50 p-4 rounded-lg">
          <p>
            Mi nombre es Frank Yomar Quintana Carranza, tengo 22 años y soy natural de la provincia de Cutervo. Actualmente estudio Tecnología Médica con especialidad en Radiología en la Universidad Señor de Sipán, cursando el cuarto ciclo. Me considero una persona responsable, con metas claras y un fuerte deseo de crecimiento académico. En mis tiempos libres disfruto practicar deporte, especialmente fútbol, pues me ayuda a mantenerme activo y despejar la mente. Aspiro a convertirme en un tecnólogo médico competente, comprometido y capaz de brindar un servicio de calidad a la comunidad.
          </p>
        </div>
      </article>

    </div>
  </div>
</section>

    <!-- FOOTER -->
    <footer class="bg-clinic-900 text-clinic-400 py-16">
        <div class="max-w-7xl mx-auto px-4">
            <div class="grid md:grid-cols-2 gap-12">
                <div>
                    <h4 class="font-bold text-white text-lg mb-6 border-l-4 border-brand-primary pl-3">Sobre el Proyecto</h4>
                    <p class="text-sm leading-relaxed mb-4">
                        Neuro-Gestión 2025 es una iniciativa académica de la Escuela de Tecnología Médica de la Universidad Señor de Sipán, diseñada para abordar la problemática del diagnóstico tardío de tumores cerebrales en la región Lambayeque.
                    </p>
                    <p class="text-xs uppercase tracking-widest font-bold text-brand-accent">Pimentel - Perú 2025</p>
                </div>
                <div>
                    <h4 class="font-bold text-white text-lg mb-6 border-l-4 border-brand-secondary pl-3">Referencias (Vancouver)</h4>
                    <ul class="text-xs space-y-2 font-mono">
                        <li>1. Global Cancer Observatory. Brain, Central Nervous System Fact Sheet. 2024.</li>
                        <li>2. CBTRUS. Statistical Report: Primary Brain Tumors. 2025.</li>
                        <li>3. Instituto de Salud Global de Barcelona. One Health. 2025.</li>
                        <li>4. UNESCO. Neurotecnologías y derechos humanos. 2025.</li>
                        <li>5. OPS/OMS. Equidad en la atención de salud en Perú. 2024.</li>
                    </ul>
                </div>
            </div>
            <div class="border-t border-clinic-800 mt-12 pt-8 text-center text-xs uppercase tracking-widest font-bold">
                &copy; 2025 Universidad Señor de Sipán - Todos los derechos reservados.
            </div>
        </div>
    </footer>

    <!-- ==============================================
         COMPONENTES FLOTANTES (MODALES & BOT)
    =============================================== -->

    <!-- BOT ASISTENTE -->
    <div id="bot-window" class="fixed bottom-24 right-6 w-80 bg-white border border-clinic-200 rounded-2xl shadow-2xl hidden z-50 flex flex-col h-[480px] overflow-hidden transition-all origin-bottom-right">
        <div class="bg-brand-primary p-4 text-white flex justify-between items-center shadow-md relative z-10">
            <div class="flex items-center gap-3">
                <i class="fas fa-robot text-xl"></i>
                <div>
                    <span class="font-bold text-sm block">Neuro-Assistant</span>
                    <span class="text-[10px] opacity-90 font-mono">En línea • Soporte</span>
                </div>
            </div>
            <button onclick="toggleBot()" class="hover:text-clinic-200 transition"><i class="fas fa-times"></i></button>
        </div>
        <div class="flex-1 p-4 bg-clinic-50 overflow-y-auto space-y-4" id="chat-content">
            <div class="flex gap-3">
                <div class="w-8 h-8 rounded-full bg-brand-primary flex-shrink-0 flex items-center justify-center text-white text-xs shadow-sm"><i class="fas fa-robot"></i></div>
                <div class="bg-white p-3 rounded-2xl rounded-tl-none shadow-sm text-xs text-clinic-600 border border-clinic-100">
                    Hola. Soy la IA del proyecto. Tengo acceso a toda la tesis. ¿Qué deseas saber sobre el proyecto?
                </div>
            </div>
        </div>
        <div class="p-3 bg-white border-t border-clinic-100 grid grid-cols-2 gap-2">
            <button onclick="botReply('problema')" class="text-[10px] bg-clinic-50 hover:bg-brand-primary hover:text-white text-clinic-600 py-3 rounded-lg transition font-bold border border-clinic-100">Problema</button>
            <button onclick="botReply('solucion')" class="text-[10px] bg-clinic-50 hover:bg-state-success hover:text-white text-clinic-600 py-3 rounded-lg transition font-bold border border-clinic-100">Solución</button>
            <button onclick="botReply('signos')" class="text-[10px] bg-clinic-50 hover:bg-state-danger hover:text-white text-clinic-600 py-3 rounded-lg transition font-bold border border-clinic-100">Signos Alarma</button>
            <button onclick="botReply('autores')" class="text-[10px] bg-clinic-50 hover:bg-brand-dark hover:text-white text-clinic-600 py-3 rounded-lg transition font-bold border border-clinic-100">Equipo</button>
        </div>
    </div>

    <!-- MODAL DETALLE ACTIVIDAD GIGANTE -->
    <div id="activity-modal" class="fixed inset-0 z-[100] hidden flex items-center justify-center p-4">
        <div class="absolute inset-0 modal-overlay" onclick="closeModal()"></div>
        <div class="relative w-full max-w-6xl bg-white rounded-[32px] shadow-2xl overflow-hidden flex flex-col md:flex-row max-h-[95vh] modal-body">
            <!-- Imagen Lateral -->
            <div class="md:w-4/12 relative bg-clinic-900 hidden md:block">
                <img id="m-img" src="" class="absolute inset-0 w-full h-full object-cover opacity-80">
                <div class="absolute inset-0 bg-gradient-to-t from-brand-primary/90 to-transparent flex flex-col justify-end p-10">
                    <i id="m-icon" class="text-6xl text-white drop-shadow-lg mb-6"></i>
                    <h3 id="m-title-overlay" class="text-2xl font-bold text-white leading-tight font-header"></h3>
                </div>
            </div>
            <!-- Contenido Scrollable -->
            <div class="md:w-8/12 p-12 overflow-y-auto">
                <button onclick="closeModal()" class="absolute top-6 right-6 text-slate-400 hover:text-alert-red transition bg-clinic-50 w-12 h-12 rounded-full flex items-center justify-center hover:bg-red-50"><i class="fas fa-times text-xl"></i></button>
                
                <span id="m-tag" class="inline-block px-4 py-1.5 rounded-full bg-clinic-100 text-clinic-700 text-xs font-black uppercase tracking-widest mb-8 border border-clinic-200"></span>
                <h2 id="m-title" class="text-3xl font-header font-black text-clinic-900 mb-8 leading-tight md:hidden"></h2>
                
                <div class="space-y-10">
                    <div>
                        <h4 class="font-bold text-clinic-900 mb-4 border-l-4 border-clinic-300 pl-4 text-lg">Descripción Detallada</h4>
                        <p id="m-desc" class="text-base text-clinic-600 text-justify-medical leading-loose"></p>
                    </div>
                    <div class="bg-clinic-50 p-8 rounded-3xl border border-clinic-100 shadow-inner">
                        <h4 class="font-bold text-clinic-600 text-xs uppercase tracking-widest mb-4 flex items-center gap-2"><i class="fas fa-brain mr-2"></i> Fundamentación Neurocientífica</h4>
                        <p id="m-neuro" class="text-sm text-clinic-700 italic text-justify-medical leading-relaxed"></p>
                    </div>
                    <div>
                        <h4 class="font-bold text-clinic-900 mb-3 border-l-4 border-brand-dark pl-3">Estrategia de Implementación</h4>
                        <p id="m-imp" class="text-sm text-clinic-600 text-justify-medical leading-relaxed"></p>
                    </div>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                        <div>
                            <h4 class="font-bold text-clinic-900 mb-2 border-l-4 border-clinic-300 pl-3">Determinante Social</h4>
                            <p id="m-dss" class="text-xs text-clinic-500 text-justify-medical leading-relaxed"></p>
                        </div>
                        <div>
                            <h4 class="font-bold text-clinic-900 mb-2 border-l-4 border-alert-green pl-3">Consejo Práctico</h4>
                            <p id="m-strat" class="text-xs text-clinic-500 text-justify-medical leading-relaxed font-medium bg-green-50 p-2 rounded-lg"></p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- JAVASCRIPT LOGIC -->
    <script>
        // --- 1. INICIALIZACIÓN ---
        AOS.init({ duration: 1000, once: true, offset: 120 });

        // --- 2. GRÁFICO REALIDAD (Chart.js) ---
        const ctx = document.getElementById('chartRealidad').getContext('2d');
        new Chart(ctx, {
            type: 'bar',
            data: {
                labels: ['Diagnóstico Tardío', 'Tiempo >60 Días', 'Downtime Equipos', 'Déficit Personal'],
                datasets: [{
                    label: 'Nivel Crítico (%)',
                    data: [64, 85, 40, 70],
                    backgroundColor: ['#EF4444', '#F59E0B', '#00B4D8', '#6366F1'],
                    borderRadius: 6,
                    barThickness: 40
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: { legend: { display: false } },
                scales: { 
                    y: { beginAtZero: true, grid: { color: '#F1F5F9' }, ticks: { font: { family: 'Lato' } } }, 
                    x: { grid: { display: false }, ticks: { font: { family: 'Montserrat', weight: 'bold' } } } 
                }
            }
        });

        // --- 3. DICOM VIEWER LINEAL (Lógica de Escáner Vertical) ---
        function updateDicomScan(e) {
            const viewer = document.getElementById('dicomViewer');
            const revealLayer = document.getElementById('dicomReveal');
            const scanBar = document.getElementById('scanBar');
            const sliceInfo = document.getElementById('slicePos');
            const alert = document.getElementById('tumorAlert');
            
            const rect = viewer.getBoundingClientRect();
            const y = e.clientY - rect.top; // Posición Y del mouse dentro del div
            
            // Asegurar límites
            let percent = (y / rect.height) * 100;
            if (percent < 0) percent = 0;
            if (percent > 100) percent = 100;

            // Mover la barra de escaneo
            scanBar.style.top = percent + '%';

            // Lógica de "Barrido": La capa de patología se muestra SOLO ARRIBA de la barra
            // Usamos clip-path inset: top right bottom left
            // Mostramos la imagen "revelada" desde arriba hasta la posición del mouse
            revealLayer.style.clipPath = `polygon(0 0, 100% 0, 100% ${percent}%, 0 ${percent}%)`;

            // Actualizar datos HUD
            sliceInfo.innerText = Math.round(percent * 1.5); // Simular mm

            // Detección de tumor (Si la barra pasa por el área del tumor: 30% a 50%)
            if (percent > 35 && percent < 50) {
                alert.classList.remove('hidden');
                alert.classList.add('block');
            } else {
                alert.classList.add('hidden');
                alert.classList.remove('block');
            }
        }
        function resetDicom() {
            document.getElementById('scanBar').style.top = '0%';
            document.getElementById('dicomReveal').style.clipPath = `polygon(0 0, 100% 0, 100% 0%, 0 0%)`;
            document.getElementById('tumorAlert').classList.add('hidden');
        }

        // --- 4. TABS LOGIC ---
        function openTab(id, btn) {
            // Ocultar todos
            document.querySelectorAll('.tab-content').forEach(el => el.style.display = 'none');
            // Mostrar target
            const selected = document.getElementById('tab-' + id);
            selected.style.display = 'block';
            selected.classList.add('animate-fade-in');
            
            // Estilos botones
            document.querySelectorAll('button[onclick^="openTab"]').forEach(b => {
                b.className = "px-6 py-2 rounded-full text-xs font-bold uppercase tracking-wide transition text-clinic-600 hover:bg-clinic-100";
            });
            btn.className = "px-6 py-2 rounded-full text-xs font-bold uppercase tracking-wide transition bg-brand-primary text-white shadow-md";
        }

        // --- 5. DATA COMPLETA ACTIVIDADES (EXPANDIDA) ---
        const activities = [
            { 
                id: 1, title: "Cine-Neuro: Conexión Visual", cat: "EDUCACIÓN", icon: "fas fa-film", 
                img: "https://images.unsplash.com/photo-1536440136628-849c177e76a1", 
                desc: "Esta actividad consiste en la proyección itinerante de películas y documentales seleccionados que abordan temáticas sobre el funcionamiento del cerebro y la superación de enfermedades neurológicas. Se realizará en plazas públicas y centros comunales de Lambayeque para alcanzar a la mayor cantidad de población posible. El objetivo es utilizar la narrativa visual para humanizar la enfermedad y reducir el estigma asociado a los trastornos neurológicos.", 
                neuro: "Activa las neuronas espejo, facilitando la empatía y el aprendizaje a través de la observación de experiencias ajenas. Reduce la ansiedad anticipatoria ante lo desconocido mediante la familiarización con el entorno médico.", 
                dss: "Acceso a Información Sanitaria y Educación.", 
                imp: "Implementación: Se realizarán funciones quincenales en auditorios municipales y plazas. Dinámica: Cine-foro con preguntas y respuestas guiadas por psicólogos y tecnólogos médicos. Meta: Alcanzar a 500 familias en el primer trimestre.",
                strat: "Consejo: Participa activamente en los debates post-función. Preguntar ayuda a desmitificar los miedos sobre los equipos de resonancia magnética." 
            },
            { 
                id: 2, title: "Ruta del Sabor Cerebral", cat: "NUTRICIÓN", icon: "fas fa-utensils", 
                img: "https://images.unsplash.com/photo-1546069901-ba9599a7e63c", 
                desc: "Una feria gastronómica innovadora que utiliza insumos locales de la región Lambayeque (como el pescado de carne oscura, el loche y frutas nativas) para enseñar recetas neuro-protectoras. Se realizarán demostraciones de cocina en vivo ('show-cooking') donde chefs locales y nutricionistas explicarán cómo preparar platos económicos y deliciosos que potencien la salud cerebral.", 
                neuro: "El eje intestino-cerebro es clave para la salud mental. Nutrientes como el Omega-3 y antioxidantes protegen la mielina y reducen la neuroinflamación crónica, creando un ambiente hostil para el desarrollo tumoral.", 
                dss: "Seguridad Alimentaria y Cultura Local.", 
                imp: "Implementación: Stands de demostración con chefs locales y nutricionistas. Entrega de recetarios 'Cerebro Fuerte' con costos bajos. Degustación de platos ricos en hierro y antioxidantes.",
                strat: "Consejo: Incluye pescado de carne oscura (Bonito, Jurel) al menos 3 veces por semana en tu dieta para asegurar la ingesta de ácidos grasos esenciales." 
            },
            { 
                id: 3, title: "Máquina VR", cat: "TECNOLOGÍA", icon: "fas fa-vr-cardboard", 
                img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSrCVtgVciLJXbKfUQ52D6QF6rWNyyHnZd40g&s", 
                desc: "Implementación de estaciones de Realidad Virtual (VR) en colegios y ferias de salud para simular la experiencia de entrar a un resonador magnético. Los niños y adultos podrán usar visores para vivir el procedimiento de forma lúdica, escuchando los sonidos reales del equipo en un entorno controlado y seguro.", 
                neuro: "La exposición virtual controlada reduce la actividad de la amígdala (centro del miedo) frente al encierro, disminuyendo el 'scanxiety' o ansiedad por el escáner.", 
                dss: "Tecnofobia y Barreras Culturales.", 
                imp: "Implementación: Visitas a colegios con kits de VR de cartón. Los niños 'viajan' al interior del cerebro como astronautas. Se mide el pulso antes y después para mostrar la calma.",
                strat: "Consejo: Si tienes claustrofobia, usa la app de simulación en casa varias veces antes de tu cita médica para habituar a tu cerebro a los sonidos." 
            },
            { 
                id: 4, title: "Semáforo del Dolor", cat: "PREVENCIÓN", icon: "fas fa-traffic-light", 
                img: "https://clinicarozalen.com/wp-content/uploads/2024/06/migrana-imagen.png", 
                desc: "Campaña visual masiva que utiliza tarjetas magnéticas para el hogar clasificando los dolores de cabeza por colores: Verde (Leve/Tensional), Amarillo (Moderado/Migraña) y Rojo (Grave/Tumoral). El objetivo es educar a las familias para que puedan diferenciar una cefalea común de un signo de alarma.", 
                neuro: "Entrenamiento en el reconocimiento de patrones nociceptivos para diferenciar cefaleas benignas de signos neurológicos graves de hipertensión endocraneana.", 
                dss: "Acceso Oportuno a Servicios de Urgencia.", 
                imp: "Implementación: Distribución casa por casa en zonas de riesgo. Capacitación a líderes vecinales para replicar la información. Uso de stickers en postas médicas.",
                strat: "ALERTA ROJA: Si el dolor de cabeza te despierta en la noche o viene acompañado de vómitos explosivos sin náusea, acude inmediatamente a urgencias." 
            },
            { 
                id: 5, title: "Olimpiadas de la Mente", cat: "COGNICIÓN", icon: "fas fa-chess", 
                img: "https://images.unsplash.com/photo-1529699211952-734e80c4d42b", 
                desc: "Organización de concursos comunitarios e interescolares de ajedrez, memoria, rompecabezas y juegos de estrategia. Estas 'olimpiadas' buscan promover la gimnasia mental como un hábito de vida saludable, similar al ejercicio físico.", 
                neuro: "La estimulación cognitiva constante fortalece la 'Reserva Cognitiva' y las funciones ejecutivas (memoria de trabajo, planificación, atención), protegiendo al cerebro contra el deterioro.", 
                dss: "Educación y Desarrollo Cognitivo Infantil.", 
                imp: "Implementación: Torneos fines de semana en parques zonales. Categorías intergeneracionales (abuelos vs nietos). Premios: Libros y kits de salud.",
                strat: "Consejo: Aprender una habilidad nueva (idioma, instrumento, juego) crea nuevas sinapsis. Mantén tu cerebro desafiado constantemente." 
            },
            { 
                id: 6, title: "Sueño Reparador", cat: "SALUD", icon: "fas fa-bed", 
                img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQn1HohnEStUn4f1X2NRqdd7g6yP9wS5pnK_w&s", 
                desc: "Talleres prácticos sobre higiene del sueño y desconexión digital para prevenir enfermedades neurodegenerativas. Se explicará la importancia de dormir en oscuridad total y sin dispositivos electrónicos para permitir la correcta secreción de melatonina.", 
                neuro: "El sistema glinfático se activa durante el sueño profundo para limpiar toxinas y desechos metabólicos (como beta-amiloide) acumulados en el cerebro durante el día.", 
                dss: "Condiciones de Vivienda y Estrés Laboral.", 
                imp: "Implementación: Charlas en empresas y sindicatos. Entrega de antifaces para dormir. Reto de 'Apagón Digital' 1 hora antes de dormir.",
                strat: "Consejo: Establece una rutina de sueño estricta. Deja las pantallas 1 hora antes de dormir y asegúrate que tu habitación esté totalmente oscura." 
            },
            { 
                id: 7, title: "Arte-Neuro: Expresión", cat: "EMOCIÓN", icon: "fas fa-palette", 
                img: "https://images.unsplash.com/photo-1460661419201-fd4cecdf8a8b", 
                desc: "Talleres de pintura, música y escultura dirigidos a pacientes oncológicos y sus familias en las salas de espera del hospital. El arte sirve como una vía de escape y expresión para emociones complejas que a veces no se pueden verbalizar.", 
                neuro: "El arte estimula redes neuronales distintas al lenguaje, reduce el cortisol y activa el sistema límbico para procesar emociones complejas y reducir el estrés.", 
                dss: "Salud Mental y Apoyo Emocional.", 
                imp: "Implementación: Espacios de arte en el Hospital Regional con voluntarios locales. Exposiciones de las obras de los pacientes para validar su experiencia.",
                strat: "Consejo: Lleva un cuaderno de dibujo o escucha música relajante mientras esperas tu turno. La expresión creativa reduce la tensión arterial." 
            },
            { 
                id: 8, title: "Mitos y Verdades", cat: "CIENCIA", icon: "fas fa-bullhorn", 
                img: "https://images.unsplash.com/photo-1532938911079-1b06ac7ceec7", 
                desc: "Charlas interactivas tipo 'Cazadores de Mitos' en centros de madres y asociaciones vecinales para desmentir creencias erróneas sobre la radiación y la salud. Se explicará la diferencia entre radiación ionizante y no ionizante.", 
                neuro: "Educación científica para diferenciar riesgos reales de imaginarios (radiofobia), combatiendo sesgos cognitivos que retrasan el diagnóstico oportuno.", 
                dss: "Desinformación y Creencias Erróneas.", 
                imp: "Implementación: Uso de infografías gigantes. Demostraciones físicas con imanes para explicar la Resonancia Magnética. Sesiones de preguntas anónimas.",
                strat: "Dato Clave: La resonancia magnética NO utiliza radiación ionizante (rayos X), funciona con imanes y ondas de radio, siendo segura." 
            },
            { 
                id: 9, title: "Neuro-Dance", cat: "MOVIMIENTO", icon: "fas fa-running", 
                img: "https://images.unsplash.com/photo-1518611012118-696072aa579a", 
                desc: "Sesiones de baile aeróbico y ejercicios en parques públicos que incorporan retos de coordinación motora y 'dual-tasking' (moverse y pensar a la vez). El ejercicio es un factor protector potente.", 
                neuro: "El ejercicio aeróbico estimula la liberación de BDNF, promoviendo la neurogénesis en el hipocampo (memoria) y mejorando la vascularización cerebral.", 
                dss: "Estilos de Vida Sedentarios.", 
                imp: "Implementación: Clases gratuitas en parques zonales. Uso de música tradicional local. Retos de coordinación motora fina y gruesa.",
                strat: "Consejo: Bailar es uno de los mejores ejercicios para el cerebro porque requiere coordinación, ritmo y memoria espacial simultáneamente." 
            },
            { 
                id: 10, title: "Móvil-Brain", cat: "ACCESO", icon: "fas fa-ambulance", 
                img: "https://images.unsplash.com/photo-1631815589968-fdb09a223b1e", 
                desc: "Una unidad móvil de salud que visita zonas rurales y periféricas de Lambayeque realizando tamizajes neurológicos básicos. Lleva profesionales capacitados para realizar exámenes físicos y gestión de citas.", 
                neuro: "Acercar la evaluación básica permite la detección de signos sutiles (focales) antes de que sean graves e irreversibles, reduciendo la morbilidad.", 
                dss: "Inequidad Geográfica y Transporte.", 
                imp: "Implementación: Cronograma de visitas a Incahuasi, Cañaris y Olmos. Equipo multidisciplinario a bordo. Referencia directa al Hospital Regional.",
                strat: "Consejo: Acude a la unidad móvil ante cualquier debilidad muscular repentina, adormecimiento o cambio de conducta persistente." 
            }
        ];

        // --- 6. RENDERIZADO GALERÍA ---
        const grid = document.getElementById('activitiesGrid');
        activities.forEach(act => {
            grid.innerHTML += `
                <div class="activity-card group cursor-pointer h-full flex flex-col" onclick="openDetail(${act.id})">
                    <span class="card-number" style="position: absolute; top: -10px; right: 10px; font-size: 4rem; font-weight: 900; color: #f1f5f9; z-index: 0;">${act.id < 10 ? '0'+act.id : act.id}</span>
                    <div class="h-48 overflow-hidden relative z-10 rounded-t-xl mx-4 mt-4">
                        <img src="${act.img}" class="w-full h-full object-cover transition duration-700 group-hover:scale-110 rounded-xl">
                        <div class="absolute inset-0 bg-gradient-to-t from-black/70 to-transparent opacity-80"></div>
                        <div class="absolute bottom-3 left-3 text-white">
                            <span class="text-[10px] uppercase font-bold bg-brand-primary px-2 py-1 rounded shadow-sm">${act.cat}</span>
                        </div>
                    </div>
                    <div class="p-6 flex flex-col flex-grow z-10 relative">
                        <h3 class="font-bold text-slate-800 text-lg leading-tight mb-3 group-hover:text-brand-primary transition">${act.title}</h3>
                        <p class="text-xs text-slate-500 line-clamp-3 mb-4 flex-grow leading-relaxed">${act.desc}</p>
                        <div class="text-xs font-bold text-brand-dark flex items-center gap-2 border-t border-slate-100 pt-4 mt-auto group-hover:gap-3 transition-all">
                            Ver Detalles Completos <i class="fas fa-arrow-right"></i>
                        </div>
                    </div>
                </div>
            `;
        });

        // --- 7. MODALES Y TABS ---
        function openDetail(id) {
            const act = activities.find(x => x.id === id);
            document.getElementById('m-title').innerText = act.title;
            document.getElementById('m-title-overlay').innerText = act.title;
            document.getElementById('m-tag').innerText = act.cat;
            document.getElementById('m-desc').innerText = act.desc;
            document.getElementById('m-neuro').innerText = act.neuro;
            document.getElementById('m-dss').innerText = act.dss;
            document.getElementById('m-imp').innerText = act.imp;
            document.getElementById('m-strat').innerText = act.strat;
            document.getElementById('m-img').src = act.img;
            document.getElementById('m-icon').className = act.icon + " text-6xl text-white drop-shadow-lg mb-4";
            document.getElementById('activity-modal').classList.remove('hidden');
        }
        function closeModal() { document.getElementById('activity-modal').classList.add('hidden'); }

        // --- 8. LOGICA JUEGO NUTRICIÓN ---
        let selectedSlots = 0;
        function selectFood(element, isHealthy, name) {
            if (selectedSlots >= 3) return;
            const slot = document.getElementById(`slot${selectedSlots + 1}`);
            
            // Animación visual
            slot.innerHTML = `<div class="text-center"><span class="text-3xl">${element.querySelector('div').innerText}</span><p class="text-xs font-bold ${isHealthy ? 'text-state-success' : 'text-state-danger'}">${name}</p></div>`;
            slot.classList.add(isHealthy ? 'border-state-success' : 'border-state-danger', 'bg-white');
            
            selectedSlots++;
            updateFeedback();
        }

        function updateFeedback() {
            const feedback = document.getElementById('nutriFeedback');
            if (selectedSlots === 3) {
                feedback.innerText = "¡Lonchera Completa! Revisa si tus elecciones son neuro-protectoras.";
                feedback.className = "mt-6 font-bold text-sm h-6 text-brand-primary animate-pulse";
            }
        }

        function resetGame() {
            selectedSlots = 0;
            [1, 2, 3].forEach(i => {
                const slot = document.getElementById(`slot${i}`);
                slot.innerHTML = '';
                slot.className = 'lunchbox-slot';
            });
            document.getElementById('nutriFeedback').innerText = '';
        }

        // --- 9. BOT & BIOS ---
        function toggleBot() { document.getElementById('bot-window').classList.toggle('hidden'); }
        function toggleBio(id) { document.getElementById(id).classList.toggle('open'); }
        
        function botReply(type) {
            const feed = document.getElementById('chat-content');
            let msg = "";
            if (type === 'problema') msg = "El problema central es la centralización y el 'downtime' de equipos. Los pacientes esperan >60 días en el sector público, llegando al diagnóstico en estadios tardíos (64%).";
            if (type === 'solucion') msg = "Nuestra solución es el 'Programa Estratégico de Diagnóstico': Protocolos rápidos, gestión de mantenimiento (GCEB) y capacitación de tecnólogos.";
            if (type === 'signos') msg = "⚠️ SIGNOS DE ALARMA: Dolor de cabeza que despierta en la noche, vómitos explosivos sin náusea, cambios visuales y convulsiones de inicio reciente.";
            if (type === 'autores') msg = "El equipo investigador está conformado por: Gerardo Becerra, Mashory Chimoven, Isaac Delgado y Frank Quintana.";

            const userMsg = document.createElement('div');
            userMsg.className = "flex justify-end";
            userMsg.innerHTML = `<div class="bg-brand-primary text-white px-4 py-2 rounded-2xl rounded-tr-none text-xs font-bold uppercase shadow-sm border border-brand-secondary">${type}</div>`;
            feed.appendChild(userMsg);

            setTimeout(() => {
                const botMsg = document.createElement('div');
                botMsg.className = "flex gap-3";
                botMsg.innerHTML = `
                    <div class="w-8 h-8 rounded-full bg-brand-primary flex-shrink-0 flex items-center justify-center text-white text-xs"><i class="fas fa-robot"></i></div>
                    <div class="bg-white p-4 rounded-2xl rounded-tl-none shadow-md text-xs text-slate-600 border border-slate-100 leading-relaxed">${msg}</div>
                `;
                feed.appendChild(botMsg);
                feed.scrollTop = feed.scrollHeight;
            }, 400);
        }

        // Init
        AOS.init({ duration: 800, once: true });
    </script>
</body>
</html>
