<script setup>
import FooterAttribution from './components/FooterAttribution.vue';
import AdviceItem from './components/AdviceItem.vue';
</script>

<template>
  <main>
    <AdviceItem/>
  </main>
  <footer>
    <FooterAttribution/>
  </footer>
</template>

<style scoped>

footer {
    position: absolute;
    bottom: 10px;
}
</style>
