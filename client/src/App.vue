<template>
  <div id="app" class="container">
    =={{msg}}==
    <MainNav class="navbar" />
    <router-view></router-view>
  
  </div>
</template>
<script>
import MainNav from '@/components/MainNav';

export default {
  name: 'app',
  data() {
    return {
      msg:'App.vue',
    }
  },
    created() {
    },
    methods: {
    },
  components: {
    MainNav,
  }
}
</script>


<style lang="scss">

// .container{
//   background-color: blue;
// }

@import url('https://fonts.googleapis.com/css?family=Kurale');
#app {
  // display: flex;
  // flex-direction: column;  
  font-family: 'Kurale', Helvetica, Arial, sans-serif;
  text-align: center;
  color: #652456;
  background: rgba(230, 230, 230, 0.7);
  max-width: 768px;
  height: 100%;
  ;
  margin: auto;
}

.navbar {
  border-bottom: 1px solid lightgrey;
  width: 100%;
}



body {
 // background: #C02425; 
  background: #C02425; 
  background: linear-gradient(to bottom, #eb5757, #e1b496); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  margin: 0;
  height:100%;
  overflow-y: hidden;
  a {
    text-decoration: none!important;
  }
}

</style>
