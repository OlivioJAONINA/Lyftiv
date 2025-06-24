<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lyftiv – Transformez vos entraînements en progrès mesurables</title>
    
    <meta name="description" content="Lyftiv est l'application tout-en-un pour suivre vos séances, analyser vos performances (tonnage, 1RM), gérer votre jeûne et rejoindre une communauté motivante. 5 séances gratuites par semaine.">
    <meta property="og:title" content="Lyftiv – L'application de musculation intelligente">
    <meta property="og:description" content="Arrêtez de deviner. Commencez à progresser avec des outils puissants et simples.">
    <meta property="og:type" content="website">
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;900&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; background-color: #F8F9FA; }
        
        .logo-fluo-text {
            color: #ABFF00; /* Bright lime green */
        }

        .pastel-gradient-text { 
            background: -webkit-linear-gradient(135deg, #8A72EE, #B08ADC); 
            -webkit-background-clip: text; 
            -webkit-text-fill-color: transparent; 
            background-clip: text; 
        }

        .floating { animation: float 6s ease-in-out infinite; }
        @keyframes float { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-10px)} }
        
        .slide-up { opacity: 0; transform: translateY(30px); transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94); }
        .slide-up.visible { opacity: 1; transform: translateY(0); }
        
        .pulse-glow-pastel { 
            animation: pulseGlowPastel 4s ease-in-out infinite alternate; 
        }
        @keyframes pulseGlowPastel { 
            from{box-shadow:0 0 20px rgba(162,155,254,.2)} 
            to{box-shadow:0 0 40px rgba(162,155,254,.4)} 
        }
        
        .blob { position: absolute; border-radius: 50%; filter: blur(70px); animation: blob 12s ease-in-out infinite; opacity: 0.2; }
        .blob:nth-child(1) { top: 10%; left: 10%; width: 350px; height: 350px; background: #a29bfe; animation-delay: 0s; }
        .blob:nth-child(2) { bottom: 10%; right: 10%; width: 250px; height: 250px; background: #d6a2e8; animation-delay: 3s; }
        @keyframes blob { 0%,100%{transform:translate(0,0) scale(1)} 33%{transform:translate(30px,-50px) scale(1.05)} 66%{transform:translate(-20px,20px) scale(.95)} }
        
        .magnetic-hover { transition: all 0.3s ease; }
        .magnetic-hover:hover { transform: translateY(-6px) scale(1.02); box-shadow: 0 15px 30px rgba(0,0,0,0.08); }
        
        .scroll-progress { position: fixed; top: 0; left: 0; width: 0%; height: 4px; background: linear-gradient(90deg, #a29bfe, #d6a2e8); z-index: 10000; transition: width 0.1s ease-out; }
        
        .stagger-item { opacity: 0; transform: translateX(-20px); transition: all 0.5s ease-out; }
        .stagger-item.visible { opacity: 1; transform: translateX(0); }
        
        .count-up { font-variant-numeric: tabular-nums; }
        
        .btn-pastel-primary {
            background-color: #8A72EE; /* Soft Lavender */
            color: white;
            transition: all 0.3s ease;
        }
        .btn-pastel-primary:hover {
            background-color: #7469B6; 
            box-shadow: 0 4px 15px rgba(138, 114, 238, 0.4);
            transform: translateY(-2px);
        }
        .text-pastel-accent { color: #7469B6; }

        @media (prefers-reduced-motion: reduce) {
            *, ::before, ::after { animation-duration: 0.01ms!important; animation-iteration-count: 1!important; transition-duration: 0.01ms!important; scroll-behavior: auto!important; }
        }
    </style>
</head>
<body class="bg-gray-100 text-gray-800 antialiased">
    <div class="scroll-progress" id="scrollProgress"></div>

    <header class="bg-white/70 backdrop-blur-lg fixed top-0 left-0 right-0 z-50 border-b border-gray-200/50">
        <div class="container mx-auto px-6 py-3 flex justify-between items-center">
            <h1 class="text-3xl font-black logo-fluo-text">Lyftiv</h1>
            
            <nav class="hidden md:flex space-x-8 items-center">
                <a href="#features" class="text-gray-600 hover:text-pastel-accent font-medium">Fonctionnalités</a>
                <a href="#social-proof" class="text-gray-600 hover:text-pastel-accent font-medium">Avis</a>
                <a href="#pricing" class="text-gray-600 hover:text-pastel-accent font-medium">Tarifs</a>
            </nav>
            <a href="#pricing" class="hidden md:block px-6 py-2 btn-pastel-primary text-white font-semibold rounded-lg shadow-md hover:shadow-lg transition-all duration-300 transform hover:scale-105">
                Commencer
            </a>
            <button id="mobile-menu-button" class="md:hidden p-2 rounded-md text-gray-700 hover:bg-gray-200">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path></svg>
            </button>
        </div>
        <div id="mobile-menu" class="hidden md:hidden px-6 pb-4">
             <a href="#features" class="block py-2 text-gray-700 font-semibold">Fonctionnalités</a>
             <a href="#social-proof" class="block py-2 text-gray-700 font-semibold">Avis</a>
             <a href="#pricing" class="block py-2 text-gray-700 font-semibold">Tarifs</a>
             <a href="#pricing" class="block mt-4 w-full text-center py-3 btn-pastel-primary text-white font-semibold rounded-lg shadow-lg">Commencer</a>
        </div>
    </header>

    <main>
        <section class="pt-32 pb-20 text-center relative overflow-hidden flex items-center min-h-[90vh] bg-gradient-to-br from-purple-50 via-indigo-50 to-pink-50">
            <div class="absolute inset-0 z-0">
                <div class="blob"></div>
                <div class="blob"></div>
            </div>
            
            <div class="container mx-auto px-6 relative z-10">
                <div class="grid lg:grid-cols-2 gap-12 items-center">
                    <div class="text-center lg:text-left">
                        <h2 class="text-4xl md:text-5xl font-black text-gray-900 leading-tight slide-up">
                            Transformez vos efforts
                            <br>
                            <span class="pastel-gradient-text" style="animation-delay: 0.2s;">en progrès mesurables.</span>
                        </h2>
                        <p class="mt-6 text-lg md:text-xl text-gray-700 max-w-xl mx-auto lg:mx-0 slide-up" style="animation-delay: 0.3s;">
                            Plus qu'un simple carnet. Lyftiv analyse vos performances, vous guide pour franchir vos paliers et vous connecte à une communauté qui vous pousse à vous dépasser.
                        </p>
                        <div class="mt-10 flex flex-col sm:flex-row justify-center lg:justify-start items-center gap-4 slide-up" style="animation-delay: 0.5s;">
                            <a href="#pricing" class="w-full sm:w-auto btn-pastel-primary text-white font-bold rounded-lg shadow-xl hover:shadow-2xl transition-all duration-300 transform hover:scale-105 px-8 py-4">
                                Créer mon compte gratuit
                            </a>
                        </div>
                         <p class="mt-4 text-sm text-gray-600 slide-up" style="animation-delay: 0.6s;">
                            <span class="font-bold">5 séances par semaine offertes.</span> Aucune carte de crédit requise.
                        </p>
                    </div>

                    <div class="slide-up floating" style="animation-delay: 0.8s;">
                        <div class="relative mx-auto border-gray-700 bg-gray-700 border-[12px] rounded-[2.2rem] h-[580px] w-[290px] pulse-glow-pastel">
                            <div class="h-[30px] w-[3px] bg-gray-700 absolute -left-[15px] top-[70px] rounded-l-lg"></div>
                            <div class="h-[44px] w-[3px] bg-gray-700 absolute -left-[15px] top-[120px] rounded-l-lg"></div>
                            <div class="h-[44px] w-[3px] bg-gray-700 absolute -left-[15px] top-[170px] rounded-l-lg"></div>
                            <div class="h-[60px] w-[3px] bg-gray-700 absolute -right-[15px] top-[140px] rounded-r-lg"></div>
                            <div class="rounded-[1.8rem] overflow-hidden w-full h-full bg-white">
                                <div class="bg-gray-700 text-white p-2 text-xs flex justify-between items-center">
                                    <span class="font-semibold">Développé Couché</span>
                                    <span class="text-xs">1RM Est: <strong class="text-purple-300">102.5 kg</strong></span>
                                </div>
                                <div class="p-3 space-y-2 flex-1 overflow-y-auto bg-gray-50 h-full">
                                    <div class="flex items-center gap-2 opacity-60">
                                        <span class="w-7 h-7 flex items-center justify-center bg-purple-400 text-white font-bold rounded-full flex-shrink-0 text-xs">1</span>
                                        <div class="w-full p-1.5 rounded bg-gray-200 text-gray-700 text-center font-medium text-sm">80 kg</div>
                                        <span class="font-bold text-gray-400 text-sm">×</span>
                                        <div class="w-full p-1.5 rounded bg-gray-200 text-gray-700 text-center font-medium text-sm">8 reps</div>
                                        <div class="w-7 h-7 flex items-center justify-center bg-green-400 rounded-full flex-shrink-0">
                                            <svg class="w-3 h-3 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"></path></svg>
                                        </div>
                                    </div>
                                    <div class="flex items-center gap-2 opacity-60">
                                        <span class="w-7 h-7 flex items-center justify-center bg-purple-400 text-white font-bold rounded-full flex-shrink-0 text-xs">2</span>
                                        <div class="w-full p-1.5 rounded bg-gray-200 text-gray-700 text-center font-medium text-sm">80 kg</div>
                                        <span class="font-bold text-gray-400 text-sm">×</span>
                                        <div class="w-full p-1.5 rounded bg-gray-200 text-gray-700 text-center font-medium text-sm">7 reps</div>
                                        <div class="w-7 h-7 flex items-center justify-center bg-green-400 rounded-full flex-shrink-0">
                                            <svg class="w-3 h-3 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"></path></svg>
                                        </div>
                                    </div>
                                    <div class="flex items-center gap-2 p-1.5 rounded-md bg-purple-100 ring-2 ring-purple-500">
                                        <span class="w-7 h-7 flex items-center justify-center bg-purple-500 text-white font-bold rounded-full flex-shrink-0 text-xs">3</span>
                                        <input type="text" placeholder="Poids" class="w-full p-1.5 rounded bg-white text-gray-700 text-center font-medium text-sm">
                                        <span class="font-bold text-lg text-gray-500">×</span>
                                        <input type="text" placeholder="Reps" class="w-full p-1.5 rounded bg-white text-gray-700 text-center font-medium text-sm">
                                        <div class="w-7 h-7 flex-shrink-0"></div>
                                    </div>
                                     <div class="flex items-center gap-2">
                                        <span class="w-7 h-7 flex items-center justify-center bg-gray-300 text-gray-500 font-bold rounded-full flex-shrink-0 text-xs">4</span>
                                        <div class="w-full p-1.5 rounded bg-gray-200 text-center font-medium text-gray-400 text-sm">...</div>
                                        <span class="font-bold text-gray-400 text-sm">×</span>
                                        <div class="w-full p-1.5 rounded bg-gray-200 text-center font-medium text-gray-400 text-sm">...</div>
                                        <div class="w-7 h-7 flex-shrink-0"></div>
                                    </div>
                                </div>
                                <div class="p-3 border-t border-gray-200 text-center bg-white">
                                    <button class="w-full py-2.5 bg-purple-500 text-white font-bold rounded-md shadow-md hover:bg-purple-600 transition text-sm">Valider & Repos</button>
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
                    <div class="magnetic-hover bg-purple-50 p-8 rounded-2xl shadow-lg slide-up">
                        <div class="w-12 h-12 btn-pastel-primary rounded-lg flex items-center justify-center floating">
                             <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6" /></svg>
                        </div>
                        <h4 class="mt-6 text-xl font-bold text-pastel-accent">Ne vous demandez plus si vous progressez</h4>
                        <p class="mt-2 text-gray-600">Suivez votre tonnage, estimez votre 1RM et créez des supersets en un clic. Lyftiv traduit vos efforts en graphiques clairs.</p>
                    </div>
                    <div class="magnetic-hover bg-indigo-50 p-8 rounded-2xl shadow-lg slide-up" style="animation-delay: 0.2s;">
                        <div class="w-12 h-12 btn-pastel-primary rounded-lg flex items-center justify-center floating" style="animation-delay: 0.3s;">
                           <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" /></svg>
                        </div>
                        <h4 class="mt-6 text-xl font-bold text-pastel-accent">Un coach pour votre style de vie</h4>
                        <p class="mt-2 text-gray-600">Calculez vos charges idéales, définissez vos objectifs (Force, Hypertrophie...) et suivez votre jeûne intermittent sans effort.</p>
                    </div>
                    <div class="magnetic-hover bg-pink-50 p-8 rounded-2xl shadow-lg slide-up" style="animation-delay: 0.4s;">
                        <div class="w-12 h-12 btn-pastel-primary rounded-lg flex items-center justify-center floating" style="animation-delay: 0.6s;">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283-.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z" /></svg>
                        </div>
                        <h4 class="mt-6 text-xl font-bold text-pastel-accent">Partagez vos résultats en 1 clic</h4>
                        <p class="mt-2 text-gray-600">Rejoignez une Squad pour des défis collectifs ou exportez votre historique sur Excel pour le partager avec votre coach.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="social-proof" class="py-20 bg-gray-50">
            <div class="container mx-auto px-6">
                 <div class="text-center mb-16 slide-up">
                    <h3 class="text-3xl md:text-4xl font-bold text-gray-900">Ils ont arrêté de deviner.</h3>
                    <p class="mt-4 text-lg text-gray-700 max-w-2xl mx-auto">Découvrez pourquoi nos utilisateurs nous adorent.</p>
                </div>
                <div class="grid md:grid-cols-3 gap-8">
                    <div class="magnetic-hover bg-white p-8 rounded-2xl shadow-xl border border-gray-200 slide-up">
                        <img src="https://placehold.co/80x80/a29bfe/ffffff?text=A" alt="Avatar d'un utilisateur" class="w-20 h-20 rounded-full mx-auto mb-4">
                        <p class="text-gray-600 italic">"Enfin une app qui comprend ce que veulent les puristes. Les stats sont précises, l'interface est rapide et je peux créer n'importe quelle séance. Le calculateur de plaques est un bonus génial!"</p>
                        <p class="mt-4 font-bold text-pastel-accent">- Alex R., Powerlifter</p>
                    </div>
                     <div class="magnetic-hover bg-white p-8 rounded-2xl shadow-xl border border-gray-200 slide-up" style="animation-delay: 0.2s;">
                        <img src="https://placehold.co/80x80/d6a2e8/ffffff?text=S" alt="Avatar d'une utilisatrice" class="w-20 h-20 rounded-full mx-auto mb-4">
                        <p class="text-gray-600 italic">"J'adore la fonction de jeûne intermittent! C'est super simple à suivre. L'app n'est pas intimidante et me guide vraiment. J'ai enfin une routine qui me convient."</p>
                        <p class="mt-4 font-bold text-pastel-accent">- Sophie L., Maman Wellness</p>
                    </div>
                     <div class="magnetic-hover bg-white p-8 rounded-2xl shadow-xl border border-gray-200 slide-up" style="animation-delay: 0.4s;">
                        <img src="https://placehold.co/80x80/fd79a8/ffffff?text=M" alt="Avatar d'un utilisateur" class="w-20 h-20 rounded-full mx-auto mb-4">
                        <p class="text-gray-600 italic">"La fonction Squad est incroyable. On se motive entre potes pour les raids de tonnage, c'est devenu notre rituel. Lyftiv a rendu l'entraînement fun et social."</p>
                        <p class="mt-4 font-bold text-pastel-accent">- Marc D., Membre de Squad</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="comparison" class="py-20 bg-white">
             <div class="container mx-auto px-6">
                <div class="text-center mb-16 slide-up">
                    <h3 class="text-3xl md:text-4xl font-bold text-gray-900">Le match : Lyftiv vs le reste du monde.</h3>
                </div>
                <div class="max-w-6xl mx-auto grid md:grid-cols-3 gap-0 border border-gray-200/50 rounded-2xl overflow-hidden shadow-2xl slide-up">
                    <div class="bg-white p-6 md:p-8">
                        <h4 class="text-2xl font-bold pastel-gradient-text">Lyftiv</h4>
                        <ul class="mt-6 space-y-4 text-gray-600">
                            <li class="flex items-start stagger-item"><svg class="w-5 h-5 text-green-500 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-900">Freemium généreux.</strong> 5 vraies séances par semaine, gratuites.</span></li>
                            <li class="flex items-start stagger-item" style="animation-delay: 0.1s;"><svg class="w-5 h-5 text-green-500 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-900">Stats simples ET puissantes.</strong> Nous traduisons votre tonnage et votre 1RM en victoires motivantes.</span></li>
                            <li class="flex items-start stagger-item" style="animation-delay: 0.2s;"><svg class="w-5 h-5 text-green-500 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-900">Guidage intelligent.</strong> Recevez des conseils pour franchir vos paliers et des programmes adaptés.</span></li>
                            <li class="flex items-start stagger-item" style="animation-delay: 0.3s;"><svg class="w-5 h-5 text-green-500 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-900">Communauté & Outils.</strong> Rejoignez une Squad et utilisez nos calculateurs pour progresser.</span></li>
                        </ul>
                    </div>
                    <div class="bg-gray-50 p-6 md:p-8 border-t md:border-t-0 md:border-l border-gray-200/50">
                        <h4 class="text-2xl font-bold text-gray-500">Carnet Papier</h4>
                        <ul class="mt-6 space-y-4 text-gray-600">
                            <li class="flex items-start"><svg class="w-5 h-5 text-red-400 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-700">Pas de calcul.</strong> Vous devez tout estimer vous-même (1RM, tonnage).</span></li>
                            <li class="flex items-start"><svg class="w-5 h-5 text-red-400 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-700">Statique.</strong> Aucune vision de la progression, pas de graphiques.</span></li>
                            <li class="flex items-start"><svg class="w-5 h-5 text-red-400 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-700">Pas de sauvegarde.</strong> Vous le perdez, vous perdez tout votre historique.</span></li>
                            <li class="flex items-start"><svg class="w-5 h-5 text-red-400 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-700">Isolé.</strong> Vous êtes seul face à votre carnet.</span></li>
                        </ul>
                    </div>
                    <div class="bg-gray-50 p-6 md:p-8 border-t md:border-t-0 md:border-l border-gray-200/50">
                        <h4 class="text-2xl font-bold text-gray-500">Autres Apps</h4>
                         <ul class="mt-6 space-y-4 text-gray-600">
                            <li class="flex items-start"><svg class="w-5 h-5 text-red-400 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-700">Gratuit limité.</strong> Publicités, fonctions essentielles bloquées.</span></li>
                            <li class="flex items-start"><svg class="w-5 h-5 text-red-400 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-700">Programmes rigides.</strong> Des plans génériques qui ne s'adaptent pas.</span></li>
                            <li class="flex items-start"><svg class="w-5 h-5 text-red-400 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-700">Trop complexes.</strong> Des tonnes de graphiques sans explication.</span></li>
                            <li class="flex items-start"><svg class="w-5 h-5 text-red-400 mr-3 flex-shrink-0 mt-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path></svg><span><strong class="text-gray-700">Communauté basique.</strong> Juste un "like" ou un commentaire.</span></li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>

        <section id="pricing" class="py-20 bg-gray-50">
            <div class="container mx-auto px-6">
                 <div class="text-center mb-16 slide-up">
                    <h3 class="text-3xl md:text-4xl font-bold text-gray-900">Un tarif aussi simple que l'application.</h3>
                    <p class="mt-4 text-lg text-gray-700 max-w-2xl mx-auto">Commencez gratuitement, passez au premium quand vous voulez.</p>
                </div>
                <div class="flex flex-col lg:flex-row justify-center items-stretch gap-8">
                    <div class="w-full lg:w-1/3 border-2 border-gray-200/80 rounded-2xl p-8 flex flex-col magnetic-hover slide-up bg-white">
                        <h4 class="text-2xl font-bold text-gray-900">Gratuit</h4>
                        <p class="mt-2 text-gray-600">Pour s'entraîner sérieusement, sans compromis.</p>
                        <p class="my-8"><span class="text-5xl font-black">0€</span><span class="text-gray-600">/pour toujours</span></p>
                        <ul class="space-y-4 text-gray-700 mb-8 flex-1">
                           <li class="flex items-center stagger-item"><svg class="w-6 h-6 text-green-500 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>Jusqu'à 5 séances/semaine</li>
                           <li class="flex items-center stagger-item" style="animation-delay: 0.1s;"><svg class="w-6 h-6 text-green-500 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>Suivi basique (poids, reps)</li>
                           <li class="flex items-center stagger-item" style="animation-delay: 0.2s;"><svg class="w-6 h-6 text-green-500 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>Calculateur 1RM</li>
                           <li class="flex items-center stagger-item" style="animation-delay: 0.3s;"><svg class="w-6 h-6 text-green-500 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>Accès à la communauté</li>
                        </ul>
                        <button class="w-full py-3 bg-gray-200 text-gray-800 font-bold rounded-lg hover:bg-gray-300 transition-colors">Votre plan actuel</button>
                    </div>
                    <div class="w-full lg:w-1/3 btn-pastel-primary text-white rounded-2xl p-8 flex flex-col shadow-2xl pulse-glow-pastel transform lg:scale-105 slide-up" style="animation-delay: 0.2s;">
                         <div class="text-center mb-4"><span class="bg-white/20 text-white font-semibold px-4 py-1 rounded-full text-sm">Le plus populaire</span></div>
                         <h4 class="text-2xl font-bold">Premium</h4>
                        <p class="mt-2 opacity-90">Pour libérer tout votre potentiel.</p>
                        <p class="my-8"><span class="text-5xl font-black">7€</span><span class="opacity-90">/mois</span></p>
                        <ul class="space-y-4 mb-8 flex-1">
                           <li class="flex items-center stagger-item"><svg class="w-6 h-6 text-white mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>Tout du plan gratuit, et...</li>
                           <li class="flex items-center stagger-item" style="animation-delay: 0.1s;"><svg class="w-6 h-6 text-white mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>Séances illimitées</li>
                           <li class="flex items-center stagger-item" style="animation-delay: 0.2s;"><svg class="w-6 h-6 text-white mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>Programmes personnalisés</li>
                           <li class="flex items-center stagger-item" style="animation-delay: 0.3s;"><svg class="w-6 h-6 text-white mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>Statistiques avancées & alertes</li>
                           <li class="flex items-center stagger-item" style="animation-delay: 0.4s;"><svg class="w-6 h-6 text-white mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>Suivi complet (jeûne, poids, etc.)</li>
                           <li class="flex items-center stagger-item" style="animation-delay: 0.5s;"><svg class="w-6 h-6 text-white mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>Défis de Squad exclusifs</li>
                        </ul>
                        <button class="w-full py-3 bg-white text-purple-600 font-bold rounded-lg hover:bg-gray-100 transition-colors">Essayer Premium 7 jours</button>
                    </div>
                </div>
            </div>
        </section>

        <section class="py-20">
            <div class="container mx-auto px-6 text-center">
                 <h3 class="text-3xl md:text-4xl font-bold text-gray-900 slide-up">Prêt à transformer votre entraînement?</h3>
                 <p class="mt-4 text-lg text-gray-700 max-w-2xl mx-auto slide-up" style="animation-delay: 0.2s;">Rejoignez des milliers d'utilisateurs qui ont déjà fait le pas. Téléchargez Lyftiv aujourd'hui.</p>
                 <div class="mt-10 flex flex-col sm:flex-row justify-center items-center gap-4 slide-up" style="animation-delay: 0.4s;">
                    <a href="#" class="inline-block"><img src="https://placehold.co/180x60/E9E7FD/7469B6?text=App+Store" alt="Bientôt sur l'App Store" class="h-14 rounded-lg shadow-md hover:shadow-lg transition-shadow"></a>
                    <a href="#" class="inline-block"><img src="https://placehold.co/180x60/E9E7FD/7469B6?text=Google+Play" alt="Bientôt sur Google Play" class="h-14 rounded-lg shadow-md hover:shadow-lg transition-shadow"></a>
                 </div>
            </div>
        </section>
    </main>

    <footer class="bg-gray-200 border-t border-gray-300/50">
        <div class="container mx-auto px-6 py-10 text-center">
            <h4 class="text-2xl font-black logo-fluo-text">Lyftiv</h4>
            <div class="mt-4 flex justify-center space-x-6">
                <a href="#" class="text-gray-600 hover:text-pastel-accent">Presse</a>
                <a href="#" class="text-gray-600 hover:text-pastel-accent">Contact</a>
                <a href="#" class="text-gray-600 hover:text-pastel-accent">Mentions légales</a>
            </div>
            <p class="mt-6 text-sm text-gray-500">&copy; 2025 Lyftiv. Tous droits réservés.</p>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('visible');
                    }
                });
            }, { threshold: 0.1 });

            document.querySelectorAll('.slide-up,.reveal,.stagger-item').forEach(el => observer.observe(el));
            
            window.addEventListener('scroll', () => {
                const scrollProgress = document.getElementById('scrollProgress');
                if(!scrollProgress) return;
                const scrollTop = document.documentElement.scrollTop;
                const scrollHeight = document.documentElement.scrollHeight - document.documentElement.clientHeight;
                scrollProgress.style.width = `${(scrollTop / scrollHeight) * 100}%`;
            });

            const countUpObserver = new IntersectionObserver((entries, observer) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        const el = entry.target;
                        const countTo = parseInt(el.getAttribute('data-count'), 10);
                        let from = 0;
                        const duration = 2000; 
                        const frameDuration = 1000 / 60;
                        const totalFrames = Math.round(duration / frameDuration);
                        let currentFrame = 0;
                        const increment = countTo / totalFrames;

                        const timer = setInterval(() => {
                            currentFrame++;
                            from += increment;
                            el.textContent = Math.round(from).toLocaleString();
                            if(currentFrame === totalFrames) {
                                el.textContent = countTo.toLocaleString();
                                clearInterval(timer);
                            }
                        }, frameDuration);
                        observer.unobserve(el);
                    }
                });
            }, { threshold: 0.7 });

            document.querySelectorAll('.count-up').forEach(el => countUpObserver.observe(el));
            
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
