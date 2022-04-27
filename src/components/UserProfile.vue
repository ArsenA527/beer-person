<template>
  <div>
    <div class="user-content" v-if="loading">Идет загрузка...</div>
    <div class="user-content" v-else-if="!userData">Не удалось загрузить пользователя</div>
    <div class="user-content" v-else>
      <div class="user-left">
        <img :alt="user.first_name" :src="user.avatar" class="user-image"/>
      </div>
      <div class="user-right">
        <h2 class="user__item user__name">Name: {{ user.first_name }}</h2>
        <p class="user__item user__age">Age: {{ getCurrentAge(user.date_of_birth) }}</p>
        <p class="user__item user__post">Post: {{ user.employment.title }}</p>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios';
import { API_USER_URL } from '@/config.js';

export default {
  components: {},

  data() {
    return {
      userData: null,
      loading: true,
      errored: false,
    };
  },

  computed: {
    user() {
      return this.userData;
    },
  },

  methods: {
    loadUser() {
      this.loading = true;
      this.errored = false;
      clearTimeout(this.loadUserTimer);

      this.loadUserTimer = setTimeout(() => {
      return axios.get(API_USER_URL)
        .then((response) => this.userData = response.data)
        .catch(() => this.errored = true)
        .then(() => this.loading = false);
      }, 1500);

  },

    getCurrentAge(birthDate) {
      return (new Date().getFullYear() - new Date(birthDate).getFullYear());
    },
  },

  created() {
    this.loadUser();
  },

  // watch: {
  //   userData() {
  //     this.loadUser();
  //   },
  // },

};
</script>

<style>
  .user-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: #fff;
  }

  .user-left { width: 30%; }
  .user-right { width: 60%; }

  .user__item {
    margin-bottom: 20px;
  }

  @media (max-width: 768px) {
    .user-content {
      flex-direction: column;
    }

    .user-left {
      width: 200px;
      margin-bottom: 20px;
    }

    .user-right {
      width: 100%;
      text-align: center;
    }
  }

</style>
