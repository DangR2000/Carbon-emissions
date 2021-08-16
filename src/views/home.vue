<template>
  <div v-if="index == 0" class="index-container">
    <div class="txt-index">
      <h1>
        城区组团碳排放与用地布局关系模拟平台
      </h1>
    </div>
    <div class="bg-index"></div>
    <homeTopMenu @change="change" />
  </div>
  <div v-else-if="index == 1" class="index-container">
    <homeTopMenu @change="change" />
    <introduce />
  </div>
  <div v-else-if="index == 2" class="index-container">
    <homeTopMenu @change="change" />
    <funct />
  </div>
  <div v-else-if="index == 3" class="index-container">
    <homeTopMenu @change="change" />
    <!-- <About/> -->
  </div>
</template>

<script>
// @ is an alias to /src
import homeTopMenu from "@/components/home/HomeTopMenu.vue";
import introduce from "@/components/home/introduce.vue";
import funct from "@/components/home/funct.vue";
import About from '@/components/home/About.vue';
export default {
  components: {
    homeTopMenu,
    introduce,
    funct,
    About
  },
  data() {
    return {
      index: 0
    };
  },
  methods: {
    change(index) {
      this.index = index;
    }
  }
};
</script>
<style scoped>

</style>
