<script setup lang="ts">
import { computed } from "vue";
import { useData } from "vitepress";
import { AsyncThemeConfig } from "types";
import { useAllPosts, useCategories, usePageUrl } from "../composables";
import { useCurrentPageIndex } from "../blog";

import TrmCardCategorie from "./global/TrmCardCategorie.vue";
import TrmCardPost from "./global/TrmCardPost.vue";
import TrmPagination from "./TrmPagination.vue";
import TrmDividerTitle from "./global/TrmDividerTitle.vue";

const { page, theme } = useData<AsyncThemeConfig>();
const pageUrl = usePageUrl();
const currentPageIndex = useCurrentPageIndex();
const allPosts = useAllPosts();
const pageSize = theme.value.indexGenerator?.perPage || 10;

const categories = useCategories()
  .sort((a, b) => b[1] - a[1])
  .slice(0, 2);

const pageList = computed(() => {
  const startIdx = (currentPageIndex.value - 1) * pageSize;
  const endIdx = startIdx + pageSize;
  return allPosts.slice(startIdx, endIdx);
});
</script>

<template>
  <section class="hero">
    <div class="hero-content">
      <div class="typing-container">
        <span class="typing-text">{{ message }}</span>
      </div>
    </div>
  </section>
  <div style="height: 10vh; flex-shrink: 0;"></div>
  <div v-if="categories.length > 0"
       class="row hidden-sm narrow-margin">
    <div v-for="(item, index) in categories"
         class="col-lg-6"
         :key="index">
      <TrmCardCategorie :name="item[0]"
                        :length="item[1]"
                        :category-url="pageUrl.categorys + '?q=' + item[0]" />
    </div>
  </div>
  <div class="row narrow-margin">
    <div class="col-lg-12"
         v-if="categories.length > 0">
      <TrmDividerTitle :title="$t('title.newPublish')"
                       index="01" />
    </div>
    <div class="col-lg-4"
         v-for="item in pageList.slice(0, 3)"
         :key="item.url">
      <TrmCardPost :post="item"
                   :category-url="pageUrl.categorys"
                   :sticky="page.frontmatter.index && item.sticky && item.sticky > 0" />
    </div>
  </div>
  <TrmPagination :total="allPosts.length"
                 :size="pageSize" />
</template>

<script lang="ts">
export default {
  name: "TrmIndexUpCom",
  data() {
    return {
      message: "",
      fullMessage: "是乍见之欢，也是天各一方",
      typingSpeed: 200, // Typing speed in milliseconds
    };
  },
  mounted() {
    this.typeMessage();
  },
  methods: {
    typeMessage() {
      let currentIndex = 0;
      const type = () => {
        if (currentIndex < this.fullMessage.length) {
          this.message += this.fullMessage[currentIndex];
          currentIndex++;
          setTimeout(type, this.typingSpeed);
        } else {
          setTimeout(() => {
            this.message = "";
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
  top: 66.7%; /* Adjust for centering */
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

.narrow-margin {
  margin-left: 80px;
  margin-right: 80px;
}
</style>