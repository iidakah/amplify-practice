<script>
import GoogleLogin from './components/GoogleLogin.vue'
import { getCurrentUser, signOut, fetchAuthSession } from 'aws-amplify/auth';
import { useAuthenticator, Authenticator } from '@aws-amplify/ui-vue';

export default {
  components: {
    Authenticator
  },
  data() {
    return {
      currentUser: {},
      session: {},
      isLogin: false,
      auth: null
    }
  },
  methods:{
    signOutFromApp() {
      signOut().then(
        () => {
          this.isLogin = false
          this.currentUser = {}
        },
        (error) => {
          console.log(error)
          this.isLogin = true
        }
      )
    }
  },
  created() {
    this.auth = useAuthenticator()
    getCurrentUser().then(
        (user) => {
          this.isLogin = true
          this.currentUser = user
          currentSession().then(
            (value) => {
              this.session = value
            }
          )
        },
        (error) => {
          console.log(error)
          this.isLogin = false
        }
      );
    
  }
  
}
async function currentSession() {
  try {
    return (await fetchAuthSession()).tokens ?? {};
  } catch (err) {
    console.log(err);
  }
}

</script>

<template>
  <header>
    <h1>Practice</h1>
  </header>
  <authenticator :social-providers="['google']">

  </authenticator>
  <div>
    <div v-if="auth.route === 'authenticated'">
      <button class="btn btn-primary" @click="signOutFromApp()">Sign Out</button>
    </div>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
