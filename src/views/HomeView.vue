<template>
  <div class="home">
    
     <InfoBelowHeader/>
     

    
    
    <Properties :propertiesData = "propertiesData"/>
      
    


        
    <div class="home__slider">
      <CarouselPictureContent/>
      </div>
      
      </div>
</template>
<script>
import {featureData, propertiesData}  from '../data/data.dummy'


import Properties from '@/components/Properties.vue'
import InfoBelowHeader from '../components/InfoBelowHeader.vue'
import Accordion from "../components/Accordion-item.vue";
import AccordionItem from "../components/Accordion.vue";





export default{
  name: 'HomeView',
  components: {
    Properties,
    InfoBelowHeader,
    Accordion,
    AccordionItem,
    Accordion,
    Accordion
},

data(){
  return{
    featureData: featureData,
    propertiesData: propertiesData,
    }
  },
}

</script>


