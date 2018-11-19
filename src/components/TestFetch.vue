<template>
    <div>
        <button class="btn btn-primary" @click.prevent="fetchUsers">Fetch Users</button>
        <ul>
            <li v-for="user in users" :key="user.id">{{user}}</li>
        </ul>
    </div>
</template>

<script>
    import axios from 'axios'

    export default {
        props: [
        ],
        data: function () {
            return {
                users: []
            }
        },
        methods: {
            fetchUsers: function () {
                const baseUrl = 'https://jsonplaceholder.typicode.com/users';
                axios.get(baseUrl)
                    .then((result) => {
                    this.users = result.data;
                });
            }
        }
    }
</script>


