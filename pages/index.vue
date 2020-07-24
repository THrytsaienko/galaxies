<template>
  <section class="container">
    <Sidebar />
    <div class="inner-wrapper">
      <MainContent />
    </div>
  </section>
</template>

<script>
import Sidebar from '~/components/Sidebar.vue';
import MainContent from '~/components/Content.vue';

export default {
  components: {
    Sidebar,
    MainContent
  }
}
</script>

<style>
  .container {
    min-height: 100vh;
    display: flex;
  }
  .inner-wrapper {
    width: 100%;
    padding: 70px 60px;
  }
</style>

