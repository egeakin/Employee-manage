<template>
    <body>
    <div id="dashboard">
        <ul class="collection with-header">
            <li
            class="collection-header"><h4>Movies and TV Series</h4>
            </li>
            <li v-for="employee in employees"
            v-bind:key="employee.id"
            class= "collection-item">
            <div class="chip">{{employee.dept}}</div>
            {{employee.employee_id}} : {{employee.name}}

            <router-link class="secondary-content"
            v-bind:to="{name: 'view-employee', params: {employee_id: employee.employee_id}}">
                <i class="fa fa-eye"></i>
            </router-link>
            </li>
        </ul>
        
        <div class="fixed-action-btn">
            <router-link to="/new" class="btn-floating btn-large red">
                <i class="fa fa-plus"></i>
            </router-link>    
        </div>    
    </div>
    </body>    
</template>

<script>
import db from './firebaseInit'
export default {
    name: 'dashboard',
    data() {
        return {
            employees: []
        }
    },
    created() {
        db.collection('employees').orderBy('dept').get().then(querySnapshot => {
            querySnapshot.forEach(doc => {
                const data = {
                    'id': doc.id,
                    'employee_id': doc.data().employee_id,
                    'name': doc.data().name,
                    'dept': doc.data().dept,
                    'posiiton': doc.data().position
                }
                this.employees.push(data)
            })
        })
    }
}
</script>

<style>
    #dashboard{
        background-color:yellow;
    }
    body {
        background-color: rgb(95,113,123);
        background-image: url("http://www.sclance.com/backgrounds/best-website-background-color/best-website-background-color_326505.jpg");

    }
</style>
