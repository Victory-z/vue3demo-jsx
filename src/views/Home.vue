<template>
  <div class="home">
    <div class="box">
      <img alt="Vue logo" src="../assets/logo.png" />
      <a-button class="pre-btn" @click="showPre = true">预览</a-button>
      <teleport to="body">
        <pre-img v-if="showPre" v-model:showPre="showPre" name="vue"></pre-img>
      </teleport>
      <!-- <pre-img v-if="showPre" v-model:showPre="showPre" name="vue"></pre-img> -->
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import PreImg from "../components/PreImg.vue";
export default defineComponent({
  name: "Home",
  components: {
    PreImg,
  },
  setup() {
    const showPre = ref(false);
    return {
      showPre,
    };
  },
});
</script>
<style>
.box {
  width: 100px;
  height: 100px;
  margin: 0 auto;
  border: 2px double brown;
  position: relative;
}
.pre-btn {
  display: none;
  position: absolute;
  top: 32px;
  left: 15px;
}
.box:hover .pre-btn {
  display: inline-block;
}
.pre {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}
.pre img {
  width: 100%;
}
.box img {
  width: 100%;
}
</style>
