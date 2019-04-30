<template>
  <table class="w-full">
    <caption class="bg-blue-500 text-white text-xl p-4">
      <div class="flex flex-row justify-between items-center">
        <span class="font-semibold">{{ titel }}</span>
        <slot name="titel-knop"></slot>
      </div>
    </caption>
    <thead></thead>
    <tbody></tbody>
    <tfoot></tfoot>
  </table>
</template>

<script>
export default {
  props: {
    titel: {
      type: String,
      default: "Titel"
    },
    items: {
      type: Array,
      // zelfde als:
      // function() {
      //   return []
      // }
      default: () => []
    },
    kolommen: {
      type: Array,
      default: () => []
    }
  }
};
</script>

<style></style>
