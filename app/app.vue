<template>
  <NuxtPage />
</template>
<script setup>
useHead({
  script: [
    {
      src: "https://cdn.tailwindcss.com"
    }
  ]
})
</script>
<style>
@media print {
  .mt-4.relative.pl-6.print-block {
    padding-left: 0rem !important;
  }
}
</style>

