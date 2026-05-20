<template>
    <div class="container mt-4">
      <h1 class="mb-4">Latest News</h1>
  
      <div class="row mb-4">
        <div class="col-md-12">
          <input 
            v-model="searchQuery" 
            type="text" 
            class="form-control" 
            placeholder="Search by title, date, category or content..."
          />
        </div>
      </div>
  
      <div class="row">
        <div v-for="item in paginatedNews" :key="item.id" class="col-md-4 mb-3">
          <div class="card h-100">
            <div class="card-body">
              <h5 class="card-title">{{ item.title }}</h5>
              <h6 class="card-subtitle mb-2 text-muted">{{ item.category }} | {{ item.date }}</h6>
              <p class="card-text">{{ item.content }}</p>
            </div>
          </div>
        </div>
      </div>
  
      <nav class="mt-4">
        <ul class="pagination justify-content-center">
          <li class="page-item" :class="{ disabled: currentPage === 1 }">
            <button class="page-link" @click="currentPage--">Previous</button>
          </li>
          <li class="page-item" :class="{ disabled: currentPage === totalPages }">
            <button class="page-link" @click="currentPage++">Next</button>
          </li>
        </ul>
      </nav>
    </div>
  </template>
  
  <script setup>
  import { ref, computed, onMounted } from 'vue';
  import newsData from '../../public/news.json'; // Adjust path as needed
  
  const news = ref([]);
  const searchQuery = ref('');
  const currentPage = ref(1);
  const itemsPerPage = 3;
  
  onMounted(() => {
    news.value = newsData;
  });
  
  // Logic for Search (Filters date, title, content, and category) [cite: 28]
  const filteredNews = computed(() => {
    return news.value.filter(item => {
      const query = searchQuery.value.toLowerCase();
      return (
        item.title.toLowerCase().includes(query) ||
        item.content.toLowerCase().includes(query) ||
        item.category.toLowerCase().includes(query) ||
        item.date.includes(query)
      );
    });
  });
  
  // Logic for Pagination [cite: 29, 59]
  const totalPages = computed(() => Math.ceil(filteredNews.value.length / itemsPerPage));
  
  const paginatedNews = computed(() => {
    const start = (currentPage.value - 1) * itemsPerPage;
    const end = start + itemsPerPage;
    return filteredNews.value.slice(start, end);
  });
  </script>