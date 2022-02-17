<template>
    <div>
     <v-form >
      <v-container>
        <v-simple-table dense>
            <template v-slot:default>
                <thead>
                    <tr>
                        <th>
                            Central Frequency
                        </th>
                        <th>
                            Distance
                        </th>
                        <th>
                            Central Frequency
                        </th>
                        <th>
                            Distance
                        </th>
                        <th>
                            Central Frequency
                        </th>
                        <th>
                            Distance
                        </th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                     <td>
                        
                                <v-text-field 
                                @change="generateData"
                                v-model="fc"
                                :counter="5"
                                type="number"
                                label="Central Frequency"
                                required
                                
                                ></v-text-field>
                        
                    
                    </td>
                    <td>
                        
                                <v-text-field 
                                    @change="generateData"
                                v-model="fc"
                                :counter="5"
                                type="number"
                                label="Central Frequency"
                                required
                               
                                ></v-text-field>
                        
                    
                    </td>
                    <td>
                        
                                <v-text-field 
                                    @change="generateData"
                                v-model="fc"
                                :counter="5"
                                type="number"
                                label="Central Frequency"
                                required
                                
                                ></v-text-field>
                        
                    
                    </td>
                    <td>
                        
                                <v-text-field 
                                    @change="generateData"
                                v-model="fc"
                                :counter="5"
                                type="number"
                                label="Central Frequency"
                                required
                               
                                ></v-text-field>
                        
                    
                    </td>
                    <td>
                        
                                <v-text-field 
                                    @change="generateData"
                                v-model="fc"
                                :counter="5"
                                type="number"
                                label="Central Frequency"
                                required
                                
                                ></v-text-field>
                        
                    
                    </td>
                    <td>
                        
                                <v-text-field 
                                    @change="generateData"
                                v-model="fc"
                                :counter="5"
                                type="number"
                                label="Central Frequency"
                                required
                                
                                ></v-text-field>
                        
                    
                    </td>
                    <td>
                        
                                <v-text-field 
                                    @change="generateData"
                                v-model="fc"
                                :counter="5"
                                type="number"
                                label="Central Frequency"
                                required
                                
                                ></v-text-field>
                        
                    
                    </td>
                    </tr> 
                    
                </tbody>

            </template>

        </v-simple-table>
        <v-row  >
          <v-col
          dense
            class="shrink"
            cols="12"
            md="4"
          >
            <v-text-field 
                @change="generateData"
              v-model="fc"
              :counter="5"
              type="number"
              label="Central Frequency"
              required
              outlined
            ></v-text-field>
          </v-col>
  
          <v-col
          class="shrink"
            cols="12"
            md="4"
          >
            <v-text-field
              v-model="hbs"
              type="number"
              @change="generateData"
              :counter="5"
              label="Height Of Base station"
              required
              outlined
            ></v-text-field>
          </v-col>
  
          <v-col
            cols="12"
            class="shrink"
            md="4"
          >
            <v-text-field
              v-model="hut"
              @change="generateData"
              type ="number"
              :counter ="5"
              label="Height of User Terminal"
              required
              outlined
            ></v-text-field>

          </v-col>
           <v-col
            cols="12"
            md="4"
          >
            <v-text-field
              v-model="d2D_min"
              @change="generateData"
              type ="number"
              :counter ="5"
              label="Distance b/w Bs to UT(Min)"
              required
              outlined
            ></v-text-field>

          </v-col>
              <v-col
            cols="12"
            md="4"
          >
            <v-text-field
               @change="generateData"
              v-model="d2D_max"
              type ="number"
              :counter ="5"
              label="Distance b/w Bs to UT(Max)"
              required
              outlined
              class="shrink"
            ></v-text-field>

          </v-col>
          

        </v-row>
      </v-container>
    </v-form>
    <div class="small">
    <line-chart :chart-data="graphData"></line-chart>
      <v-text-field
               disabled
              v-model="d3D_temp"
              type ="number"
              :counter ="5"
              label="Direct Distance b/w BS and UT "
              
              outlined
              
            ></v-text-field>
         <v-text-field
               disabled
              v-model="PLL"
              type ="number"
              :counter ="5"
              label="Pathloss "
              
              outlined
              
            ></v-text-field>
    </div>
    </div>
</template>

<script>
   import LineChart from './LineChart.js'

  export default {
    name: 'UMAFormula',
     components: {
      LineChart,
    },
    data () {
        return{
            fc:10,
            hbs:25,
            hut:1.5,
            d2D_min:10,
            d2D_max:5000,
            d3D_temp:0,
            d3D_arr:[],
            PLL: 0,
            graphData : {labels:[],
          datasets:[]},

        }
    },
    created(){
        this.generateData()
    },
    methods:{
        inputChanged(){
            
        },

        generateData () {
            let np = require('jsnumpy');
            
            //console.log(np.arange(0, 5, 0.5));
            
            let d2D_range = np.arange (this.d2D_min, this.d2D_max,50);
            let PLL_arr = [];
            this.d3D_arr= []
            

            d2D_range.map(d => {
                const he = 1;
                this.d3D_temp =0;
                const c = 300000000; // speed of light
                //let dbp = 4*( this.fc/c) * this.hbs * this.hut; 
                let h_bs = this.hbs - he;
                let h_ut = this.hut - he;
                let d_bp = 4*( this.fc/c) * h_bs * h_ut; 
                
                this.d3D_temp= Math.sqrt( ((d)*(d))  + ((this.hbs-this.hut)*(this.hbs-this.hut) )  )
                this.d3D_arr.push(this.d3D_temp);


                let PL1 = 28.0 + 22 * Math.log10(this.d3D_temp) + 20*Math.log10(this.fc);
                let PL2 = 28.0 + 40* Math.log10(this.d3D_temp)  + 20*Math.log10(this.fc) - 9*Math.log10((d_bp*d_bp) + ((this.hbs - this.hut)*(this.hbs - this.hut)))
                
                 this.PLL = Math.max(PL1, PL2)

                PLL_arr.push(this.PLL)
               


            
            })

            
            var scaled_PLL_arr= PLL_arr.map(function(x) { return x * 5; });


            this.graphData = {labels:this.d3D_arr,
                                datasets:[ {
                                            label: "Pathloss",
                                            borderColor: "#32a852",
                                            backgroundColor: 'rgba(0, 0, 0, 0)',
                                            data :PLL_arr
                                },
                                {
                                            label: "Pathloss",
                                            borderColor: "#000000",
                                            backgroundColor: 'rgba(0, 0, 0, 0)',
                                            data :scaled_PLL_arr
                                }]
                                }
        },
    

    
    }
   
  }
</script>


