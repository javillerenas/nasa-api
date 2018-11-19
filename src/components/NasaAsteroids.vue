<template>
    <div class="container">

        <div class="card mt-5">
            <h2 class="card-header bg-dark text-white">asteroids</h2>
            <table class="table table-dark">
                <thead>
                    <tr>
                        <th>#</th>
                        <th>name</th>
                        <th>Approach Date</th>
                        <th>Miss Distance</th>
                        <th>Hazardous?</th>
                        <th>Remove</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(a, idx) in asteroids" :key="a.neo_reference_id">
                        <td>{{ idx+1 }}</td>
                        <td>{{ a.name }}</td>
                        <td>{{ getAsteroidDate(a) }}</td>
                        <td>
                            <ul v-if="a.close_approach_data.length > 0">
                                <li v-for="(value, key) in a.close_approach_data[0].miss_distance" :key="key">
                                    {{key}}: {{value}}
                                </li>
                            </ul>
                        <td>{{ a.is_potentially_hazardous_asteroid }}</td>
                        <td><button @click="removeAsteroid(idx)" class="btn btn-danger">Delete</button></td>
                    </tr>
                </tbody>
            </table>
        </div>

    </div>
</template>

// Script
<script>
import axios from 'axios'

export default {
    data: function () {
        return {
            asteroids: null
        }
    },
    created: function () {
        this.getAsteroids();
    },
    methods: {
        getAsteroids: function () {
            const apiKey = "t96xofCQtYjqxfxNMIuKakw2bfc6KSEZjWMJUC4l";
            const url = "https://api.nasa.gov/neo/rest/v1/neo/browse?api_key="
            axios.get(url + apiKey)
                .then((res) => {
                    this.asteroids = res.data.near_earth_objects;
                });
        },
        getAsteroidDate: function (a) {
            if (a.close_approach_data.length > 0)
                return a.close_approach_data[0].close_approach_date;
            else
                return 'N/A';
        },
        removeAsteroid: function (idx) {
            this.asteroids.splice(idx, 1);
        }
    }
    
}
</script>

