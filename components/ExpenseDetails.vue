<script setup>
import { initTooltips } from "flowbite";

onMounted(() => {
  initTooltips();
});

defineProps({
  details: {
    type: Object,
    required: true,
  },
  category: {
    type: Object,
    required: true,
  },
});
const emit = defineEmits(["removeExpense"]);

function handleRemove() {
  emit("removeExpense");
}
</script>

<template>
  <div class="flex items-center py-2">
    <button
      :data-tooltip-target="`tooltip-${details.id}`"
      data-tooltip-trigger="hover"
      class="cursor-default"
      type="button"
    >
      <Icon
        :name="category.icon"
        :color="category.color"
        class="w-10 h-10 p-2 mr-3 rounded-full dynamic-bg"
      />
    </button>

    <div
      :id="`tooltip-${details.id}`"
      role="tooltip"
      class="absolute z-10 invisible inline-block px-3 py-2 text-sm text-white bg-gray-700 rounded-lg shadow-sm opacity-0 tooltip transition-opacity duration-300 ease-in-out"
    >
      {{ category.name }}
      <div class="tooltip-arrow" data-popper-arrow></div>
    </div>

    <div
      class="w-full"
      @mouseover="showTrash = true"
      @mouseout="showTrash = false"
    >
      <div class="flex font-bold justify-between text-gray-800">
        <span>{{ details.name }}</span>
        <span class="text-sm">$ {{ details.expense }}</span>
      </div>
      <div class="flex justify-between">
        <p class="text-sm">{{ details.description }}</p>
        <button @click="handleRemove">
          <Icon
            name="material-symbols-light:delete-outline"
            class="w-5 h-5 text-red-700 hover:text-red-800 transition-all duration-100 ease-in-out"
          />
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.dynamic-bg {
  background-color: v-bind(category.bgColor);
}
</style>
