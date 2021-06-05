<template>
  <div id="wrapper" class="d-flex flex-column min-vh-100 justify-content-center align-items-center">
    <div id="firebaseui-auth-container"></div>
  </div>
</template>
<script lang ="ts">
import { auth } from '../config/firebase'
import * as firebaseui from 'firebaseui'
import { onMounted } from 'vue'

export default {
  name: 'auth',
  setup () {
    onMounted(async () => {
      await auth().signOut()
      const uiConfig = {
        signInSuccessUrl: '/',
        signInOptions: [
          auth.EmailAuthProvider.PROVIDER_ID,
          auth.GoogleAuthProvider.PROVIDER_ID,
          auth.FacebookAuthProvider.PROVIDER_ID,
          auth.TwitterAuthProvider.PROVIDER_ID,
          auth.GithubAuthProvider.PROVIDER_ID
        ],
        tosUrl: 'https://example.com/',
        privacyPolicyUrl: () => {
          window.open('https://example.com/')
        }
      }
      const ui = new firebaseui.auth.AuthUI(auth())
      ui.start('#firebaseui-auth-container', uiConfig)
    })
  }
}
</script>
<style lang="postcss" scoped>
  @import '../../node_modules/firebaseui/dist/firebaseui.css'
</style>
