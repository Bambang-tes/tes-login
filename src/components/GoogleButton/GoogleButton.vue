<template>
  <div>
    <div class="button" ref="button">
      <img
        class="icon"
        src="https://developers-dot-devsite-v2-prod.appspot.com/identity/sign-in/g-normal.png"
      >
      <span>Google</span>
    </div>
    
  </div>
</template>

<script>

export default {
  methods: {
    showModalLogin() {
       if (!window.gapiPromise) {
          window.gapiPromise = new Promise(resolve => {
            let script = document.createElement("script");
            script.addEventListener("load", () => {
              resolve(window.gapi);
            });
            script.src = "https://apis.google.com/js/api:client.js";
            document.head.appendChild(script);
          });
        }


        window.gapiPromise.then(gapi => {
          gapi.load("client:auth2", () => {
            let auth2 = gapi.auth2.init({
              client_id: '634872920355-ubl5dsf4r4l8anlpthpbui32g5n080ts.apps.googleusercontent.com',
              cookiepolicy: "single_host_origin",
              "cross_origin_opener_policy": {
                "value": "same-origin"
              },
            });
            auth2.then(() => {
              gapi.signin2.render('google-signin-button', {
                'scope': 'profile email',
                'width': 200,
                'height': 40,
                'longtitle': true,
                'theme': 'dark',
                'onsuccess': this.onSignIn,
                'onfailure': this.onSignInFailure
              })
            }).catch(err=> {
              console.log("error", err);
            })
            auth2.attachClickHandler(this.$refs.button, {});
          });
        });
      
    },

    onSignIn(googleUser) {
      console.log(googleUser);
    },

    onSignInFailure(err){
      console.log("hanya dia", err);
    }
    
  },
  mounted() {
    this.showModalLogin()

    
  }
};
</script>

<style>
.button {
  display: inline-flex;
  align-items: center;
  padding: 4px 16px;
  border: 1px solid gray;
  color: #212121;
  border-radius: 4px;
  font-family: "Roboto";
  cursor: pointer;
}

.button .icon {
  margin-right: 8px;
  height: 28px;
}
</style>