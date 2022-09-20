<script setup lang="ts">
import CalendarYear from "./components/CalendarYear.vue";
</script>
<template>
  <nav class="navbar" role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
      <a class="navbar-item" href="">
        <img
          src="https://www.lifepng.com/wp-content/uploads/2020/11/Grumpy-Cat-Tongue-png-hd.png"
        />
      </a>

      <a
        role="button"
        class="navbar-burger"
        aria-label="menu"
        aria-expanded="false"
        data-target="navbarBasicExample"
      >
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
      </a>
    </div>
  </nav>
  <main>
    <div class="container mt-6">
      <CalendarYear />
    </div>
  </main>
</template>

<style scoped>
.navbar {
  background-color: black;
  color: white;
}
</style>
