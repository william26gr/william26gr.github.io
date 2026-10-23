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
    /* Custom Smooth Scrollbar */
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
      line-height: 1.85;
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
        <div class="flex items-center space-x-3 cursor-pointer" onclick="switchTab('principal')">
          <div class="w-10 h-10 rounded-full bg-warm-700 text-warm-50 dark:bg-amber-600 flex items-center justify-center font-display font-bold text-xl shadow-md">
            E
          </div>
          <div>
            <div class="flex items-center gap-2">
              <h1 id="site-title" class="font-display text-xl sm:text-2xl font-bold tracking-tight text-warm-900 dark:text-warm-100">
                Ecos y Reflexiones
              </h1>
              <button onclick="editSiteText('site-title')" class="admin-edit-btn hidden text-xs text-amber-600 hover:underline" title="Editar Título Principal">
                <i class="fa-solid fa-pen-to-square"></i>
              </button>
            </div>
            <div class="flex items-center gap-2">
              <p id="site-subtitle" class="text-xs text-warm-600 dark:text-amber-500 font-serif italic hidden sm:block">
                Un refugio para las palabras de la vida
              </p>
              <button onclick="editSiteText('site-subtitle')" class="admin-edit-btn hidden text-xs text-amber-600 hover:underline" title="Editar Subtítulo Principal">
                <i class="fa-solid fa-pen-to-square"></i>
              </button>
            </div>
          </div>
        </div>

        <!-- Navigation Tabs Desktop -->
        <nav class="hidden md:flex space-x-1 lg:space-x-2">
          <button onclick="switchTab('principal')" id="nav-principal" class="px-4 py-2 rounded-xl text-sm font-medium transition-all duration-200">
            <i class="fa-solid fa-feather-pointed mr-2"></i>Escritos Principales
          </button>
          <button onclick="switchTab('comunidad')" id="nav-comunidad" class="px-4 py-2 rounded-xl text-sm font-medium transition-all duration-200">
            <i class="fa-solid fa-users mr-2"></i>Comunidad
          </button>
          <button onclick="switchTab('escribir')" id="nav-escribir" class="px-4 py-2 rounded-xl text-sm font-medium transition-all duration-200">
            <i class="fa-solid fa-pen-nib mr-2"></i>Escribir
          </button>
        </nav>

        <!-- User Controls & Dark Mode -->
        <div class="flex items-center space-x-3">
          <!-- Dark Mode Toggle -->
          <button onclick="toggleDarkMode()" class="p-2.5 rounded-full text-warm-700 dark:text-amber-400 hover:bg-warm-200 dark:hover:bg-zinc-800 transition-colors" title="Cambiar tema">
            <i id="theme-icon" class="fa-solid fa-moon text-lg"></i>
          </button>

          <!-- User Pill -->
          <button onclick="switchTab('perfil')" id="user-pill" class="flex items-center space-x-2 px-3 py-1.5 rounded-full border border-warm-300 dark:border-zinc-700 hover:border-warm-500 transition-all bg-warm-50 dark:bg-zinc-800">
            <div id="user-avatar" class="w-6 h-6 rounded-full bg-warm-600 dark:bg-amber-600 text-white text-xs flex items-center justify-center font-bold">
              ?
            </div>
            <span id="user-name" class="text-xs font-semibold max-w-[90px] truncate">Invitado</span>
            <span id="admin-badge" class="hidden px-1.5 py-0.5 text-[10px] font-bold uppercase tracking-wider bg-amber-600 text-white rounded shadow">Admin</span>
          </button>
        </div>
      </div>
    </div>

    <!-- Mobile Navigation Bar (Bottom) -->
    <div class="md:hidden border-t border-warm-200 dark:border-zinc-800 bg-warm-50 dark:bg-zinc-900 flex justify-around py-2 text-xs font-medium">
      <button onclick="switchTab('principal')" id="mobile-nav-principal" class="flex flex-col items-center p-1 text-warm-800 dark:text-zinc-300">
        <i class="fa-solid fa-feather-pointed text-base mb-1"></i>
        <span>Inicio</span>
      </button>
      <button onclick="switchTab('comunidad')" id="mobile-nav-comunidad" class="flex flex-col items-center p-1 text-warm-800 dark:text-zinc-300">
        <i class="fa-solid fa-users text-base mb-1"></i>
        <span>Comunidad</span>
      </button>
      <button onclick="switchTab('escribir')" id="mobile-nav-escribir" class="flex flex-col items-center p-1 text-warm-800 dark:text-zinc-300">
        <i class="fa-solid fa-pen-nib text-base mb-1"></i>
        <span>Escribir</span>
      </button>
      <button onclick="switchTab('perfil')" id="mobile-nav-perfil" class="flex flex-col items-center p-1 text-warm-800 dark:text-zinc-300">
        <i class="fa-solid fa-user text-base mb-1"></i>
        <span>Perfil</span>
      </button>
    </div>
  </header>

  <!-- MAIN CONTAINER -->
  <main class="flex-grow max-w-6xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8">

    <!-- VIEW 1: ESCRITOS PRINCIPALES -->
    <section id="view-principal" class="space-y-8">
      <!-- Hero Banner -->
      <div class="relative overflow-hidden rounded-3xl bg-gradient-to-r from-warm-800 via-warm-900 to-zinc-900 text-warm-100 p-8 sm:p-12 shadow-xl border border-warm-700/30">
        <div class="absolute -right-10 -bottom-10 opacity-10 text-white pointer-events-none">
          <i class="fa-solid fa-book-open text-[240px]"></i>
        </div>
        <div class="relative z-10 max-w-2xl space-y-4">
          <span class="inline-block px-3 py-1 bg-amber-600/30 border border-amber-500/40 text-amber-300 rounded-full text-xs font-semibold tracking-wider uppercase">
            Canal Principal del Autor
          </span>
          
          <div class="flex items-center gap-2">
            <h2 id="hero-title" class="font-display text-3xl sm:text-5xl font-bold tracking-wide leading-tight">
              Reflexiones sobre la condición humana y el paso del tiempo.
            </h2>
            <button onclick="editSiteText('hero-title')" class="admin-edit-btn hidden text-sm text-amber-400 hover:underline">
              <i class="fa-solid fa-pen-to-square"></i>
            </button>
          </div>

          <div class="flex items-center gap-2">
            <p id="hero-subtitle" class="text-warm-200 text-base sm:text-lg font-serif italic">
              "No vivimos los días; vivimos las pausas que dejamos entre ellos."
            </p>
            <button onclick="editSiteText('hero-subtitle')" class="admin-edit-btn hidden text-sm text-amber-400 hover:underline">
              <i class="fa-solid fa-pen-to-square"></i>
            </button>
          </div>
        </div>
      </div>

      <!-- Articles Section Header -->
      <div class="space-y-6">
        <div class="flex flex-col sm:flex-row sm:items-center justify-between border-b border-warm-200 dark:border-zinc-800 pb-3 gap-3">
          <div class="flex items-center gap-2">
            <h3 id="principal-section-title" class="font-display text-2xl font-bold text-warm-900 dark:text-warm-100 flex items-center gap-2">
              <i class="fa-solid fa-star text-amber-600 text-lg"></i>
              Ensayos y Escritos Destacados
            </h3>
            <button onclick="editSiteText('principal-section-title')" class="admin-edit-btn hidden text-xs text-amber-600 hover:underline">
              <i class="fa-solid fa-pen-to-square"></i>
            </button>
          </div>

          <!-- BOTÓN DE DESCARGA DE ESCRITOS PRINCIPALES -->
          <button onclick="downloadPrincipalPosts()" class="inline-flex items-center space-x-2 px-4 py-2 rounded-xl bg-warm-200 dark:bg-zinc-800 hover:bg-warm-300 dark:hover:bg-zinc-700 text-warm-900 dark:text-zinc-100 text-xs font-bold transition-all border border-warm-300 dark:border-zinc-700 shadow-sm">
            <i class="fa-solid fa-file-arrow-down text-amber-600 text-sm"></i>
            <span>Descargar Escritos (.TXT)</span>
          </button>
        </div>

        <!-- Featured Grid -->
        <div id="grid-principal" class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <!-- Dynamically populated -->
        </div>
      </div>
    </section>


    <!-- VIEW 2: COMUNIDAD -->
    <section id="view-comunidad" class="hidden space-y-8">
      <div class="flex flex-col md:flex-row md:items-center md:justify-between gap-4 border-b border-warm-200 dark:border-zinc-800 pb-6">
        <div>
          <div class="flex items-center gap-2">
            <h2 id="community-title" class="font-display text-3xl font-bold text-warm-900 dark:text-warm-100">
              Voces de la Comunidad
            </h2>
            <button onclick="editSiteText('community-title')" class="admin-edit-btn hidden text-xs text-amber-600 hover:underline">
              <i class="fa-solid fa-pen-to-square"></i>
            </button>
          </div>

          <div class="flex items-center gap-2 mt-1">
            <p id="community-subtitle" class="text-sm text-warm-600 dark:text-zinc-400">
              Espacio abierto donde lectores y autores comparten sus propias visiones del mundo.
            </p>
            <button onclick="editSiteText('community-subtitle')" class="admin-edit-btn hidden text-xs text-amber-600 hover:underline">
              <i class="fa-solid fa-pen-to-square"></i>
            </button>
          </div>
        </div>

        <!-- Category Filters -->
        <div class="flex flex-wrap gap-2" id="category-filters">
          <!-- Filter buttons rendered dynamically -->
        </div>
      </div>

      <!-- Search Input -->
      <div class="relative max-w-md">
        <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-warm-400"></i>
        <input type="text" id="search-input" oninput="onSearchInput(event)" placeholder="Buscar por título, contenido o autor..." class="w-full pl-10 pr-4 py-2.5 rounded-xl border border-warm-300 dark:border-zinc-700 bg-warm-50 dark:bg-zinc-900 text-sm focus:outline-none focus:ring-2 focus:ring-warm-600 dark:focus:ring-amber-500">
      </div>

      <!-- Community Grid -->
      <div id="grid-comunidad" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <!-- Dynamically populated -->
      </div>
    </section>


    <!-- VIEW 3: ESCRIBIR / PUBLICAR -->
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

        <form id="post-form" onsubmit="submitNewPost(event)" class="space-y-6">
          <div>
            <label class="block text-xs font-bold uppercase tracking-wider text-warm-700 dark:text-zinc-300 mb-2">
              Título del Escrito *
            </label>
            <input type="text" id="post-title" required placeholder="Ej. La quietud de las primeras horas" class="w-full px-4 py-3 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 text-base font-serif focus:outline-none focus:ring-2 focus:ring-warm-600 dark:focus:ring-amber-500">
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
            <div>
              <label class="block text-xs font-bold uppercase tracking-wider text-warm-700 dark:text-zinc-300 mb-2">
                Categoría *
              </label>
              <select id="post-category" onchange="handleCategoryChange(event)" class="w-full px-4 py-2.5 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 text-sm focus:outline-none focus:ring-2 focus:ring-warm-600 dark:focus:ring-amber-500">
                <option value="Reflexiones">Reflexiones</option>
                <option value="Filosofía">Filosofía</option>
                <option value="Historias">Historias</option>
                <option value="Poesía">Poesía</option>
                <option value="Vida">Vida</option>
                <option value="NEW_CUSTOM">+ Otra categoría...</option>
              </select>
              
              <!-- Campo dinámico para escribir categoría propia -->
              <input type="text" id="custom-category-input" placeholder="Escribe el tema..." class="hidden mt-2 w-full px-3 py-2 rounded-xl border border-amber-300 dark:border-amber-700 bg-white dark:bg-zinc-800 text-xs focus:outline-none focus:ring-2 focus:ring-amber-500">
            </div>

            <div>
              <label class="block text-xs font-bold uppercase tracking-wider text-warm-700 dark:text-zinc-300 mb-2">
                Tu Nombre / Seudónimo
              </label>
              <input type="text" id="post-author" placeholder="Ej. Gabriel M." class="w-full px-4 py-2.5 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 text-sm focus:outline-none focus:ring-2 focus:ring-warm-600 dark:focus:ring-amber-500">
            </div>

            <div>
              <label class="block text-xs font-bold uppercase tracking-wider text-warm-700 dark:text-zinc-300 mb-2">
                Tiempo Lectura (min)
              </label>
              <input type="number" id="post-readtime" min="1" max="60" value="3" class="w-full px-4 py-2.5 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 text-sm focus:outline-none focus:ring-2 focus:ring-warm-600 dark:focus:ring-amber-500">
            </div>
          </div>

          <!-- Section Selection (Admin privilege) -->
          <div id="admin-section-picker" class="hidden bg-amber-50 dark:bg-amber-950/30 border border-amber-200 dark:border-amber-900/50 p-4 rounded-xl">
            <label class="block text-xs font-bold uppercase tracking-wider text-amber-800 dark:text-amber-300 mb-2">
              <i class="fa-solid fa-shield-halved mr-1"></i> Opción Administrador: Ubicación del Escrito
            </label>
            <div class="flex items-center space-x-6 text-sm font-medium">
              <label class="inline-flex items-center cursor-pointer">
                <input type="radio" name="post-section" value="principal" checked class="text-amber-600 focus:ring-amber-500">
                <span class="ml-2">Escritos Principales (Canal Oficial)</span>
              </label>
              <label class="inline-flex items-center cursor-pointer">
                <input type="radio" name="post-section" value="comunidad" class="text-amber-600 focus:ring-amber-500">
                <span class="ml-2">Sección Comunidad</span>
              </label>
            </div>
          </div>

          <div>
            <label class="block text-xs font-bold uppercase tracking-wider text-warm-700 dark:text-zinc-300 mb-2">
              Contenido del Escrito *
            </label>
            <textarea id="post-content" rows="10" required placeholder="Escribe aquí tus reflexiones... Puedes incluir párrafos bien definidos." class="w-full px-4 py-3 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 font-serif text-base leading-relaxed focus:outline-none focus:ring-2 focus:ring-warm-600 dark:focus:ring-amber-500"></textarea>
          </div>

          <div class="flex items-center justify-end space-x-4 pt-4 border-t border-warm-200 dark:border-zinc-800">
            <button type="button" onclick="switchTab('principal')" class="px-5 py-2.5 rounded-xl border border-warm-300 dark:border-zinc-700 text-sm font-semibold hover:bg-warm-100 dark:hover:bg-zinc-800">
              Cancelar
            </button>
            <button type="submit" id="submit-post-btn" class="px-6 py-2.5 rounded-xl bg-warm-800 hover:bg-warm-900 dark:bg-amber-600 dark:hover:bg-amber-500 text-white text-sm font-bold shadow-md transition-all">
              <i class="fa-solid fa-paper-plane mr-2"></i>Publicar Escrito
            </button>
          </div>
        </form>
      </div>
    </section>


    <!-- VIEW 4: PERFIL Y MODO ADMIN -->
    <section id="view-perfil" class="hidden max-w-2xl mx-auto space-y-6">
      
      <!-- Current Status Card -->
      <div class="bg-warm-50 dark:bg-zinc-900 border border-warm-200 dark:border-zinc-800 rounded-2xl p-6 shadow-md text-center">
        <div id="profile-avatar-large" class="w-20 h-20 rounded-full bg-warm-700 dark:bg-amber-600 text-white font-bold text-3xl flex items-center justify-center mx-auto mb-4 shadow-lg">
          ?
        </div>
        <h2 id="profile-display-name" class="font-display text-2xl font-bold">Invitado</h2>
        <p id="profile-role-desc" class="text-sm text-warm-600 dark:text-zinc-400 mt-1">Lector de la plataforma</p>
        
        <div class="mt-4 inline-flex items-center px-3 py-1 rounded-full text-xs font-bold uppercase tracking-wider" id="profile-role-pill">
          Rol: Usuario Visitante
        </div>

        <div id="logout-container" class="mt-4 hidden">
          <button onclick="logout()" class="text-xs font-bold text-rose-600 hover:underline">
            <i class="fa-solid fa-right-from-bracket mr-1"></i> Salir del modo Administrador
          </button>
        </div>
      </div>

      <!-- Admin Password Elevation Box -->
      <div class="bg-gradient-to-br from-amber-500/10 to-amber-700/10 border border-amber-500/30 rounded-2xl p-6 shadow-md">
        <h3 class="font-display text-lg font-bold text-warm-900 dark:text-amber-300 flex items-center gap-2">
          <i class="fa-solid fa-key text-amber-600"></i> Acceso Propietario / Código de Administrador
        </h3>
        <p class="text-xs text-warm-700 dark:text-zinc-400 mt-1 mb-4">
          Introduce tu código maestro para activar los privilegios de edición, moderación y edición de títulos de la web.
        </p>

        <div class="flex gap-2">
          <input type="password" id="admin-key-input" placeholder="Ingresa tu código..." class="flex-grow px-4 py-2.5 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 text-sm focus:outline-none focus:ring-2 focus:ring-amber-500">
          <button onclick="loginAdminWithCode()" class="px-5 py-2.5 rounded-xl bg-amber-600 hover:bg-amber-700 text-white text-sm font-bold transition-all shadow-md">
            Desbloquear Admin
          </button>
        </div>
      </div>

      <!-- Quick Auth / Custom Username Form -->
      <div class="bg-warm-50 dark:bg-zinc-900 border border-warm-200 dark:border-zinc-800 rounded-2xl p-6 shadow-md space-y-4">
        <h3 class="font-display text-lg font-bold">Personalizar Tu Nombre de Autor</h3>
        
        <div class="space-y-3">
          <input type="text" id="custom-username-input" placeholder="Tu nombre o firma literaria..." class="w-full px-4 py-2.5 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 text-sm focus:outline-none focus:ring-2 focus:ring-warm-600">
          
          <div class="flex gap-3">
            <button onclick="setCustomUser()" class="flex-1 py-2.5 rounded-xl bg-warm-800 dark:bg-zinc-700 hover:bg-warm-900 text-white font-bold text-sm shadow">
              Guardar Nombre
            </button>
            
            <!-- BOTÓN PARA PONER EL NOMBRE PREDETERMINADO "ANÓNIMO" -->
            <button onclick="setAnonymousUser()" class="px-4 py-2.5 rounded-xl bg-warm-200 dark:bg-zinc-800 hover:bg-warm-300 text-warm-800 dark:text-zinc-300 font-bold text-sm border border-warm-300 dark:border-zinc-700">
              Poner "Anónimo"
            </button>
          </div>
        </div>
      </div>
    </section>

  </main>


  <!-- MODAL: ARTICLE READER OVERLAY (DESPLAZAMIENTO LIBRE CORREGIDO) -->
  <div id="post-modal" class="fixed inset-0 z-50 hidden overflow-y-auto bg-zinc-950/75 backdrop-blur-sm p-3 sm:p-6 flex items-start justify-center" onclick="handleModalBackdropClick(event)">
    <div class="relative w-full max-w-3xl bg-warm-50 dark:bg-zinc-900 my-8 rounded-2xl border border-warm-200 dark:border-zinc-800 shadow-2xl overflow-hidden flex flex-col">
      
      <!-- Top Bar -->
      <div class="sticky top-0 z-10 flex items-center justify-between px-6 py-4 border-b border-warm-200 dark:border-zinc-800 bg-warm-50/95 dark:bg-zinc-900/95 backdrop-blur-md">
        <div class="flex items-center space-x-2 text-xs font-semibold text-warm-600 dark:text-amber-500">
          <span id="modal-category" class="px-2.5 py-1 bg-warm-200 dark:bg-zinc-800 rounded-full uppercase tracking-wider">Reflexiones</span>
          <span>•</span>
          <span id="modal-readtime">3 min de lectura</span>
        </div>
        
        <button onclick="closePostModal()" class="w-8 h-8 rounded-full flex items-center justify-center bg-warm-200 dark:bg-zinc-800 text-warm-800 dark:text-zinc-200 hover:bg-warm-300 dark:hover:bg-zinc-700 transition-colors">
          <i class="fa-solid fa-xmark text-lg"></i>
        </button>
      </div>

      <!-- Modal Body -->
      <div class="p-6 sm:p-10 space-y-8">
        
        <!-- Header -->
        <div class="space-y-4 text-left border-b border-warm-200 dark:border-zinc-800 pb-6">
          <h1 id="modal-title" class="font-display text-2xl sm:text-4xl font-bold text-warm-900 dark:text-warm-100 leading-tight">
            Título del Escrito
          </h1>
          <div class="flex items-center space-x-3 text-sm text-warm-600 dark:text-zinc-400">
            <div id="modal-author-avatar" class="w-8 h-8 rounded-full bg-warm-700 text-white font-bold flex items-center justify-center text-xs">
              A
            </div>
            <div>
              <span id="modal-author" class="font-bold text-warm-900 dark:text-warm-200">Nombre Autor</span>
              <span class="mx-1.5">•</span>
              <span id="modal-date">24 Oct, 2026</span>
            </div>
          </div>
        </div>

        <!-- Article Content -->
        <article id="modal-content" class="prose-editorial text-warm-900 dark:text-zinc-200 whitespace-pre-line space-y-4">
          <!-- Main Content -->
        </article>

        <!-- Actions Bar -->
        <div class="pt-6 border-t border-warm-200 dark:border-zinc-800 flex flex-wrap items-center justify-between gap-4">
          <button onclick="likePost()" id="like-btn" class="flex items-center space-x-3 px-5 py-2.5 rounded-full bg-warm-200 dark:bg-zinc-800 hover:bg-amber-100 dark:hover:bg-amber-950/40 text-warm-800 dark:text-amber-400 font-bold transition-all transform active:scale-95 border border-warm-300 dark:border-zinc-700">
            <i class="fa-solid fa-hands-clapping text-xl text-amber-600"></i>
            <span>Aplausos</span>
            <span id="modal-likes-count" class="bg-warm-300 dark:bg-zinc-700 px-2.5 py-0.5 rounded-full text-xs">0</span>
          </button>

          <div id="modal-admin-actions" class="hidden flex items-center space-x-2">
            <!-- Dynamic Admin Controls -->
          </div>
        </div>

        <!-- Comments Section -->
        <section class="pt-8 border-t border-warm-200 dark:border-zinc-800 space-y-6">
          <h3 class="font-display text-xl font-bold text-warm-900 dark:text-warm-100 flex items-center gap-2">
            <i class="fa-regular fa-comments text-amber-600"></i>
            Comentarios y Respuestas
          </h3>

          <form onsubmit="addComment(event)" class="space-y-3">
            <div class="flex gap-3">
              <input type="text" id="comment-author-input" placeholder="Tu nombre..." class="w-1/3 px-3 py-2 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 text-xs focus:outline-none focus:ring-2 focus:ring-warm-600">
              <input type="text" id="comment-text-input" required placeholder="Escribe tu reflexión o respuesta..." class="flex-grow px-4 py-2 rounded-xl border border-warm-300 dark:border-zinc-700 bg-white dark:bg-zinc-800 text-xs focus:outline-none focus:ring-2 focus:ring-warm-600">
            </div>
            <div class="flex justify-end">
              <button type="submit" class="px-5 py-2 rounded-xl bg-warm-800 dark:bg-amber-600 hover:bg-warm-900 text-white text-xs font-bold transition-all shadow">
                Enviar Comentario
              </button>
            </div>
          </form>

          <div id="modal-comments-list" class="space-y-3 pt-2">
            <!-- Comments List -->
          </div>
        </section>

      </div>
    </div>
  </div>


  <!-- TOAST CONTAINER -->
  <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>


  <!-- FOOTER -->
  <footer class="mt-auto border-t border-warm-200 dark:border-zinc-800 bg-warm-50 dark:bg-zinc-900 py-8 transition-colors">
    <div class="max-w-6xl mx-auto px-4 text-center space-y-2">
      <p id="footer-title" class="font-display font-semibold text-warm-900 dark:text-warm-100">Ecos y Reflexiones</p>
      <p id="footer-subtitle" class="text-xs text-warm-600 dark:text-zinc-400 font-serif">Un espacio personal y colectivo para pensar la vida a través de las letras.</p>
      <p class="text-[11px] text-warm-400 dark:text-zinc-600 pt-2">© 2026 Ecos y Reflexiones. Todos los derechos reservados.</p>
    </div>
  </footer>


  <!-- APPLICATION LOGIC & FIREBASE INTEGRATION -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
    import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
    import { getFirestore, collection, doc, addDoc, updateDoc, deleteDoc, onSnapshot } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

    // --- SEED POSTS FOR FIRST LOAD ---
    const SEED_POSTS = [
      {
        id: "seed-1",
        title: "El arte de la pausa en un mundo acelerado",
        category: "Reflexiones",
        readTime: 4,
        section: "principal",
        authorName: "Administrador (Creador)",
        authorUid: "admin",
        content: "Vivimos sumergidos en una vorágine ininterrumpida de estímulos, notificaciones y urgencias artificiales. Nos hemos acostumbrado a medir el valor del día por la cantidad de tareas tachadas en una lista interminable. Sin embargo, en el fondo sabemos que la verdadera sustancia de la vida ocurre precisamente en los intersticios, en esos silencios entre nota y nota.\n\nHacer una pausa no es perder el tiempo; es recuperar la perspectiva. Cuando nos detenemos a contemplar el atardecer o a escuchar con atención sincera a un amigo, restablecemos el contacto con lo esencial.",
        claps: 32,
        createdAt: new Date().toISOString()
      },
      {
        id: "seed-2",
        title: "Sobre los libros que nos leen a nosotros",
        category: "Filosofía",
        readTime: 5,
        section: "principal",
        authorName: "Administrador (Creador)",
        authorUid: "admin",
        content: "A menudo pensamos que somos nosotros quienes elegimos y devoramos las obras literarias. Pero existen ciertos libros raros y luminosos que invierten la ecuación: cuando abrimos sus páginas, son ellos los que nos examinan, revelando rincones oscuros y anhelos olvidados de nuestra propia psique.\n\nUn buen texto funciona como un espejo pulido. No te ofrece respuestas masticadas, sino que te devuelve tus preguntas con una claridad renovada.",
        claps: 27,
        createdAt: new Date(Date.now() - 86400000).toISOString()
      },
      {
        id: "seed-3",
        title: "Un café al atardecer en el viejo barrio",
        category: "Historias",
        readTime: 3,
        section: "comunidad",
        authorName: "Lucía M.",
        authorUid: "user-1",
        content: "Ayer me senté en la esquina de siempre. El olor a grano tostado se mezclaba con la brisa fresca de otoño. Una anciana alimentaba a las palomas con migas de pan mientras le sonreía a un niño. En ese instante comprendí que la felicidad no es una meta lejana, sino la suma de pequeños fotogramas cotidianos que solemos ignorar por andar con prisa.",
        claps: 14,
        createdAt: new Date(Date.now() - 172800000).toISOString()
      },
      {
        id: "seed-4",
        title: "Cartas al tiempo que se fue",
        category: "Poesía",
        readTime: 2,
        section: "comunidad",
        authorName: "Carlos R.",
        authorUid: "user-2",
        content: "No le pido al tiempo que regrese,\nni que detenga sus manecillas doradas,\nsólo le agradezco las huellas suaves\nque dejó grabadas en la mirada.",
        claps: 19,
        createdAt: new Date(Date.now() - 250000000).toISOString()
      }
    ];

    let CATEGORIES = ["Todos", "Reflexiones", "Filosofía", "Historias", "Poesía", "Vida"];

    // --- APPLICATION STATE ---
    let state = {
      activeTab: 'principal',
      categoryFilter: 'Todos',
      searchQuery: '',
      darkMode: localStorage.getItem('ecos_theme') === 'dark',
      currentUser: {
        name: localStorage.getItem('ecos_username') || 'Anónimo',
        isAdmin: localStorage.getItem('ecos_is_admin') === 'true',
        uid: null
      },
      customTitles: JSON.parse(localStorage.getItem('ecos_titles') || '{}'),
      posts: [],
      comments: [],
      activePostId: null
    };

    // --- INITIALIZE DATA FROM LOCALSTORAGE OR SEED ---
    function loadSavedState() {
      try {
        const localPosts = localStorage.getItem('ecos_posts');
        if (localPosts) {
          state.posts = JSON.parse(localPosts);
        } else {
          state.posts = [...SEED_POSTS];
          localStorage.setItem('ecos_posts', JSON.stringify(state.posts));
        }

        const localComments = localStorage.getItem('ecos_comments');
        if (localComments) {
          state.comments = JSON.parse(localComments);
        } else {
          state.comments = [
            { id: 'c1', postId: 'seed-1', authorName: 'Elena V.', text: 'Hermosa reflexión. A veces olvidamos respirar.', createdAt: new Date().toISOString() }
          ];
        }

        // Cargar categorías guardadas dinámicas
        state.posts.forEach(p => {
          if (p.category && !CATEGORIES.includes(p.category)) {
            CATEGORIES.push(p.category);
          }
        });

      } catch (e) {
        console.warn("LocalStorage parse error, using defaults:", e);
        state.posts = [...SEED_POSTS];
      }
    }

    function saveStateToLocal() {
      try {
        localStorage.setItem('ecos_posts', JSON.stringify(state.posts));
        localStorage.setItem('ecos_comments', JSON.stringify(state.comments));
        localStorage.setItem('ecos_is_admin', state.currentUser.isAdmin);
        localStorage.setItem('ecos_username', state.currentUser.name);
        localStorage.setItem('ecos_titles', JSON.stringify(state.customTitles));
      } catch (e) {
        console.warn("LocalStorage save error:", e);
      }
    }

    // --- FIREBASE SETUP WITH FALLBACK ---
    let db = null;
    let appId = typeof __app_id !== 'undefined' ? __app_id : 'ecos-app';

    try {
      if (typeof __firebase_config !== 'undefined') {
        const firebaseConfig = JSON.parse(__firebase_config);
        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        db = getFirestore(app);

        if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
          signInWithCustomToken(auth, __initial_auth_token).catch(() => signInAnonymously(auth));
        } else {
          signInAnonymously(auth).catch(() => {});
        }

        onAuthStateChanged(auth, (user) => {
          if (user) state.currentUser.uid = user.uid;
        });

        const postsCol = collection(db, 'artifacts', appId, 'public', 'data', 'posts');
        onSnapshot(postsCol, (snapshot) => {
          if (!snapshot.empty) {
            const remotePosts = [];
            snapshot.forEach(docSnap => remotePosts.push({ id: docSnap.id, ...docSnap.data() }));
            if (remotePosts.length > 0) {
              state.posts = remotePosts.sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));
              saveStateToLocal();
              renderApp();
            }
          }
        }, (err) => console.warn("Firestore snapshot skipped:", err));

      }
    } catch (e) {
      console.warn("Running in local offline mode:", e);
    }

    // --- RENDER FUNCTIONS ---
    function renderApp() {
      // Dark mode class
      if (state.darkMode) {
        document.documentElement.classList.add('dark');
        document.getElementById('theme-icon').className = 'fa-solid fa-sun text-lg text-amber-400';
      } else {
        document.documentElement.classList.remove('dark');
        document.getElementById('theme-icon').className = 'fa-solid fa-moon text-lg text-warm-700';
      }

      // Aplica títulos personalizados
      Object.keys(state.customTitles).forEach(id => {
        const el = document.getElementById(id);
        if (el) el.textContent = state.customTitles[id];
      });

      // Tab visibility
      ['principal', 'comunidad', 'escribir', 'perfil'].forEach(tab => {
        const viewEl = document.getElementById(`view-${tab}`);
        const navEl = document.getElementById(`nav-${tab}`);
        const mobNavEl = document.getElementById(`mobile-nav-${tab}`);

        if (tab === state.activeTab) {
          viewEl?.classList.remove('hidden');
          navEl?.classList.add('bg-warm-200', 'dark:bg-zinc-800', 'text-warm-900', 'dark:text-amber-400', 'font-bold');
          mobNavEl?.classList.add('text-amber-600', 'font-bold');
        } else {
          viewEl?.classList.add('hidden');
          navEl?.classList.remove('bg-warm-200', 'dark:bg-zinc-800', 'text-warm-900', 'dark:text-amber-400', 'font-bold');
          mobNavEl?.classList.remove('text-amber-600', 'font-bold');
        }
      });

      // User UI
      const userAvatar = document.getElementById('user-avatar');
      const userAvatarLarge = document.getElementById('profile-avatar-large');
      const userName = document.getElementById('user-name');
      const profileName = document.getElementById('profile-display-name');
      const adminBadge = document.getElementById('admin-badge');
      const rolePill = document.getElementById('profile-role-pill');
      const roleDesc = document.getElementById('profile-role-desc');
      const adminPicker = document.getElementById('admin-section-picker');
      const logoutBtn = document.getElementById('logout-container');

      const initial = (state.currentUser.name || 'A').charAt(0).toUpperCase();
      userAvatar.textContent = initial;
      userAvatarLarge.textContent = initial;
      userName.textContent = state.currentUser.name;
      profileName.textContent = state.currentUser.name;

      const editBtns = document.querySelectorAll('.admin-edit-btn');

      if (state.currentUser.isAdmin) {
        adminBadge.classList.remove('hidden');
        adminPicker.classList.remove('hidden');
        logoutBtn.classList.remove('hidden');
        editBtns.forEach(b => b.classList.remove('hidden'));
        rolePill.className = "mt-4 inline-flex items-center px-3 py-1 rounded-full text-xs font-bold uppercase tracking-wider bg-amber-600 text-white shadow";
        rolePill.textContent = "Rol: Administrador Propietario";
        roleDesc.textContent = "Control total de publicaciones, textos de la web y moderación";
      } else {
        adminBadge.classList.add('hidden');
        adminPicker.classList.add('hidden');
        logoutBtn.classList.add('hidden');
        editBtns.forEach(b => b.classList.add('hidden'));
        rolePill.className = "mt-4 inline-flex items-center px-3 py-1 rounded-full text-xs font-bold uppercase tracking-wider bg-warm-200 dark:bg-zinc-800 text-warm-800 dark:text-zinc-300";
        rolePill.textContent = "Rol: Miembro de la Comunidad";
        roleDesc.textContent = "Lector y autor comunitario";
      }

      // Render grids
      renderPrincipalGrid();
      renderCommunityFilters();
      renderCommunityGrid();

      // Render modal if active
      if (state.activePostId) {
        renderModalContent();
      }
    }

    function renderPrincipalGrid() {
      const container = document.getElementById('grid-principal');
      if (!container) return;

      const principalPosts = state.posts.filter(p => p.section === 'principal');

      if (principalPosts.length === 0) {
        container.innerHTML = `
          <div class="col-span-full text-center py-12 text-warm-500 font-serif">
            Aún no hay escritos en el canal principal.
          </div>
        `;
        return;
      }

      container.innerHTML = principalPosts.map(post => `
        <div onclick="openPostModal('${post.id}')" class="group cursor-pointer bg-warm-50 dark:bg-zinc-900 border border-warm-200 dark:border-zinc-800 rounded-2xl p-6 shadow-sm hover:shadow-xl transition-all duration-300 flex flex-col justify-between hover:-translate-y-1">
          <div class="space-y-3">
            <div class="flex items-center justify-between text-xs font-bold uppercase tracking-wider text-amber-700 dark:text-amber-500">
              <span class="px-2.5 py-0.5 rounded-full bg-amber-100 dark:bg-amber-950/60">${escapeHtml(post.category)}</span>
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

    function renderCommunityFilters() {
      const container = document.getElementById('category-filters');
      if (!container) return;

      container.innerHTML = CATEGORIES.map(cat => `
        <button onclick="filterCommunity('${cat}')" class="px-3 py-1.5 rounded-full text-xs font-semibold transition-all ${
          state.categoryFilter === cat
            ? 'bg-warm-800 dark:bg-amber-600 text-white shadow'
            : 'bg-warm-200 dark:bg-zinc-800 text-warm-800 dark:text-zinc-300 hover:bg-warm-300'
        }">
          ${cat}
        </button>
      `).join('');
    }

    function renderCommunityGrid() {
      const container = document.getElementById('grid-comunidad');
      if (!container) return;

      let list = state.posts.filter(p => p.section === 'comunidad');

      if (state.categoryFilter !== 'Todos') {
        list = list.filter(p => p.category === state.categoryFilter);
      }

      if (state.searchQuery.trim()) {
        const q = state.searchQuery.toLowerCase();
        list = list.filter(p => 
          p.title.toLowerCase().includes(q) || 
          p.content.toLowerCase().includes(q) || 
          (p.authorName && p.authorName.toLowerCase().includes(q))
        );
      }

      if (list.length === 0) {
        container.innerHTML = `
          <div class="col-span-full text-center py-12 bg-warm-50 dark:bg-zinc-900 rounded-2xl border border-dashed border-warm-300 dark:border-zinc-800">
            <i class="fa-solid fa-pen-fountain text-3xl text-warm-400 mb-3 block"></i>
            <p class="font-serif text-warm-600 dark:text-zinc-400">No hay escritos disponibles en esta selección.</p>
            <button onclick="switchTab('escribir')" class="mt-4 px-4 py-2 bg-warm-800 dark:bg-amber-600 text-white text-xs font-bold rounded-xl shadow">
              Sé el primero en publicar
            </button>
          </div>
        `;
        return;
      }

      container.innerHTML = list.map(post => `
        <div class="bg-warm-50 dark:bg-zinc-900 border border-warm-200 dark:border-zinc-800 rounded-2xl p-6 shadow-sm hover:shadow-lg transition-all flex flex-col justify-between">
          <div class="space-y-3">
            <div class="flex items-center justify-between text-xs font-semibold text-warm-500">
              <span class="px-2 py-0.5 rounded bg-warm-200 dark:bg-zinc-800 text-warm-800 dark:text-zinc-300 uppercase">${escapeHtml(post.category)}</span>
              <span>${post.readTime || 3} min</span>
            </div>

            <h4 onclick="openPostModal('${post.id}')" class="font-display text-xl font-bold cursor-pointer text-warm-900 dark:text-warm-100 hover:text-amber-600 transition-colors leading-snug line-clamp-2">
              ${escapeHtml(post.title)}
            </h4>

            <p onclick="openPostModal('${post.id}')" class="font-serif text-xs text-warm-700 dark:text-zinc-300 line-clamp-3 leading-relaxed cursor-pointer">
              ${escapeHtml(post.content)}
            </p>
          </div>

          <div class="pt-4 mt-4 border-t border-warm-200/60 dark:border-zinc-800/60 space-y-3">
            <div class="flex items-center justify-between text-xs text-warm-500">
              <span class="font-semibold text-warm-800 dark:text-zinc-200">${escapeHtml(post.authorName || 'Anónimo')}</span>
              <span><i class="fa-solid fa-hands-clapping text-amber-600"></i> ${post.claps || 0}</span>
            </div>

            ${state.currentUser.isAdmin ? `
              <div class="pt-2 flex items-center justify-between text-[11px] bg-amber-50 dark:bg-amber-950/40 px-2.5 py-1.5 rounded-lg border border-amber-200 dark:border-amber-900/40">
                <span class="font-bold text-amber-800 dark:text-amber-400">Admin:</span>
                <div class="flex gap-2">
                  <button onclick="promotePost('${post.id}')" class="text-amber-700 dark:text-amber-300 hover:underline font-semibold">
                    <i class="fa-solid fa-arrow-up-right-from-square mr-1"></i>Promover
                  </button>
                  <button onclick="deletePost('${post.id}')" class="text-rose-600 dark:text-rose-400 hover:underline font-semibold">
                    <i class="fa-solid fa-trash mr-1"></i>Borrar
                  </button>
                </div>
              </div>
            ` : ''}
          </div>
        </div>
      `).join('');
    }

    function renderModalContent() {
      const post = state.posts.find(p => p.id === state.activePostId);
      if (!post) return;

      document.getElementById('modal-title').textContent = post.title;
      document.getElementById('modal-category').textContent = post.category;
      document.getElementById('modal-readtime').textContent = `${post.readTime || 3} min de lectura`;
      document.getElementById('modal-author').textContent = post.authorName || 'Anónimo';
      document.getElementById('modal-author-avatar').textContent = (post.authorName || 'A').charAt(0).toUpperCase();
      document.getElementById('modal-date').textContent = formatDate(post.createdAt);
      document.getElementById('modal-content').textContent = post.content;
      document.getElementById('modal-likes-count').textContent = post.claps || 0;

      // Admin options inside modal
      const adminActions = document.getElementById('modal-admin-actions');
      if (state.currentUser.isAdmin) {
        adminActions.classList.remove('hidden');
        adminActions.innerHTML = `
          <button onclick="promotePost('${post.id}')" class="px-3 py-1.5 bg-amber-600 hover:bg-amber-700 text-white rounded-lg text-xs font-bold shadow">
            ${post.section === 'principal' ? 'Mover a Comunidad' : 'Promover a Principal'}
          </button>
          <button onclick="deletePost('${post.id}')" class="px-3 py-1.5 bg-rose-600 hover:bg-rose-700 text-white rounded-lg text-xs font-bold shadow">
            Eliminar
          </button>
        `;
      } else {
        adminActions.classList.add('hidden');
      }

      // Render Comments
      renderCommentsList(post.id);
    }

    function renderCommentsList(postId) {
      const container = document.getElementById('modal-comments-list');
      if (!container) return;

      const postComments = state.comments.filter(c => c.postId === postId);

      if (postComments.length === 0) {
        container.innerHTML = `
          <p class="text-xs text-warm-500 italic">Aún no hay respuestas. Sé el primero en compartir tu punto de vista.</p>
        `;
        return;
      }

      container.innerHTML = postComments.map(c => `
        <div class="bg-warm-100 dark:bg-zinc-800/60 p-3.5 rounded-xl border border-warm-200 dark:border-zinc-700/60 space-y-1">
          <div class="flex items-center justify-between text-xs">
            <span class="font-bold text-warm-900 dark:text-warm-100">${escapeHtml(c.authorName || 'Lector')}</span>
            <div class="flex items-center space-x-2">
              <span class="text-warm-500 dark:text-zinc-400">${formatDate(c.createdAt)}</span>
              ${state.currentUser.isAdmin ? `
                <button onclick="deleteComment('${c.id}')" class="text-rose-500 hover:underline text-[11px] font-bold">Borrar</button>
              ` : ''}
            </div>
          </div>
          <p class="text-xs font-serif text-warm-800 dark:text-zinc-200 leading-relaxed">
            ${escapeHtml(c.text)}
          </p>
        </div>
      `).join('');
    }

    // --- INTERACTIVE HANDLERS ---

    window.switchTab = function(tabName) {
      state.activeTab = tabName;
      window.scrollTo({ top: 0, behavior: 'smooth' });
      renderApp();
    };

    window.toggleDarkMode = function() {
      state.darkMode = !state.darkMode;
      localStorage.setItem('ecos_theme', state.darkMode ? 'dark' : 'light');
      renderApp();
    };

    window.filterCommunity = function(category) {
      state.categoryFilter = category;
      renderApp();
    };

    window.onSearchInput = function(e) {
      state.searchQuery = e.target.value;
      renderCommunityGrid();
    };

    // FUNCIÓN PARA DESCARGAR ESCRITOS PRINCIPALES
    window.downloadPrincipalPosts = function() {
      const principalPosts = state.posts.filter(p => p.section === 'principal');

      if (principalPosts.length === 0) {
        showToast("No hay escritos principales para descargar.", "error");
        return;
      }

      let content = "=========================================\n";
      content += "    ECOS Y REFLEXIONES - CANAL OFICIAL    \n";
      content += "=========================================\n\n";

      principalPosts.forEach((p, idx) => {
        content += `[${idx + 1}] ${p.title.toUpperCase()}\n`;
        content += `Autor: ${p.authorName || 'Administrador'} | Categoría: ${p.category} | Fecha: ${formatDate(p.createdAt)}\n`;
        content += "-----------------------------------------\n";
        content += `${p.content}\n\n`;
        content += "=========================================\n\n";
      });

      const blob = new Blob([content], { type: 'text/plain;charset=utf-8' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = `escritos_principales_${new Date().toISOString().slice(0, 10)}.txt`;
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      URL.revokeObjectURL(url);

      showToast("Descargando escritos principales...", "success");
    };

    // EDICIÓN DINÁMICA DE TEXTOS/TÍTULOS WEB
    window.editSiteText = function(elementId) {
      if (!state.currentUser.isAdmin) return;

      const element = document.getElementById(elementId);
      if (!element) return;

      const currentVal = element.textContent.trim();
      const newVal = prompt("Escribe el nuevo texto para este apartado:", currentVal);

      if (newVal !== null && newVal.trim() !== '') {
        element.textContent = newVal.trim();
        state.customTitles[elementId] = newVal.trim();
        saveStateToLocal();
        showToast("Texto actualizado correctamente.", "success");
      }
    };

    window.loginAdminWithCode = function() {
      const input = document.getElementById('admin-key-input');
      const val = input.value.trim();

      if (val === 'SarieroGuillem2005' || val.toLowerCase() === 'admin') {
        state.currentUser.isAdmin = true;
        state.currentUser.name = state.currentUser.name !== 'Invitado' ? state.currentUser.name : 'Administrador';
        input.value = '';
        saveStateToLocal();
        showToast("¡Modo Administrador activado con éxito!", "success");
        renderApp();
      } else {
        showToast("Código incorrecto. Inténtalo de nuevo.", "error");
      }
    };

    window.setCustomUser = function() {
      const input = document.getElementById('custom-username-input');
      const val = input.value.trim();
      if (!val) return;

      state.currentUser.name = val;
      input.value = '';
      saveStateToLocal();
      showToast(`Nombre actualizado a "${val}"`, "success");
      renderApp();
    };

    window.setAnonymousUser = function() {
      state.currentUser.name = 'Anónimo';
      saveStateToLocal();
      showToast('Firma configurada como "Anónimo"', "info");
      renderApp();
    };

    window.logout = function() {
      state.currentUser.isAdmin = false;
      saveStateToLocal();
      showToast("Has salido del modo administrador.", "info");
      renderApp();
    };

    // CATEGORÍAS PERSONALIZADAS EN EL FORMULARIO
    window.handleCategoryChange = function(e) {
      const customInput = document.getElementById('custom-category-input');
      if (e.target.value === 'NEW_CUSTOM') {
        customInput.classList.remove('hidden');
        customInput.focus();
      } else {
        customInput.classList.add('hidden');
      }
    };

    window.submitNewPost = function(e) {
      e.preventDefault();

      const title = document.getElementById('post-title').value.trim();
      const categorySelect = document.getElementById('post-category').value;
      const customCategory = document.getElementById('custom-category-input').value.trim();
      const authorInput = document.getElementById('post-author').value.trim();
      const readTime = parseInt(document.getElementById('post-readtime').value) || 3;
      const content = document.getElementById('post-content').value.trim();

      let category = categorySelect;
      if (categorySelect === 'NEW_CUSTOM') {
        if (!customCategory) {
          showToast("Por favor, escribe la categoría personalizada.", "error");
          return;
        }
        category = customCategory;
        if (!CATEGORIES.includes(category)) {
          CATEGORIES.push(category);
        }
      }

      let section = 'comunidad';
      if (state.currentUser.isAdmin) {
        const radio = document.querySelector('input[name="post-section"]:checked');
        if (radio) section = radio.value;
      }

      if (!title || !content) {
        showToast("Por favor rellena el título y el contenido.", "error");
        return;
      }

      const authorName = authorInput || state.currentUser.name || 'Anónimo';

      const newPost = {
        id: 'post-' + Date.now(),
        title,
        category,
        readTime,
        content,
        section,
        authorName,
        claps: 0,
        createdAt: new Date().toISOString()
      };

      state.posts.unshift(newPost);
      saveStateToLocal();

      if (db) {
        try {
          addDoc(collection(db, 'artifacts', appId, 'public', 'data', 'posts'), newPost).catch(() => {});
        } catch (e) {}
      }

      document.getElementById('post-form').reset();
      document.getElementById('custom-category-input').classList.add('hidden');
      showToast("¡Escrito publicado correctamente!", "success");
      window.switchTab(section);
    };

    window.openPostModal = function(postId) {
      state.activePostId = postId;
      renderModalContent();
      document.getElementById('post-modal').classList.remove('hidden');
    };

    window.closePostModal = function() {
      document.getElementById('post-modal').classList.add('hidden');
      state.activePostId = null;
    };

    window.handleModalBackdropClick = function(e) {
      if (e.target.id === 'post-modal') {
        window.closePostModal();
      }
    };

    window.likePost = function() {
      if (!state.activePostId) return;
      const post = state.posts.find(p => p.id === state.activePostId);
      if (!post) return;

      post.claps = (post.claps || 0) + 1;
      saveStateToLocal();
      renderApp();

      if (db) {
        try {
          updateDoc(doc(db, 'artifacts', appId, 'public', 'data', 'posts', post.id), { claps: post.claps }).catch(() => {});
        } catch (e) {}
      }
    };

    window.addComment = function(e) {
      e.preventDefault();
      if (!state.activePostId) return;

      const textInput = document.getElementById('comment-text-input');
      const authorInput = document.getElementById('comment-author-input');
      const text = textInput.value.trim();
      const author = authorInput.value.trim() || state.currentUser.name || 'Lector';

      if (!text) return;

      const newComment = {
        id: 'comm-' + Date.now(),
        postId: state.activePostId,
        authorName: author,
        text,
        createdAt: new Date().toISOString()
      };

      state.comments.push(newComment);
      saveStateToLocal();
      textInput.value = '';

      if (db) {
        try {
          addDoc(collection(db, 'artifacts', appId, 'public', 'data', 'comments'), newComment).catch(() => {});
        } catch (e) {}
      }

      renderCommentsList(state.activePostId);
      showToast("Comentario enviado", "success");
    };

    window.deleteComment = function(commentId) {
      state.comments = state.comments.filter(c => c.id !== commentId);
      saveStateToLocal();
      if (state.activePostId) renderCommentsList(state.activePostId);
      showToast("Comentario eliminado", "info");
    };

    window.promotePost = function(postId) {
      if (!state.currentUser.isAdmin) return;
      const post = state.posts.find(p => p.id === postId);
      if (!post) return;

      post.section = post.section === 'principal' ? 'comunidad' : 'principal';
      saveStateToLocal();
      showToast(`Escrito movido a: ${post.section === 'principal' ? 'Canal Principal' : 'Comunidad'}`, "success");
      
      if (state.activePostId === postId) {
        window.closePostModal();
      }
      renderApp();
    };

    window.deletePost = function(postId) {
      if (!state.currentUser.isAdmin) return;
      state.posts = state.posts.filter(p => p.id !== postId);
      saveStateToLocal();
      showToast("Escrito eliminado", "info");

      if (state.activePostId === postId) {
        window.closePostModal();
      }
      renderApp();
    };

    // --- UTILITIES ---
    function showToast(msg, type = "info") {
      const container = document.getElementById('toast-container');
      if (!container) return;

      const toast = document.createElement('div');
      let bg = "bg-warm-900 text-white";
      if (type === "success") bg = "bg-emerald-700 text-white";
      if (type === "error") bg = "bg-rose-700 text-white";

      toast.className = `${bg} px-4 py-3 rounded-xl shadow-2xl text-xs font-semibold flex items-center space-x-2 transition-all transform translate-y-2 opacity-0 pointer-events-auto`;
      toast.innerHTML = `<span>${escapeHtml(msg)}</span>`;

      container.appendChild(toast);

      setTimeout(() => toast.classList.remove('translate-y-2', 'opacity-0'), 10);
      setTimeout(() => {
        toast.classList.add('opacity-0', 'translate-y-2');
        setTimeout(() => toast.remove(), 300);
      }, 3000);
    }

    function formatDate(dateStr) {
      if (!dateStr) return '';
      const d = new Date(dateStr);
      return d.toLocaleDateString('es-ES', { day: 'numeric', month: 'short', year: 'numeric' });
    }

    function escapeHtml(str) {
      if (!str) return '';
      return str.replace(/[&<>"']/g, m => ({
        '&': '&amp;',
        '<': '&lt;',
        '>': '&gt;',
        '"': '&quot;',
        "'": '&#039;'
      }[m]));
    }

    // Keyboard support for Modal
    window.addEventListener('keydown', (e) => {
      if (e.key === 'Escape' && state.activePostId) {
        window.closePostModal();
      }
    });

    // STARTUP
    loadSavedState();
    renderApp();
  </script>
</body>
</html>
