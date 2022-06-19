 <script>
 import axios from 'axios'
import Avatar from '../components/Avatar.vue';

export default {
  name: 'HomeView',
  components: { Avatar },

  data() {
    return {
      users:[],
      avatar: '',
      loading: true,
      loadingImage:new URL('../assets/rolling.gif', import.meta.url).href,
    }
  },

  methods: {
    async fetchUserData() {
      const res = await axios.get('https://jsonplaceholder.typicode.com/users');
      const data =  res.data
      return data
    },
    async fetchAvatar(username) {
      this.avatar = username;
    },
  },
  async created() {

    const data = await this.fetchUserData()
    this.users = data
    this.loading = false
  },
 
 }
 </script>

<template>
<main v-if="!loading">
 <h1 class="heading">
   User Data
  </h1>

<div  class="grid grid-cols-3 gap-5 pt-10 px-5">

<a class="card" v-for="user in users" :key="user">
    <Avatar :avatar="user.username"/>
    <div class="flex flex-col justify-between p-6 leading-normal">
        <h5 class="userName">{{user.username}}</h5>
        <p class="name">Name: {{user.name}}</p>
        <p class="company">Company: {{user.company.name}}</p>
        <p class="details"><i class="fa-solid fa-location-dot"></i> {{user.address.street}}, {{user.address.suite}},<br> {{user.address.city}}, {{user.address.zipcode}}</p>
        <p class="details"><i class="fa-solid fa-envelope"></i> {{user.email}}</p>
        <p class="details"> <i class="fa-solid fa-phone"></i> {{user.phone}}</p>
        <p class="details"><i class="fa-solid fa-globe"></i> {{user.website}}</p>
    </div>
</a>
</div>
</main>
<main v-else class="flex flex-col align-center justify-center text-center">
       <div class="text-gray-500 text-3xl mt-10 bm-6">
            Fetching Data
      </div>
<img :src="loadingImage" class="w-24 m-auto pt-10" alt="">
</main>
</template>


