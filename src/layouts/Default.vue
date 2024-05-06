<template>
  <div class="wrapper">
    <div class="container">
        <Header />
        <slot />
    </div>
  </div>
</template>
<script>
import Header from "../components/Header.vue";
export default {
  name: 'Default',
  components: {
    Header
  }
}
</script>
