<template>
    <div>
      <header>
        <nav id="#about" class="navbar navbar-expand-lg navbar-light">
                <a class="navbar-brand" href="#"><!-- navbar brand -->
                    <img class="logo-main scale-with-grid" src="https://speech.com/wp-content/uploads/2019/11/sps_logo.jpg" data-retina="https://speech.com/wp-content/uploads/2019/11/sps_logo_retina.jpg" data-height="66" alt="SPS Logo" data-no-retina=""></a>
                <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                  <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarNav">
                  <ul class="navbar-nav">
                    <li class="nav-item active" v-for="(navbarLink, index) in navbarLinks" v-bind:key="index">
                      <a class="nav-link" v-bind:href="navbarLink.link">{{navbarLink.linkTitle}}</a>
                    </li>
                  </ul>
                </div>
        </nav>
      </header>
    </div>
</template>
<script>
export default {
  data () {
    return {
      navbarLinks: [{linkTitle: 'Why Speech Processing  Solutions', link: '#about'},{linkTitle: 'Speech-to-text solutions',link: '#careers'},{linkTitle: 'Careers',link: '#footer'}, {linkTitle: 'Blog',link: '#blog'}, {linkTitle: 'Contact',link: '#contact'} ]
    }
  },
  methods: {
  },
  mounted(){
     
    }
}
</script>

<style lang="scss" scoped>
     @import url('https://fonts.googleapis.com/css?family=Nunito+Sans&display=swap');
    
     $text-color: rgb(128, 128, 128);
   .navbar-brand {
        height: 5rem;
        width: 12rem;
        margin-left: 3rem;
    }
    .navbar-toggler {
        border: none; 
    }
    #navbarNav {
      justify-content: flex-end;
    }
    
    header > nav {
        
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        color: $text-color;
         @media (min-width:1025px) {
          width: 90%;
          margin: auto;
       }
    }

    header > nav div:last-child {
        margin-left: 3rem;
        width: 60%;
        
    }
    ul{
          display: flex;
          justify-content: space-around;
          margin-right: 8rem;
    }
    
    ul > li {
       @media (min-width:1025px) {
          padding-left: 5rem;
       }
    }

    ul > li  > a {
         
            color: $text-color !important;
            font-family: "Nunito Sans", "Arial", "Tahoma", "sans-serif";
            font-weight: 500;
            text-transform: uppercase;
            font-size: 14px;
            font-variant-ligatures:none;
            font-weight:500;
            letter-spacing:2px;
            list-style-type:none;
            text-shadow:rgba(0, 0, 0, 0.01) 0px 0px 1px;
            text-size-adjust:100%;
    }
    
</style>