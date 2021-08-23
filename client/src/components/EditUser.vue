<template>
<div>
    <h1>แก้ไขข้อมูลน้องแมว</h1>
    <form v-on:submit.prevent = "editUser">
        <p>ชื่อน้องแมว: <input type="text" v-model="user.name"></p>
        <p>ราคาน้องแมว: <input type="text" v-model="user.lastname"></p>
        <p>ข้อมูลแมว: <input type="text" v-model="user.email"></p>
        <p>สายพันธ์: <input type="text" v-model="user.password"></p>
        <p><button type="submit">edit user</button></p>
    </form>
    <hr>
    <div>
        <p>ชื่อน้องแมว: {{user.name}}</p>
        <p>ราคาน้องแมว: {{user.lastname}}</p>
        <p>ข้อมูลแมว: {{user.email}}</p>
        <p>สายพันธ์: {{user.password}}</p>
    </div>
</div>
</template>
<script>import UsersService from '@/services/UsersService'

export default {
    data(){
        return{
            user:{
                name: '',
                lastname: '',
                email: '',
                password: '',
                status: 'active'
            }
        }
    },
    methods:{
        async editUser(){
            try{
                await UsersService.put(this.user)
                this.$router.push({
                    name: 'users'
                })

            }catch(error){
                console.log(error)
            }
        }
    }, 
    async created(){
        try{
            let userId = this.$route.params.userId
            this.user = (await UsersService.show(userId)).data
        }catch(error){
            console.log(error)
        }
    }
}
</script>
<style scoped>


</style>