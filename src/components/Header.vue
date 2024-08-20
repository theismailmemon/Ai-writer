<template>
  <div
    class="h-[83px] w-[calc(100vw-280px)] flex items-center justify-between px-10 py-3 border-r z-[35] bg-[#f9f9f9]"
  >
    <div class="flex items-center gap-2">
      <div>
        <img
          src="../assets/user-placeholder.png"
          alt="logo"
          class="w-[58px] h-[58px] rounded-full p-[2px] border border-gray-400"
        />
      </div>
      <div>
        <span class="text-black font-bold">Welcome back, </span>
        <span class="font-medium text-gray-600">Ibrahim Shahid</span>
        <h4 class="font-medium text-gray-600 text-[14px]">
          Last Logged in 20 Aug 01:36 AM
        </h4>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "HeaderComponent",
  components: {},
};
</script>