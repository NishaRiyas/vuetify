<template>
<p>View Job Post</p>

<div class="container">
    <v-row align="center">
        <v-col class="d-flex" cols="12" sm="6">
            <h3>{{ viewjob.title }}</h3>
        </v-col>
        <v-col class="d-flex" cols="12" sm="6">
            <p>Posted on,{{ getDayOfWeek(viewjob.date) }} {{ viewjob.date}}</p>
        </v-col>
    </v-row>
    <p>{{ viewjob.des }}</p>

    <v-row align="center">
        <v-col class="d-flex" cols="12" sm="6">
            <div class="card-body" style="text-align: left;">
                <p class="card-title">Booking Days</p>

                <v-btn outlined rounded text>
                    {{ getDayOfWeek(viewjob.date) }}
                </v-btn>
            </div>
        </v-col>
        <v-col class="d-flex" cols="12" sm="6">
            <div class="col-md-8">
                <div class="card-body" style="text-align: left;">
                    <p class="card-title">{{ viewjob.userName }}</p>
                    <p class="card-text">{{ viewjob.date }}</p>
                </div>
            </div>

        </v-col>
    </v-row>

    <v-row>
        <div class="box">
            <v-col class="d-flex" cols="6" sm="3">

                <div class="card-body" style="text-align: left;">
                    <p class="card-title">StartTime</p>
                    <p class="card-text">{{ viewjob.start }}</p>
                </div>

            </v-col>
            <v-col class="d-flex" cols="6" sm="3">

                <div class="card-body" style="text-align: left;">
                    <p class="card-title">EndTime</p>
                    <p class="card-text">{{ viewjob.end }}</p>
                </div>

            </v-col>
        </div>
    </v-row>

</div>
<div class="button">
    <v-btn color="blue" prepend-icon="mdi-plus" @click="saveData">Post Job</v-btn>
</div>
</template>

<script>
import {
    useRoute
} from 'vue-router';

export default {
    name: 'ViewJob',
    data() {
        return {
            viewjob: {
                userName: '',
                date: '',
                title: '',
                des: ''

            }
        }
    },
    mounted() {
        const route = useRoute();
        this.viewjob = this.$store.getters.getUserDesc[route.params.userName];
    },
    methods: {
        saveData() {
            console.log("saved")
        },
        getDayOfWeek(date) {
            const daysOfWeek = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
            const dayIndex = new Date(date).getDay();
            return daysOfWeek[dayIndex];
        }
    }
}
</script>

<style>
.container {
    border: 1px solid;
    background-color: lightgrey;

    border: 1px solid rgb(80, 120, 195);
    padding: 25px;
    margin: 20px 170px;
}

.button {
    text-align: center;
}

.box {
    border: 1px solid;
    background-color: white;

    border: 1px solid rgb(144, 13, 124);
    padding: 50px;
    margin: 1px;
}
</style>
