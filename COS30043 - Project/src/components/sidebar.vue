<template>
    <div v-if="isOpen" class="sidebar-overlay" @click="$emit('toggle')"></div>
  
    <nav 
      class="sidebar text-white shadow" 
      :class="{ 'sidebar-open': isOpen }"
    >
      <button 
        class="toggle-btn shadow" 
        @click="$emit('toggle')"
        :aria-label="isOpen ? 'Close Sidebar' : 'Open Sidebar'"
      >
        <i class="bi" :class="isOpen ? 'bi-chevron-left' : 'bi-chevron-right'"></i>
      </button>
  
      <div class="logo-section d-flex align-items-center p-3">
        <img src="/logo.jpg" alt="CNH Logo" class="logo-img">
        <div v-if="isOpen" class="ms-3 logo-text animate__animated animate__fadeIn">
          <div class="fw-bold lh-1 text-truncate">CNH Digital Campus</div>
          <div class="sub-text mt-1">
            Cong Nghiep Highschool Online
          </div>
        </div>
      </div>
  
      <hr class="text-secondary mx-3">
  
      <div class="list-group list-group-flush px-2">
        <router-link to="/" class="nav-item">
          <i class="bi bi-house-door fs-4"></i>
          <span v-if="isOpen" class="ms-3">Home</span>
        </router-link>
  
        <router-link to="/news" class="nav-item">
          <i class="bi bi-file-earmark-text fs-4"></i>
          <span v-if="isOpen" class="ms-3">News</span>
        </router-link>
  
        <router-link to="/about" class="nav-item">
          <i class="bi bi-info-circle fs-4"></i>
          <span v-if="isOpen" class="ms-3">About</span>
        </router-link>
  
        <div class="mt-4 mb-2 px-3 account-label" v-if="isOpen">ACCOUNT</div>
  
        <router-link to="/login" class="nav-item">
          <i class="bi bi-box-arrow-in-right fs-4"></i>
          <span v-if="isOpen" class="ms-3">Login</span>
        </router-link>
  
        <router-link to="/register" class="nav-item">
          <i class="bi bi-person-plus fs-4"></i>
          <span v-if="isOpen" class="ms-3">Register</span>
        </router-link>
      </div>
    </nav>
  </template>
  
  <script setup>
  defineProps(['isOpen']);
  defineEmits(['toggle']);
  </script>
  
  <style scoped>
  .sidebar {
    position: fixed;
    top: 0;
    left: 0;
    height: 100vh;
    width: 70px;
    z-index: 2100;
    transition: width 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    overflow: visible;
    /* CUSTOM BACKGROUND COLOR */
    background-color: #2c2e30; 
  }
  
  .sidebar-open {
    width: 300px;
  }
  
  /* Sub-text Slogan Styling */
  .sub-text {
    font-size: 0.65rem;
    white-space: normal;
    color: #ced4da; /* Light grey for contrast */
    line-height: 1.2;
  }
  
  /* Account Category Label */
  .account-label {
    font-size: 0.75rem;
    color: #6c757d;
    font-weight: bold;
    letter-spacing: 1px;
  }
  
  /* Toggle Button Styling */
  .toggle-btn {
    position: absolute;
    right: -15px;
    top: 50%;
    transform: translateY(-50%);
    width: 30px;
    height: 30px;
    background-color: #0d6efd;
    color: white;
    border: none;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    z-index: 2101;
  }
  
  .sidebar-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: rgba(0, 0, 0, 0.5);
    z-index: 2050;
  }
  
  .logo-img {
    width: 40px;
    height: 40px;
    border-radius: 8px;
    flex-shrink: 0;
  }
  
  .nav-item {
    display: flex;
    align-items: center;
    padding: 12px 15px;
    color: #adb5bd;
    text-decoration: none;
    border-radius: 8px;
    margin-bottom: 4px;
    transition: all 0.2s;
  }
  
  .nav-item:hover {
    background: rgba(255, 255, 255, 0.1);
    color: #fff;
  }
  
  .router-link-active {
    background-color: #0d6efd !important;
    color: white !important;
  }
  </style>