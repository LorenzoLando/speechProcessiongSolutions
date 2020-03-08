<template>
  <body>
    <div class="content">
      <app-header></app-header>
      <app-body></app-body>
    </div>
       <app-footer></app-footer>
    </body>
</template>

<script>
import Header from './components/header.vue'
import Body from './components/body.vue'
import Footer from './components/footer.vue'
export default {
  
  components: {
    'app-header': Header,
    'app-body': Body,
    'app-footer': Footer
  },
  data () {
    return {
      counter: true
    }
  },
  methods:{
    
  }
}
</script>

<style lang="scss">
html {
  scroll-behavior: smooth;
  height: 100%;
}
body {
  display: flex;
  flex-direction: column;
  height: 100vh; 
}
.content {
  flex: 1 0 auto; 
  padding: 20px;
}
.footer {
  flex-shrink: 0; 
  padding: 20px;
}


</style>
