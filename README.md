<!DOCTYPE html>
<html lang="es" class="h-full">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ecos y Reflexiones - Plataforma Literaria</title>
  
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  
  <!-- Google Fonts: Playfair Display, Merriweather, Inter -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Merriweather:ital,wght@0,300;0,400;0,700;1,300;1,400&family=Playfair+Display:ital,wght@0,500;0,600;0,700;1,400;1,600&display=swap" rel="stylesheet">
  
  <!-- FontAwesome Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: {
            warm: {
              50: '#FDFBF7',
              100: '#FAF6F0',
              200: '#F3ECE1',
              300: '#E6D7C3',
              400: '#D2B99B',
              500: '#B8946E',
              600: '#9B744B',
              700: '#7B5835',
              800: '#5C3E23',
              900: '#3D2714',
            },
            sepia: {
              base: '#2C2520',
              accent: '#C05621',
              gold: '#D69E2E',
            }
          },
          fontFamily: {
            sans: ['Inter', 'sans-serif'],
            serif: ['Merriweather', 'serif'],
            display: ['Playfair Display', 'serif'],
          }
        }
      }
    }
  </script>

  <style>
    /* Custom Scrollbar */
    ::-webkit-scrollbar {
      width: 6px;
    }
    ::-webkit-scrollbar-track {
      background: transparent;
    }
    ::-webkit-scrollbar-thumb {
      background: rgba(156, 116, 75, 0.3);
      border-radius: 9999px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: rgba(156, 116, 75, 0.6);
    }
    .prose-editorial {
      font-family: 'Merriweather', serif;
      line-height: 1.8;
      font-size: 1.05rem;
    }
  </style>
</head>
<body class="bg-warm-100 dark:bg-zinc-950 text-zinc-800 dark:text-zinc-200 min-h-full flex flex-col font-sans transition-colors duration-300">

  <!-- TOP HEADER / NAVBAR -->
  <header class="sticky top-0 z-30 bg-warm-50/90 dark:bg-zinc-900/90 backdrop-blur-md border-b border-warm-200 dark:border-zinc-800 transition-colors duration-300">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-20">
        
        <!-- Brand Logo -->
        <div class="flex items-center space-x-3 cursor-pointer" onclick="navigateTo('principal')">
          <div class="w-10 h-10 rounded-full bg-warm-700 text-warm-50 dark:bg-amber-600 flex items-center justify-center font-display font-bold text-xl shadow-md">
            E
          </div>
          <div>
            <h1 class="font-display text-xl sm:text-2xl font-bold tracking-tight text-warm-900 dark:text-warm-100">
              Ecos y Reflexiones
            </h1>
            <p class="text-xs text-warm-600 dark:text-amber-500 font-serif italic hidden sm:block">
              Un refugio para las palabras de la vida
            </p>
          </div>
        </div>

        <!-- Navigation Tabs -->
        <nav class="hidden md:flex space-x-1 lg:space-x-2">
          <button onclick="navigateTo('principal')" id="nav-principal" class="nav-tab px-4 py-2 rounded-lg text-sm font-medium transition-all">
            <i class="fa-solid fa-feather-pointed mr-2"></i>Escritos Principales
          </button>
          <button onclick="navigateTo('comunidad')" id="nav-comunidad" class="nav-tab px-4 py-2 rounded-lg text-sm font-medium transition-all">
            <i class="fa-solid fa-users mr-2"></i>Comunidad
          </button>
          <button onclick="navigateTo('escribir')" id="nav-escribir" class="nav-tab px-4 py-2 rounded-lg text-sm font-medium transition-all">
            <i class="fa-solid fa-pen-nib mr-2"></i>Escribir
          </button>
        </nav>

        <!-- User Controls & Dark Mode -->
        <div class="flex items-center space-x-3">
          <!-- Theme Toggle Button -->
          <button onclick="toggleDarkMode()" class="p-2.5 rounded-full text-warm-700 dark:text-amber-400 hover:bg-warm-200 dark:hover:bg-zinc-800 transition-colors" title="Cambiar tema">
            <i id="theme-icon" class="fa-solid fa-moon text-lg"></i>
          </button>

          <!-- User Badge / Login Trigger -->
          <button onclick="navigateTo('perfil')" id="user-pill" class="flex items-center space-x-2 px-3 py-1.5 rounded-full border border-warm-300 dark:border-zinc-700 hover:border-warm-500 transition-all bg-warm-50 dark:bg-zinc-800">
            <div id="user-avatar" class="w-6 h-6 rounded-full bg-warm-600 dark:bg-amber-600 text-white text-xs flex items-center justify-center font-bold">
              ?
            </div>
            <span id="user-name" class="text-xs font-semibold max-w-[90px] truncate">Invitado</span>
            <span id="admin-badge" class="hidden px-1.5 py-0.5 text-[10px] font-bold uppercase tracking-wider bg-amber-600 text-white rounded">Admin</span>
          </button>
        </div>
      </div>
    </div>

    <!-- Mobile Navigation Bottom Bar -->
    <div class="md:hidden border-t border-warm-200 dark:border-zinc-800 bg-warm-50 dark:bg-zinc-900 flex justify-around py-2 text-xs font-medium">
      <button onclick="navigateTo('principal')" id="mobile-nav-principal" class="flex flex-col items-center p-1 text-warm-800 dark:text-zinc-300">
        <i class="fa-solid fa-feather-pointed text-base mb-1"></i>
        <span>Inicio</span>
      </button>
      <button onclick="navigateTo('comunidad')" id="mobile-nav-comunidad" class="flex flex-col items-center p-1 text-warm-800 dark:text-zinc-300">
        <i class="fa-solid fa-users text-base mb-1"></i>
        <span>Comunidad</span>
      </button>
      <button onclick="navigateTo('escribir')" id="mobile-nav-escribir" class="flex flex-col items-center p-1 text-warm-800 dark:text-zinc-300">
        <i class="fa-solid fa-pen-nib text-base mb-1"></i>
        <span>Escribir</span>
      </button>
      <button onclick="navigateTo('perfil')" id="mobile-nav-perfil" class="flex flex-col items-center p-1 text-warm-800 dark:text-zinc-300">
        <i class="fa-solid fa-user text-base mb-1"></i>
        <span>Perfil</span>
      </button>
    </div>
  </header>

  <!-- MAIN CONTENT CONTAINER -->
  <main class="flex-grow max-w-6xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8">

    <!-- VIEW 1: ESCRITOS PRINCIPALES (ADMIN HIGHLIGHTS) -->
    <section id="view-principal" class="space-y-8">
      <!-- Hero Banner -->
      <div class="relative overflow-hidden rounded-2xl bg-gradient-to-r from-warm-800 via-warm-900 to-zinc-900 text-warm-100 p-8 sm:p-12 shadow-xl border border-warm-700/30">
        <div class="absolute -right-10 -bottom-10 opacity-10 text-white pointer-events-none">
          <i class="fa-solid fa-book-open text-[240px]"></i>
        </div>
        <div class="relative z-10 max-w-2xl space-y-4">
          <span class="inline-block px-3 py-1 bg-amber-600/30 border border-amber-500/40 text-amber-300 rounded-full text-xs font-semibold tracking-wider uppercase">
            Pensamientos del Autor
          </span>
          <h2 class="font-display text-3xl sm:text-5xl font-bold tracking-wide leading-tight">
            Reflexiones sobre la condición humana y el paso del tiempo.
          </h2>
          <p class="text-warm-200 text-base sm:text-lg font-serif italic">
            "No vivimos los días; vivimos las pausas que dejamos entre ellos."
          </p>
        </div>
      </div>

      <!-- Main Articles Feed -->
      <div class="space-y-6">
        <div class="flex items-center justify-between border-b border-warm-200 dark:border-zinc-800 pb-3">
          <h3 class="font-display text-2xl font-bold text-warm-900 dark:text-warm-100 flex items-center gap-2">
            <i class="fa-solid fa-star text-amber-600 text-lg"></i>
            Ensayos y Escritos Destacados
          </h3>
          <span class="text-xs font-semibold text-warm-600 dark:text-zinc-400">Canal Oficial</span>
        </div>

        <!-- Featured Writings Grid -->
        <div id="grid-principal" class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <!-- Dynamically populated -->
        </div>
      </div>
    </section>


    <!-- VIEW 2: COMUNIDAD -->
    <section id="view-comunidad" class="hidden space-y-8">
      <!-- Header & Filters -->
      <div class="flex flex-col md:flex-row md:items-center md:justify-between gap-4 border-b border-warm-200 dark:border-zinc-800 pb-6">
        <div>
          <h2 class="font-display text-3xl font-bold text-warm-900 dark:text-warm-100">
            Voces de la Comunidad
          </h2>
          <p class="text-sm text-warm-600 dark:text-zinc-400 mt-1">
            Espacio abierto donde lectores y autores comparten sus propias visiones del mundo.
          </p>
        </div>

        <!-- Category Filters -->
        <div class="flex flex-wrap gap-2" id="category-filters">
          <button onclick="setCategoryFilter('Todos')" class="cat-btn active-cat px-3 py-1.5 rounded-full text-xs font-semibold transition-all">Todos</button>
          <button onclick="setCategoryFilter('Reflexiones')" class="cat-btn px-3 py-1.5 rounded-full text-xs font-semibold transition-all">Reflexiones</button>
          <button onclick="setCategoryFilter('Filosofía')" class="cat-btn px-3 py-1.5 rounded-full text-xs font-semibold transition-all">Filosofía</button>
          <button onclick="setCategoryFilter('Historias')" class="cat-btn px-3 py-1.5 rounded-full text-xs font-semibold transition-all">Historias</button>
          <button onclick="setCategoryFilter('Poesía')" class="cat-btn px-3 py-1.5 rounded-full text-xs font-semibold transition-all">Poesía</button>
        </div>
      </div>

      <!-- Search Box -->
      <div class="relative max-w-md">
        <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-warm-400"></i>
        <input type="text" id="search-input" oninput="renderCommunityPosts()" placeholder="Buscar por título, contenido o autor..." class="w-full pl-10 pr-4 py-2.5 rounded-xl border border-warm-300 dark:border-zinc-700 bg-warm-50 dark:bg-zinc-900 text-sm focus:outline-none focus:ring-2 focus:ring-warm-600 dark:focus:ring-amber-500">
      </div>

      <!-- Community Writings Grid -->
      <div id="grid-comunidad" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <!-- Dynamically populated -->
      </div>
    </section>


    <!-- VIEW 3: FORMULARIO PUBLICAR / ESCRIBIR -->
    <section id="view-escribir" class="hidden max-w-3xl mx-auto">
      <div class="bg-warm-50 dark:bg-zinc-900 border border-warm-200 dark:border-zinc-800 rounded-2xl p-6 sm:p-10 shadow-lg">
        <div class="border-b border-warm-200 dark:border-zinc-800 pb-4 mb-6">
          <h2 class="font-display text-2xl sm:text-3xl font-bold text-warm-900 dark:text-warm-100 flex items-center gap-3">
            <i class="fa-solid fa-feather text-amber-600"></i>
            Crear Nueva Publicación
          </h2>
          <p class="text-sm text-warm-600 dark:text-zinc-400 mt-1">
            Plasma tus pensamientos. Sé honesto, profundo y respetuoso con la palabra.
          </p>
        </div>

        <form id="post-form" onsubmit="handlePostSubmit(event)" class="space-y-6">
          <!-- Title -->
          <div>
            <label class="block text-xs font-bold uppercase tracking-wider text-warm-700 dark:text-zinc-300 mb-2">
              Título del Escrito *
            </label>
            <input type="text" id="post-title" required placeholder="Ej. La quietud de las primeras horas" class="w-full px-4 py-3 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 text-base font-serif focus:outline-none focus:ring-2 focus:ring-warm-600 dark:focus:ring-amber-500">
          </div>

          <!-- Metadata row -->
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div>
              <label class="block text-xs font-bold uppercase tracking-wider text-warm-700 dark:text-zinc-300 mb-2">
                Categoría *
              </label>
              <select id="post-category" class="w-full px-4 py-2.5 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 text-sm focus:outline-none focus:ring-2 focus:ring-warm-600 dark:focus:ring-amber-500">
                <option value="Reflexiones">Reflexiones</option>
                <option value="Filosofía">Filosofía</option>
                <option value="Historias">Historias</option>
                <option value="Poesía">Poesía</option>
              </select>
            </div>

            <div>
              <label class="block text-xs font-bold uppercase tracking-wider text-warm-700 dark:text-zinc-300 mb-2">
                Tiempo Est. de Lectura (min)
              </label>
              <input type="number" id="post-readtime" min="1" max="60" value="3" class="w-full px-4 py-2.5 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 text-sm focus:outline-none focus:ring-2 focus:ring-warm-600 dark:focus:ring-amber-500">
            </div>
          </div>

          <!-- Section Selection (Admin privilege) -->
          <div id="admin-section-picker" class="hidden bg-amber-50 dark:bg-amber-950/30 border border-amber-200 dark:border-amber-900/50 p-4 rounded-xl">
            <label class="block text-xs font-bold uppercase tracking-wider text-amber-800 dark:text-amber-300 mb-2">
              <i class="fa-solid fa-shield-halved mr-1"></i> Opciones de Administrador: Destino del Escrito
            </label>
            <div class="flex items-center space-x-6 text-sm font-medium">
              <label class="inline-flex items-center cursor-pointer">
                <input type="radio" name="post-section" value="principal" checked class="text-amber-600 focus:ring-amber-500">
                <span class="ml-2">Escritos Principales (Página Oficial)</span>
              </label>
              <label class="inline-flex items-center cursor-pointer">
                <input type="radio" name="post-section" value="comunidad" class="text-amber-600 focus:ring-amber-500">
                <span class="ml-2">Sección Comunidad</span>
              </label>
            </div>
          </div>

          <!-- Content Body -->
          <div>
            <label class="block text-xs font-bold uppercase tracking-wider text-warm-700 dark:text-zinc-300 mb-2">
              Contenido *
            </label>
            <textarea id="post-content" rows="12" required placeholder="Escribe aquí tus párrafos... Puedes usar saltos de línea normales." class="w-full px-4 py-3 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 font-serif text-base leading-relaxed focus:outline-none focus:ring-2 focus:ring-warm-600 dark:focus:ring-amber-500"></textarea>
          </div>

          <!-- Actions -->
          <div class="flex items-center justify-end space-x-4 pt-4 border-t border-warm-200 dark:border-zinc-800">
            <button type="button" onclick="navigateTo('principal')" class="px-5 py-2.5 rounded-xl border border-warm-300 dark:border-zinc-700 text-sm font-semibold hover:bg-warm-100 dark:hover:bg-zinc-800">
              Cancelar
            </button>
            <button type="submit" id="submit-post-btn" class="px-6 py-2.5 rounded-xl bg-warm-800 hover:bg-warm-900 dark:bg-amber-600 dark:hover:bg-amber-500 text-white text-sm font-bold shadow-md transition-all">
              <i class="fa-solid fa-paper-plane mr-2"></i>Publicar Escrito
            </button>
          </div>
        </form>
      </div>
    </section>


    <!-- VIEW 4: PERFIL Y AUTENTICACIÓN / MODO ADMIN -->
    <section id="view-perfil" class="hidden max-w-2xl mx-auto space-y-6">
      
      <!-- Current Status Card -->
      <div class="bg-warm-50 dark:bg-zinc-900 border border-warm-200 dark:border-zinc-800 rounded-2xl p-6 shadow-md text-center">
        <div id="profile-avatar-large" class="w-20 h-20 rounded-full bg-warm-700 dark:bg-amber-600 text-white font-bold text-3xl flex items-center justify-center mx-auto mb-4 shadow-lg">
          ?
        </div>
        <h2 id="profile-display-name" class="font-display text-2xl font-bold">Invitado</h2>
        <p id="profile-email" class="text-sm text-warm-600 dark:text-zinc-400">Sin sesión iniciada</p>
        
        <div class="mt-4 inline-flex items-center px-3 py-1 rounded-full text-xs font-bold uppercase tracking-wider" id="profile-role-pill">
          Rol: Usuario Visitante
        </div>
      </div>

      <!-- Admin Password Elevation Box -->
      <div class="bg-gradient-to-br from-amber-500/10 to-amber-700/10 border border-amber-500/30 rounded-2xl p-6 shadow-md">
        <h3 class="font-display text-lg font-bold text-warm-900 dark:text-amber-300 flex items-center gap-2">
          <i class="fa-solid fa-key text-amber-600"></i> Acceso Propietario / Modo Administrador
        </h3>
        <p class="text-xs text-warm-700 dark:text-zinc-400 mt-1 mb-4">
          Ingresa la clave maestra para activar los privilegios de edición, moderación y publicación en la sección principal.
        </p>

        <div class="flex gap-2">
          <input type="password" id="admin-key-input" placeholder="Clave de Administrador..." class="flex-grow px-4 py-2.5 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 text-sm focus:outline-none focus:ring-2 focus:ring-amber-500">
          <button onclick="unlockAdminWithKey()" class="px-5 py-2.5 rounded-xl bg-amber-600 hover:bg-amber-700 text-white text-sm font-bold transition-all shadow-md">
            Desbloquear Admin
          </button>
        </div>
        <span class="text-[11px] text-warm-500 dark:text-zinc-500 mt-2 block italic">Pista de prueba: prueba la clave <b>admin123</b></span>
      </div>

      <!-- Quick Auth Form -->
      <div class="bg-warm-50 dark:bg-zinc-900 border border-warm-200 dark:border-zinc-800 rounded-2xl p-6 shadow-md space-y-4">
        <h3 class="font-display text-lg font-bold">Opciones de Registro e Identificación</h3>
        
        <div class="space-y-3">
          <button onclick="loginWithGoogle()" class="w-full flex items-center justify-center gap-3 px-4 py-3 border border-warm-300 dark:border-zinc-700 rounded-xl font-semibold text-sm hover:bg-warm-100 dark:hover:bg-zinc-800 transition-colors">
            <i class="fa-brands fa-google text-red-500 text-base"></i>
            Continuar con Cuenta de Google
          </button>
          
          <div class="relative flex py-2 items-center">
            <div class="flex-grow border-t border-warm-200 dark:border-zinc-800"></div>
            <span class="flex-shrink mx-4 text-xs text-warm-400">o nombre personalizado</span>
            <div class="flex-grow border-t border-warm-200 dark:border-zinc-800"></div>
          </div>

          <div class="space-y-2">
            <input type="text" id="custom-username-input" placeholder="Tu nombre o seudónimo literario..." class="w-full px-4 py-2.5 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 text-sm focus:outline-none focus:ring-2 focus:ring-warm-600">
            <button onclick="setCustomUser()" class="w-full py-2.5 rounded-xl bg-warm-800 dark:bg-zinc-700 hover:bg-warm-900 text-white font-bold text-sm">
              Guardar Perfil
            </button>
          </div>
        </div>
      </div>
    </section>

  </main>


  <!-- MODAL: READER / FULL ARTICLE VIEW -->
  <div id="reader-modal" class="fixed inset-0 z-50 hidden overflow-y-auto bg-zinc-950/70 backdrop-blur-sm flex justify-center p-2 sm:p-4 md:p-6">
    <div class="relative w-full max-w-3xl bg-warm-50 dark:bg-zinc-900 my-auto rounded-2xl border border-warm-200 dark:border-zinc-800 shadow-2xl overflow-hidden flex flex-col max-h-[92vh]">
      
      <!-- Sticky Modal Top Bar -->
      <div class="flex items-center justify-between px-6 py-4 border-b border-warm-200 dark:border-zinc-800 bg-warm-100/80 dark:bg-zinc-900/80 backdrop-blur-md">
        <div class="flex items-center space-x-2 text-xs font-semibold text-warm-600 dark:text-amber-500">
          <span id="reader-category" class="px-2.5 py-1 bg-warm-200 dark:bg-zinc-800 rounded-full uppercase tracking-wider">Reflexiones</span>
          <span>•</span>
          <span id="reader-readtime">3 min de lectura</span>
        </div>
        
        <button onclick="closeReaderModal()" class="w-8 h-8 rounded-full flex items-center justify-center bg-warm-200 dark:bg-zinc-800 text-warm-800 dark:text-zinc-200 hover:bg-warm-300 transition-colors">
          <i class="fa-solid fa-xmark"></i>
        </button>
      </div>

      <!-- Modal Body (Scrollable) -->
      <div class="p-6 sm:p-10 overflow-y-auto space-y-8">
        
        <!-- Article Header -->
        <div class="space-y-4 text-center sm:text-left border-b border-warm-200 dark:border-zinc-800 pb-6">
          <h1 id="reader-title" class="font-display text-3xl sm:text-4xl md:text-5xl font-bold text-warm-900 dark:text-warm-100 leading-tight">
            Título del Escrito
          </h1>
          <div class="flex items-center justify-center sm:justify-start space-x-3 text-sm text-warm-600 dark:text-zinc-400">
            <div id="reader-author-avatar" class="w-8 h-8 rounded-full bg-warm-700 text-white font-bold flex items-center justify-center text-xs">
              A
            </div>
            <div>
              <span id="reader-author" class="font-bold text-warm-900 dark:text-warm-200">Nombre Autor</span>
              <span class="mx-1.5">•</span>
              <span id="reader-date">24 Oct, 2026</span>
            </div>
          </div>
        </div>

        <!-- Article Content Prose -->
        <article id="reader-content" class="prose-editorial text-warm-900 dark:text-zinc-200 whitespace-pre-line space-y-4">
          <!-- Text dynamically loaded -->
        </article>

        <!-- Reactions / Claps Section -->
        <div class="pt-8 border-t border-warm-200 dark:border-zinc-800 flex items-center justify-between">
          <button onclick="handleClap()" id="clap-btn" class="group flex items-center space-x-3 px-5 py-2.5 rounded-full bg-warm-200 dark:bg-zinc-800 hover:bg-amber-100 dark:hover:bg-amber-950/40 text-warm-800 dark:text-amber-400 font-bold transition-all transform active:scale-95 border border-warm-300 dark:border-zinc-700">
            <i class="fa-solid fa-hands-clapping text-xl group-hover:scale-125 transition-transform text-amber-600"></i>
            <span>Aplausos</span>
            <span id="reader-claps-count" class="bg-warm-300 dark:bg-zinc-700 px-2.5 py-0.5 rounded-full text-xs">0</span>
          </button>

          <div id="admin-article-controls" class="hidden flex items-center space-x-2">
            <!-- Admin Buttons populated via JS -->
          </div>
        </div>

        <!-- COMMENTS SECTION -->
        <section class="pt-8 border-t border-warm-200 dark:border-zinc-800 space-y-6">
          <h3 class="font-display text-2xl font-bold text-warm-900 dark:text-warm-100 flex items-center gap-2">
            <i class="fa-regular fa-comments text-amber-600"></i>
            Comentarios y Respuestas
          </h3>

          <!-- New Comment Input -->
          <div class="space-y-3">
            <textarea id="comment-input" rows="3" placeholder="Añade tu reflexión o respuesta respetuosa sobre este texto..." class="w-full px-4 py-3 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 text-sm focus:outline-none focus:ring-2 focus:ring-warm-600"></textarea>
            <div class="flex justify-end">
              <button onclick="submitComment()" class="px-5 py-2 rounded-xl bg-warm-800 dark:bg-amber-600 hover:bg-warm-900 text-white text-xs font-bold transition-all">
                Publicar Comentario
              </button>
            </div>
          </div>

          <!-- Comment List -->
          <div id="comments-list" class="space-y-4 pt-2">
            <!-- Dynamically populated comments -->
          </div>
        </section>

      </div>
    </div>
  </div>


  <!-- CUSTOM TOAST NOTIFICATION CONTAINER -->
  <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>


  <!-- FOOTER -->
  <footer class="mt-auto border-t border-warm-200 dark:border-zinc-800 bg-warm-50 dark:bg-zinc-900 py-8 transition-colors">
    <div class="max-w-6xl mx-auto px-4 text-center space-y-2">
      <p class="font-display font-semibold text-warm-900 dark:text-warm-100">Ecos y Reflexiones</p>
      <p class="text-xs text-warm-600 dark:text-zinc-400 font-serif">Un espacio personal y colectivo para pensar la vida a través de las letras.</p>
      <p class="text-[11px] text-warm-400 dark:text-zinc-600 pt-2">© 2026 Ecos y Reflexiones. Todos los derechos reservados.</p>
    </div>
  </footer>


  <!-- FIREBASE & APP LOGIC MODULE -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
    import { 
      getAuth, 
      signInAnonymously, 
      signInWithCustomToken, 
      GoogleAuthProvider, 
      signInWithPopup, 
      signOut, 
      onAuthStateChanged 
    } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
    import { 
      getFirestore, 
      doc, 
      getDoc, 
      setDoc, 
      updateDoc, 
      deleteDoc, 
      collection, 
      onSnapshot, 
      addDoc 
    } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

    // --- FIREBASE INITIALIZATION & CONFIG ---
    const appId = typeof __app_id !== 'undefined' ? __app_id : 'ecos-reflexiones-app';
    const firebaseConfig = typeof __firebase_config !== 'undefined' 
      ? JSON.parse(__firebase_config) 
      : {
          apiKey: "demo-api-key",
          authDomain: "demo-app.firebaseapp.com",
          projectId: "demo-app",
          storageBucket: "demo-app.appspot.com",
          messagingSenderId: "123456789",
          appId: "1:123456789:web:abcdef"
        };

    const app = initializeApp(firebaseConfig);
    const auth = getAuth(app);
    const db = getFirestore(app);

    // --- HELPER TIMEOUT & LOCAL STORAGE FALLBACKS ---
    function timeoutPromise(promise, ms = 2500) {
      return new Promise((resolve, reject) => {
        const timer = setTimeout(() => reject(new Error("Database timeout")), ms);
        promise.then(
          (res) => { clearTimeout(timer); resolve(res); },
          (err) => { clearTimeout(timer); reject(err); }
        );
      });
    }

    function savePostsToLocal() {
      try {
        localStorage.setItem('ecos_local_posts', JSON.stringify(state.posts));
      } catch (e) { console.warn("Local storage write error:", e); }
    }

    function loadPostsFromLocal() {
      try {
        const saved = localStorage.getItem('ecos_local_posts');
        if (saved) return JSON.parse(saved);
      } catch (e) { console.warn("Local storage read error:", e); }
      return null;
    }

    // --- APP STATE ---
    let state = {
      currentUser: {
        uid: null,
        displayName: 'Invitado',
        email: '',
        isAdmin: false
      },
      activeTab: 'principal',
      categoryFilter: 'Todos',
      posts: [],
      comments: [],
      activePostId: null,
      theme: localStorage.getItem('ecos_theme') || 'light'
    };

    // Firebase strict paths
    const POSTS_COLLECTION = collection(db, 'artifacts', appId, 'public', 'data', 'posts');
    const COMMENTS_COLLECTION = collection(db, 'artifacts', appId, 'public', 'data', 'comments');

    // --- SEED SAMPLE DATA IF FIRESTORE IS EMPTY ---
    const SAMPLE_POSTS = [
      {
        title: "El arte de la pausa en un mundo acelerado",
        category: "Reflexiones",
        readTime: 4,
        section: "principal",
        authorName: "Administrador (Creador)",
        authorUid: "admin_master",
        content: `Vivimos sumergidos en una vorágine ininterrumpida de estímulos, notificaciones y urgencias artificiales. Nos hemos acostumbrado a medir el valor del día por la cantidad de tareas tachadas en una lista interminable. Sin embargo, en el fondo sabemos que la verdadera sustancia de la vida ocurre precisamente en los intersticios, en esos silencios entre nota y nota.\n\nHacer una pausa no es perder el tiempo; es recuperar la perspectiva. Cuando nos detenemos a contemplar el atardecer o a escuchar con atención sincera a un amigo, restablecemos el contacto con lo esencial. Apaguemos los dispositivos por un momento y reaprendamos a habitarnos.`,
        claps: 18,
        createdAt: new Date().toISOString()
      },
      {
        title: "Sobre los libros que nos leen a nosotros",
        category: "Filosofía",
        readTime: 5,
        section: "principal",
        authorName: "Administrador (Creador)",
        authorUid: "admin_master",
        content: `A menudo pensamos que somos nosotros quienes elegimos y devoramos las obras literarias. Pero existen ciertos libros raros y luminosos que invierten la ecuación: cuando abrimos sus páginas, son ellos los que nos examinan, revelando rincones oscuros y anhelos olvidados de nuestra propia psique.\n\nUn buen texto funciona como un espejo pulido. No te ofrece respuestas masticadas, sino que te devuelve tus preguntas con una claridad renovada. ¿Cuál ha sido ese escrito que cambió tu manera de mirar el mundo?`,
        claps: 24,
        createdAt: new Date(Date.now() - 86400000).toISOString()
      },
      {
        title: "Un café al atardecer en el viejo barrio",
        category: "Historias",
        readTime: 3,
        section: "comunidad",
        authorName: "Lucía M.",
        authorUid: "user_sample_1",
        content: `Ayer me senté en la esquina de siempre. El olor a grano tostado se mezclaba con la brisa fresca de otoño. Una anciana alimentaba a las palomas con migas de pan mientras le sonreía a un niño. En ese instante comprendí que la felicidad no es una meta lejana, sino la suma de pequeños fotogramas cotidianos que solemos ignorar por andar con prisa.`,
        claps: 9,
        createdAt: new Date(Date.now() - 172800000).toISOString()
      }
    ];

    // --- INITIALIZATION LOGIC ---
    window.addEventListener('DOMContentLoaded', async () => {
      applyTheme(state.theme);
      setupAuth();
    });

    async function setupAuth() {
      try {
        if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
          await signInWithCustomToken(auth, __initial_auth_token);
        } else {
          await signInAnonymously(auth);
        }
      } catch (err) {
        console.warn("Auth initial fallback:", err);
      }

      onAuthStateChanged(auth, (user) => {
        if (user) {
          state.currentUser.uid = user.uid;
          if (user.displayName) state.currentUser.displayName = user.displayName;
          if (user.email) state.currentUser.email = user.email;
        } else {
          state.currentUser.uid = 'guest_' + Math.random().toString(36).substring(2, 8);
        }
        updateUserUI();
        attachFirestoreListeners();
      });
    }

    // --- FIRESTORE REALTIME LISTENERS ---
    function attachFirestoreListeners() {
      // Load cached/local posts immediately for fast UI rendering
      const localPosts = loadPostsFromLocal();
      if (localPosts && localPosts.length > 0) {
        state.posts = localPosts;
        renderAllViews();
      }

      if (!auth.currentUser && !state.currentUser.uid) return;

      // Listen to Posts
      onSnapshot(POSTS_COLLECTION, (snapshot) => {
        const postsList = [];
        snapshot.forEach(docSnap => {
          postsList.push({ id: docSnap.id, ...docSnap.data() });
        });

        if (postsList.length === 0 && (!localPosts || localPosts.length === 0)) {
          seedDatabase();
          return;
        }

        if (postsList.length > 0) {
          state.posts = postsList.sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));
          savePostsToLocal();
          renderAllViews();
        }
      }, (error) => {
        console.warn("Firestore snapshot error, using local state:", error);
        if (!state.posts || state.posts.length === 0) {
          state.posts = SAMPLE_POSTS;
          renderAllViews();
        }
      });

      // Listen to Comments
      onSnapshot(COMMENTS_COLLECTION, (snapshot) => {
        const commentsList = [];
        snapshot.forEach(docSnap => {
          commentsList.push({ id: docSnap.id, ...docSnap.data() });
        });
        if (commentsList.length > 0) {
          state.comments = commentsList.sort((a, b) => new Date(a.createdAt) - new Date(b.createdAt));
          if (state.activePostId) {
            renderComments(state.activePostId);
          }
        }
      }, (error) => {
        console.warn("Firestore comments error:", error);
      });
    }

    async function seedDatabase() {
      try {
        for (const p of SAMPLE_POSTS) {
          await addDoc(POSTS_COLLECTION, p);
        }
      } catch (e) {
        console.error("Error seeding DB:", e);
      }
    }

    // --- THEME MANAGEMENT ---
    window.toggleDarkMode = function() {
      state.theme = state.theme === 'light' ? 'dark' : 'light';
      localStorage.setItem('ecos_theme', state.theme);
      applyTheme(state.theme);
    };

    function applyTheme(theme) {
      const html = document.documentElement;
      const themeIcon = document.getElementById('theme-icon');
      if (theme === 'dark') {
        html.classList.add('dark');
        themeIcon.className = 'fa-solid fa-sun text-lg';
      } else {
        html.classList.remove('dark');
        themeIcon.className = 'fa-solid fa-moon text-lg';
      }
    }

    // --- NAVIGATION TABS ---
    window.navigateTo = function(tabName) {
      state.activeTab = tabName;
      
      // Toggle Views
      ['principal', 'comunidad', 'escribir', 'perfil'].forEach(tab => {
        const viewEl = document.getElementById(`view-${tab}`);
        const navEl = document.getElementById(`nav-${tab}`);
        if (tab === tabName) {
          viewEl.classList.remove('hidden');
          if (navEl) navEl.classList.add('bg-warm-200', 'dark:bg-zinc-800', 'text-warm-900', 'dark:text-amber-400', 'font-bold');
        } else {
          viewEl.classList.add('hidden');
          if (navEl) navEl.classList.remove('bg-warm-200', 'dark:bg-zinc-800', 'text-warm-900', 'dark:text-amber-400', 'font-bold');
        }
      });

      // Special handling for Escribir (Show Admin options if admin)
      if (tabName === 'escribir') {
        const adminPicker = document.getElementById('admin-section-picker');
        if (state.currentUser.isAdmin) {
          adminPicker.classList.remove('hidden');
        } else {
          adminPicker.classList.add('hidden');
        }
      }

      window.scrollTo({ top: 0, behavior: 'smooth' });
    };

    // --- USER MANAGEMENT & ADMIN UNLOCK ---
    window.unlockAdminWithKey = function() {
      const input = document.getElementById('admin-key-input');
      const val = input.value.trim();

      // Master key check (e.g., 'admin123' or 'admin')
      if (val === 'admin123' || val.toLowerCase() === 'admin') {
        state.currentUser.isAdmin = true;
        state.currentUser.displayName = "Propietario / Admin";
        input.value = '';
        showToast("¡Modo Administrador Activado con éxito!", "success");
        updateUserUI();
        renderAllViews();
      } else {
        showToast("Clave incorrecta. Inténtalo de nuevo.", "error");
      }
    };

    window.loginWithGoogle = async function() {
      try {
        const provider = new GoogleAuthProvider();
        const res = await signInWithPopup(auth, provider);
        state.currentUser.displayName = res.user.displayName || 'Usuario Google';
        state.currentUser.email = res.user.email || '';
        showToast(`Bienvenido/a, ${state.currentUser.displayName}`, "success");
        updateUserUI();
      } catch (err) {
        showToast("No se pudo iniciar sesión con Google.", "error");
      }
    };

    window.setCustomUser = function() {
      const nameInput = document.getElementById('custom-username-input');
      if (!nameInput.value.trim()) return;
      state.currentUser.displayName = nameInput.value.trim();
      showToast(`Perfil actualizado a "${state.currentUser.displayName}"`, "info");
      updateUserUI();
    };

    function updateUserUI() {
      const avatarEl = document.getElementById('user-avatar');
      const avatarLargeEl = document.getElementById('profile-avatar-large');
      const nameEl = document.getElementById('user-name');
      const profileNameEl = document.getElementById('profile-display-name');
      const profileEmailEl = document.getElementById('profile-email');
      const adminBadge = document.getElementById('admin-badge');
      const rolePill = document.getElementById('profile-role-pill');

      const initial = (state.currentUser.displayName || '?').charAt(0).toUpperCase();
      avatarEl.textContent = initial;
      avatarLargeEl.textContent = initial;
      nameEl.textContent = state.currentUser.displayName;
      profileNameEl.textContent = state.currentUser.displayName;
      profileEmailEl.textContent = state.currentUser.email || 'Usuario Registrado';

      if (state.currentUser.isAdmin) {
        adminBadge.classList.remove('hidden');
        rolePill.className = "mt-4 inline-flex items-center px-3 py-1 rounded-full text-xs font-bold uppercase tracking-wider bg-amber-600 text-white shadow";
        rolePill.textContent = "Rol: Administrador Propietario";
      } else {
        adminBadge.classList.add('hidden');
        rolePill.className = "mt-4 inline-flex items-center px-3 py-1 rounded-full text-xs font-bold uppercase tracking-wider bg-warm-200 dark:bg-zinc-800 text-warm-800 dark:text-zinc-300";
        rolePill.textContent = "Rol: Miembro / Comunidad";
      }
    }

    // --- RENDER VIEWS ---
    function renderAllViews() {
      renderPrincipalPosts();
      renderCommunityPosts();
    }

    function renderPrincipalPosts() {
      const container = document.getElementById('grid-principal');
      const principalPosts = state.posts.filter(p => p.section === 'principal');

      if (principalPosts.length === 0) {
        container.innerHTML = `
          <div class="col-span-full text-center py-12 text-warm-500 font-serif">
            Aún no hay escritos en la sección principal.
          </div>
        `;
        return;
      }

      container.innerHTML = principalPosts.map(post => `
        <div onclick="openReaderModal('${post.id}')" class="group cursor-pointer bg-warm-50 dark:bg-zinc-900 border border-warm-200 dark:border-zinc-800 rounded-2xl p-6 shadow-sm hover:shadow-xl transition-all duration-300 flex flex-col justify-between hover:-translate-y-1">
          <div class="space-y-3">
            <div class="flex items-center justify-between text-xs font-bold uppercase tracking-wider text-amber-700 dark:text-amber-500">
              <span class="px-2.5 py-0.5 rounded-full bg-amber-100 dark:bg-amber-950/60">${post.category}</span>
              <span><i class="fa-regular fa-clock mr-1"></i>${post.readTime || 3} min</span>
            </div>
            
            <h4 class="font-display text-2xl font-bold text-warm-900 dark:text-warm-100 group-hover:text-amber-700 dark:group-hover:text-amber-400 transition-colors line-clamp-2 leading-snug">
              ${escapeHtml(post.title)}
            </h4>
            
            <p class="font-serif text-sm text-warm-700 dark:text-zinc-300 line-clamp-3 leading-relaxed">
              ${escapeHtml(post.content)}
            </p>
          </div>

          <div class="pt-6 mt-4 border-t border-warm-200/60 dark:border-zinc-800/60 flex items-center justify-between text-xs text-warm-500 dark:text-zinc-400">
            <span class="font-bold text-warm-800 dark:text-zinc-200">${escapeHtml(post.authorName || 'Autor')}</span>
            <div class="flex items-center space-x-3">
              <span><i class="fa-solid fa-hands-clapping text-amber-600 mr-1"></i>${post.claps || 0}</span>
              <span>${formatDate(post.createdAt)}</span>
            </div>
          </div>
        </div>
      `).join('');
    }

    window.setCategoryFilter = function(cat) {
      state.categoryFilter = cat;
      document.querySelectorAll('#category-filters button').forEach(btn => {
        if (btn.textContent.trim() === cat) {
          btn.className = "cat-btn active-cat px-3 py-1.5 rounded-full text-xs font-semibold bg-warm-800 dark:bg-amber-600 text-white shadow";
        } else {
          btn.className = "cat-btn px-3 py-1.5 rounded-full text-xs font-semibold bg-warm-200 dark:bg-zinc-800 text-warm-800 dark:text-zinc-300 hover:bg-warm-300";
        }
      });
      renderCommunityPosts();
    };

    window.renderCommunityPosts = function() {
      const container = document.getElementById('grid-comunidad');
      const searchVal = (document.getElementById('search-input')?.value || '').toLowerCase();

      let filtered = state.posts.filter(p => p.section === 'comunidad');

      if (state.categoryFilter !== 'Todos') {
        filtered = filtered.filter(p => p.category === state.categoryFilter);
      }

      if (searchVal) {
        filtered = filtered.filter(p => 
          p.title.toLowerCase().includes(searchVal) ||
          p.content.toLowerCase().includes(searchVal) ||
          (p.authorName && p.authorName.toLowerCase().includes(searchVal))
        );
      }

      if (filtered.length === 0) {
        container.innerHTML = `
          <div class="col-span-full text-center py-16 bg-warm-50 dark:bg-zinc-900 rounded-2xl border border-dashed border-warm-300 dark:border-zinc-800">
            <i class="fa-solid fa-pen-fountain text-3xl text-warm-400 mb-3 block"></i>
            <p class="font-serif text-warm-600 dark:text-zinc-400">No se encontraron escritos en esta categoría.</p>
            <button onclick="navigateTo('escribir')" class="mt-4 px-4 py-2 bg-warm-800 dark:bg-amber-600 text-white text-xs font-bold rounded-xl shadow">
              Sé el primero en escribir
            </button>
          </div>
        `;
        return;
      }

      container.innerHTML = filtered.map(post => `
        <div class="bg-warm-50 dark:bg-zinc-900 border border-warm-200 dark:border-zinc-800 rounded-2xl p-6 shadow-sm hover:shadow-lg transition-all flex flex-col justify-between">
          <div class="space-y-3">
            <div class="flex items-center justify-between text-xs font-semibold text-warm-500">
              <span class="px-2 py-0.5 rounded bg-warm-200 dark:bg-zinc-800 text-warm-800 dark:text-zinc-300 uppercase">${post.category}</span>
              <span>${post.readTime || 3} min</span>
            </div>

            <h4 onclick="openReaderModal('${post.id}')" class="font-display text-xl font-bold cursor-pointer text-warm-900 dark:text-warm-100 hover:text-amber-600 transition-colors leading-snug line-clamp-2">
              ${escapeHtml(post.title)}
            </h4>

            <p onclick="openReaderModal('${post.id}')" class="font-serif text-xs text-warm-700 dark:text-zinc-300 line-clamp-3 leading-relaxed cursor-pointer">
              ${escapeHtml(post.content)}
            </p>
          </div>

          <div class="pt-4 mt-4 border-t border-warm-200/60 dark:border-zinc-800/60 space-y-3">
            <div class="flex items-center justify-between text-xs text-warm-500">
              <span class="font-semibold text-warm-800 dark:text-zinc-200">${escapeHtml(post.authorName || 'Anónimo')}</span>
              <div class="flex items-center gap-2">
                <span><i class="fa-solid fa-hands-clapping text-amber-600"></i> ${post.claps || 0}</span>
              </div>
            </div>

            <!-- Admin action bar for community posts -->
            ${state.currentUser.isAdmin ? `
              <div class="pt-2 flex items-center justify-between text-[11px] bg-amber-50 dark:bg-amber-950/40 px-2.5 py-1.5 rounded-lg border border-amber-200 dark:border-amber-900/40">
                <span class="font-bold text-amber-800 dark:text-amber-400">Admin:</span>
                <div class="flex gap-2">
                  <button onclick="promotePost('${post.id}')" class="text-amber-700 dark:text-amber-300 hover:underline font-semibold" title="Mover a Sección Principal">
                    <i class="fa-solid fa-arrow-up-right-from-square mr-1"></i>Promover
                  </button>
                  <button onclick="deletePost('${post.id}')" class="text-red-600 dark:text-red-400 hover:underline font-semibold">
                    <i class="fa-solid fa-trash mr-1"></i>Borrar
                  </button>
                </div>
              </div>
            ` : ''}
          </div>
        </div>
      `).join('');
    };

    // --- FORM SUBMISSION ---
    window.handlePostSubmit = async function(e) {
      e.preventDefault();
      
      const title = document.getElementById('post-title').value.trim();
      const category = document.getElementById('post-category').value;
      const readTime = parseInt(document.getElementById('post-readtime').value) || 3;
      const content = document.getElementById('post-content').value.trim();
      
      let section = 'comunidad';
      if (state.currentUser.isAdmin) {
        const selectedRadio = document.querySelector('input[name="post-section"]:checked');
        if (selectedRadio) section = selectedRadio.value;
      }

      if (!title || !content) {
        showToast("Por favor completa los campos obligatorios.", "error");
        return;
      }

      const submitBtn = document.getElementById('submit-post-btn');
      submitBtn.disabled = true;
      submitBtn.innerHTML = `<i class="fa-solid fa-spinner fa-spin mr-2"></i>Guardando...`;

      const newPost = {
        id: 'post_' + Date.now() + '_' + Math.random().toString(36).substring(2, 7),
        title,
        category,
        readTime,
        content,
        section,
        authorName: state.currentUser.displayName || 'Escritor de la Comunidad',
        authorUid: state.currentUser.uid || 'anon',
        claps: 0,
        createdAt: new Date().toISOString()
      };

      try {
        // Attempt cloud write with 2.5s timeout
        await timeoutPromise(addDoc(POSTS_COLLECTION, newPost), 2500);
        showToast("¡Escrito publicado con éxito!", "success");
      } catch (err) {
        console.warn("Cloud publish timed out/failed. Saving locally:", err);
        // Fallback: save to local memory & localStorage
        state.posts.unshift(newPost);
        savePostsToLocal();
        renderAllViews();
        showToast("¡Escrito publicado localmente!", "success");
      } finally {
        // ALWAYS restore submit button and navigate
        submitBtn.disabled = false;
        submitBtn.innerHTML = `<i class="fa-solid fa-paper-plane mr-2"></i>Publicar Escrito`;
        document.getElementById('post-form').reset();
        navigateTo(section);
      }
    };

    // --- READER MODAL & INTERACTIONS ---
    window.openReaderModal = function(postId) {
      const post = state.posts.find(p => p.id === postId);
      if (!post) return;

      state.activePostId = postId;
      
      document.getElementById('reader-title').textContent = post.title;
      document.getElementById('reader-category').textContent = post.category;
      document.getElementById('reader-readtime').textContent = `${post.readTime || 3} min de lectura`;
      document.getElementById('reader-author').textContent = post.authorName || 'Autor';
      document.getElementById('reader-author-avatar').textContent = (post.authorName || 'A').charAt(0).toUpperCase();
      document.getElementById('reader-date').textContent = formatDate(post.createdAt);
      document.getElementById('reader-content').textContent = post.content;
      document.getElementById('reader-claps-count').textContent = post.claps || 0;

      // Admin Controls inside reader
      const adminControls = document.getElementById('admin-article-controls');
      if (state.currentUser.isAdmin) {
        adminControls.classList.remove('hidden');
        adminControls.innerHTML = `
          <button onclick="promotePost('${post.id}')" class="px-3 py-1.5 bg-amber-600 text-white rounded-lg text-xs font-bold shadow hover:bg-amber-700">
            ${post.section === 'principal' ? 'Mover a Comunidad' : 'Promover a Principal'}
          </button>
          <button onclick="deletePost('${post.id}')" class="px-3 py-1.5 bg-red-600 text-white rounded-lg text-xs font-bold shadow hover:bg-red-700">
            Eliminar
          </button>
        `;
      } else {
        adminControls.classList.add('hidden');
      }

      renderComments(postId);
      document.getElementById('reader-modal').classList.remove('hidden');
      document.body.style.overflow = 'hidden';
    };

    window.closeReaderModal = function() {
      document.getElementById('reader-modal').classList.add('hidden');
      document.body.style.overflow = '';
      state.activePostId = null;
    };

    window.handleClap = async function() {
      if (!state.activePostId) return;
      const post = state.posts.find(p => p.id === state.activePostId);
      if (!post) return;

      const newClaps = (post.claps || 0) + 1;
      post.claps = newClaps;
      document.getElementById('reader-claps-count').textContent = newClaps;
      renderAllViews();
      savePostsToLocal();

      try {
        const postRef = doc(db, 'artifacts', appId, 'public', 'data', 'posts', state.activePostId);
        await timeoutPromise(updateDoc(postRef, { claps: newClaps }), 2000);
      } catch (err) {
        console.warn("Claps update saved locally:", err);
      }
    };

    // --- COMMENTS SYSTEM ---
    async function renderComments(postId) {
      const container = document.getElementById('comments-list');
      const postComments = state.comments.filter(c => c.postId === postId);

      if (postComments.length === 0) {
        container.innerHTML = `
          <p class="text-xs text-warm-500 italic">Aún no hay comentarios. Sé el primero en iniciar el diálogo.</p>
        `;
        return;
      }

      container.innerHTML = postComments.map(c => `
        <div class="bg-warm-100 dark:bg-zinc-800/60 p-4 rounded-xl border border-warm-200 dark:border-zinc-700/60 space-y-2">
          <div class="flex items-center justify-between text-xs">
            <div class="flex items-center space-x-2">
              <span class="font-bold text-warm-900 dark:text-warm-100">${escapeHtml(c.authorName)}</span>
              <span class="text-warm-400">•</span>
              <span class="text-warm-500 dark:text-zinc-400">${formatDate(c.createdAt)}</span>
            </div>
            ${(state.currentUser.isAdmin || state.currentUser.uid === c.authorUid) ? `
              <button onclick="deleteComment('${c.id}')" class="text-red-500 hover:text-red-700 text-[11px] font-semibold">
                Borrar
              </button>
            ` : ''}
          </div>
          <p class="text-sm font-serif text-warm-800 dark:text-zinc-200 leading-relaxed">
            ${escapeHtml(c.text)}
          </p>
        </div>
      `).join('');
    }

    window.submitComment = async function() {
      if (!state.activePostId) return;
      const input = document.getElementById('comment-input');
      const text = input.value.trim();

      if (!text) {
        showToast("Escribe un comentario antes de enviar.", "error");
        return;
      }

      const commentData = {
        id: 'comm_' + Date.now() + '_' + Math.random().toString(36).substring(2, 6),
        postId: state.activePostId,
        text,
        authorName: state.currentUser.displayName || 'Lector Anónimo',
        authorUid: state.currentUser.uid || 'anon',
        createdAt: new Date().toISOString()
      };

      // Add to local state first for instant response
      state.comments.push(commentData);
      renderComments(state.activePostId);
      input.value = '';
      showToast("Comentario publicado", "success");

      try {
        await timeoutPromise(addDoc(COMMENTS_COLLECTION, commentData), 2000);
      } catch (err) {
        console.warn("Comment saved locally:", err);
      }
    };

    window.deleteComment = async function(commentId) {
      state.comments = state.comments.filter(c => c.id !== commentId);
      if (state.activePostId) renderComments(state.activePostId);
      showToast("Comentario eliminado", "info");

      try {
        const commentRef = doc(db, 'artifacts', appId, 'public', 'data', 'comments', commentId);
        await timeoutPromise(deleteDoc(commentRef), 2000);
      } catch (err) {
        console.warn("Comment deleted locally:", err);
      }
    };

    // --- ADMIN ACTIONS: PROMOTE & DELETE ---
    window.promotePost = async function(postId) {
      if (!state.currentUser.isAdmin) return;
      const post = state.posts.find(p => p.id === postId);
      if (!post) return;

      const newSection = post.section === 'principal' ? 'comunidad' : 'principal';
      post.section = newSection;
      renderAllViews();
      savePostsToLocal();
      showToast(`Escrito movido a: ${newSection === 'principal' ? 'Sección Principal' : 'Comunidad'}`, "success");
      if (state.activePostId === postId) closeReaderModal();

      try {
        const postRef = doc(db, 'artifacts', appId, 'public', 'data', 'posts', postId);
        await timeoutPromise(updateDoc(postRef, { section: newSection }), 2000);
      } catch (err) {
        console.warn("Section update saved locally:", err);
      }
    };

    window.deletePost = async function(postId) {
      if (!state.currentUser.isAdmin) return;
      state.posts = state.posts.filter(p => p.id !== postId);
      renderAllViews();
      savePostsToLocal();
      showToast("Escrito eliminado.", "info");
      if (state.activePostId === postId) closeReaderModal();

      try {
        const postRef = doc(db, 'artifacts', appId, 'public', 'data', 'posts', postId);
        await timeoutPromise(deleteDoc(postRef), 2000);
      } catch (err) {
        console.warn("Post deleted locally:", err);
      }
    };

    // --- READER MODAL & INTERACTIONS ---
    window.openReaderModal = function(postId) {
      const post = state.posts.find(p => p.id === postId);
      if (!post) return;

      state.activePostId = postId;
      
      document.getElementById('reader-title').textContent = post.title;
      document.getElementById('reader-category').textContent = post.category;
      document.getElementById('reader-readtime').textContent = `${post.readTime || 3} min de lectura`;
      document.getElementById('reader-author').textContent = post.authorName || 'Autor';
      document.getElementById('reader-author-avatar').textContent = (post.authorName || 'A').charAt(0).toUpperCase();
      document.getElementById('reader-date').textContent = formatDate(post.createdAt);
      document.getElementById('reader-content').textContent = post.content;
      document.getElementById('reader-claps-count').textContent = post.claps || 0;

      // Admin Controls inside reader
      const adminControls = document.getElementById('admin-article-controls');
      if (state.currentUser.isAdmin) {
        adminControls.classList.remove('hidden');
        adminControls.innerHTML = `
          <button onclick="promotePost('${post.id}')" class="px-3 py-1.5 bg-amber-600 text-white rounded-lg text-xs font-bold shadow hover:bg-amber-700">
            ${post.section === 'principal' ? 'Mover a Comunidad' : 'Promover a Principal'}
          </button>
          <button onclick="deletePost('${post.id}')" class="px-3 py-1.5 bg-red-600 text-white rounded-lg text-xs font-bold shadow hover:bg-red-700">
            Eliminar
          </button>
        `;
      } else {
        adminControls.classList.add('hidden');
      }

      renderComments(postId);
      document.getElementById('reader-modal').classList.remove('hidden');
      document.body.style.overflow = 'hidden';
    };

    window.closeReaderModal = function() {
      document.getElementById('reader-modal').classList.add('hidden');
      document.body.style.overflow = '';
      state.activePostId = null;
    };

    window.handleClap = async function() {
      if (!state.activePostId) return;
      const post = state.posts.find(p => p.id === state.activePostId);
      if (!post) return;

      const newClaps = (post.claps || 0) + 1;
      document.getElementById('reader-claps-count').textContent = newClaps;

      try {
        const postRef = doc(db, 'artifacts', appId, 'public', 'data', 'posts', state.activePostId);
        await updateDoc(postRef, { claps: newClaps });
      } catch (err) {
        console.error("Error updating claps:", err);
      }
    };

    // --- COMMENTS SYSTEM ---
    async function renderComments(postId) {
      const container = document.getElementById('comments-list');
      const postComments = state.comments.filter(c => c.postId === postId);

      if (postComments.length === 0) {
        container.innerHTML = `
          <p class="text-xs text-warm-500 italic">Aún no hay comentarios. Sé el primero en iniciar el diálogo.</p>
        `;
        return;
      }

      container.innerHTML = postComments.map(c => `
        <div class="bg-warm-100 dark:bg-zinc-800/60 p-4 rounded-xl border border-warm-200 dark:border-zinc-700/60 space-y-2">
          <div class="flex items-center justify-between text-xs">
            <div class="flex items-center space-x-2">
              <span class="font-bold text-warm-900 dark:text-warm-100">${escapeHtml(c.authorName)}</span>
              <span class="text-warm-400">•</span>
              <span class="text-warm-500 dark:text-zinc-400">${formatDate(c.createdAt)}</span>
            </div>
            ${(state.currentUser.isAdmin || state.currentUser.uid === c.authorUid) ? `
              <button onclick="deleteComment('${c.id}')" class="text-red-500 hover:text-red-700 text-[11px] font-semibold">
                Borrar
              </button>
            ` : ''}
          </div>
          <p class="text-sm font-serif text-warm-800 dark:text-zinc-200 leading-relaxed">
            ${escapeHtml(c.text)}
          </p>
        </div>
      `).join('');
    }

    window.submitComment = async function() {
      if (!state.activePostId) return;
      const input = document.getElementById('comment-input');
      const text = input.value.trim();

      if (!text) {
        showToast("Escribe un comentario antes de enviar.", "error");
        return;
      }

      try {
        const commentData = {
          postId: state.activePostId,
          text,
          authorName: state.currentUser.displayName || 'Lector Anónimo',
          authorUid: state.currentUser.uid || 'anon',
          createdAt: new Date().toISOString()
        };

        await addDoc(COMMENTS_COLLECTION, commentData);
        input.value = '';
        showToast("Comentario añadido", "success");
      } catch (err) {
        console.error("Error adding comment:", err);
        showToast("Error al publicar el comentario.", "error");
      }
    };

    window.deleteComment = async function(commentId) {
      try {
        const commentRef = doc(db, 'artifacts', appId, 'public', 'data', 'comments', commentId);
        await deleteDoc(commentRef);
        showToast("Comentario eliminado", "info");
      } catch (err) {
        showToast("No se pudo eliminar el comentario.", "error");
      }
    };

    // --- ADMIN ACTIONS: PROMOTE & DELETE ---
    window.promotePost = async function(postId) {
      if (!state.currentUser.isAdmin) return;
      const post = state.posts.find(p => p.id === postId);
      if (!post) return;

      const newSection = post.section === 'principal' ? 'comunidad' : 'principal';
      try {
        const postRef = doc(db, 'artifacts', appId, 'public', 'data', 'posts', postId);
        await updateDoc(postRef, { section: newSection });
        showToast(`Escrito movido a: ${newSection === 'principal' ? 'Sección Principal' : 'Comunidad'}`, "success");
        if (state.activePostId === postId) closeReaderModal();
      } catch (err) {
        showToast("Error al promover el escrito.", "error");
      }
    };

    window.deletePost = async function(postId) {
      if (!state.currentUser.isAdmin) return;
      try {
        const postRef = doc(db, 'artifacts', appId, 'public', 'data', 'posts', postId);
        await deleteDoc(postRef);
        showToast("Escrito eliminado del sistema.", "info");
        if (state.activePostId === postId) closeReaderModal();
      } catch (err) {
        showToast("Error al eliminar el escrito.", "error");
      }
    };

    // --- UTILITIES ---
    function showToast(msg, type = "info") {
      const container = document.getElementById('toast-container');
      const toast = document.createElement('div');
      
      let bg = "bg-warm-900 text-white";
      if (type === "success") bg = "bg-emerald-700 text-white";
      if (type === "error") bg = "bg-rose-700 text-white";

      toast.className = `${bg} px-4 py-3 rounded-xl shadow-2xl text-xs font-semibold flex items-center space-x-2 transition-all transform translate-y-2 opacity-0 pointer-events-auto`;
      toast.innerHTML = `<span>${escapeHtml(msg)}</span>`;

      container.appendChild(toast);

      setTimeout(() => {
        toast.classList.remove('translate-y-2', 'opacity-0');
      }, 10);

      setTimeout(() => {
        toast.classList.add('opacity-0', 'translate-y-2');
        setTimeout(() => toast.remove(), 300);
      }, 3500);
    }

    function formatDate(dateStr) {
      if (!dateStr) return '';
      const d = new Date(dateStr);
      return d.toLocaleDateString('es-ES', { day: 'numeric', month: 'short', year: 'numeric' });
    }

    function escapeHtml(str) {
      if (!str) return '';
      return str.replace(/[&<>"']/g, function(m) {
        return {
          '&': '&amp;',
          '<': '&lt;',
          '>': '&gt;',
          '"': '&quot;',
          "'": '&#039;'
        }[m];
      });
    }

    // Set default active tab UI
    navigateTo('principal');
  </script>
</body>
</html>
