<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lyftiv – L'application intelligente pour vos entraînements</title>
    
    <meta name="description" content="Lyftiv est l'application tout-en-un pour suivre vos séances, analyser vos performances, utiliser des calculateurs intelligents et créer vos propres programmes. Entièrement gratuit.">
    <meta property="og:title" content="Lyftiv – Votre partenaire de musculation intelligent">
    <meta property="og:description" content="Arrêtez de deviner. Progressez avec des outils puissants, des calculateurs précis et une interface intuitive.">
    <meta property="og:type" content="website">
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">

    <style>
        :root {
            --color-blue-base: 220 60% 50%;
            --color-background-gradient-start: hsl(200, 60%, 95%);
            --color-background-gradient-end: hsl(220, 70%, 98%);
            --color-surface-default: hsla(0, 0%, 100%, 0.95);
            --color-text-header: hsl(220, 20%, 20%);
            --color-text-subheader: hsl(220, 10%, 45%);
            --color-primary-default: hsl(var(--color-blue-base));
            --color-primary-gradient-start: hsl(220, 60%, 70%);
            --color-primary-gradient-end: hsl(240, 70%, 75%);
            --btn-primary-bg: linear-gradient(135deg, var(--color-primary-gradient-start), var(--color-primary-gradient-end));
            --shadow-md: hsla(220, 20%, 20%, 0.08);
            --shadow-lg: hsla(220, 20%, 20%, 0.15);
        }

        body { 
            font-family: 'Inter', sans-serif; 
            background-color: #F8F9FA; 
            color: var(--color-text-subheader);
        }
        
        .logo-text {
            font-weight: 800;
            color: var(--color-text-header);
        }

        .gradient-text { 
            background: var(--btn-primary-bg);
            -webkit-background-clip: text; 
            -webkit-text-fill-color: transparent; 
            background-clip: text; 
        }

        .floating { animation: float 6s ease-in-out infinite; }
        @keyframes float { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-10px)} }
        
        .slide-up { opacity: 0; transform: translateY(30px); transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94); }
        .slide-up.visible { opacity: 1; transform: translateY(0); }
        
        .pulse-glow { 
            animation: pulseGlow 4s ease-in-out infinite alternate; 
        }
        @keyframes pulseGlow { 
            from{box-shadow:0 0 20px hsla(var(--color-blue-base), .2)} 
            to{box-shadow:0 0 40px hsla(var(--color-blue-base), .4)} 
        }
        
        .blob { position: absolute; border-radius: 50%; filter: blur(80px); animation: blob 12s ease-in-out infinite; opacity: 0.3; }
        .blob:nth-child(1) { top: 10%; left: 10%; width: 350px; height: 350px; background: var(--color-primary-gradient-start); animation-delay: 0s; }
        .blob:nth-child(2) { bottom: 10%; right: 10%; width: 250px; height: 250px; background: var(--color-primary-gradient-end); animation-delay: 3s; }
        @keyframes blob { 0%,100%{transform:translate(0,0) scale(1)} 33%{transform:translate(30px,-50px) scale(1.05)} 66%{transform:translate(-20px,20px) scale(.95)} }
        
        .magnetic-hover { transition: all 0.3s ease; }
        .magnetic-hover:hover { transform: translateY(-6px) scale(1.02); box-shadow: 0 15px 30px rgba(0,0,0,0.08); }
        
        .scroll-progress { position: fixed; top: 0; left: 0; width: 0%; height: 4px; background: var(--btn-primary-bg); z-index: 10000; transition: width 0.1s ease-out; }
        
        .stagger-item { opacity: 0; transform: translateX(-20px); transition: all 0.5s ease-out; }
        .stagger-item.visible { opacity: 1; transform: translateX(0); }
        
        .btn-primary {
            background: var(--btn-primary-bg);
            color: white;
            transition: all 0.3s ease;
        }
        .btn-primary:hover {
            box-shadow: 0 4px 15px hsla(var(--color-blue-base), 0.4);
            transform: translateY(-2px);
        }
        .text-accent { color: var(--color-primary-default); }

        .mockup-window {
            border: 1px solid #e5e7eb;
            border-radius: 0.75rem;
            background-color: white;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            overflow: hidden;
        }
        .mockup-window-header {
            height: 2rem;
            display: flex;
            align-items: center;
            padding-left: 0.75rem;
            gap: 0.5rem;
            background-color: #f3f4f6;
            border-bottom: 1px solid #e5e7eb;
        }
        .mockup-window-dot {
            width: 0.75rem;
            height: 0.75rem;
            border-radius: 9999px;
        }

        @media (prefers-reduced-motion: reduce) {
            *, ::before, ::after { animation-duration: 0.01ms!important; animation-iteration-count: 1!important; transition-duration: 0.01ms!important; scroll-behavior: auto!important; }
        }
    </style>
</head>
<body class="antialiased">
    <div class="scroll-progress" id="scrollProgress"></div>

    <header class="bg-white/70 backdrop-blur-lg fixed top-0 left-0 right-0 z-50 border-b border-gray-200/50">
        <div class="container mx-auto px-6 py-3 flex justify-between items-center">
            <div class="flex items-center gap-2">
                <svg class="w-8 h-8" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
                    <defs><linearGradient id="g" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" stop-color="hsl(200, 80%, 85%)" /><stop offset="100%" stop-color="hsl(260, 60%, 85%)" /></linearGradient></defs>
                    <rect x="0" y="0" width="100" height="100" rx="20" ry="20" fill="url(#g)"/>
                    <path d="M 15 50 C 15 35 30 30 50 30 C 70 30 85 35 85 50 C 85 65 70 70 50 70 C 30 70 15 65 15 50 Z M 25 50 L 75 50 M 25 35 L 25 65 M 75 35 L 75 65" stroke="hsl(220, 60%, 55%)" stroke-width="3.5" fill="none" stroke-linecap="round"/>
                    <circle cx="25" cy="50" r="14" stroke="hsl(220, 60%, 55%)" stroke-width="2" fill="none"/><circle cx="25" cy="50" r="10" stroke="hsl(220, 60%, 55%)" stroke-width="2" fill="none"/><circle cx="25" cy="50" r="6" stroke="hsl(220, 60%, 55%)" stroke-width="2" fill="none"/>
                    <circle cx="75" cy="50" r="14" stroke="hsl(220, 60%, 55%)" stroke-width="2" fill="none"/><circle cx="75" cy="50" r="10" stroke="hsl(220, 60%, 55%)" stroke-width="2" fill="none"/><circle cx="75" cy="50" r="6" stroke="hsl(220, 60%, 55%)" stroke-width="2" fill="none"/>
                    <rect x="35" y="48.5" width="30" height="3" rx="1.5" ry="1.5" fill="white"/>
                </svg>
                <h1 class="text-3xl logo-text">Lyftiv</h1>
            </div>
            
            <nav class="hidden md:flex space-x-8 items-center">
                <a href="#features" class="text-gray-600 hover:text-accent font-medium">Fonctionnalités</a>
                <a href="#gallery" class="text-gray-600 hover:text-accent font-medium">Aperçus</a>
                <a href="#comparison" class="text-gray-600 hover:text-accent font-medium">Pourquoi nous ?</a>
                <a href="#start" class="text-gray-600 hover:text-accent font-medium">Commencer</a>
            </nav>
            <a href="index.html" target="_blank" class="hidden md:block px-6 py-2 btn-primary text-white font-semibold rounded-lg shadow-md hover:shadow-lg transition-all duration-300 transform hover:scale-105">
                Lancer l'app
            </a>
            <button id="mobile-menu-button" class="md:hidden p-2 rounded-md text-gray-700 hover:bg-gray-200">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path></svg>
            </button>
        </div>
        <div id="mobile-menu" class="hidden md:hidden px-6 pb-4">
             <a href="#features" class="block py-2 text-gray-700 font-semibold">Fonctionnalités</a>
             <a href="#gallery" class="block py-2 text-gray-700 font-semibold">Aperçus</a>
             <a href="#comparison" class="block py-2 text-gray-700 font-semibold">Pourquoi nous ?</a>
             <a href="#start" class="block py-2 text-gray-700 font-semibold">Commencer</a>
             <a href="index.html" target="_blank" class="block mt-4 w-full text-center py-3 btn-primary text-white font-semibold rounded-lg shadow-lg">Lancer l'app</a>
        </div>
    </header>

    <main>
        <section class="pt-32 pb-20 text-center relative overflow-hidden flex items-center min-h-[90vh]" style="background: linear-gradient(135deg, var(--color-background-gradient-start) 0%, var(--color-background-gradient-end) 100%);">
            <div class="absolute inset-0 z-0">
                <div class="blob"></div>
                <div class="blob"></div>
            </div>
            
            <div class="container mx-auto px-6 relative z-10">
                <div class="grid lg:grid-cols-2 gap-12 items-center">
                    <div class="text-center lg:text-left">
                        <h2 class="text-4xl md:text-5xl font-black text-gray-900 leading-tight slide-up">
                            Votre entraînement,
                            <br>
                            <span class="gradient-text" style="animation-delay: 0.2s;">enfin maîtrisé.</span>
                        </h2>
                        <p class="mt-6 text-lg md:text-xl text-gray-700 max-w-xl mx-auto lg:mx-0 slide-up" style="animation-delay: 0.3s;">
                            Plus qu'un simple carnet. Lyftiv analyse vos performances, vous guide avec des calculateurs intelligents et s'adapte à votre routine.
                        </p>
                        <div class="mt-10 flex flex-col sm:flex-row justify-center lg:justify-start items-center gap-4 slide-up" style="animation-delay: 0.5s;">
                            <a href="index.html" target="_blank" class="w-full sm:w-auto btn-primary text-white font-bold rounded-lg shadow-xl hover:shadow-2xl transition-all duration-300 transform hover:scale-105 px-8 py-4">
                                Lancer l'application
                            </a>
                        </div>
                         <p class="mt-4 text-sm text-gray-600 slide-up" style="animation-delay: 0.6s;">
                            <span class="font-bold">100% gratuit.</span> Lancez-vous sans attendre.
                        </p>
                    </div>

                    <!-- App Mockup -->
                    <div class="slide-up floating" style="animation-delay: 0.8s;">
                        <div class="relative mx-auto border-gray-800 bg-gray-800 border-[12px] rounded-[2.2rem] h-[580px] w-[290px] pulse-glow">
                            <div class="h-[30px] w-[3px] bg-gray-800 absolute -left-[15px] top-[70px] rounded-l-lg"></div>
                            <div class="h-[44px] w-[3px] bg-gray-800 absolute -left-[15px] top-[120px] rounded-l-lg"></div>
                            <div class="h-[60px] w-[3px] bg-gray-800 absolute -right-[15px] top-[140px] rounded-r-lg"></div>
                            <div class="rounded-[1.8rem] overflow-hidden w-full h-full bg-gray-50">
                                <div class="p-4 bg-white/50">
                                    <div class="flex items-center justify-center gap-2 mb-4">
                                        <svg class="w-8 h-8" viewBox="0 0 100 100"><use href="#g"/></svg>
                                        <span class="text-2xl font-black text-gray-800">Lyftiv</span>
                                    </div>
                                    <h3 class="text-center text-gray-700 font-semibold">Choisissez votre séance</h3>
                                </div>
                                <div class="p-3 space-y-2">
                                    <div class="p-4 rounded-xl bg-white shadow-md text-center">
                                        <span class="text-3xl">🏋️‍♂️</span>
                                        <h4 class="font-bold text-gray-800 mt-1">Haut du corps (force)</h4>
                                        <p class="text-xs text-gray-500">9 exercices</p>
                                    </div>
                                    <div class="p-4 rounded-xl bg-white shadow-md text-center">
                                        <span class="text-3xl">🦵</span>
                                        <h4 class="font-bold text-gray-800 mt-1">Bas du corps (force)</h4>
                                        <p class="text-xs text-gray-500">5 exercices</p>
                                    </div>
                                    <div class="p-4 rounded-xl bg-white/80 shadow-sm text-center border-2 border-dashed border-gray-300">
                                        <span class="text-3xl text-blue-500">➕</span>
                                        <h4 class="font-bold text-blue-600 mt-1">Créer une séance</h4>
                                        <p class="text-xs text-gray-500">Bâtissez votre entraînement</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="features" class="py-20 bg-white">
            <div class="container mx-auto px-6">
                <div class="text-center mb-16 slide-up">
                    <h3 class="text-3xl md:text-4xl font-bold text-gray-900">La salle de sport, réinventée.</h3>
                    <p class="mt-4 text-lg text-gray-700 max-w-2xl mx-auto">Des outils puissants, conçus pour être incroyablement simples.</p>
                </div>
                <div class="grid md:grid-cols-3 gap-8">
                    <div class="magnetic-hover bg-blue-50 p-8 rounded-2xl shadow-lg slide-up">
                        <div class="w-12 h-12 btn-primary rounded-lg flex items-center justify-center floating">
                             <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6" /></svg>
                        </div>
                        <h4 class="mt-6 text-xl font-bold text-accent">Visualisez vos progrès</h4>
                        <p class="mt-2 text-gray-600">Suivez le volume total soulevé, estimez votre 1RM et enchaînez les exercices. Lyftiv traduit vos efforts en victoires.</p>
                    </div>
                    <div class="magnetic-hover bg-indigo-50 p-8 rounded-2xl shadow-lg slide-up" style="animation-delay: 0.2s;">
                        <div class="w-12 h-12 btn-primary rounded-lg flex items-center justify-center floating" style="animation-delay: 0.3s;">
                           <i class="fas fa-calculator text-2xl text-white"></i>
                        </div>
                        <h4 class="mt-6 text-xl font-bold text-accent">Des calculateurs qui pensent pour vous</h4>
                        <p class="mt-2 text-gray-600">Calculez les poids pour vos objectifs (force, prise de muscle...) et déterminez quelles plaques charger sur la barre, sans prise de tête.</p>
                    </div>
                    <div class="magnetic-hover bg-purple-50 p-8 rounded-2xl shadow-lg slide-up" style="animation-delay: 0.4s;">
                        <div class="w-12 h-12 btn-primary rounded-lg flex items-center justify-center floating" style="animation-delay: 0.6s;">
                            <i class="fas fa-edit text-2xl text-white"></i>
                        </div>
                        <h4 class="mt-6 text-xl font-bold text-accent">Votre entraînement, vos règles</h4>
                        <p class="mt-2 text-gray-600">Créez vos propres séances de A à Z, ajoutez des exercices à la volée, et organisez votre routine comme vous l'entendez.</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- New Gallery Section -->
        <section id="gallery" class="py-20 bg-gray-50">
            <div class="container mx-auto px-6">
                <div class="text-center mb-16 slide-up">
                    <h3 class="text-3xl md:text-4xl font-bold text-gray-900">Un aperçu de l'application</h3>
                    <p class="mt-4 text-lg text-gray-700 max-w-2xl mx-auto">Découvrez l'interface claire et les outils à votre disposition.</p>
                </div>
                <div class="grid lg:grid-cols-3 gap-8 items-start">
                    <!-- Gallery Item 1: Workout View -->
                    <div class="slide-up">
                        <h4 class="text-xl font-bold text-center mb-4 text-gray-800">Suivi de séance simple</h4>
                        <div class="mockup-window">
                            <div class="mockup-window-header">
                                <div class="mockup-window-dot bg-red-400"></div><div class="mockup-window-dot bg-yellow-400"></div><div class="mockup-window-dot bg-green-400"></div>
                            </div>
                            <div class="p-4 bg-gray-100">
                                <div class="bg-white rounded-lg p-3 shadow-sm">
                                    <h5 class="font-bold text-gray-800">Développé couché barre</h5>
                                    <div class="mt-2 space-y-2">
                                        <div class="flex items-center gap-2 text-sm">
                                            <span class="font-semibold text-gray-500 w-12">Série 1:</span>
                                            <input type="text" value="80" class="w-16 text-center bg-green-100 text-green-800 font-semibold rounded p-1" disabled> <span class="text-gray-400">kg</span>
                                            <input type="text" value="8" class="w-16 text-center bg-green-100 text-green-800 font-semibold rounded p-1" disabled> <span class="text-gray-400">reps</span>
                                        </div>
                                        <div class="flex items-center gap-2 text-sm">
                                            <span class="font-semibold text-gray-500 w-12">Série 2:</span>
                                            <input type="text" placeholder="kg" class="w-16 text-center bg-white border rounded p-1"> <span class="text-gray-400">kg</span>
                                            <input type="text" placeholder="reps" class="w-16 text-center bg-white border rounded p-1"> <span class="text-gray-400">reps</span>
                                        </div>
                                    </div>
                                    <div class="mt-3 flex justify-between items-center text-xs text-gray-500">
                                        <span>1RM Est: <strong class="text-blue-600">102.5kg</strong></span>
                                        <span>Repos: <strong class="text-blue-600">2 min</strong></span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <!-- Gallery Item 2: Calculators -->
                    <div class="slide-up" style="animation-delay: 0.2s;">
                        <h4 class="text-xl font-bold text-center mb-4 text-gray-800">Calculateurs Intelligents</h4>
                        <div class="mockup-window">
                            <div class="mockup-window-header">
                                <div class="mockup-window-dot bg-red-400"></div><div class="mockup-window-dot bg-yellow-400"></div><div class="mockup-window-dot bg-green-400"></div>
                            </div>
                            <div class="p-4 bg-gray-100">
                                <h5 class="font-bold text-center text-gray-800 mb-2">Objectifs (1RM: 100kg)</h5>
                                <div class="space-y-2">
                                    <div class="bg-green-100 p-2 rounded-lg text-center">
                                        <p class="font-semibold text-green-800">Force (1-5 reps)</p>
                                        <p class="text-sm text-green-700">80 - 100 kg</p>
                                    </div>
                                    <div class="bg-blue-100 p-2 rounded-lg text-center">
                                        <p class="font-semibold text-blue-800">Prise de muscle (6-12 reps)</p>
                                        <p class="text-sm text-blue-700">60 - 80 kg</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <!-- Gallery Item 3: History -->
                    <div class="slide-up" style="animation-delay: 0.4s;">
                        <h4 class="text-xl font-bold text-center mb-4 text-gray-800">Historique Détaillé</h4>
                        <div class="mockup-window">
                            <div class="mockup-window-header">
                                <div class="mockup-window-dot bg-red-400"></div><div class="mockup-window-dot bg-yellow-400"></div><div class="mockup-window-dot bg-green-400"></div>
                            </div>
                            <div class="p-4 bg-gray-100">
                                <div class="space-y-2">
                                    <div class="bg-white p-2 rounded-lg shadow-sm flex justify-between items-center">
                                        <div>
                                            <p class="font-semibold text-sm text-gray-800">Haut du corps (force)</p>
                                            <p class="text-xs text-gray-500">04/08/2025 - 45:12</p>
                                        </div>
                                        <i class="fas fa-chevron-right text-gray-400"></i>
                                    </div>
                                    <div class="bg-white p-2 rounded-lg shadow-sm flex justify-between items-center">
                                        <div>
                                            <p class="font-semibold text-sm text-gray-800">Bas du corps (prise de muscle)</p>
                                            <p class="text-xs text-gray-500">02/08/2025 - 55:30</p>
                                        </div>
                                        <i class="fas fa-chevron-right text-gray-400"></i>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="social-proof" class="py-20 bg-white">
            <div class="container mx-auto px-6">
                 <div class="text-center mb-16 slide-up">
                    <h3 class="text-3xl md:text-4xl font-bold text-gray-900">Ils ont arrêté de deviner.</h3>
                    <p class="mt-4 text-lg text-gray-700 max-w-2xl mx-auto">Découvrez pourquoi nos utilisateurs nous adorent.</p>
                </div>
                <div class="grid md:grid-cols-3 gap-8">
                    <div class="magnetic-hover bg-white p-8 rounded-2xl shadow-xl border border-gray-200 slide-up">
                        <img src="https://placehold.co/80x80/7F9CF5/ffffff?text=A" alt="Avatar d'un utilisateur" class="w-20 h-20 rounded-full mx-auto mb-4">
                        <p class="text-gray-600 italic">"Enfin une app qui comprend ce que veulent les puristes. Les stats sont précises, l'interface est rapide et je peux créer n'importe quelle séance. Le calculateur de plaques est un bonus génial!"</p>
                        <p class="mt-4 font-bold text-accent">- Alex R., Powerlifter</p>
                    </div>
                     <div class="magnetic-hover bg-white p-8 rounded-2xl shadow-xl border border-gray-200 slide-up" style="animation-delay: 0.2s;">
                        <img src="https://placehold.co/80x80/A3BFFA/ffffff?text=S" alt="Avatar d'une utilisatrice" class="w-20 h-20 rounded-full mx-auto mb-4">
                        <p class="text-gray-600 italic">"J'adore la simplicité. Pas de fioritures, juste les outils dont j'ai besoin. Le mode sombre est parfait pour mes séances matinales. Je l'ai installée sur mon téléphone, c'est comme une vraie app."</p>
                        <p class="mt-4 font-bold text-accent">- Sophie L., Adepte du fitness</p>
                    </div>
                     <div class="magnetic-hover bg-white p-8 rounded-2xl shadow-xl border border-gray-200 slide-up" style="animation-delay: 0.4s;">
                        <img src="https://placehold.co/80x80/6366F1/ffffff?text=M" alt="Avatar d'un utilisateur" class="w-20 h-20 rounded-full mx-auto mb-4">
                        <p class="text-gray-600 italic">"Les calculateurs sont une révolution. Je sais exactement quoi soulever pour mes objectifs de prise de muscle. Fini les approximations ! Et pouvoir créer mes propres routines, c'est la liberté."</p>
                        <p class="mt-4 font-bold text-accent">- Marc D., Athlète passionné</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="comparison" class="py-20 bg-gray-50">
             <div class="container mx-auto px-6">
                <div class="text-center mb-16 slide-up">
                    <h3 class="text-3xl md:text-4xl font-bold text-gray-900">Le match : Lyftiv vs le reste du monde.</h3>
                </div>
                <div class="max-w-6xl mx-auto grid md:grid-cols-3 gap-0 border border-gray-200/50 rounded-2xl overflow-hidden shadow-2xl slide-up">
                    <div class="bg-white p-6 md:p-8">
                        <h4 class="text-2xl font-bold gradient-text">Lyftiv</h4>
                        <ul class="mt-6 space-y-4 text-gray-600">
                            <li class="flex items-start stagger-item"><svg class="w-5 h-5 text-green-500 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-900">Entièrement gratuit.</strong> Toutes les fonctionnalités, sans aucune limite.</span></li>
                            <li class="flex items-start stagger-item"><svg class="w-5 h-5 text-green-500 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-900">Suivi et personnalisation.</strong> Créez vos séances, ajoutez des exercices, enchaînez-les et prenez des notes.</span></li>
                            <li class="flex items-start stagger-item"><svg class="w-5 h-5 text-green-500 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-900">Analyse des performances.</strong> Suivez votre 1RM, votre progression et consultez l'historique de vos séances.</span></li>
                            <li class="flex items-start stagger-item"><svg class="w-5 h-5 text-green-500 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-900">Outils malins.</strong> Des calculateurs pour vos charges et des minuteurs pour vos temps de repos.</span></li>
                             <li class="flex items-start stagger-item"><svg class="w-5 h-5 text-green-500 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-900">Contrôle des données.</strong> Importez ou exportez facilement votre historique.</span></li>
                            <li class="flex items-start stagger-item"><svg class="w-5 h-5 text-green-500 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-900">App agréable à utiliser.</strong> Thème clair ou sombre et installation sur votre téléphone.</span></li>
                        </ul>
                    </div>
                    <div class="bg-gray-50 p-6 md:p-8 border-t md:border-t-0 md:border-l border-gray-200/50">
                        <h4 class="text-2xl font-bold text-gray-500">Carnet Papier</h4>
                        <ul class="mt-6 space-y-4 text-gray-600">
                            <li class="flex items-start"><svg class="w-5 h-5 text-red-400 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-700">Pas de calcul.</strong> Vous devez tout estimer vous-même (1RM, charges...).</span></li>
                            <li class="flex items-start"><svg class="w-5 h-5 text-red-400 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-700">Statique.</strong> Aucune vision de la progression, pas de graphiques.</span></li>
                            <li class="flex items-start"><svg class="w-5 h-5 text-red-400 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-700">Pas de sauvegarde.</strong> Vous le perdez, vous perdez tout votre historique.</span></li>
                        </ul>
                    </div>
                    <div class="bg-gray-50 p-6 md:p-8 border-t md:border-t-0 md:border-l border-gray-200/50">
                        <h4 class="text-2xl font-bold text-gray-500">Autres Apps</h4>
                         <ul class="mt-6 space-y-4 text-gray-600">
                            <li class="flex items-start"><svg class="w-5 h-5 text-red-400 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-700">Gratuit limité.</strong> Publicités intrusives, fonctions essentielles bloquées.</span></li>
                            <li class="flex items-start"><svg class="w-5 h-5 text-red-400 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-700">Programmes rigides.</strong> Des plans génériques qui ne s'adaptent pas.</span></li>
                            <li class="flex items-start"><svg class="w-5 h-5 text-red-400 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-700">Trop complexes.</strong> Des tonnes de graphiques sans explication.</span></li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>

        <section id="start" class="py-20 bg-gray-50">
            <div class="container mx-auto px-6 text-center">
                 <div class="max-w-3xl mx-auto bg-white rounded-2xl shadow-2xl p-10 slide-up">
                    <h3 class="text-3xl md:text-4xl font-bold text-gray-900">Prêt à transformer votre entraînement ?</h3>
                    <p class="mt-4 text-lg text-gray-700 max-w-2xl mx-auto">Rejoignez des milliers d'utilisateurs qui ont déjà fait le pas. Lyftiv est une web-app 100% gratuite, accessible sur tous vos appareils.</p>
                    <div class="mt-10 flex flex-col sm:flex-row justify-center items-center gap-4">
                        <a href="index.html" target="_blank" class="w-full sm:w-auto btn-primary text-white font-bold rounded-lg shadow-xl hover:shadow-2xl transition-all duration-300 transform hover:scale-105 px-10 py-4 text-lg">
                            Lancer Lyftiv maintenant
                        </a>
                    </div>
                    <p class="mt-6 text-sm text-gray-500">
                        <i class="fas fa-mobile-alt"></i> Installez l'application sur votre appareil pour un accès rapide et hors ligne.
                    </p>
                 </div>
            </div>
        </section>
    </main>

    <footer class="bg-gray-200 border-t border-gray-300/50">
        <div class="container mx-auto px-6 py-10 text-center">
            <div class="flex items-center justify-center gap-2">
                <svg class="w-7 h-7" viewBox="0 0 100 100"><use href="#g"/></svg>
                <h4 class="text-2xl logo-text">Lyftiv</h4>
            </div>
            <div class="mt-4 flex justify-center space-x-6">
                <a href="#" class="text-gray-600 hover:text-accent">Presse</a>
                <a href="#" class="text-gray-600 hover:text-accent">Contact</a>
                <a href="#" class="text-gray-600 hover:text-accent">Mentions légales</a>
            </div>
            <p class="mt-6 text-sm text-gray-500">&copy; 2025 Lyftiv. Tous droits réservés.</p>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // --- Intersection Observer for animations ---
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('visible');
                    }
                });
            }, { threshold: 0.1 });

            document.querySelectorAll('.slide-up, .stagger-item').forEach(el => observer.observe(el));
            
            // --- Scroll Progress Bar ---
            window.addEventListener('scroll', () => {
                const scrollProgress = document.getElementById('scrollProgress');
                if(!scrollProgress) return;
                const scrollTop = document.documentElement.scrollTop;
                const scrollHeight = document.documentElement.scrollHeight - document.documentElement.clientHeight;
                const progress = scrollHeight > 0 ? (scrollTop / scrollHeight) * 100 : 0;
                scrollProgress.style.width = `${progress}%`;
            });

            // --- Mobile Menu Toggle ---
            const menuButton = document.getElementById('mobile-menu-button');
            const mobileMenu = document.getElementById('mobile-menu');
            if(menuButton && mobileMenu) {
                menuButton.addEventListener('click', () => {
                    mobileMenu.classList.toggle('hidden');
                });
            }
        });
    </script>
</body>
</html>
