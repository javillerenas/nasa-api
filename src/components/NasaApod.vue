<template>
    <div>
        <!-- <button class="btn btn-primary" @click.prevent="fetchApod">Fetch Users</button> -->
        <div class="container">
            <h1 m-5>{{data.title}}</h1>
            <img style="max-height: 500px;" :src="data.url" :title="data.title">
        </div>
    </div>
</template>

// Script!
<script>
    import axios from 'axios'

    export default {
        props: [
        ],
        data: function () {
            return {
                data: [],
                hasData: false,
            }
        },
        created: function () {
            this.fetchApod();
        },
        methods: {
            fetchApod: function () {
                const apiKey = "t96xofCQtYjqxfxNMIuKakw2bfc6KSEZjWMJUC4l";
                const url = "https://api.nasa.gov/planetary/apod?api_key=";
                axios.get(url + apiKey)
                    .then((result) => {
                        // console.log(result.data);
                        this.data = result.data;
                        this.hasData = true;
                });
            }
        }
    }
</script>



