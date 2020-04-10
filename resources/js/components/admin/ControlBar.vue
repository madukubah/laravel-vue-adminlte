<template>
  <aside class="control-sidebar control-sidebar-dark">
    <!-- Control sidebar content goes here -->
    <div class="p-3">
        <h5>{{ $auth.user().name }}</h5>
        <a class="d-block" href="#" @click.prevent="$auth.logout()">Logout</a>
    </div>
</aside>
</template>
<script>
  export default {
    created() {
    },
    mounted() {
      //
    }
  }
</script>
