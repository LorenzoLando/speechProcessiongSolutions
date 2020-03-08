<template>
  <div>
    <!-- Footer -->
    <footer class="page-footer font-small indigo">
    <!-- Grid row-->
        <div class="row text-center d-flex justify-content-center pt-5 mb-3">
          <!-- Grid column -->
          <div class="col-md-2 " v-for="(footerLink, index) in footerLinks" v-bind:key="index">
            <h6 class="text-uppercase font-weight-bold">
              <a class="nav-link" v-bind:href="footerLink.link">{{footerLink.linkTitle}}</a>
            </h6>
          
          </div>
        </div>
        <!-- Grid row-->
        <hr style="margin: 0 15%;">
         <!-- Copyright -->
        <div class="footer-copyright text-center py-3">© 2020 Copyright:
          <a href="#"> Lorenzo Lando</a>
        </div>
      <!-- Copyright -->
    </footer>
    <!-- Footer -->
  </div>
</template>

<script>
export default {
  data () {
    return {
      footerLinks: [
        {linkTitle: 'General business principles', link: '#'},
        {linkTitle: 'Terms and conditions',link: '#'},
        {linkTitle: 'Cookie notice',link: '#'},
        {linkTitle: 'Legal notice',link: '#'},
        {linkTitle: 'Privacy policy',link: '#'},
        ]
    }
  }
}
</script>

<style lang="scss" scoped>
 @import url('https://fonts.googleapis.com/css?family=Nunito+Sans&display=swap');
$text-color: #3c3c3c;
 
 .page-footer  {
   height: 25vh;
   background-color: rgb(245, 245, 245);
 }

 .page-footer div,
 .page-footer hr  {
   background-color: rgb(245, 245, 245);
 }

//  link styling for the footer
 a {
   
            color: $text-color !important;
            font-family: "Nunito Sans", "Arial", "Tahoma", "sans-serif";
            font-weight: 500;
            text-transform: uppercase;
            font-size: 12px;
            font-variant-ligatures:none;
            font-weight:500;
            letter-spacing:2px;
            list-style-type:none;
            text-shadow:rgba(0, 0, 0, 0.01) 0px 0px 1px;
            text-size-adjust:100%
 }
 </style>