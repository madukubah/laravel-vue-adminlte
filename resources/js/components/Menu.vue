<template>
  <div>
    <div class="top-right">
        <div class="links" v-if="!$auth.check()">
            <router-link :to="'register'"  >Register</router-link>
            <router-link :to="'login'"  >Login</router-link>
        </div>
        <div class="links" v-if="$auth.check()">
            <router-link :to="{ name : 'admin.index' }"  >Dashboard</router-link>
        </div>
    </div>
  </div>
</template>
<script>
  export default {
    created() {
      console.log( this.$auth.token() );
    },
    mounted() {
      //
    }
  }
</script>

<style>
.navbar {
  margin-bottom: 30px;
}
</style>
