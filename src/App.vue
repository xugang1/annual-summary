<template>
  <div class="container" @wheel="handleScroll">
    <transition :name="transitionName">
      <component :is="currentPage" :key="currentIndex" />
    </transition>
  </div>
</template>

<script>
import Page1 from "./components/Page1";
import Page2 from "./components/Page2";
import Page3 from "./components/Page3";
import Page4 from "./components/Page4";
import Page5 from "./components/Page5";
const _ = require("lodash");
export default {
  data() {
    return {
      pages: [Page1, Page2, Page3, Page4, Page5],
      currentIndex: 0,
      transitionName: "fade",
    };
  },
  computed: {
    currentPage() {
      return this.pages[this.currentIndex];
    },
  },
  methods: {
    handleScroll: _.debounce(function (event) {
      if (event.deltaY > 0 && this.currentIndex < this.pages.length - 1) {
        this.transitionName = "fade-next";
        this.currentIndex++;
      } else if (event.deltaY < 0 && this.currentIndex > 0) {
        this.transitionName = "fade-prev";
        this.currentIndex--;
      }
    }, 300),
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
.container {
  overflow: hidden;
  height: 100vh;
  position: relative;
}

.page {
  width: 100%;
  height: 100%;
}

.fade-next-enter-active,
.fade-next-leave-active,
.fade-prev-enter-active,
.fade-prev-leave-active {
  transition: opacity 0.5s;
}

.fade-next-enter,
.fade-prev-enter {
  opacity: 0;
}

.fade-next-leave-to,
.fade-prev-leave-to {
  opacity: 0;
}

</style>
