<template>
  <div class="button-div">
    <div v-for="color in colors" :key="color">
      <el-button @click="$colorMode.preference = color" class="button-nuxt">{{
        color.toUpperCase()
      }}</el-button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      colors: ["system", "light", "dark", "sepia"]
    };
  }
};
</script>
<style>
.button-div {
  display: flex;
  justify-content: space-between;
}
.button-nuxt {
  width: 200px;
}
</style>
