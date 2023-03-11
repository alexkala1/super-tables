<template>
  <div class="flex items-center">
    <button
      class="bg-gray-500 text-gray-50 p-1 mx-2 mt-2 rounded-full w-10 h-10"
      :class="{ 'bg-gray-400 text-gray-50': currentPage === pageNumber }"
      @click="$emit('change', pageNumber)"
      v-for="pageNumber in totalPages"
      :key="pageNumber"
    >
      {{ pageNumber }}
    </button>
  </div>
</template>

<script lang="ts" setup>
defineProps({
  totalPages: Number,
  currentPage: Number,
});
defineEmits(["change"]);
</script>
