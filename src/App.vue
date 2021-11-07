<template>
  <div id="app">
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
        this.$router.push('/login');
      })
    }
  }

};
</script>
<style lang="scss">
   @import "./assets/all"
</style>
