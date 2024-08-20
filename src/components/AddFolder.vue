<template>
    <div v-if="isOpen" class="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-50">
      <div class="relative bg-white w-full h-full max-w-full max-h-full overflow-auto">
        <button @click="onClose" class="absolute top-4 right-4 text-gray-600 hover:text-gray-800">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" class="w-8 h-8">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
        <div class="p-8">
          <h2 class="text-2xl font-bold mb-4">Add Folder</h2>
          <!-- Form or content goes here -->
          <button @click="onClose" class="mt-4 px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700">
            Close
          </button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      isOpen: {
        type: Boolean,
        required: true,
      },
    },
    methods: {
      onClose() {
        this.$emit('onClose');
      },
    },
  };
  </script>
  