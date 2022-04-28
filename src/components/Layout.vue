<template>
  <div>
    <Header />
    <main class="container main">
      <UserProfile />
    </main>
  </div>
</template>

<script>
import Header from './Header.vue';
import UserProfile from './UserProfile.vue';

export default {
  components: {
    Header,
    UserProfile,
  },
};
</script>

<style>
  .main {
    min-height: 100%;
    padding-top: 20px;
    padding-bottom: 20px;
  }
</style>
