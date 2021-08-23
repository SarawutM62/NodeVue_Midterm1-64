<template>
  <div>
    <h1>Show CAT</h1>
    <p>id: {{ userId }}</p>
    <p>ชื่อน้องแมว{{ user.name }} - {{ user.lastname }}</p>
    <p>ข้อมูลแมว: {{ user.email }}</p>
    <p>สายพันธ์: {{ user.password }}</p>
  </div>
</template>
<script>
import UserService from "@/services/UsersService";
export default {
  data() {
    return {
      user: null,
    };
  },
  async created() {
    try {
      let userId = this.$route.params.userId;
      this.user = (await UserService.show(userId)).data;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
<style scoped>
</style>