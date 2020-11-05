<template>
  <div>
    <div>Please verify email address</div>

    <button @click="signOut">signout</button>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { auth } from '@/lib/firebase/client'
export default Vue.extend({
  methods: {
    signOut() {
      auth.signOut().then(() => {
        this.$router.push('signin')
      })
    },
  },
})
</script>
