<template>
  <div class="pre">
    name:{{name}}
    <img @click="closePre" alt="Vue logo" src="../assets/logo.png" />
  </div>
</template>
<script lang="ts">
import { defineComponent, ref } from "vue";
export default defineComponent({
  name: "Pre",
  props: {
    name: {
      type: String,
      default: "",
    },
  },
  emits: ["update:showPre"],
  setup(props, ctx) {
    const closePre = () => {
      ctx.emit("update:showPre", false);
    };
    return {
      closePre,
    };
  },
});
</script>
<style>
.pre {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  border: 10px double brown;
  background-color: #eee;
}
.pre img {
  width: 100%;
}
</style>