<template>
  <div class="flex">
    <div>
      <Sidebar />
    </div>
    <div>
      <Header />
      <Content />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Sidebar from "./components/Sidebar.vue";
import Content from "./components/Content.vue";
export default {
  name: "App",
  components: {
    Header,
    Sidebar,
    Content,
  },
};
</script>
<style>
body {
  font-family: 'Jost', sans-serif;
}
</style>