<template>
  <section class="hero">
    <div class="hero-content">
      <div class="typing-container">
        <span class="typing-text">{{ message }}</span>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'TrmIndexUpCom',
  data () {
    return {
      message: '',
      fullMessage: "是乍见之欢，也是天各一方",
      typingSpeed: 200, // Typing speed in milliseconds
    };
  },
  mounted () {
    this.typeMessage();
  },
  methods: {
    typeMessage () {
      let currentIndex = 0;
      const type = () => {
        if (currentIndex < this.fullMessage.length) {
          this.message += this.fullMessage[currentIndex];
          currentIndex++;
          setTimeout(type, this.typingSpeed);
        } else {
          setTimeout(() => {
            this.message = '';
            currentIndex = 0;
            type();
          }, this.typingSpeed * 20); // Delay before restarting
        }
      };
      type();
    },
  },
};
</script>

<style scoped>
.hero {
  height: 105vh;
  display: flex;
  justify-content: center;
  align-items: flex-start; /* Align items to the start */
  background-color: #f5f5f5;
  text-align: center;
  background-image: url("../assets/banner.jpg");
  background-size: cover;
  background-position: center;
  position: relative;
}

.hero-content {
  max-width: 600px;
  padding: 20px; /* Optional: to add some padding around the content */
  position: absolute;
  top: 66.6%; /* Position at 3/4 of the height */
  transform: translateY(-50%); /* Adjust for centering */
}

.typing-container {
  display: inline-block;
  padding: 10px 40px;
  border-radius: 20px;
  background-color: rgba(255, 255, 255, 0.389);
  color: #fff;
  font-size: 1.3rem;
  font-family: "Courier New", Courier, monospace;
  white-space: nowrap;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.typing-text {
  display: inline-block;
}
</style>