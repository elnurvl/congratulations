<template>
  <div>
    <v-btn @click="logInWithFacebook">Get Started</v-btn>
  </div>
</template>
<script>
export default {
  name: 'FacebookLogin',
  data: () => ({
    disabled: true,
  }),
  methods: {
    logInWithFacebook() {
      const vm = this
      window.FB.getLoginStatus(
        function (response) {
          if (response.authResponse) {
            // Now you can redirect the user or do an AJAX request to
            // a PHP script that grabs the signed request from the cookie.
            vm.statusChangeCallback(response)
          } else {
            window.FB.login(function (response) {
              vm.statusChangeCallback(response)
            })
          }
        },
        {
          scope:
            'pages_show_list,pages_show_list,pages_manage_metadata,pages_messaging',
        }
      )
      return false
    },
    statusChangeCallback(response) {
      this.$emit(
        'loggedIn',
        response.authResponse.accessToken,
        response.authResponse.userID
      )
    },
  },
}
</script>
<style>
.button {
  color: white;
  min-width: 150px;
  background-color: #000000a1;
  height: 2.5rem;
  border-radius: 2rem;
  font-weight: 400;
  font-size: 0.8rem;
}
</style>
