<template>
  <main-container>
    <template v-slot:header>
    <Header />
    <Swiper/>
    
    </template>
    
    <main >
      <router-view/>
      
    </main>
    <template v-slot:footer>
    <Footer />
    </template>
  </main-container>
</template>







<script>
// @ is an alias to /src

import Header from '@/components/Header.vue'
import Footer from '@/components/Footer/Footer.vue'
import MainContainer from './components/MainContainer.vue'
import Swiper from './components/Swiper.vue'







export default {
 
  components: {
    Header,
    Footer,
    MainContainer,
    Swiper,
   
},
}
</script>

