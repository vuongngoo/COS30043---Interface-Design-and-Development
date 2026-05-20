<template>
    <div class="container mt-5">
      <div class="row">
        <div class="col-lg-8 mx-auto">
          <section class="mb-5">
            <h2 class="h3">About This Project</h2>
            <p>
              This web application serves as a custom interface designed for the COS30043 unit. 
              It highlights the integration of reactive data binding and responsive layouts 
              using the Bootstrap framework.
            </p>
          </section>
  
          <section class="card p-4 shadow-sm mb-5">
            <h3 class="h5 mb-4">User Personalization</h3>
            <div class="row mb-3">
              <div class="col-md-6 mb-3">
                <label for="firstName" class="form-label">First Name</label>
                <input v-model="firstName" type="text" class="form-control" id="firstName" placeholder="Enter first name">
              </div>
              <div class="col-md-6 mb-3">
                <label for="lastName" class="form-label">Last Name</label>
                <input v-model="lastName" type="text" class="form-control" id="lastName" placeholder="Enter last name">
              </div>
            </div>
  
            <div v-if="firstName || lastName" class="alert alert-primary">
              <h4 class="mb-0">Welcome, {{ firstName }} {{ lastName }}!</h4>
            </div>
          </section>
  
          <section class="card p-4 shadow-sm text-center">
            <h3 class="h5 mb-4">Choose Your View</h3>
            <div class="d-flex justify-content-center gap-4 mb-4">
              <div class="form-check">
                <input v-model="viewChoice" class="form-check-input" type="radio" value="mountain" id="radioMountain">
                <label class="form-check-label" for="radioMountain">Mountain</label>
              </div>
              <div class="form-check">
                <input v-model="viewChoice" class="form-check-input" type="radio" value="ocean" id="radioOcean">
                <label class="form-check-label" for="radioOcean">Ocean</label>
              </div>
            </div>
  
            <div class="mt-3">
              <img v-if="viewChoice === 'mountain'" src="https://picsum.photos/id/10/800/400" class="img-fluid rounded shadow" alt="Mountain View">
              <img v-else-if="viewChoice === 'ocean'" src="https://picsum.photos/id/11/800/400" class="img-fluid rounded shadow" alt="Ocean View">
              <p v-else class="text-muted">Please select an option to see an image.</p>
            </div>
          </section>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const firstName = ref('');
  const lastName = ref('');
  const viewChoice = ref(''); // Options: 'mountain' or 'ocean'
  </script>