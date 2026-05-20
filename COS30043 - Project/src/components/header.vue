<template>
  <nav class="navbar navbar-expand border-bottom sticky-top px-4">
    <div class="container-fluid px-0">
      <!-- Left or Center content can go here if needed later -->
      <div class="navbar-brand-placeholder"></div>

      <!-- Reorganized Actions Right-Side Alignment -->
      <div class="ms-auto d-flex align-items-center gap-3">
        
        <!-- 1. Language Switcher -->
        <div class="btn-group btn-group-sm" role="group" aria-label="Language Selector">
          <button type="button" class="btn btn-outline-primary active px-3">EN</button>
          <button type="button" class="btn btn-outline-primary px-3">VN</button>
        </div>
        
        <!-- 2. Global Daylight / Theme Mode Toggle Trigger -->
        <button 
          @click="$emit('toggle-theme')" 
          type="button" 
          class="btn btn-link p-2 theme-toggle-btn"
          :title="theme === 'dark-mode' ? 'Switch to Light Mode' : 'Switch to Dark Mode'"
        >
          <i :class="theme === 'dark-mode' ? 'bi bi-sun-fill text-warning' : 'bi bi-moon-fill text-secondary-theme'"></i>
        </button>

        <!-- Divider Line -->
        <div class="vr opacity-25 divider-theme" style="height: 30px;"></div>

        <!-- 3. User Action Dropdown Container -->
        <div class="position-relative" ref="dropdownContainer">
          <div class="user-action d-flex align-items-center ms-1" @click="toggleDropdown">
            <div class="profile-info text-end me-2 d-none d-lg-block">
              <div class="fw-bold small text-main-theme">Guest User</div>
              <div class="text-muted-theme" style="font-size: 0.65rem;">Account Actions</div>
            </div>
            <div class="avatar-box shadow-sm" :class="{ 'active': isDropdownOpen }">
              <i class="bi bi-person-circle"></i>
            </div>
          </div>

          <!-- Custom Popup Menu (Dropdown) -->
          <Transition name="dropdown">
            <div v-if="isDropdownOpen" class="avatar-popup shadow border rounded bg-popup-theme py-2">
              <div class="px-3 py-2 border-bottom d-lg-none border-popup-theme">
                <div class="fw-bold small text-main-theme">Guest User</div>
                <hr class="my-1 opacity-25 divider-theme">
              </div>
              <a href="#" class="dropdown-item px-3 py-2" @click.prevent="handleAction('profile')">
                <i class="bi bi-person me-2 text-primary"></i> View Profile
              </a>
              <a href="#" class="dropdown-item px-3 py-2" @click.prevent="handleAction('settings')">
                <i class="bi bi-gear me-2 text-secondary-theme"></i> Settings
              </a>
              <hr class="my-1 opacity-25 divider-theme">
              <a href="#" class="dropdown-item px-3 py-2 text-danger animate-logout" @click.prevent="handleAction('logout')">
                <i class="bi bi-box-arrow-right me-2"></i> Log Out
              </a>
            </div>
          </Transition>
        </div>
        
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// --- Props & Emits linked to App.vue Global State ---
defineProps({
  theme: {
    type: String,
    default: 'light-mode'
  }
})

defineEmits(['toggle-sidebar', 'toggle-theme'])

// --- Dropdown Management State ---
const isDropdownOpen = ref(false)
const dropdownContainer = ref(null)

const toggleDropdown = () => {
  isDropdownOpen.value = !isDropdownOpen.value
}

const handleAction = (actionType) => {
  console.log(`Navigating to: ${actionType}`)
  isDropdownOpen.value = false 
}

// Close dropdown if clicked anywhere outside the user module container
const handleClickOutside = (event) => {
  if (dropdownContainer.value && !dropdownContainer.value.contains(event.target)) {
    isDropdownOpen.value = false
  }
}

onMounted(() => {
  window.addEventListener('click', handleClickOutside)
})

onUnmounted(() => {
  window.removeEventListener('click', handleClickOutside)
})
</script>

<style scoped>
/* Theme tokens mapped directly to the parent layout wrapper definitions */
.navbar {
  z-index: 1030; 
  height: 64px;
  background-color: var(--bg-surface) !important;
  border-color: var(--border-color) !important;
}

/* User Action Trigger area */
.user-action {
  cursor: pointer;
  user-select: none;
}

.avatar-box {
  width: 40px;
  height: 40px;
  background-color: #f0f5ff;
  color: #0d6efd;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  font-size: 1.4rem;
  transition: all 0.2s ease;
}

/* Dark theme specific override for inactive avatar background */
:deep(.dark-mode) .avatar-box {
  background-color: #1e293b;
  color: #38bdf8;
}

.user-action:hover .avatar-box,
.avatar-box.active {
  background-color: #0d6efd !important;
  color: white !important;
  transform: translateY(-1px);
}

/* Light / Dark Mode Icon Styling */
.theme-toggle-btn {
  font-size: 1.15rem;
  transition: transform 0.2s ease;
  text-decoration: none;
}
.theme-toggle-btn:hover {
  transform: scale(1.15);
}

/* Custom Theme Adaptors for Layout Text and Borders */
.text-main-theme {
  color: var(--text-main);
}
.text-muted-theme {
  color: #6c757d;
}
:deep(.dark-mode) .text-muted-theme {
  color: #94a3b8;
}
.text-secondary-theme {
  color: #6c757d;
}
:deep(.dark-mode) .text-secondary-theme {
  color: #94a3b8;
}
.divider-theme, .border-popup-theme {
  color: var(--border-color);
  border-color: var(--border-color) !important;
}

/* Custom Popup Panel Styling matching current theme colors */
.avatar-popup {
  position: absolute;
  top: 100%;
  right: 0;
  margin-top: 0.5rem;
  width: 200px;
  z-index: 1040;
  transform-origin: top right;
  background-color: var(--bg-surface);
  border-color: var(--border-color) !important;
}

.dropdown-item {
  display: flex;
  align-items: center;
  color: var(--text-main);
  font-size: 0.875rem;
  text-decoration: none;
  transition: background-color 0.15s ease, color 0.15s ease;
}

.dropdown-item:hover {
  background-color: rgba(13, 110, 253, 0.08);
  color: #0d6efd;
}

.dropdown-item.text-danger:hover {
  background-color: rgba(220, 53, 69, 0.08);
  color: #dc3545;
}

/* Dropdown Menu Transition Effects */
.dropdown-enter-active,
.dropdown-leave-active {
  transition: transform 0.2s cubic-bezier(0.25, 0.8, 0.25, 1), opacity 0.15s ease;
}

.dropdown-enter-from,
.dropdown-leave-to {
  opacity: 0;
  transform: scale(0.95) translateY(-5px);
}

.btn-outline-primary {
  border-color: #0d6efd;
  color: #0d6efd;
  font-weight: 600;
}

.btn-outline-primary.active {
  background-color: #0d6efd;
  color: white;
}

@media (max-width: 576px) {
  .navbar {
    padding-left: 1rem;
    padding-right: 1rem;
  }
}
</style>