<template>
  <div style="display: flex;justify-content: center;align-items: center;height: 100vh;">
    <form @submit.prevent="login">
      <h1 class="h3 mb-3 fw-normal">Please log in</h1>
      <div class="form-floating">
        <input type="email" class="form-control" id="floatingInput" placeholder="name@example.com" v-model="loginObj.username">
        <label for="floatingInput">Email address</label>
      </div>
      <div class="form-floating">
        <input type="password" class="form-control" id="floatingPassword" placeholder="Password" v-model="loginObj.password">
        <label for="floatingPassword">Password</label>
      </div>

      <div class="checkbox mb-3">
        <label>
          <input type="checkbox" value="remember-me"> Remember me
        </label>
      </div>
      <button class="w-100 btn btn-lg btn-primary" type="submit">Log in</button>
      <p class="mt-5 mb-3 text-muted">&copy;copy right</p>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      loginObj:{
        'username':'',
        'password':''
      }  
    }
  },
  methods:{
    login(){
      var vm = this;
      const api = `${process.env.APIPATH}/admin/signin`
      this.$http.post(api,vm.loginObj).then((response) => {
      console.log(response.data.success)
        if(response.data.success === true){
           const token = response.data.token;
           const expired = response.data.expired;
           document.cookie = `hexToken=${token};expires=${new Date(expired)};`;
           const replace_token = document.cookie.replace(/(?:(?:^|.*;\s*)hexToken\s*=\s*([^;]*).*$)|^.*$/, '$1');
           this.$http.defaults.headers.common.Authorization = `${replace_token}`;
           this.$router.push('/');
        }
  })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
html,
body {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  padding-top: 40px;
  padding-bottom: 40px;
  background-color: #f5f5f5;
}

form{
  width: 23%;
  padding: 10px;
  border: 1px solid #80808052;
  border-radius: 2px;
}

.form-signin {
  width: 100%;
  max-width: 330px;
  padding: 15px;
  margin: auto;
}

.form-signin .checkbox {
  font-weight: 400;
}

.form-signin .form-floating:focus-within {
  z-index: 2;
}

.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}

.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
</style>
