<template>
<div>
  
   <v-card>
      <v-tabs
        background-color="deep-purple"
        center-active
        dark
      >
        <v-tab>Random Chart</v-tab>
         <v-tab-item>
          <random-chart/>
        </v-tab-item>

        <v-tab>Uma Formula</v-tab>
        <v-tab-item>
          <UMAFormula></UMAFormula>
        </v-tab-item>
        
        
        <v-tab>Rma Formula </v-tab>
        <v-tab-item>
          <UMAFormulaV2></UMAFormulaV2>
        </v-tab-item>
        <v-tab>Formula 3</v-tab>

        
        
      </v-tabs>
    </v-card>

</div>
</template>

<script>

  import RandomChart from '../components/RandomChart'
  import UMAFormula from '../components/Uma_formula'
   import UMAFormulaV2 from '../components/Uma_formula_v2'
  



  export default {
    name: 'Formulas',
    

    components: {
      
        UMAFormula,  
        UMAFormulaV2,
        RandomChart,
        
        
        
    },
  }
</script>
