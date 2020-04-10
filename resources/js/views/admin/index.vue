<template>
    <div class="wrapper" >
       <Nav></Nav> 
       <SideBar></SideBar> 
        <div class="content-wrapper">
          <router-view></router-view>
        </div>
       <ControlBar></ControlBar>
       <Footer></Footer>
    </div>
</template>

<script>
    import Nav from '../../components/admin/Nav.vue'
    import SideBar from '../../components/admin/SideBar.vue'
    import ControlBar from '../../components/admin/ControlBar.vue'
    import Footer from '../../components/admin/Footer.vue'
    export default {

    data() {
      return {
        //
      }
    },
    created() {
      console.log();
    },
    components: {
      Nav,
      SideBar,
      ControlBar,
      Footer
    }
  }

</script>
<style>
.navbar {
  margin-bottom: 0!important;
}
</style>
