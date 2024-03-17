<template>
  <div class="admin">
    <SideBar />
    <AddScore />
  </div>
</template>

<script>
import SideBar from "@/components/Admin/SideBar.vue";
import AddScore from "@/components/Admin/AddScore.vue";
export default {
  components: { SideBar, AddScore },
};
</script>

<style>
</style>