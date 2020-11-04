<template>
  <span id="oauth-container"></span>
</template>

<script lang="ts">
import Vue from 'vue'
import { auth } from '@/lib/firebase/client'
import firebase from 'firebase'
import * as firebaseui from 'firebaseui'
import 'firebaseui/dist/firebaseui.css'

export default Vue.extend({
  name: 'OAuthSignInButton',
  mounted() {
    const ui =
      firebaseui.auth.AuthUI.getInstance() || new firebaseui.auth.AuthUI(auth)
    const uiConfig = {
      signInSuccessUrl: '/profile',
      signInOptions: [firebase.auth.GoogleAuthProvider.PROVIDER_ID],
    }
    ui.start('#oauth-container', uiConfig)
  },
})
</script>
