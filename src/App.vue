<template>
  <div id="app">
    <FormValidation />
  </div>
</template>

<script>
import FormValidation from "./components/FormValidation.vue";

export default {
  name: "App",
  components: {
    FormValidation,
  },
};
</script>

<style lang="scss">
$font-body: Helvetica, sans-serif;
body {
  font: 100% $font-body;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
