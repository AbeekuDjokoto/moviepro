<template>
    <navigationbar></navigationbar>
    <FooterComponent></FooterComponent>
  <router-view/>
</template>

<script>
  import NavBarComponentVue from "@/components/NavBarComponent.vue";
  import FooterComponentVue from "./components/FooterComponent.vue";
import FooterComponent from "./components/FooterComponent.vue";
  export default {
    components: {
    "navigationbar": NavBarComponentVue,
    "footerComponent": FooterComponentVue,
    FooterComponent
},
    data() {
      return {
        searchtxt: "Search",
      };
    },
  };
  </script>

<style>
:root{
  --primary-font: DM Sans, sans-serif;
  --background-primary-color: #242222;
  --background-btn-color: #C53939;
  --background-outline-btn-color: #C43838;
  --background-nav-color: #313030;
}

*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body{
  background-color: var(--background-primary-color);
}

#app {
  font-family: var(--primary-font); 

}


</style>
