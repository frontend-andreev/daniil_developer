<template>
  <component :is="layout">
    <Transition>
      <router-view />
    </Transition>
  </component>
</template>
<script>
import Default from './layouts/Default.vue';
export default {
  components: {Default},
  computed: {
    layout() {
      return 'Default'
    }
  }
}
</script>
<style scoped>
.v-enter-active,
.v-leave-active {
  transition: opacity 0.8s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>