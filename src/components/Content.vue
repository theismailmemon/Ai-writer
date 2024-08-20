<template>
  <div>
    <div class="bg-gray-100 h-16 flex items-center justify-between px-8">
      <h1 class="text-black text-2xl font-bold">AI Writer</h1>
      <div class="flex items-center gap-2" v-if="isStep == 2">
        <button
          @click="isAddDocument = true"
          class="flex items-center gap-2 px-4 py-2 border border-[#b08f6c] text-[18px] text-gray-800 rounded-lg bg-white"
        >
          <span>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="icon icon-tabler icon-tabler-circle-plus"
              width="22"
              height="22"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="#1f2937"
              fill="none"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M3 12a9 9 0 1 0 18 0a9 9 0 0 0 -18 0" />
              <path d="M9 12h6" />
              <path d="M12 9v6" />
            </svg>
          </span>
          <span>Document</span>
        </button>

        <button
          @click="isAddFolder = true"
          class="flex items-center gap-2 px-4 py-2 border border-[#b08f6c] text-[18px] text-gray-800 rounded-lg bg-white"
        >
          <span>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="icon icon-tabler icon-tabler-circle-plus"
              width="22"
              height="22"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="#1f2937"
              fill="none"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M3 12a9 9 0 1 0 18 0a9 9 0 0 0 -18 0" />
              <path d="M9 12h6" />
              <path d="M12 9v6" />
            </svg>
          </span>
          <span>Folder</span>
        </button>
      </div>
    </div>
    <div class="mt-3 px-8">
      <div class="flex items-center justify-between gap-10">
        <div class="flex items-center">
          <button
            @click="handleRecentDocument"
            :class="`${
              isStep === 1
                ? 'bg-indigo-500 text-white'
                : 'bg-gray-500 text-white'
            }`"
            class="px-3 py-[6px] rounded-l-lg flex items-center gap-2"
          >
            <span>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="size-5 text-white"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M19.5 14.25v-2.625a3.375 3.375 0 0 0-3.375-3.375h-1.5A1.125 1.125 0 0 1 13.5 7.125v-1.5a3.375 3.375 0 0 0-3.375-3.375H8.25M9 16.5v.75m3-3v3M15 12v5.25m-4.5-15H5.625c-.621 0-1.125.504-1.125 1.125v17.25c0 .621.504 1.125 1.125 1.125h12.75c.621 0 1.125-.504 1.125-1.125V11.25a9 9 0 0 0-9-9Z"
                ></path>
              </svg>
            </span>
            <span> Recent Documents </span>
          </button>
          <button
            @click="handleFolder"
            :class="`${
              isStep === 2
                ? 'bg-indigo-500 text-white'
                : 'bg-gray-500 text-white'
            }`"
            class="px-3 py-[6px] rounded-r-lg flex items-center gap-2"
          >
            <span>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="size-5 text-white"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M2.25 12.75V12A2.25 2.25 0 0 1 4.5 9.75h15A2.25 2.25 0 0 1 21.75 12v.75m-8.69-6.44-2.12-2.12a1.5 1.5 0 0 0-1.061-.44H4.5A2.25 2.25 0 0 0 2.25 6v12a2.25 2.25 0 0 0 2.25 2.25h15A2.25 2.25 0 0 0 21.75 18V9a2.25 2.25 0 0 0-2.25-2.25h-5.379a1.5 1.5 0 0 1-1.06-.44Z"
                ></path>
              </svg>
            </span>
            <span> Folders </span>
          </button>
        </div>

        <div class="flex items-center gap-4">
          <div>
            <select
              class="border border-[#b08f6c] font-light px-3 py-[8px] rounded-xl w-64 text-gray-500 transition ease-in-out duration-1000 focus:border-2 focus:border-[#b08f6c] focus:outline-none appearance-none pl-3 pr-10"
              v-model="sortOption"
            >
              <option value="lastModified">Sort by last modified</option>
              <option value="title">Sort by Title (A-Z)</option>
              <option value="titleDesc">Sort by Title (Z-A)</option>
            </select>
          </div>
          <div class="relative">
            <input
              type="text"
              v-model="searchQuery"
              @input="handleSearch"
              class="border border-[#b08f6c] font-light px-3 py-[8px] rounded-xl w-64 placeholder:text-gray-500 text-sm transition ease-in-out duration-1000 focus:border-2 focus:border-[#b08f6c] focus:outline-none pr-16"
              placeholder="Search"
            />
            <div
              class="absolute top-1/2 right-3 transform -translate-y-1/2 flex items-center space-x-1"
            >
              <svg
                @click="clearSearch"
                v-if="searchQuery"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-4 h-4 cursor-pointer"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M6 18L18 6M6 6l12 12"
                />
              </svg>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="w-5 h-5"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="#b08f6c"
                fill="none"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                <path d="M10 10m-7 0a7 7 0 1 0 14 0a7 7 0 1 0 -14 0" />
                <path d="M21 21l-6 -6" />
              </svg>
            </div>
          </div>
        </div>
      </div>

      <div class="mt-3">
        <div v-if="isStep === 1">
          <RecentDocument :documents="filteredAndSortedDocuments" />
        </div>

        <div v-if="isStep === 2">
          <FolderDocument :documents="filteredAndSortedDocuments" />
        </div>
      </div>
    </div>

    <AddDocument :isOpen="isAddDocument" @onClose="isAddDocument = false" />
    <AddFolder :isOpen="isAddFolder" @onClose="isAddFolder = false" />
  </div>
</template>


<script>
import { ref, computed } from "vue";
import RecentDocument from "./RecentDocument.vue";
import FolderDocument from "./FolderDocument.vue";
import AddFolder from "./AddFolder.vue";
import AddDocument from "./AddDocument.vue";

export default {
  components: {
    FolderDocument,
    RecentDocument,
    AddFolder,
    AddDocument,
  },
  name: "ContentComponent",
  setup() {
    const documents = ref([
      { title: "Document A", owner: "Owner 1", lastModified: "2024-08-20" },
      { title: "Document B", owner: "Owner 2", lastModified: "2024-08-19" },
      // Add more documents here
    ]);

    const searchQuery = ref("");
    const sortOption = ref("lastModified");
    const isStep = ref(1);
    const isAddDocument = ref(false);
    const isAddFolder = ref(false);

    const filteredAndSortedDocuments = computed(() => {
      // Filter documents based on searchQuery
      const filteredDocuments = documents.value.filter((document) =>
        document.title.toLowerCase().includes(searchQuery.value.toLowerCase())
      );

      // Sort documents based on sortOption
      return filteredDocuments.sort((a, b) => {
        switch (sortOption.value) {
          case "lastModified":
            return new Date(b.lastModified) - new Date(a.lastModified);
          case "title":
            return a.title.localeCompare(b.title);
          case "titleDesc":
            return b.title.localeCompare(a.title);
          default:
            return 0;
        }
      });
    });
    const clearSearch = () => {
      searchQuery.value = "";
    };

    const handleRecentDocument = () => {
      sortOption.value = "lastModified";
      searchQuery.value = "";
      setStep(1);
    };

    const handleFolder = () => {
      sortOption.value = "lastModified";
      searchQuery.value = "";
      setStep(2);
    };

    const setStep = (step) => {
      isStep.value = step;
    };

    const editDocument = (index) => {
      // Handle edit logic here
      console.log("Edit document at index:", index);
    };

    return {
      documents,
      searchQuery,
      sortOption,
      isStep,
      filteredAndSortedDocuments,
      setStep,
      editDocument,
      clearSearch,
      handleRecentDocument,
      handleFolder,
      isAddDocument,
      isAddFolder,
    };
  },
};
</script>


<style scoped>
/* Tooltip styles */
.tooltip {
  visibility: hidden;
  opacity: 0;
  transition: opacity 0.3s ease;
  white-space: nowrap;
}

.relative:hover .tooltip {
  visibility: visible;
  opacity: 1;
}
</style>