<template>
  <div id="app">
    <button class="logout" @click.prevent="logOut">Log out</button>
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",
  methods:{
    logOut(){
      const api = `${process.env.APIPATH}/logout`;
      this.$http.post(api).then((res)=>{
        console.log(res.data);
      })
    }
  }

};
</script>
<style lang="scss">
   @import "./assets/all"
</style>
