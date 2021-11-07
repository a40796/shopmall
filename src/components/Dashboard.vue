<template>
  <div>
    <Nav></Nav>
  <div class="container-fluid">
  <div class="row">
    <Sidebar></Sidebar>
    <main class="col-md-9 ms-sm-auto col-lg-10 px-md-4">
      <router-view/>
    </main>
  </div>
</div>
  </div>
</template>

<script>
import Sidebar from './Sidebar';
import Nav from './Nav';

export default {
  components:{
    Sidebar,
    Nav
  },
  name: 'HelloWorld',
  data () {
    return {
     
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
