<template>
  <div class="">
    <table class="min-w-full bg-white">
      <thead>
        <tr>
          <th class="py-[6px] px-4 bg-gray-100 text-left font-bold w-1/4">
            Name
          </th>
          <th class="py-[6px] px-4 bg-gray-100 text-left font-bold w-1/8">
            Owner
          </th>
          <th class="py-[6px] px-4 bg-gray-100 text-left font-bold w-1/8">
            Folders
          </th>
          <th class="py-[6px] px-4 bg-gray-100 text-left font-bold w-1/8">
            Documents
          </th>
          <th class="py-[6px] px-4 bg-gray-100 text-left font-bold w-1/6">
            Last Modified
          </th>
          <th class="py-[6px] px-4 bg-gray-100 text-left font-bold w-1/6">
            Actions
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-if="documents.length === 0">
          <td colspan="6" class="text-center text-gray-500 text-lg py-4">
            No documents found
          </td>
        </tr>
        <tr
          v-for="(item, index) in documents"
          :key="index"
          :class="{ 'border-t border-gray-200': index !== 0 }"
        >
          <td class="py-2 px-4 text-lg w-1/6">
            {{ item.title || "--" }}
          </td>
          <td class="py-2 px-4 text-lg w-1/6">
            {{ item.owner || "--" }}
          </td>
          <td class="py-2 px-4 text-lg w-1/6">
            {{ item.folders || "--" }}
          </td>
          <td class="py-2 px-4 text-lg w-1/6">
            {{ item.documents || "--" }}
          </td>
          <td class="py-2 px-4 text-lg w-1/6">
            {{ item.lastModified || "--" }}
          </td>
          <td class="py-2 px-4 w-1/6">
            <div class="flex items-center gap-2">
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
              <div class="relative inline-block">
                <div
                  class="absolute bottom-full mb-2 left-1/2 transform -translate-x-1/2 bg-gray-700 text-white text-[13px] py-1 px-[10px] opacity-0 tooltip transition-opacity duration-300"
                >
                  Delete
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
                    class="size-5 fill-[#b08f6c]"
                    xmlns="http://www.w3.org/2000/svg"
                    width="21"
                    height="20"
                    viewBox="0 0 21 20"
                  >
                    <path
                      d="M17.7491 5.60833C17.7324 5.60833 17.7074 5.60833 17.6824 5.60833C13.2741 5.16667 8.87408 5 4.51574 5.44167L2.81574 5.60833C2.46574 5.64167 2.15741 5.39167 2.12408 5.04167C2.09074 4.69167 2.34074 4.39167 2.68241 4.35833L4.38241 4.19167C8.81574 3.74167 13.3074 3.91667 17.8074 4.35833C18.1491 4.39167 18.3991 4.7 18.3657 5.04167C18.3407 5.36667 18.0657 5.60833 17.7491 5.60833Z"
                    ></path>
                    <path
                      d="M7.33265 4.76699C7.29932 4.76699 7.26598 4.76699 7.22432 4.75866C6.89098 4.70033 6.65765 4.37533 6.71598 4.04199L6.89932 2.95033C7.03265 2.15033 7.21598 1.04199 9.15765 1.04199H11.341C13.291 1.04199 13.4743 2.19199 13.5993 2.95866L13.7826 4.04199C13.841 4.38366 13.6076 4.70866 13.2743 4.75866C12.9326 4.81699 12.6076 4.58366 12.5576 4.25033L12.3743 3.16699C12.2576 2.44199 12.2326 2.30033 11.3493 2.30033H9.16598C8.28265 2.30033 8.26598 2.41699 8.14098 3.15866L7.94932 4.24199C7.89932 4.55033 7.63265 4.76699 7.33265 4.76699Z"
                    ></path>
                    <path
                      d="M12.924 18.9586H7.57402C4.66569 18.9586 4.54902 17.3503 4.45735 16.0503L3.91569 7.65864C3.89069 7.31697 4.15735 7.01697 4.49902 6.99197C4.84902 6.97531 5.14069 7.23364 5.16569 7.57531L5.70735 15.967C5.79902 17.2336 5.83235 17.7086 7.57402 17.7086H12.924C14.674 17.7086 14.7074 17.2336 14.7907 15.967L15.3324 7.57531C15.3574 7.23364 15.6574 6.97531 15.999 6.99197C16.3407 7.01697 16.6074 7.30864 16.5824 7.65864L16.0407 16.0503C15.949 17.3503 15.8324 18.9586 12.924 18.9586Z"
                    ></path>
                    <path
                      d="M11.6324 14.375H8.85742C8.51576 14.375 8.23242 14.0917 8.23242 13.75C8.23242 13.4083 8.51576 13.125 8.85742 13.125H11.6324C11.9741 13.125 12.2574 13.4083 12.2574 13.75C12.2574 14.0917 11.9741 14.375 11.6324 14.375Z"
                    ></path>
                    <path
                      d="M12.3327 11.042H8.16602C7.82435 11.042 7.54102 10.7587 7.54102 10.417C7.54102 10.0753 7.82435 9.79199 8.16602 9.79199H12.3327C12.6743 9.79199 12.9577 10.0753 12.9577 10.417C12.9577 10.7587 12.6743 11.042 12.3327 11.042Z"
                    ></path>
                  </svg>
                </button>
              </div>
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
