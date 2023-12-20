<template>
    <div>
    <h3>User Info</h3>
    </div>

    <ul>
        <li>{{ username }}</li>
        <li>{{ userId }}</li>
        <li>{{ signInDetails }}</li>
    </ul>

</template>

<script>
import { getCurrentUser } from 'aws-amplify/auth';

export default {
    data() {
        username: null
        userId: null
        signInDetails: null
    },
    methods: {
        async  currentAuthenticatedUser() {
            try {
                { username, userId, signInDetails } = await getCurrentUser();
                console.log(`The username: ${username}`);
                console.log(`The userId: ${userId}`);
                console.log(`The signInDetails: ${signInDetails}`);
            } catch (err) {
                console.log(err);
            }
        }
    }
}
</script>