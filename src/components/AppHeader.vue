<script>
export default {
  name: "AppHeader",
};
</script>

<template>
  <header>
    <nav class="navbar navbar-expand-lg bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Boolfolio</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <router-link :to="{name: 'home'}" class="nav-link active" aria-current="page">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link :to="{name: 'projects'}" class="nav-link active" aria-current="page">Projects</router-link>
            </li>
            <li class="nav-item">
              <router-link :to="{name: 'about'}" class="nav-link active" aria-current="page">About us</router-link>
            </li>
           </ul>
        </div>
      </div>
    </nav>
  </header>
</template>
