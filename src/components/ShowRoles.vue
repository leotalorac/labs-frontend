<template>
    <div class="container-fluid">
        <div class="list-group">
            <a href="#" class="list-group-item list-group-item-action" v-for="r in roles">
                <div class="d-flex w-100 justify-content-between">
                    <h5 class="mb-1">{{r.roleName}}</h5>
                    <small>{{r.id}}</small>
                </div>
            </a>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';

    export default {
        name: "ShowRoles",
        data(){
            return{
                roles:[]
            };
        },
        beforeCreate() {
            //the path to get the user roles
            const pathToGetRoles = "/user/roles"
            //make the get request
            axios
                //use the path
                .get(this.$store.state.backURL + pathToGetRoles,{
                    //send the token
                    params:{
                        access_token: localStorage.getItem("token")
                    }
                })
                //get the response
                .then(res =>{
                    //correct response
                    if(res.status == 200){
                        this.roles = res.data;
                    }
                    //error response
                    else{
                        alert("Se ha presentado un error")
                    }
                })
        }
    }
</script>

<style scoped>

</style>