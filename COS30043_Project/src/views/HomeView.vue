<template>
  <div class="home-container">
    <!-- FIX: Background Image binding clean-up -->
    <div class="hero-banner shadow">
      <div class="hero-overlay">
        <div class="container text-center text-md-start">
          <div class="row align-items-center">
            <div class="col-md-8">
              <h1 class="display-3 fw-bold text-white">CNH Digital Campus</h1>
              <p class="fs-4 text-white-50">
                An All-in-One Management System for Cong Nghiep Highschool
              </p>
              <div class="mt-4">
                <router-link to="/news" class="btn btn-primary btn-lg me-3 px-4 shadow">News</router-link>
                <router-link to="/about" class="btn btn-outline-light btn-lg px-4">Learn More</router-link>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Student Resources Grid Section -->
    <div class="container my-5">
      <div class="row text-center mb-4">
        <h2 class="fw-bold text-main-theme">Student Resources</h2>
        <p class="text-muted-theme">Access essential campus tools</p>
      </div>

      <div class="row g-4">
        <div v-for="link in quickLinks" :key="link.title" class="col-md-4 col-sm-6">
          <div class="card h-100 border-0 shadow-sm hover-card bg-surface-theme border-theme">
            <div class="card-body p-4 text-center">
              <div class="icon-box mb-3 mx-auto">
                <i :class="link.icon"></i>
              </div>
              <h5 class="fw-bold text-main-theme">{{ link.title }}</h5>
              <p class="text-muted-theme small">{{ link.desc }}</p>
              <router-link :to="link.path" class="stretched-link"></router-link>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Hall of Fame Section -->
    <div class="container my-5 pb-5">
      <div class="row align-items-center mb-4 gap-3 gap-md-0">
        <div class="col-md-6">
          <h2 class="fw-bold mb-0 text-main-theme">Hall of Fame</h2>
          <p class="text-muted-theme mb-0">Celebrating our tradition of excellence and outstanding achievements.</p>
        </div>
        <div class="col-md-6 text-md-end">
          <router-link to="/hall-of-fame" class="btn btn-outline-primary rounded-pill px-4">
            View All Achievements <i class="bi bi-arrow-right ms-2"></i>
          </router-link>
        </div>
      </div>

      <div class="row g-4">
        <div class="col-lg-8">
          <div class="achievement-card main shadow-sm overflow-hidden">
            <img src="/cn2.jpg" alt="School Ceremony" class="img-fluid achievement-img">
            <div class="achievement-overlay p-4">
              <span class="badge bg-warning text-dark mb-2">Badge of Excellence</span>
              <h3 class="text-white fw-bold">A Legacy of Community & Pride</h3>
              <p class="text-white-50 mb-0">Experience the grand traditions of CNH, where students and faculty unite to celebrate our collective journey and future aspirations.</p>
            </div>
          </div>
        </div>

        <div class="col-lg-4 d-flex flex-column gap-4">
          <div class="achievement-card secondary shadow-sm overflow-hidden flex-grow-1">
            <img src="/cn1.jpg" alt="Student Assembly" class="img-fluid achievement-img">
            <div class="achievement-overlay p-3">
              <h5 class="text-white fw-bold mb-1">Student Leadership & Spirit</h5>
              <p class="text-white-50 small mb-0">Fostering the next generation of leaders through active engagement and vibrant student assemblies.</p>
            </div>
          </div>
          
          <div class="achievement-card secondary shadow-sm overflow-hidden flex-grow-1">
            <img src="/cn3.jpg" alt="Classroom Success" class="img-fluid achievement-img">
            <div class="achievement-overlay p-3">
              <h5 class="text-white fw-bold mb-1">Modern Learning Spaces</h5>
              <p class="text-white-50 small mb-0">Architecture designed to inspire, providing a bright and innovative environment for academic discovery.</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Community Invitation Section -->
    <div class="container my-5 py-5 border-top border-theme">
      <div class="row align-items-center g-5">
        <div class="col-lg-6">
          <h2 class="fw-bold display-6 text-main-theme">Join Our Community</h2>
          <p class="text-muted-theme fs-5">
            Stay connected with CNH Digital Campus beyond the classroom. Join our official groups to receive real-time notifications, participate in discussions, and never miss an update.
          </p>
        </div>
        <div class="col-lg-6">
          <div class="d-flex flex-column gap-3">
            <a href="https://facebook.com" target="_blank" class="social-link fb shadow-sm">
              <div class="d-flex align-items-center p-3">
                <i class="bi bi-facebook fs-1 me-3"></i>
                <div>
                  <h5 class="mb-0 fw-bold">Official Facebook Page</h5>
                  <span class="small opacity-75">Follow for news, events, and school photos</span>
                </div>
              </div>
            </a>

            <a href="https://discord.com" target="_blank" class="social-link dc shadow-sm">
              <div class="d-flex align-items-center p-3">
                <i class="bi bi-discord fs-1 me-3"></i>
                <div>
                  <h5 class="mb-0 fw-bold">Student Discord Server</h5>
                  <span class="small opacity-75">Chat with classmates and get instant study help</span>
                </div>
              </div>
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const quickLinks = ref([
  { 
    title: 'Schedule', 
    desc: 'View your daily class timetable, room assignments, and exam dates.', 
    icon: 'bi bi-calendar3', 
    path: '/schedule' 
  },
  { 
    title: 'Grade', 
    desc: 'Access your academic transcripts, semester GPA, and teacher feedback.', 
    icon: 'bi bi-mortarboard-fill', 
    path: '/grades' 
  },
  { 
    title: 'Your Class', 
    desc: 'Connect with classmates and access course materials and assignments.', 
    icon: 'bi bi-journal-bookmark-fill', 
    path: '/class' 
  },
  { 
    title: 'Clubs', 
    desc: 'Explore extracurricular activities, join groups, and view club events.', 
    icon: 'bi bi-trophy-fill', 
    path: '/clubs' 
  },
  { 
    title: 'Staffs', 
    desc: 'Browse the faculty directory to find teacher contact info and office hours.', 
    icon: 'bi bi-person-lines-fill', 
    path: '/staff' 
  },
  { 
    title: 'Support', 
    desc: 'Submit technical queries or contact the student office for assistance.', 
    icon: 'bi bi-chat-dots-fill', 
    path: '/support' 
  }
]);
</script>

<style scoped>
.home-container {
  /* Prevent any nested content from leaking pass wrapper layout boundaries */
  width: 100%;
}

.hero-banner {
  height: 450px;
  background-size: cover;
  background-position: center;
  position: relative;
  margin-top: -24px;
  /* Fixed direct routing for public resources in Vite build configurations */
  background-image: url('/banner.png'); 
  transition: all 0.3s ease;
}

.hero-overlay {
  height: 100%;
  width: 100%;
  background: linear-gradient(90deg, rgba(0,0,0,0.8) 0%, rgba(0,0,0,0.4) 50%, rgba(0,0,0,0) 100%);
  display: flex;
  align-items: center;
}

/* --- Global Theme Integration Classes --- */
.text-main-theme {
  color: var(--text-main);
  transition: color 0.3s ease;
}

.text-muted-theme {
  color: #6c757d;
  transition: color 0.3s ease;
}
:deep(.dark-mode) .text-muted-theme {
  color: #94a3b8;
}

.bg-surface-theme {
  background-color: var(--bg-surface) !important;
  transition: background-color 0.3s ease;
}

.border-theme {
  border-color: var(--border-color) !important;
  transition: border-color 0.3s ease;
}

/* Icon Box adaptation */
.icon-box {
  width: 60px;
  height: 60px;
  background-color: #e7f1ff;
  color: #0d6efd;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 12px;
  font-size: 1.5rem;
  transition: background-color 0.3s ease, color 0.3s ease;
}
:deep(.dark-mode) .icon-box {
  background-color: #1e293b;
  color: #38bdf8;
}

.hover-card {
  transition: transform 0.3s ease, box-shadow 0.3s ease, background-color 0.3s ease;
  border-radius: 15px;
}
.hover-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 1rem 2.5rem rgba(0,0,0,0.12) !important;
}
:deep(.dark-mode) .hover-card:hover {
  box-shadow: 0 1rem 2.5rem rgba(0,0,0,0.4) !important;
}

/* Hall of Fame Area Setup */
.achievement-card {
  position: relative;
  border-radius: 20px;
  background: #000;
  height: 100%;
  cursor: pointer;
}

.achievement-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0.85;
  transition: transform 0.5s ease, opacity 0.5s ease;
}

.achievement-card:hover .achievement-img {
  transform: scale(1.03);
  opacity: 0.65;
}

.achievement-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(transparent, rgba(0, 0, 0, 0.95));
  z-index: 2;
}

.main { min-height: 450px; }
.secondary { min-height: 210px; }

@media (min-width: 992px) {
  .achievement-card.secondary {
    height: calc(50% - 12px);
  }
}

/* Community Navigation Triggers */
.social-link {
  text-decoration: none;
  color: white;
  border-radius: 12px;
  transition: transform 0.3s ease, filter 0.3s ease;
}
.social-link:hover {
  transform: translateX(6px);
  filter: brightness(1.1);
}

.fb { background: linear-gradient(45deg, #1877F2, #0056b3); }
.dc { background: linear-gradient(45deg, #5865F2, #404eed); }

/* --- MOBILE COMPATIBILITY MEDIA ADJUSTMENT --- */
@media (max-width: 576px) {
  .hero-banner {
    height: 320px;
    background-image: url('/banner_vertical.png') !important;
    background-position: bottom center;
    border-radius: 15px;
    margin-bottom: 20px;
  }

  .hero-overlay {
    background: rgba(0, 0, 0, 0.45); 
    border-radius: 15px;
  }

  .display-3 {
    font-size: 1.8rem !important;
  }
  
  .fs-4 {
    font-size: 1rem !important;
  }

  .btn-lg {
    padding: 0.5rem 1rem !important;
    font-size: 0.9rem !important;
  }
}
</style>