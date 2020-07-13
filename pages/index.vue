<template>
  <div class="container">
    <div>
      <!-- <ColorModePicker /> -->
      <logo />
      <h1 class="title">The theme will change on the go</h1>
    </div>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";
import ColorModePicker from "~/components/ColorModePicker.vue";
export default {
  components: {
    Logo,
    ColorModePicker
  }
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 400;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
