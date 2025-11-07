<template>
  <div class="overflow-hidden">
    <Navbar />
     <HeroSection/>
     <PetroleumTrading/>
     <Importexport/>
     <Phonecalls/>
     
  </div>
</template>


 <script setup>
import Navbar from './components/Navbar.vue';
import HeroSection from './components/HeroSection.vue';
import PetroleumTrading from './components/PetroleumTrading.vue';
import Phonecalls from './components/Phonecalls.vue';
import Importexport from './view/Importexport.vue';
</script>