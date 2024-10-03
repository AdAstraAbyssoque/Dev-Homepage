<template>
  <section class="hero">
    <div class="hero-content">
      <h1>Welcome to My Website</h1>
      <p>This is a hero section with 100vh height.</p>
    </div>
  </section>
</template>

<script>
export default {
  name: 'TrmIndexUpCom',
};
</script>

<style scoped>
.hero {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f5f5f5;
  text-align: center;
  background-image: url("../assets/banner.jpg");
  background-size: cover;
  background-position: center;
}

.hero-content {
  max-width: 600px;
  background-color: rgba(255, 255, 255, 0.8); /* Optional: to make text more readable */
  padding: 20px; /* Optional: to add some padding around the content */
}

h1 {
  font-size: 3rem;
  margin-bottom: 1rem;
}

p {
  font-size: 1.5rem;
  color: #666;
}
</style>