<template>
  <div
    class="w-[280px] h-screen border-r border-[#dbdbdb] z-[35] bg-[#f9f9f9] py-[14px] px-[30px]"
  >
    <img src="../assets/v-logo.png" alt="" class="w-[200px] mx-auto" />
    <div class="pt-2">
      <h4 class="font-medium text-gray-400">MENU</h4>
      <div>
        <button class="flex items-center gap-2 text-lg">
          <span class="primary-skin">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              xmlns:xlink="http://www.w3.org/1999/xlink"
              aria-hidden="true"
              role="img"
              class="iconify iconify--feather sidebar-svg"
              width="1em"
              height="1em"
              preserveAspectRatio="xMidYMid meet"
              viewBox="0 0 24 24"
              data-icon="feather:video"
              data-v-05c89d09=""
            >
              <g
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <path d="M23 7l-7 5l7 5V7z"></path>
                <rect x="1" y="5" width="15" height="14" rx="2" ry="2"></rect>
              </g>
            </svg>
          </span>
          <span class="text-black">Video Curator</span>
        </button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "SidebarComponent",
  components: {},
};
</script>