<template>
    <div class="container">

        <div class="card mt-5">
            <h2 class="card-header bg-dark text-white">asteroids</h2>
            <div v-show="numAsteroids > 0">
                <p class="mt-2">Showing {{ numAsteroids }} items.</p>
                <p> Closest object is {{ closestObject.name }} with {{ closestObject.miles }} miles.</p>
            </div>

            <table class="table table-striped table-dark">
                <thead class="thead-light">
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
                    <tr v-for="(a, idx) in asteroids" :key="a.neo_reference_id" 
                        :class="{dangerous: isDangerous(a)}">
                        <td>{{ idx+1 }}</td>
                        <td>{{ a.name }}</td>
                        <td>{{ getAsteroidDate(a) }}</td>
                        <td :class="{missingData: isMissingData(a)}">
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
    computed: {
        numAsteroids: function () {
            if (this.asteroids == null) return 0;
            else return this.asteroids.length;
        },
        closestObject: function () {
            if (this.asteroids === null) return {};

            var filtered = this.asteroids.filter(a => a.close_approach_data.length > 0);
            filtered = filtered.map(a => { return {
                                            'name': a.name,
                                            'miles': a.close_approach_data[0].miss_distance.miles,
            }});
            filtered = filtered.sort( (a,b) => {
                return a.miles - b.miles;
            });
            return filtered[0];
        }
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
        },
        isDangerous: function (a) {
            return a.is_potentially_hazardous_asteroid;
        },
        isMissingData: function (a) {
            return ! a.close_approach_data.length > 0;
        }
    }
    
}
</script>


<style scoped>

.missingData {
    border: rgb(219, 168, 31) 3px groove;
    background: rgba(219, 168, 31, 0.5) !important;
}

.dangerous {
    border: red 3px solid;
    background: rgb(255, 76, 66) !important;
}

</style>
