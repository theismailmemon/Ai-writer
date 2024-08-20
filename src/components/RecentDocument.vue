<template>
  <div class="">
    <table class="min-w-full bg-white">
      <thead>
        <tr>
          <th class="py-[6px] px-4 bg-gray-100 text-left font-bold w-1/4">
            Title
          </th>
          <th class="py-[6px] px-4 bg-gray-100 text-left font-bold w-1/6">
            Owner
          </th>
          <th class="py-[6px] px-4 bg-gray-100 text-left font-bold w-1/4">
            Last Modified
          </th>
          <th class="py-[6px] px-4 bg-gray-100 text-left font-bold w-1/6">
            Actions
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-if="documents.length === 0">
          <td colspan="4" class="text-center text-gray-500 text-lg py-4">
            No documents found
          </td>
        </tr>
        <tr
          v-for="(item, index) in documents"
          :key="index"
          :class="{ 'border-t border-gray-200': index !== 0 }"
        >
          <td class="py-2 px-4 text-lg w-1/4">
            {{ item.title || "--" }}
          </td>
          <td class="py-2 px-4 text-lg w-1/6">
            {{ item.owner || "--" }}
          </td>
          <td class="py-2 px-4 text-lg w-1/4">
            {{ item.lastModified || "--" }}
          </td>
          <td class="py-2 px-4 w-1/6">
            <div class="relative inline-block">
              <div
                class="absolute bottom-full mb-2 left-1/2 transform -translate-x-1/2 bg-gray-700 text-white text-[13px] py-1 px-[10px] opacity-0 tooltip transition-opacity duration-300"
              >
                Edit
                <div
                  class="absolute bottom-[-5px] left-1/2 transform -translate-x-1/2 w-0 h-0 border-l-[6px] border-r-[6px] border-t-[6px] border-l-transparent border-r-transparent border-t-gray-700"
                ></div>
              </div>
              <button
                class="w-[34px] h-[34px] border rounded-full flex items-center justify-center border-[#b08f6c] hover:tooltip-show"
                aria-label="Edit"
                @click="editDocument(index)"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 24 24"
                  fill="currentColor"
                  class="size-5 text-[#b08f6c]"
                >
                  <path
                    d="M21.731 2.269a2.625 2.625 0 0 0-3.712 0l-1.157 1.157 3.712 3.712 1.157-1.157a2.625 2.625 0 0 0 0-3.712ZM19.513 8.199l-3.712-3.712-8.4 8.4a5.25 5.25 0 0 0-1.32 2.214l-.8 2.685a.75.75 0 0 0 .933.933l2.685-.8a5.25 5.25 0 0 0 2.214-1.32l8.4-8.4Z"
                  ></path>
                  <path
                    d="M5.25 5.25a3 3 0 0 0-3 3v10.5a3 3 0 0 0 3 3h10.5a3 3 0 0 0 3-3V13.5a.75.75 0 0 0-1.5 0v5.25a1.5 1.5 0 0 1-1.5 1.5H5.25a1.5 1.5 0 0 1-1.5-1.5V8.25a1.5 1.5 0 0 1 1.5-1.5h5.25a.75.75 0 0 0 0-1.5H5.25Z"
                  ></path>
                </svg>
              </button>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
  
  <script>
export default {
  name: "FolderDocument",
  components: {},
  props: {
    documents: {
      type: Array,
      required: true,
    },
  },
};
</script>
