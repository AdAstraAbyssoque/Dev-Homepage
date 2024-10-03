<template>
  <div class="full-width-index">
    <div class="front"></div>
    <div class="home">
      <div class="FPHero">
        <TrmHero />
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import TrmHero from "./TrmHero.vue";

export default defineComponent({
  name: 'TrmPageIndex',
  components: {
    TrmHero
  }
});
</script>

<style scoped>
.full-width-index h1,
.full-width-index h2 {
  font-weight: 500;
}
.full-width-index {
  width: 100vw;
  max-width: 100vw;
  margin-left: calc(-50vw + 50%);
  margin-right: calc(-50vw + 50%);
  overflow-x: hidden;
}
.FPHero {
  width: 100vw;
  height: 100vh;
}
.front {
  width: 100%;
  height: 5vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(245, 245, 245, 0);
}
.home {
  height: 230vh;
}
</style>
