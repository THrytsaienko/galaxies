<template>
    <div class="sidebar">
        <div class="sidebar__container"></div>
    </div>
</template>

<script>
  export default {
    name: "Sidebar"
  }
</script>

<style scoped lang="scss">
    .sidebar {
        &__container {
             background-color: #F9FAFB;
             width: 270px;
             height: 100%;
             position: static;
             top: 0;
             left: 0;
        }
    }
</style>
