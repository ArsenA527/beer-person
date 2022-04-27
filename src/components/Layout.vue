<template>
  <div>
    <Header />
    <main class="container main">
      <UserProfile />
      <!-- <RecommendedBeer /> -->
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
    min-height: 100%;
    padding-top: 20px;
    padding-bottom: 20px;
  }
</style>
