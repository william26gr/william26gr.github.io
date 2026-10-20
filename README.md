<!DOCTYPE html>
<html lang="es" class="h-full">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mis Notas Personales</title>
  
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: {
            brand: {
              50: '#f0f7ff',
              100: '#e0effe',
              500: '#0284c7',
              600: '#0265d2',
              700: '#0369a1',
            }
          }
        }
      }
    }
  </script>

  <!-- Font Awesome Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <!-- Marked.js for Markdown parsing -->
  <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>

  <style>
    /* Custom Scrollbar */
    ::-webkit-scrollbar { width: 6px; height: 6px; }
    ::-webkit-scrollbar-track { background: transparent; }
    ::-webkit-scrollbar-thumb { background: rgba(156, 163, 175, 0.4); border-radius: 9999px; }
    ::-webkit-scrollbar-thumb:hover { background: rgba(156, 163, 175, 0.7); }
    .note-content ul { list-style-type: disc; padding-left: 1.25rem; margin: 0.5rem 0; }
    .note-content ol { list-style-type: decimal; padding-left: 1.25rem; margin: 0.5rem 0; }
    .note-content p { margin-bottom: 0.5rem; }
    .note-content code { background: rgba(100,116,139,0.15); padding: 0.15rem 0.3rem; border-radius: 0.25rem; font-family: monospace; font-size: 0.875em; }
    .note-content pre { background: #1e293b; color: #f8fafc; padding: 0.75rem; border-radius: 0.5rem; overflow-x: auto; margin: 0.5rem 0; }
    .note-content blockquote { border-left: 3px solid #0284c7; padding-left: 0.75rem; color: #64748b; font-style: italic; }
  </style>
</head>
<body class="h-full bg-slate-50 dark:bg-slate-900 text-slate-800 dark:text-slate-100 transition-colors duration-200 antialiased font-sans flex flex-col">

  <!-- APP CONTAINER -->
  <div id="app" class="flex flex-col h-full">

    <!-- NAVBAR -->
    <header class="border-b border-slate-200 dark:border-slate-800 bg-white/80 dark:bg-slate-900/80 backdrop-blur sticky top-0 z-30">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between gap-4">
        
        <!-- Brand Logo -->
        <div class="flex items-center gap-3">
          <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-brand-600 to-indigo-500 flex items-center justify-center text-white shadow-md shadow-brand-500/20">
            <i class="fa-solid fa-note-sticky text-lg"></i>
          </div>
          <div>
            <h1 class="text-lg font-bold tracking-tight bg-gradient-to-r from-slate-900 to-slate-700 dark:from-white dark:to-slate-300 bg-clip-text text-transparent">
              Mis Notas
            </h1>
            <span id="storageBadge" class="text-[10px] uppercase tracking-wider font-semibold px-2 py-0.5 rounded-full bg-slate-100 dark:bg-slate-800 text-slate-500 dark:text-slate-400 border border-slate-200 dark:border-slate-700">
              Modo Local
            </span>
          </div>
        </div>

        <!-- Search Bar (Desk) -->
        <div id="searchContainer" class="flex-1 max-w-md hidden sm:block">
          <div class="relative">
            <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400 text-sm"></i>
            <input type="text" id="searchInput" placeholder="Buscar notas por título, texto o etiqueta..." 
              class="w-full pl-10 pr-4 py-2 text-sm rounded-xl bg-slate-100 dark:bg-slate-800 border-none focus:ring-2 focus:ring-brand-500 text-slate-900 dark:text-slate-100 placeholder-slate-400 transition">
          </div>
        </div>

        <!-- Action Controls -->
        <div class="flex items-center gap-1.5 sm:gap-2">
          <!-- Guide Modal Trigger -->
          <button id="guideBtn" title="Guía de publicación en GitHub" class="p-2.5 rounded-xl hover:bg-slate-100 dark:hover:bg-slate-800 text-slate-600 dark:text-slate-300 transition text-sm flex items-center gap-1.5 font-medium">
            <i class="fa-solid fa-cloud-arrow-up text-brand-500"></i>
            <span class="hidden md:inline">Publicar en GitHub</span>
          </button>

          <!-- Config Firebase Trigger -->
          <button id="configBtn" title="Configuración de Firebase" class="p-2.5 rounded-xl hover:bg-slate-100 dark:hover:bg-slate-800 text-slate-600 dark:text-slate-300 transition">
            <i class="fa-solid fa-gear"></i>
          </button>

          <!-- Dark/Light Mode Toggle -->
          <button id="themeToggle" title="Cambiar Tema" class="p-2.5 rounded-xl hover:bg-slate-100 dark:hover:bg-slate-800 text-slate-600 dark:text-slate-300 transition">
            <i class="fa-solid fa-moon dark:hidden"></i>
            <i class="fa-solid fa-sun hidden dark:block text-amber-400"></i>
          </button>

          <!-- User Profile / Auth Action -->
          <div id="userProfileArea" class="pl-2 border-l border-slate-200 dark:border-slate-800">
            <button id="loginBtnNav" class="px-3.5 py-1.5 text-xs font-semibold rounded-xl bg-brand-600 hover:bg-brand-700 text-white shadow-sm transition">
              Iniciar Sesión
            </button>
            <div id="userMenuNav" class="hidden flex items-center gap-2">
              <div id="userAvatar" class="w-8 h-8 rounded-full bg-brand-600 text-white font-bold flex items-center justify-center text-xs uppercase shadow">U</div>
              <button id="logoutBtn" title="Cerrar Sesión" class="p-2 rounded-lg hover:bg-red-50 dark:hover:bg-red-950/30 text-red-500 transition">
                <i class="fa-solid fa-right-from-bracket text-sm"></i>
              </button>
            </div>
          </div>
        </div>

      </div>
    </header>

    <!-- SEARCH BAR MOBILE -->
    <div class="px-4 pt-3 pb-1 sm:hidden bg-white dark:bg-slate-900 border-b border-slate-200 dark:border-slate-800">
      <div class="relative">
        <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400 text-sm"></i>
        <input type="text" id="searchInputMobile" placeholder="Buscar notas..." 
          class="w-full pl-10 pr-4 py-2 text-sm rounded-xl bg-slate-100 dark:bg-slate-800 border-none focus:ring-2 focus:ring-brand-500 text-slate-900 dark:text-slate-100 placeholder-slate-400 transition">
      </div>
    </div>

    <!-- MAIN CONTENT AREA -->
    <main class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 flex flex-col">

      <!-- WELCOME / LOCK SCREEN (If not logged in local or firebase) -->
      <section id="lockScreen" class="flex-1 flex items-center justify-center py-12">
        <div class="max-w-md w-full text-center p-8 bg-white dark:bg-slate-800/90 rounded-2xl shadow-xl border border-slate-200/80 dark:border-slate-700/60 backdrop-blur">
          <div class="w-16 h-16 mx-auto mb-5 rounded-2xl bg-brand-50 dark:bg-brand-500/10 text-brand-600 dark:text-brand-400 flex items-center justify-center text-2xl shadow-inner">
            <i class="fa-solid fa-lock"></i>
          </div>
          <h2 class="text-2xl font-bold tracking-tight mb-2">Cuaderno Privado</h2>
          <p class="text-sm text-slate-500 dark:text-slate-400 mb-6 leading-relaxed">
            Tus notas están protegidas. Inicia sesión con tu cuenta o accede mediante PIN local para añadir y gestionar tus notas.
          </p>

          <div class="space-y-3">
            <button id="mainLoginBtn" class="w-full py-2.5 px-4 rounded-xl bg-brand-600 hover:bg-brand-700 text-white font-medium text-sm transition flex items-center justify-center gap-2 shadow-lg shadow-brand-500/25">
              <i class="fa-solid fa-right-to-bracket"></i>
              Acceder / Iniciar Sesión
            </button>
            <button id="localAccessBtn" class="w-full py-2.5 px-4 rounded-xl bg-slate-100 dark:bg-slate-700 hover:bg-slate-200 dark:hover:bg-slate-600 text-slate-700 dark:text-slate-200 font-medium text-sm transition flex items-center justify-center gap-2">
              <i class="fa-solid fa-key text-amber-500"></i>
              Acceso Rápido Local (PIN)
            </button>
          </div>
        </div>
      </section>

      <!-- NOTES DASHBOARD (Visible when logged in) -->
      <section id="notesDashboard" class="hidden flex-1 flex flex-col space-y-6">

        <!-- Controls Header & Category Filters -->
        <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
          <!-- Category Filters -->
          <div id="categoryFilterContainer" class="flex items-center gap-1.5 overflow-x-auto pb-1 scrollbar-none">
            <!-- Dynamic Category Pills inserted here -->
          </div>

          <!-- Top Toolbar Actions -->
          <div class="flex items-center justify-between sm:justify-end gap-2 shrink-0">
            <!-- Backup / Export button -->
            <button id="exportBtn" title="Descargar Copia de Seguridad" class="px-3 py-2 rounded-xl border border-slate-200 dark:border-slate-700 hover:bg-white dark:hover:bg-slate-800 text-xs font-semibold text-slate-600 dark:text-slate-300 transition flex items-center gap-1.5">
              <i class="fa-solid fa-download"></i>
              <span class="hidden sm:inline">Exportar</span>
            </button>

            <!-- New Note Trigger -->
            <button id="newNoteBtn" class="px-4 py-2 rounded-xl bg-brand-600 hover:bg-brand-700 text-white text-sm font-medium shadow-md shadow-brand-500/20 transition flex items-center gap-2">
              <i class="fa-solid fa-plus"></i>
              <span>Nueva Nota</span>
            </button>
          </div>
        </div>

        <!-- Empty State -->
        <div id="emptyState" class="hidden flex-1 flex flex-col items-center justify-center py-16 text-center">
          <div class="w-20 h-20 rounded-full bg-slate-100 dark:bg-slate-800 flex items-center justify-center text-slate-400 mb-4 text-2xl">
            <i class="fa-regular fa-folder-open"></i>
          </div>
          <h3 class="text-lg font-semibold text-slate-700 dark:text-slate-300 mb-1">No hay notas por aquí</h3>
          <p class="text-sm text-slate-400 max-w-sm mb-6">Crea tu primera nota para organizar tus ideas, tareas o apuntes personales.</p>
          <button id="emptyNewNoteBtn" class="px-4 py-2 rounded-xl bg-brand-600 hover:bg-brand-700 text-white text-sm font-medium transition shadow-md">
            + Crear mi primera nota
          </button>
        </div>

        <!-- Notes Grid -->
        <div id="notesGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
          <!-- Note Cards dynamically inserted here -->
        </div>

      </section>

    </main>
  </div>

  <!-- MODAL: CREATE / EDIT NOTE -->
  <div id="noteModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden opacity-0 transition-opacity duration-200">
    <div class="bg-white dark:bg-slate-800 rounded-2xl max-w-2xl w-full shadow-2xl border border-slate-200 dark:border-slate-700 overflow-hidden flex flex-col max-h-[90vh]">
      
      <!-- Modal Header -->
      <div class="px-6 py-4 border-b border-slate-100 dark:border-slate-700/60 flex items-center justify-between">
        <h3 id="modalTitle" class="font-bold text-lg text-slate-800 dark:text-slate-100">Nueva Nota</h3>
        <div class="flex items-center gap-2">
          <button id="pinModalBtn" class="p-2 rounded-lg text-slate-400 hover:text-amber-500 hover:bg-slate-100 dark:hover:bg-slate-700 transition" title="Fijar al inicio">
            <i class="fa-solid fa-thumbtack"></i>
          </button>
          <button id="closeNoteModal" class="p-2 rounded-lg text-slate-400 hover:text-slate-600 dark:hover:text-slate-200 hover:bg-slate-100 dark:hover:bg-slate-700 transition">
            <i class="fa-solid fa-xmark text-lg"></i>
          </button>
        </div>
      </div>

      <!-- Modal Body -->
      <div class="p-6 overflow-y-auto space-y-4 flex-1">
        <!-- Title input -->
        <input type="text" id="noteTitleInput" placeholder="Título de la nota..." 
          class="w-full text-xl font-bold border-none outline-none bg-transparent placeholder-slate-400 text-slate-900 dark:text-slate-100">

        <!-- Category Tag Selection -->
        <div class="flex items-center gap-2 overflow-x-auto py-1">
          <span class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Etiqueta:</span>
          <div id="modalCategoryOptions" class="flex items-center gap-1.5">
            <!-- Dynamic categories inserted here -->
          </div>
        </div>

        <!-- Markdown Formatting Helper Toolbar -->
        <div class="flex items-center gap-1 pt-2 border-t border-slate-100 dark:border-slate-700/60 text-xs text-slate-500">
          <button type="button" onclick="insertFormat('**', '**')" class="px-2 py-1 rounded hover:bg-slate-100 dark:hover:bg-slate-700 font-bold" title="Negrita">B</button>
          <button type="button" onclick="insertFormat('*', '*')" class="px-2 py-1 rounded hover:bg-slate-100 dark:hover:bg-slate-700 italic" title="Cursiva">I</button>
          <button type="button" onclick="insertFormat('# ')" class="px-2 py-1 rounded hover:bg-slate-100 dark:hover:bg-slate-700 font-bold" title="Título">H1</button>
          <button type="button" onclick="insertFormat('- ')" class="px-2 py-1 rounded hover:bg-slate-100 dark:hover:bg-slate-700" title="Lista"><i class="fa-solid fa-list-ul"></i></button>
          <button type="button" onclick="insertFormat('```\n', '\n```')" class="px-2 py-1 rounded hover:bg-slate-100 dark:hover:bg-slate-700" title="Código"><i class="fa-solid fa-code"></i></button>
          <span class="ml-auto text-[11px] text-slate-400">Soporta Markdown</span>
        </div>

        <!-- Content Area -->
        <textarea id="noteContentInput" rows="10" placeholder="Escribe tu nota aquí..." 
          class="w-full border-none outline-none bg-transparent resize-none placeholder-slate-400 text-slate-800 dark:text-slate-200 font-normal leading-relaxed text-sm"></textarea>
      </div>

      <!-- Modal Footer -->
      <div class="px-6 py-4 bg-slate-50 dark:bg-slate-800/50 border-t border-slate-100 dark:border-slate-700/60 flex items-center justify-between">
        <button id="deleteNoteBtn" class="px-3.5 py-2 text-xs font-semibold text-red-600 dark:text-red-400 hover:bg-red-50 dark:hover:bg-red-950/30 rounded-xl transition hidden">
          <i class="fa-solid fa-trash mr-1"></i> Eliminar
        </button>
        <div class="flex items-center gap-2 ml-auto">
          <button id="cancelNoteBtn" class="px-4 py-2 text-xs font-semibold text-slate-600 dark:text-slate-300 hover:bg-slate-200/60 dark:hover:bg-slate-700 rounded-xl transition">
            Cancelar
          </button>
          <button id="saveNoteBtn" class="px-5 py-2 text-xs font-semibold bg-brand-600 hover:bg-brand-700 text-white rounded-xl shadow-md transition">
            Guardar Nota
          </button>
        </div>
      </div>

    </div>
  </div>

  <!-- MODAL: LOGIN / AUTH -->
  <div id="authModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
    <div class="bg-white dark:bg-slate-800 rounded-2xl max-w-md w-full shadow-2xl border border-slate-200 dark:border-slate-700 p-6 relative">
      <button id="closeAuthModal" class="absolute top-4 right-4 text-slate-400 hover:text-slate-600 dark:hover:text-slate-200">
        <i class="fa-solid fa-xmark text-lg"></i>
      </button>

      <h3 class="text-xl font-bold text-center mb-1">Acceder a Mis Notas</h3>
      <p class="text-xs text-slate-400 text-center mb-6">Elige el método de inicio de sesión</p>

      <div class="space-y-3">
        <!-- Firebase Login Options (Google / Email) -->
        <div id="firebaseAuthSection" class="space-y-3">
          <button id="googleAuthBtn" class="w-full py-2.5 px-4 border border-slate-200 dark:border-slate-700 rounded-xl hover:bg-slate-50 dark:hover:bg-slate-700/50 transition text-sm font-medium flex items-center justify-center gap-3">
            <svg class="w-4 h-4" viewBox="0 0 24 24"><path fill="#4285F4" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/><path fill="#34A853" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/><path fill="#FBBC05" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.06H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.94l2.85-2.22.81-.63z"/><path fill="#EA4335" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.06l3.66 2.84c.87-2.6 3.3-4.52 6.16-4.52z"/></svg>
            Continuar con Google
          </button>

          <div class="relative my-4">
            <div class="absolute inset-0 flex items-center"><div class="w-full border-t border-slate-200 dark:border-slate-700"></div></div>
            <div class="relative flex justify-center text-xs uppercase"><span class="bg-white dark:bg-slate-800 px-2 text-slate-400">O Email / Contraseña</span></div>
          </div>

          <form id="emailAuthForm" class="space-y-3">
            <input type="email" id="authEmail" placeholder="Tu correo electrónico" required class="w-full px-3.5 py-2 text-sm rounded-xl border border-slate-200 dark:border-slate-700 bg-transparent outline-none focus:ring-2 focus:ring-brand-500">
            <input type="password" id="authPassword" placeholder="Contraseña" required class="w-full px-3.5 py-2 text-sm rounded-xl border border-slate-200 dark:border-slate-700 bg-transparent outline-none focus:ring-2 focus:ring-brand-500">
            <button type="submit" class="w-full py-2.5 bg-brand-600 hover:bg-brand-700 text-white font-medium text-sm rounded-xl transition">
              Iniciar Sesión / Registrarse
            </button>
          </form>
        </div>

        <div class="pt-3 border-t border-slate-100 dark:border-slate-700">
          <button id="usePinAuthBtn" class="w-full py-2 text-xs font-semibold text-slate-500 hover:text-slate-800 dark:hover:text-slate-200 transition text-center">
            🔒 Preferir clave PIN local de protección
          </button>
        </div>

      </div>
    </div>
  </div>

  <!-- MODAL: FIREBASE CONFIG -->
  <div id="configModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
    <div class="bg-white dark:bg-slate-800 rounded-2xl max-w-lg w-full shadow-2xl border border-slate-200 dark:border-slate-700 p-6 relative">
      <button id="closeConfigModal" class="absolute top-4 right-4 text-slate-400 hover:text-slate-600 dark:hover:text-slate-200">
        <i class="fa-solid fa-xmark text-lg"></i>
      </button>

      <h3 class="text-lg font-bold mb-1 flex items-center gap-2">
        <i class="fa-solid fa-cloud text-brand-500"></i> Configurar Sincronización en la Nube
      </h3>
      <p class="text-xs text-slate-500 dark:text-slate-400 mb-4">
        Pega tu configuración de Firebase para sincronizar tus notas entre dispositivos de forma segura.
      </p>

      <div class="space-y-3">
        <label class="block text-xs font-semibold text-slate-600 dark:text-slate-300">Firebase Config (JSON):</label>
        <textarea id="firebaseConfigInput" rows="6" placeholder='{\n  "apiKey": "...",\n  "authDomain": "...",\n  "projectId": "..."\n}'
          class="w-full p-3 font-mono text-xs rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-900/50 outline-none focus:ring-2 focus:ring-brand-500"></textarea>

        <div class="flex items-center justify-between pt-2">
          <button id="clearConfigBtn" class="text-xs text-red-500 hover:underline">Limpiar / Usar Modo Local</button>
          <button id="saveConfigBtn" class="px-4 py-2 bg-brand-600 hover:bg-brand-700 text-white font-medium text-xs rounded-xl shadow transition">
            Guardar Configuración
          </button>
        </div>
      </div>
    </div>
  </div>

  <!-- MODAL: GITHUB PAGES DEPLOY GUIDE -->
  <div id="guideModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
    <div class="bg-white dark:bg-slate-800 rounded-2xl max-w-2xl w-full shadow-2xl border border-slate-200 dark:border-slate-700 overflow-hidden flex flex-col max-h-[85vh]">
      <div class="px-6 py-4 border-b border-slate-100 dark:border-slate-700 flex items-center justify-between">
        <h3 class="font-bold text-lg flex items-center gap-2">
          <i class="fa-brands fa-github text-xl"></i> Cómo publicar esta web en GitHub Pages
        </h3>
        <button id="closeGuideModal" class="text-slate-400 hover:text-slate-600 dark:hover:text-slate-200">
          <i class="fa-solid fa-xmark text-lg"></i>
        </button>
      </div>

      <div class="p-6 overflow-y-auto space-y-5 text-sm text-slate-600 dark:text-slate-300 leading-relaxed">
        
        <div class="flex gap-4 items-start">
          <div class="w-7 h-7 rounded-full bg-brand-100 dark:bg-brand-900/50 text-brand-600 dark:text-brand-400 font-bold flex items-center justify-center shrink-0">1</div>
          <div>
            <h4 class="font-semibold text-slate-800 dark:text-slate-100 mb-1">Crea o abre el archivo index.html</h4>
            <p class="text-xs">
              En tu repositorio de GitHub, haz clic en <strong>Add file &gt; Create new file</strong>, nombra el archivo exactamente <code class="bg-slate-100 dark:bg-slate-700 px-1 py-0.5 rounded text-brand-600 dark:text-brand-400">index.html</code>.
            </p>
          </div>
        </div>

        <div class="flex gap-4 items-start">
          <div class="w-7 h-7 rounded-full bg-brand-100 dark:bg-brand-900/50 text-brand-600 dark:text-brand-400 font-bold flex items-center justify-center shrink-0">2</div>
          <div>
            <h4 class="font-semibold text-slate-800 dark:text-slate-100 mb-1">Pega todo este código</h4>
            <p class="text-xs mb-2">
              Copia todo el contenido de este archivo y pégalo en el editor de GitHub.
            </p>
            <button onclick="navigator.clipboard.writeText(document.documentElement.outerHTML)" class="px-3 py-1.5 bg-slate-100 dark:bg-slate-700 hover:bg-slate-200 text-xs font-semibold rounded-lg text-slate-700 dark:text-slate-200 transition flex items-center gap-2">
              <i class="fa-solid fa-copy"></i> Copiar Código HTML Completo
            </button>
          </div>
        </div>

        <div class="flex gap-4 items-start">
          <div class="w-7 h-7 rounded-full bg-brand-100 dark:bg-brand-900/50 text-brand-600 dark:text-brand-400 font-bold flex items-center justify-center shrink-0">3</div>
          <div>
            <h4 class="font-semibold text-slate-800 dark:text-slate-100 mb-1">Guarda cambios (Commit)</h4>
            <p class="text-xs">
              Haz clic en el botón verde <strong>Commit changes...</strong> en GitHub. ¡En 1 o 2 minutos tu app estará online en tu enlace de GitHub Pages!
            </p>
          </div>
        </div>

      </div>

      <div class="p-4 bg-slate-50 dark:bg-slate-900 border-t border-slate-100 dark:border-slate-700 text-right">
        <button id="understoodGuideBtn" class="px-5 py-2 bg-brand-600 text-white rounded-xl font-medium text-xs shadow">
          Entendido
        </button>
      </div>
    </div>
  </div>

  <!-- FIREBASE MODULE LOGIC -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
    import { getAuth, GoogleAuthProvider, signInWithPopup, signInWithEmailAndPassword, createUserWithEmailAndPassword, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
    import { getFirestore, collection, doc, setDoc, getDocs, deleteDoc, onSnapshot, query, where } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

    window.FirebaseCore = {
      initializeApp, getAuth, GoogleAuthProvider, signInWithPopup, signInWithEmailAndPassword, createUserWithEmailAndPassword, signOut, onAuthStateChanged,
      getFirestore, collection, doc, setDoc, getDocs, deleteDoc, onSnapshot, query, where
    };
  </script>

  <!-- MAIN APP SCRIPT -->
  <script>
    // App State Management
    const state = {
      notes: [],
      categories: [
        { id: 'all', name: 'Todas', color: 'bg-slate-200 dark:bg-slate-700 text-slate-700 dark:text-slate-200' },
        { id: 'personal', name: 'Personal', color: 'bg-blue-100 dark:bg-blue-900/40 text-blue-600 dark:text-blue-300' },
        { id: 'work', name: 'Trabajo', color: 'bg-purple-100 dark:bg-purple-900/40 text-purple-600 dark:text-purple-300' },
        { id: 'ideas', name: 'Ideas', color: 'bg-emerald-100 dark:bg-emerald-900/40 text-emerald-600 dark:text-emerald-300' },
        { id: 'urgent', name: 'Urgente', color: 'bg-amber-100 dark:bg-amber-900/40 text-amber-600 dark:text-amber-300' }
      ],
      selectedCategory: 'all',
      searchQuery: '',
      activeNote: null,
      currentUser: null,
      isFirebaseActive: false,
      pinCode: localStorage.getItem('notes_pin_code') || '1234'
    };

    // DOM Elements
    const elements = {
      notesGrid: document.getElementById('notesGrid'),
      emptyState: document.getElementById('emptyState'),
      lockScreen: document.getElementById('lockScreen'),
      notesDashboard: document.getElementById('notesDashboard'),
      noteModal: document.getElementById('noteModal'),
      authModal: document.getElementById('authModal'),
      configModal: document.getElementById('configModal'),
      guideModal: document.getElementById('guideModal'),
      categoryFilterContainer: document.getElementById('categoryFilterContainer'),
      modalCategoryOptions: document.getElementById('modalCategoryOptions'),
      noteTitleInput: document.getElementById('noteTitleInput'),
      noteContentInput: document.getElementById('noteContentInput'),
      searchInput: document.getElementById('searchInput'),
      searchInputMobile: document.getElementById('searchInputMobile'),
      storageBadge: document.getElementById('storageBadge'),
      userProfileArea: document.getElementById('userProfileArea'),
      loginBtnNav: document.getElementById('loginBtnNav'),
      userMenuNav: document.getElementById('userMenuNav'),
      userAvatar: document.getElementById('userAvatar'),
      deleteNoteBtn: document.getElementById('deleteNoteBtn'),
      pinModalBtn: document.getElementById('pinModalBtn')
    };

    // Initialize Application
    document.addEventListener('DOMContentLoaded', () => {
      initTheme();
      initEventListeners();
      initCategories();
      checkAuthAndStorage();
    });

    // Theme Management
    function initTheme() {
      const isDark = localStorage.getItem('theme') === 'dark' || 
        (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches);
      document.documentElement.classList.toggle('dark', isDark);

      document.getElementById('themeToggle').addEventListener('click', () => {
        const dark = document.documentElement.classList.toggle('dark');
        localStorage.setItem('theme', dark ? 'dark' : 'light');
      });
    }

    // Category Chips Initialization
    function initCategories() {
      renderCategoryFilters();
      renderModalCategoryOptions();
    }

    function renderCategoryFilters() {
      elements.categoryFilterContainer.innerHTML = state.categories.map(cat => `
        <button onclick="setCategoryFilter('${cat.id}')" 
          class="px-3 py-1.5 rounded-xl text-xs font-semibold whitespace-nowrap transition flex items-center gap-1.5 ${
            state.selectedCategory === cat.id 
              ? 'bg-brand-600 text-white shadow-sm' 
              : 'bg-white dark:bg-slate-800 text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700/60 border border-slate-200 dark:border-slate-700'
          }">
          <span>${cat.name}</span>
        </button>
      `).join('');
    }

    function renderModalCategoryOptions() {
      const modalCats = state.categories.filter(c => c.id !== 'all');
      elements.modalCategoryOptions.innerHTML = modalCats.map(cat => `
        <button type="button" onclick="selectModalCategory('${cat.id}')" id="modalCat_${cat.id}"
          class="modal-cat-btn px-2.5 py-1 rounded-lg text-xs font-semibold transition border border-transparent ${cat.color}">
          ${cat.name}
        </button>
      `).join('');
    }

    window.setCategoryFilter = (catId) => {
      state.selectedCategory = catId;
      renderCategoryFilters();
      renderNotes();
    };

    window.selectModalCategory = (catId) => {
      document.querySelectorAll('.modal-cat-btn').forEach(b => b.classList.remove('ring-2', 'ring-brand-500'));
      const btn = document.getElementById(`modalCat_${catId}`);
      if (btn) btn.classList.add('ring-2', 'ring-brand-500');
      if (state.activeNote) state.activeNote.category = catId;
    };

    // Helper for formatting Markdown
    window.insertFormat = (prefix, suffix = '') => {
      const textarea = elements.noteContentInput;
      const start = textarea.selectionStart;
      const end = textarea.selectionEnd;
      const selected = textarea.value.substring(start, end);
      const replacement = prefix + selected + suffix;
      textarea.value = textarea.value.substring(0, start) + replacement + textarea.value.substring(end);
      textarea.focus();
    };

    // Auth & Storage Initialization
    function checkAuthAndStorage() {
      const savedConfig = localStorage.getItem('firebase_config');
      if (savedConfig && window.FirebaseCore) {
        try {
          const config = JSON.parse(savedConfig);
          const app = window.FirebaseCore.initializeApp(config);
          window.fbAuth = window.FirebaseCore.getAuth(app);
          window.fbDb = window.FirebaseCore.getFirestore(app);
          state.isFirebaseActive = true;
          elements.storageBadge.innerText = "Nube Firebase";
          elements.storageBadge.className = "text-[10px] uppercase tracking-wider font-semibold px-2 py-0.5 rounded-full bg-emerald-100 dark:bg-emerald-950/60 text-emerald-600 dark:text-emerald-400 border border-emerald-200 dark:border-emerald-800";

          window.FirebaseCore.onAuthStateChanged(window.fbAuth, (user) => {
            if (user) {
              state.currentUser = user;
              showDashboard();
              loadFirebaseNotes();
            } else {
              state.currentUser = null;
              showLockScreen();
            }
          });
          return;
        } catch (e) {
          console.error("Firebase Initialization Error", e);
        }
      }

      // Fallback: Local Access Mode
      state.isFirebaseActive = false;
      elements.storageBadge.innerText = "Modo Local";
      const isLocalLoggedIn = sessionStorage.getItem('local_logged_in') === 'true';
      if (isLocalLoggedIn) {
        state.currentUser = { uid: 'local_user', displayName: 'Usuario Local' };
        showDashboard();
        loadLocalNotes();
      } else {
        showLockScreen();
      }
    }

    function showDashboard() {
      elements.lockScreen.classList.add('hidden');
      elements.notesDashboard.classList.remove('hidden');
      elements.loginBtnNav.classList.add('hidden');
      elements.userMenuNav.classList.remove('hidden');
      if (state.currentUser?.displayName) {
        elements.userAvatar.innerText = state.currentUser.displayName.charAt(0).toUpperCase();
      }
    }

    function showLockScreen() {
      elements.lockScreen.classList.remove('hidden');
      elements.notesDashboard.classList.add('hidden');
      elements.loginBtnNav.classList.remove('hidden');
      elements.userMenuNav.classList.add('hidden');
    }

    // Load & Render Notes
    function loadLocalNotes() {
      const localData = localStorage.getItem('user_notes_data');
      state.notes = localData ? JSON.parse(localData) : [];
      renderNotes();
    }

    function saveLocalNotes() {
      localStorage.setItem('user_notes_data', JSON.stringify(state.notes));
      renderNotes();
    }

    function loadFirebaseNotes() {
      if (!state.currentUser || !window.fbDb) return;
      const q = window.FirebaseCore.query(
        window.FirebaseCore.collection(window.fbDb, 'notes'),
        window.FirebaseCore.where('userId', '==', state.currentUser.uid)
      );

      window.FirebaseCore.onSnapshot(q, (snapshot) => {
        state.notes = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
        renderNotes();
      }, (error) => {
        console.error("Firestore error:", error);
      });
    }

    function renderNotes() {
      const queryStr = state.searchQuery.toLowerCase();
      let filtered = state.notes.filter(n => {
        const matchesCategory = state.selectedCategory === 'all' || n.category === state.selectedCategory;
        const matchesSearch = n.title.toLowerCase().includes(queryStr) || 
                              n.content.toLowerCase().includes(queryStr) ||
                              (n.category && n.category.toLowerCase().includes(queryStr));
        return matchesCategory && matchesSearch;
      });

      // Sort: Pinned first, then by date modified
      filtered.sort((a, b) => (b.pinned ? 1 : 0) - (a.pinned ? 1 : 0) || new Date(b.updatedAt) - new Date(a.updatedAt));

      if (filtered.length === 0) {
        elements.notesGrid.innerHTML = '';
        elements.emptyState.classList.remove('hidden');
        return;
      }

      elements.emptyState.classList.add('hidden');
      elements.notesGrid.innerHTML = filtered.map(note => {
        const catObj = state.categories.find(c => c.id === note.category) || state.categories[1];
        const parsedContent = typeof marked !== 'undefined' ? marked.parse(note.content || '') : note.content;

        return `
          <div onclick="openNoteModal('${note.id}')" 
            class="group bg-white dark:bg-slate-800/90 rounded-2xl p-5 border border-slate-200/80 dark:border-slate-700/60 hover:shadow-lg hover:border-brand-500/40 transition duration-200 cursor-pointer flex flex-col justify-between relative overflow-hidden">
            
            ${note.pinned ? '<div class="absolute top-3 right-3 text-amber-500 text-xs"><i class="fa-solid fa-thumbtack"></i></div>' : ''}

            <div>
              <div class="flex items-center gap-2 mb-2">
                <span class="px-2 py-0.5 rounded-md text-[10px] font-bold uppercase tracking-wider ${catObj.color}">
                  ${catObj.name}
                </span>
                <span class="text-[11px] text-slate-400 ml-auto">${new Date(note.updatedAt).toLocaleDateString()}</span>
              </div>
              <h3 class="font-bold text-slate-800 dark:text-slate-100 text-base mb-2 group-hover:text-brand-600 dark:group-hover:text-brand-400 transition line-clamp-1">
                ${escapeHtml(note.title || 'Sin título')}
              </h3>
              <div class="note-content text-xs text-slate-600 dark:text-slate-300 line-clamp-4 leading-relaxed mb-4">
                ${parsedContent}
              </div>
            </div>

            <div class="pt-3 border-t border-slate-100 dark:border-slate-700/50 flex items-center justify-between text-xs text-slate-400">
              <span class="hover:text-slate-600 dark:hover:text-slate-200"><i class="fa-regular fa-pen-to-square"></i> Editar</span>
              <button onclick="event.stopPropagation(); togglePinNote('${note.id}')" class="hover:text-amber-500 p-1">
                <i class="fa-solid fa-thumbtack ${note.pinned ? 'text-amber-500' : ''}"></i>
              </button>
            </div>
          </div>
        `;
      }).join('');
    }

    function escapeHtml(text) {
      return text.replace(/[&<"']/g, m => ({ '&': '&amp;', '<': '&lt;', '"': '&quot;', "'": '&#039;' }[m]));
    }

    // Modal Actions
    window.openNoteModal = (noteId = null) => {
      if (noteId) {
        state.activeNote = { ...state.notes.find(n => n.id === noteId) };
        document.getElementById('modalTitle').innerText = 'Editar Nota';
        elements.deleteNoteBtn.classList.remove('hidden');
      } else {
        state.activeNote = {
          id: 'note_' + Date.now(),
          title: '',
          content: '',
          category: state.selectedCategory === 'all' ? 'personal' : state.selectedCategory,
          pinned: false,
          createdAt: new Date().toISOString(),
          updatedAt: new Date().toISOString(),
          userId: state.currentUser ? state.currentUser.uid : 'local'
        };
        document.getElementById('modalTitle').innerText = 'Nueva Nota';
        elements.deleteNoteBtn.classList.add('hidden');
      }

      elements.noteTitleInput.value = state.activeNote.title || '';
      elements.noteContentInput.value = state.activeNote.content || '';
      selectModalCategory(state.activeNote.category);
      updatePinModalBtn();

      elements.noteModal.classList.remove('hidden');
      setTimeout(() => elements.noteModal.classList.remove('opacity-0'), 10);
    };

    function closeNoteModal() {
      elements.noteModal.classList.add('opacity-0');
      setTimeout(() => elements.noteModal.classList.add('hidden'), 200);
      state.activeNote = null;
    }

    function updatePinModalBtn() {
      if (state.activeNote && state.activeNote.pinned) {
        elements.pinModalBtn.classList.add('text-amber-500');
      } else {
        elements.pinModalBtn.classList.remove('text-amber-500');
      }
    }

    window.togglePinNote = (noteId) => {
      const note = state.notes.find(n => n.id === noteId);
      if (note) {
        note.pinned = !note.pinned;
        note.updatedAt = new Date().toISOString();
        saveNoteState(note);
      }
    };

    async function saveNoteState(note) {
      if (state.isFirebaseActive && state.currentUser) {
        await window.FirebaseCore.setDoc(window.FirebaseCore.doc(window.fbDb, 'notes', note.id), note);
      } else {
        const idx = state.notes.findIndex(n => n.id === note.id);
        if (idx >= 0) state.notes[idx] = note;
        else state.notes.push(note);
        saveLocalNotes();
      }
    }

    // Event Listeners Initialization
    function initEventListeners() {
      // New Note Buttons
      document.getElementById('newNoteBtn').addEventListener('click', () => openNoteModal());
      document.getElementById('emptyNewNoteBtn').addEventListener('click', () => openNoteModal());

      // Modal Controls
      document.getElementById('closeNoteModal').addEventListener('click', closeNoteModal);
      document.getElementById('cancelNoteBtn').addEventListener('click', closeNoteModal);

      // Pin Toggle in Modal
      elements.pinModalBtn.addEventListener('click', () => {
        if (state.activeNote) {
          state.activeNote.pinned = !state.activeNote.pinned;
          updatePinModalBtn();
        }
      });

      // Save Note Action
      document.getElementById('saveNoteBtn').addEventListener('click', async () => {
        if (!state.activeNote) return;
        state.activeNote.title = elements.noteTitleInput.value.trim();
        state.activeNote.content = elements.noteContentInput.value.trim();
        state.activeNote.updatedAt = new Date().toISOString();

        if (!state.activeNote.title && !state.activeNote.content) {
          closeNoteModal();
          return;
        }

        await saveNoteState(state.activeNote);
        closeNoteModal();
      });

      // Delete Note Action
      elements.deleteNoteBtn.addEventListener('click', async () => {
        if (!state.activeNote) return;
        if (state.isFirebaseActive && state.currentUser) {
          await window.FirebaseCore.deleteDoc(window.FirebaseCore.doc(window.fbDb, 'notes', state.activeNote.id));
        } else {
          state.notes = state.notes.filter(n => n.id !== state.activeNote.id);
          saveLocalNotes();
        }
        closeNoteModal();
      });

      // Search Handler
      const handleSearch = (e) => {
        state.searchQuery = e.target.value;
        renderNotes();
      };
      elements.searchInput.addEventListener('input', handleSearch);
      elements.searchInputMobile.addEventListener('input', handleSearch);

      // Export / Backup Notes
      document.getElementById('exportBtn').addEventListener('click', () => {
        const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(state.notes, null, 2));
        const downloadAnchor = document.createElement('a');
        downloadAnchor.setAttribute("href", dataStr);
        downloadAnchor.setAttribute("download", `mis_notas_backup_${new Date().toISOString().slice(0,10)}.json`);
        document.body.appendChild(downloadAnchor);
        downloadAnchor.click();
        downloadAnchor.remove();
      });

      // Auth & Modal Triggers
      elements.loginBtnNav.addEventListener('click', () => elements.authModal.classList.remove('hidden'));
      document.getElementById('mainLoginBtn').addEventListener('click', () => elements.authModal.classList.remove('hidden'));
      document.getElementById('closeAuthModal').addEventListener('click', () => elements.authModal.classList.add('hidden'));

      // Config Modal
      document.getElementById('configBtn').addEventListener('click', () => elements.configModal.classList.remove('hidden'));
      document.getElementById('closeConfigModal').addEventListener('click', () => elements.configModal.classList.add('hidden'));

      // Guide Modal
      document.getElementById('guideBtn').addEventListener('click', () => elements.guideModal.classList.remove('hidden'));
      document.getElementById('closeGuideModal').addEventListener('click', () => elements.guideModal.classList.add('hidden'));
      document.getElementById('understoodGuideBtn').addEventListener('click', () => elements.guideModal.classList.add('hidden'));

      // Local PIN Access
      document.getElementById('localAccessBtn').addEventListener('click', promptPinAccess);
      document.getElementById('usePinAuthBtn').addEventListener('click', () => {
        elements.authModal.classList.add('hidden');
        promptPinAccess();
      });

      // Logout
      document.getElementById('logoutBtn').addEventListener('click', () => {
        if (state.isFirebaseActive && window.fbAuth) {
          window.FirebaseCore.signOut(window.fbAuth);
        }
        sessionStorage.removeItem('local_logged_in');
        state.currentUser = null;
        showLockScreen();
      });

      // Firebase Config Save
      document.getElementById('saveConfigBtn').addEventListener('click', () => {
        const raw = document.getElementById('firebaseConfigInput').value.trim();
        try {
          JSON.parse(raw);
          localStorage.setItem('firebase_config', raw);
          location.reload();
        } catch (err) {
          alert("El código ingresado no es un JSON válido. Revisa las comillas y comas.");
        }
      });

      document.getElementById('clearConfigBtn').addEventListener('click', () => {
        localStorage.removeItem('firebase_config');
        location.reload();
      });

      // Auth Forms (Firebase Google/Email)
      document.getElementById('googleAuthBtn').addEventListener('click', async () => {
        if (!state.isFirebaseActive || !window.fbAuth) {
          alert("Debes configurar las claves de Firebase en el icono de engranaje (⚙️) antes de usar Google Login.");
          return;
        }
        try {
          const provider = new window.FirebaseCore.GoogleAuthProvider();
          await window.FirebaseCore.signInWithPopup(window.fbAuth, provider);
          elements.authModal.classList.add('hidden');
        } catch (e) {
          alert("Error de autenticación con Google: " + e.message);
        }
      });

      document.getElementById('emailAuthForm').addEventListener('submit', async (e) => {
        e.preventDefault();
        if (!state.isFirebaseActive || !window.fbAuth) {
          alert("Configura Firebase primero en el icono de engranaje (⚙️).");
          return;
        }
        const email = document.getElementById('authEmail').value;
        const pass = document.getElementById('authPassword').value;

        try {
          await window.FirebaseCore.signInWithEmailAndPassword(window.fbAuth, email, pass);
          elements.authModal.classList.add('hidden');
        } catch (err) {
          try {
            await window.FirebaseCore.createUserWithEmailAndPassword(window.fbAuth, email, pass);
            elements.authModal.classList.add('hidden');
          } catch (createErr) {
            alert("Error de acceso: " + createErr.message);
          }
        }
      });
    }

    function promptPinAccess() {
      const pin = prompt("Introduce tu PIN de acceso local (Por defecto: 1234):");
      if (pin === state.pinCode) {
        sessionStorage.setItem('local_logged_in', 'true');
        state.currentUser = { uid: 'local_user', displayName: 'Usuario Local' };
        showDashboard();
        loadLocalNotes();
      } else if (pin !== null) {
        alert("PIN incorrecto.");
      }
    }
  </script>
</body>
</html>
