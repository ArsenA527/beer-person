<template>
  <div>
    <Header />
    <main class="container main">
      <UserProfile />
    </main>
    <Footer />
  </div>
</template>

<script>
import Header from './Header.vue';
import Footer from './Footer.vue';
import UserProfile from './UserProfile.vue';

export default {
  components: {
    Header,
    Footer,
    UserProfile,
  },
};
</script>

<style>
  .main {
    padding-top: 20px;
    padding-bottom: 20px;
  }
</style>
