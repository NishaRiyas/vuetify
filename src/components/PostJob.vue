<template>
<v-container fluid>
    <p>Post Job</p><br>
    <RouterView></RouterView>
    <v-row align="center">
        <v-col class="d-flex" cols="12" sm="6">
            
            <v-select :items="userList1" v-model="userName" label="Select a Service user" variant="outlined" prepend-icon="mdi-account-multiple">
        

            </v-select>

        </v-col>
        <v-col cols="12" sm="6">
            <v-menu>
                <template v-slot:activator="{ on }">
                    <v-text-field v-model="date" variant="outlined" label="Select a date" input type="date" prepend-icon="mdi-calendar" v-on="on"></v-text-field>
                </template>
                <v-date-picker v-model="date" multiple></v-date-picker>
            </v-menu>
        </v-col>

    </v-row>
    <v-row>
        <v-col class="d-flex" cols="12" sm="12">
            <v-text-field label="Job Post Title" variant="outlined" v-model="title"></v-text-field>

        </v-col>
    </v-row>
    <v-row>
        <v-col class="d-flex" cols="12" sm="12">
            <v-textarea label="Job Post Description" variant="outlined" v-model="des" rows="4"></v-textarea>
        </v-col>
    </v-row>
    <v-row>
        <v-col class="d-flex" cols="12" lg="6">
            <h3>Shifts</h3>
        </v-col>
        <v-col class="d-flex" cols="12" lg="6">
            <v-btn @click="addShift" color="blue"  prepend-icon="mdi-plus">   Add Shift</v-btn>
        </v-col>
    </v-row>
    <v-row>

        <v-alert v-model="alert" border="start" variant="tonal" closable close-label="Close Alert" color="deep-white-accent-4" background-color="white">
            click 'Add Shift' button to add new shift
        </v-alert>
    </v-row>

    <v-container> 
        <v-layout row wrap>
            <v-flex xs12 v-for="(shift, index) in shifts" :key="index">
                <v-card>
                    <v-card-title>
                        <span>Shift {{ index + 1 }}</span>
                        <v-spacer></v-spacer>
                        <v-btn icon @click="removeShift(index)">
                            <v-icon>mdi-close</v-icon>
                        </v-btn>
                    </v-card-title>
                    <v-card-text>
                        <v-row>
                            <v-col cols="12" md="6">
                                <v-text-field v-model="shifts.start" label="Start Time" type="time"></v-text-field>
                            </v-col>
                            <v-col cols="12" md="6">
                                <v-text-field v-model="shifts.end" label="End Time" type="time"></v-text-field>
                            </v-col>
                        </v-row>
                    </v-card-text>
                </v-card>
            </v-flex>
        </v-layout>

    </v-container>
    
        <v-row align="center" justify="space-around">
            <v-col class="d-flex" cols="12" sm="6">
                <v-btn @click="clearAll"   prepend-icon="mdi-close">CLEAR ALL</v-btn>
            </v-col>
          
        
            <v-col class="d-flex" cols="12" sm="6">
               <v-btn color="blue" @click="updateData"  prepend-icon="mdi-file-find" >
                    PREVIEW JOB POST
                </v-btn>
            </v-col>
        </v-row>

    

</v-container>
</template>

    
<script>
export default {
    name:'PostJob',

    data() {
        return {
            userName:'',
            date: [],
            title: '',
            des: '',
            alert: true,
            shifts: [{
                start: "",
                end: ""
            }]
        }
    },
    computed:{
        userList1(){
            console.log("asdfg");
            return this.$store.getters.getUserList;
        },
        userData(){
            return "asar";
        }
    },
    mounted(){
        console.log("mounted");
    },
    methods: {
        clearAll() {
            this.userName = '',
                this.date = '',
                this.title = '',
                this.des = '',
                this.shifts = ''

        },
        addShift() {
            this.shifts.push({
                start: "",
                end: ""
            });
        },
        removeShift(index) {
            this.shifts.splice(index, 1);
        }, 
        updateData(){
            let userData = {};
            userData['userName'] = this.userName;
            userData['date'] = this.date;
            userData['title'] = this.title;
            userData['des'] = this.des;
            userData['start'] = this.shifts.start;
            userData['end'] = this.shifts.end;

            console.log("sdfghjk");
            this.$store.commit('updateUserDesc',JSON.parse(JSON.stringify(userData)));
            this.$router.push({ name: 'viewjob', params: { userName: this.userName} })
        }
    }
}
</script>
