<template>
  <div class="admin">
    <SideBar />
    <AddPizza />
  </div>
</template>

<script>
import SideBar from "@/components/Admin/SideBar.vue";
import AddPizza from "@/components/Admin/AddPizza.vue";
export default {
  components: { SideBar, AddPizza },
};
</script>

<style>
</style>