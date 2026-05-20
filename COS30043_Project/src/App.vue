<template>
  <!-- 1. The dynamic class binds the global theme state to the parent wrapper -->
  <div id="app-container" :class="[currentTheme]">
    <AppSidebar 
      :isOpen="isSidebarOpen" 
      @toggle="isSidebarOpen = !isSidebarOpen" 
    />
    
    <div class="main-wrapper">
      <!-- 2. Pass theme state and listener down to your updated header -->
      <AppHeader 
        :theme="currentTheme"
        @toggle-sidebar="isSidebarOpen = !isSidebarOpen" 
        @toggle-theme="handleThemeToggle"
      />
      
      <main class="content-body container-fluid p-4">
        <!-- 3. Wrap your router-view in a smooth transition if desired -->
        <router-view v-slot="{ Component }">
          <transition name="page-fade" mode="out-in">
            <component :is="Component" />
          </transition>
        </router-view>
      </main>
    </div>

    <Transition name="fade">
      <div 
        v-if="isSidebarOpen" 
        class="sidebar-backdrop" 
        @click="isSidebarOpen = false"
      ></div>
    </Transition>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import AppSidebar from './components/sidebar.vue';
import AppHeader from './components/header.vue';

const isSidebarOpen = ref(false);

// --- Global Theme Logic ---
const currentTheme = ref('light-mode');

const handleThemeToggle = () => {
  currentTheme.value = currentTheme.value === 'light-mode' ? 'dark-mode' : 'light-mode';
  
  // Apply data attribute globally for Bootstrap 5.3+ framework dark mode compatibility
  const bsTheme = currentTheme.value === 'dark-mode' ? 'dark' : 'light';
  document.documentElement.setAttribute('data-bs-theme', bsTheme);
  
  // Optional: persist user choice in local storage
  localStorage.setItem('user-theme', currentTheme.value);
};

// Check for saved preference on startup
onMounted(() => {
  const savedTheme = localStorage.getItem('user-theme');
  if (savedTheme) {
    currentTheme.value = savedTheme;
    const bsTheme = savedTheme === 'dark-mode' ? 'dark' : 'light';
    document.documentElement.setAttribute('data-bs-theme', bsTheme);
  }
});
</script>

<style>
/* --- 1. SMOOTH THEME TRANSITION ANCHOR --- */
/* Placing transition properties on the common parent ensures every layout background */
/* and font color shifts linearly together instead of flashing abruptly. */
#app-container,
.main-wrapper,
.content-body,
.navbar,
aside {
  transition: background-color 0.4s cubic-bezier(0.25, 0.8, 0.25, 1), 
              color 0.4s cubic-bezier(0.25, 0.8, 0.25, 1),
              border-color 0.4s ease;
}

#app-container {
  display: flex;
  min-height: 100vh;
  position: relative;
  overflow-x: hidden;
}

/* --- 2. THEME CLASS VARIABLE DEFINITIONS --- */
.light-mode {
  --bg-main: #f8f9fa;
  --bg-surface: #ffffff;
  --text-main: #212529;
  --border-color: #dee2e6;
}

.dark-mode {
  --bg-main: #121212;
  --bg-surface: #1e1e1e;
  --text-main: #f8f9fa;
  --border-color: #2d2d2d;
}

/* --- 3. APPLYING THE VARIABLES --- */
/* By referencing CSS variables, sub-pages automatically shift states with App.vue */
.main-wrapper {
  flex: 1;
  margin-left: 70px; 
  background-color: var(--bg-main);
  min-width: 0;
  display: flex;
  flex-direction: column;
}

.content-body {
  flex: 1;
  padding: 2rem;
  width: 100%;
  color: var(--text-main);
}

/* --- 4. SMOOTH PAGE/ROUTER TRANSITION ANIMATION --- */
.page-fade-enter-active,
.page-fade-leave-active {
  transition: opacity 0.25s ease, transform 0.25s ease;
}

.page-fade-enter-from {
  opacity: 0;
  transform: translateY(8px);
}
.page-fade-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}

/* Backdrop Fade Styling */
.fade-enter-active, .fade-leave-active { transition: opacity 0.3s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; }
.sidebar-backdrop {
  position: fixed;
  top: 0; left: 0; right: 0; bottom: 0;
  background: rgba(0,0,0,0.4);
  z-index: 1020;
}

/* --- ADVANCED MOBILE RESOLUTION FIX --- */
@media (max-width: 576px) {
  .main-wrapper { margin-left: 70px; }
  .content-body { padding: 0.5rem !important; }
  .content-body h1 { font-size: 1.4rem !important; }
  .content-body h2 { font-size: 1.2rem !important; }
  .content-body p { font-size: 0.8rem !important; }
  .content-body .btn { padding: 0.4rem 0.8rem !important; font-size: 0.8rem !important; }
  .content-body img { max-width: 100%; height: auto; }
}
</style>