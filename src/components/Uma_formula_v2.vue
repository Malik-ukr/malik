<template>
    <div>
     
      <v-container >
        
        <v-simple-table  dense>
            <template v-slot:default>
              
                <thead>
                    <tr>
                      <td > {{$t('centeral_frequency')}}
                      </td>
                      <td > {{$t('Height_of_base_station')}}
                      </td>
                      <td > {{$t('Height_of_user_terminal')}}
                      </td>
                    </tr>
                </thead>
                <tbody>
                   <tr v-for="(row,index) in Table" :key=index>	
                     
                    
                     <td >
                       
                        <v-text-field  
                          
                          v-model="Table[index]['fc']"
                          :counter="5"
                          
                          type="number"
                          required
                        ></v-text-field>
                     </td>
                      <td >
                       
                        <v-text-field  
                         
                          v-model="Table[index]['hbs']"
                          :counter="5"
                          
                          type="number"
                          required
                        ></v-text-field>
                     </td>
                      <td >
                       
                        <v-text-field  
                          
                          v-model="Table[index]['hut']"
                          :counter="5"
                          
                          type="number"
                          required
                        ></v-text-field>
                     </td>
                     <td >
                       
                        <v-text-field  
                          
                          v-model="Table[index]['d2D_min']"
                          :counter="5"
                          
                          type="number"
                          required
                        ></v-text-field>
                     </td>
                      <td >
                       
                        <v-text-field  
                         
                          v-model="Table[index]['d2D_max']"
                          :counter="5"
                          
                          type="number"
                          required
                        ></v-text-field>
                     </td>
                     
                        <td> <v-menu >
                        <template v-slot:activator="{ on }">
                          <v-btn
                            :color="row.color"
                            dark
                            v-on="on"
                           
                            small
                          >
                            Color
                          </v-btn>
                        </template>
                        <v-color-picker
                        value="#7417BE"
                        @change="generateData"
                        v-model="row.color"
                        

                        show-swatches
                        class="mx-auto"
                      ></v-color-picker>
                      </v-menu></td>
                   <td> <v-btn class="mx-2" color="blue" @click="generateData()"> {{$t('update')}}</v-btn></td>     
                   <td> <v-btn class="mx-2" color="red" @click="deleteRow(row)">X</v-btn></td>
                   
                   </tr>
                    
                </tbody>
                

            </template>

        </v-simple-table>
        <v-btn @click="addRow">Add</v-btn>
        <div class="small">
            <line-chart :chart-data="graphData"></line-chart>
        </div>
        <MaximumDistance/>
      </v-container>
      </div>
</template>

<script >
   import LineChart from './LineChart.js'
   import MaximumDistance from './MaximumDistance.vue'
   
  
  export default {
    name: 'UMAFormulaV2',
     components: {
     LineChart,
     MaximumDistance
    },
    data () {
        return{
          
        
          
          Table :[
            {
                      fc:10,
                      hbs:25,
                      hut:1.5,
                      d2D_min:10,
                      d2D_max:5000,
                      color: "#4287f5",
                      PLL: [],
                  } 
                  ],
          graphData : null,
          
            
            

        }
    },
  
    created(){
        this.generateData();
        
    },
    methods:{
        addRow(){
          
          this.Table.push(
                   {
                      fc:10,
                      hbs:25,
                      hut:1.5,
                      d2D_min:10,
                      d2D_max:5000,
                      color: "#4287f5",
                      PLL_arr: [],
                  } )
          this.generateData()
          

        },

        generateData () {
            let np = require('jsnumpy');
            
            //console.log(np.arange(0, 5, 0.5));
            this.graphData={labels:[],
            datasets:[]}
            this.Table.map(row=> {
              let dmin = 0;
              let dmax= 10000;
              
              let d2D_range = np.arange (dmin,dmax,50);
              row.PLL_arr = [];
              let d3D_temp= 0;
              let d3D_arr= [];
              

              d2D_range.map(d => {
                  const he = 1;
                  
                  const c = 300000000; // speed of light
                  //let dbp = 4*( this.fc/c) * this.hbs * this.hut; 
                  let h_bs = row.hbs - he;
                  let h_ut = row.hut - he;
                  let d_bp = 4*( row.fc/c) * h_bs * h_ut; 
                  
                  d3D_temp= Math.sqrt( ((d)*(d))  + ((row.hbs-row.hut)*(row.hbs-row.hut) )  )
                  d3D_arr.push(d3D_temp);


                  let PL1 = 28.0 + 22 * Math.log10(d3D_temp) + 20*Math.log10(row.fc);
                  let PL2 = 28.0 + 40* Math.log10(d3D_temp)  + 20*Math.log10(row.fc) - 9*Math.log10((d_bp*d_bp) + ((row.hbs - row.hut)*(row.hbs - row.hut)))
                  
                  let PLL = Math.max(PL1, PL2)

                  row.PLL_arr.push(PLL)
                  

                  
                                  


            
            })
            this.graphData['labels'] = d3D_arr;
            
            
            this.graphData['datasets'].push ({
                                              label: "Pathloss(dB)",
                                              borderColor: row.color,
                                              backgroundColor: 'rgba(0, 0, 0, 0)',
                                              data :row.PLL_arr
                                  })


            });
            
            
            
        

            
        },
    
     deleteRow(row){
           {
            const index = this.Table.indexOf(row);
            if (index > -1) {
              this.Table.splice(index, 1); // 2nd parameter means remove one item only
            }
                }
            this.generateData()
                
                
                }
    
    },
   
  }
</script>


