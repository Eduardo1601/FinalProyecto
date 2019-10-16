<template>
  <div class="centered-container">
    <md-content class="md-elevation-3">
<img src="https://uploads-ssl.webflow.com/56a1006de9a99a4669bfd05c/5bc49b720bc683b8ffabc6d7_Logo-ESC-SolutionS.png">
      <div class="title">
        
      </div>

      <div class="form">
        <md-field>
          <label>Usuario</label>
          <md-input v-model="usuario" autofocus></md-input>
        </md-field>

        <md-field md-has-password>
          <label>Password</label>   
          <md-input v-model="password" type="password"></md-input>
        </md-field>
      </div>

      <div class="actions md-layout md-alignment-center">
        <md-button class="md-raised md-primary" @click="auth">Log in</md-button>
      </div>

      <div class="loading-overlay" v-if="loading">
        <md-progress-spinner md-mode="indeterminate" :md-stroke="2"></md-progress-spinner>
      </div>

    </md-content>
    <div class="background" />
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: "App",
  data() {
    return {
      loading: false,
        usuario: "",
        password: "",
        response:""
    };
  },
  methods: {
    auth() {
      // your code to login user  
      // eslint-disable-next-line
      console.log("Entrar");
      axios.post('http://localhost:3000/login',{
          usuario:this.usuario,
          password:this.password
      })
      .then(response => {
        // eslint-disable-next-line 
        console.log(response.data)
        this.$router.push(this.$route.query.redirect || '/empleados')
      }).catch(e => {
      this.errors.push(e)
    })
      // this is only for example of loading
      this.loading = true;
      setTimeout(() => {
        this.loading = false;
      }, 5000);
    }
  }
};
</script>

<style lang="scss">
.centered-container {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  height: 100vh;
  .title {
    text-align: center;
    margin-bottom: 30px;
    img {
      margin-bottom: 16px;
      max-width: 80px;
    }
  }
  .actions {
    .md-button {
      margin: 0;
    }
  }
  .form {
    margin-bottom: 60px;
  }
  .background {
    background: url(https://wallpaperaccess.com/full/1101309.jpg);
    position: absolute;
    height: 100%;
    width: 100%;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    z-index: 0;
  }
  .md-content {
    z-index: 1;
    padding: 40px;
    width: 100%;
    max-width: 400px;
    position: relative;
  }
  .img{
    width:50%;
    height:50%;
  }
  .loading-overlay {
    z-index: 10;
    top: 0;
    left: 0;
    right: 0;
    position: absolute;
    width: 100%;
    height: 100%;
    background: rgba(255, 255, 255, 0.9);
    display: flex;
    align-items: center;
    justify-content: center;
  }
}
</style>
  