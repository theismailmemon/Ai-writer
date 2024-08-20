<template>
  <div class="flex">
    <div>
      <Sidebar />
    </div>
    <div>
      <Header />
      <DocumentContent />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Sidebar from "./components/Sidebar.vue";
import DocumentContent from "./components/Content.vue";
export default {
  name: "App",
  components: {
    Header,
    Sidebar,
    DocumentContent,
  },
};
</script>
<style>
body {
  font-family: 'Jost', sans-serif;
}
</style>