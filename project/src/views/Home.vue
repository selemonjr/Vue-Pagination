<template>
<div>
  <div class="container">
    <div v-for="(user,index) in fetchUserList" :key="index">
      <div class="wrapper">
        <img :src="user.picture.thumbnail" alt="">
        <div class="userInfo">
          <p>{{user.name.title}} {{user.name.first}} {{user.name.last}}</p>
        </div>
      </div>
    </div>
  </div>
      <div class="button">
      <button type="button" class="btn" :disabled="currentPage === 1" @click="changePage(-1)">Prev</button>
       <button type="button" class="btn" :disabled="currentPage === 4" @click="changePage(1)">Next</button>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name:"Home",
  data() {
    return {
      list:[],
      currentPage:1,
      perPage:5,
    }
  },
  computed: {
    fetchUserList() {
      const start = (this.currentPage - 1) * this.perPage;
      const end = this.currentPage * this.perPage;
      const result = this.list.slice(start,end);
      return result;
    }
  },
  async created() {
    await this.fetchUsers();
  },
  methods: {
    async fetchUsers() {
      const data = await axios.get("https://randomuser.me/api/?results=20");
      this.list = data.data.results
    },
    changePage(num) {
      this.currentPage = this.currentPage + num;
    }
  },
}
</script>
<style scoped>
.container {
  padding-top:80px;
  display:flex;
  justify-content:space-evenly;
  align-items: center;
  flex-wrap: wrap;
}
img {
  border-radius:10px;
}
.wrapper {
  height:100px;
  width:300px;
  background:#eee;
    display:flex;
  justify-content:space-evenly;
  align-items: center;
  border-radius:10px;
  margin:10px;
}
.button {
  text-align:center;
}
.btn {
  padding:10px 40px;
  margin:20px;
  border-radius: 10px;
  border: none;
  outline:none;
}
.btn:active {
  background:#ff0000;
    padding:10px 40px;
  margin:20px;
  border-radius: 10px;
  border: none;
  color:#fff;
  outline:none;
}
.btn:disabled {
    background:#fff;
    padding:10px 40px;
  margin:20px;
  border-radius: 10px;
  border: none;
  outline:none;
}
</style>
