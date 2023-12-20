<template>
    <button v-on:click="handleGoogleLogin">
        <img src="../assets/google-image.png" alt="Google Sign In">
    </button> 
</template>

<script>
import GoogleLoginFunc from './GoogleLoginFunc';

export default {
    name: 'GogleLogin',
    methods: {
        handleGoogleLogin() {
            GoogleLoginFunc.handleSignInClick()
        }
    }
}
</script>