<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <span v-google-signin-button="clientId" class="google-signin-button button btn">  
    
                                 <GoogleButton />
    
    <img
        class="icon"
        src="https://developers-dot-devsite-v2-prod.appspot.com/identity/sign-in/g-normal.png"
    > Google2</span>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import GoogleSignInButton from 'vue-google-signin-button-directive'
import GoogleButton from '@/components/GoogleButton/GoogleButton.vue';

export default {
  components: {
    GoogleButton,
  },
  name: 'App',
  directives: {
    GoogleSignInButton,
    HelloWorld

  },
  data() {
    return {
      clientId: '634872920355-ubl5dsf4r4l8anlpthpbui32g5n080ts.apps.googleusercontent.com',

    }
  },
  methods: {
    OnGoogleAuthSuccess (idToken) {
      // Receive the idToken and make your magic with the backend
      console.log('success boy',idToken);
    },
    OnGoogleAuthFail (error) {
        alert(error)
      console.log("gagall",error)
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
