<template>
  <div>
    <div class="user-content content" v-if="userLoading"><Loader class="loader--position"/></div>
    <div class="user-content content" v-else-if="!userData">Failed to load user</div>
    <div class="user-content content" v-else>
      <div class="user-left">
        <img :alt="user.first_name" :src="user.avatar"/>
      </div>
      <div class="user-right">
        <h2 class="user__item user__name">Name: {{ user.first_name }}!</h2>
        <p class="user__item user__age">Age: {{ getCurrentAge(user.date_of_birth) }} years old</p>
        <p class="user__item user__post">Post: {{ user.employment.title }}</p>
      </div>
    </div>

    <div v-if="!userLoading">
      <div class="beer-content content loading-text"
        v-if="beerLoading"
      >We are looking for beer for you...</div>
      <div class="beer-content content" v-else-if="!beerData">
        Failed to load recommended beer for you
      </div>
      <div class="beer-content content" v-else>
        <p class="beer-text">
          Hello, dear <span class="prop prop--first_name">{{ user.first_name }}</span>!
        </p>
        <p class="beer-text">
          We are very glad to see you in our bar!
          Of cours, we have a lot of different types of beer from many famous brands.
          But we think, that if you choose <span class="prop prop--name">{{ beer.name }}</span>
          from <span class="prop prop--brand">{{ beer.brand }}</span> with
          <span class="prop prop--alcohol">{{ beer.alcohol }}</span> of alcohol,
          your time spending will be quite amazing.
          Have a nice day, see you soon, dear visitor!
        </p>
        <small class="beer-alcohol"></small>
      </div>
    </div>

  </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios';
import { API_USER_URL, API_BEER_URL } from '@/config.js';
import Loader from './Loader.vue'

export default {
  components: {
    Loader,
  },

  data() {
    return {
      userData: null,
      beerData: null,

      userLoading: true,
      userErrored: false,

      beerLoading: true,
      beerErrored: false,
    };
  },

  computed: {
    user() {
      return this.userData;
    },

    beer() {
      return this.beerData;
    },
  },

  methods: {
    loadUser() {
      this.userLoading = true;
      this.userErrored = false;
      clearTimeout(this.loadUserTimer);

      this.loadUserTimer = setTimeout(() => {
      return axios.get(API_USER_URL)
        .then((response) => this.userData = response.data)
        .catch(() => this.userErrored = true)
        .then(() => this.userLoading = false);
      }, 1500);
    },

    loadBeer() {
      this.beerLoading = true;
      this.beerErrored = false;
      clearTimeout(this.loadBeerTimer);

      this.loadBeerTimer = setTimeout(() => {
      return axios.get(API_BEER_URL)
        .then((response) => this.beerData = response.data)
        .catch(() => this.beerErrored = true)
        .then(() => this.beerLoading = false);
      }, 4500);
    },

    getCurrentAge(birthDate) {
      return (new Date().getFullYear() - new Date(birthDate).getFullYear());
    },
  },

  created() {
    this.loadUser();
    this.loadBeer();
  },

  // watch: {
  //   userData() {
  //     this.loadUser();
  //   },
  // },

};
</script>

<style>
  .content {
    color: #fff;
  }

  .user-content {
    margin-bottom: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .user-left { width: 30%; }
  .user-right { width: 60%; }

  .user__item {
    margin-bottom: 20px;
  }

  .beer-text {
    max-width: 50%;
    margin: 0 auto;
    font-size: 18px;
    line-height: 1.5;
    letter-spacing: 1.5px;
  }

  .loading-text {
    max-width: 50%;
    margin: 0 auto;
    margin: 0 auto;
    text-transform: uppercase;
  }

  .prop {
    text-transform: uppercase;
  }

  .prop--first_name { color: red; }
  .prop--name { color: orange; }
  .prop--brand { color: yellow; }
  .prop--alcohol { color: green; }

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
