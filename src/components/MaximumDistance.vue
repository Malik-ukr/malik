<template>
<v-card>
    <h1> {{$t('Transmission_gNode')}} </h1>
    <v-simple-table>
        <tbody>
            <tr>
                <td>
                    <v-text-field
                    label="gNodeB Power"
                    v-model="gNodeB_Power"
                    @change="calculate"
                    type="number"
                    counter="5"
                    placeholder="gNodeB Power"


                    />
                </td>
                <td>
                    <v-text-field
                    label="gNode Gain"
                    v-model="gNodeGain"
                    @change="calculate"
                    type="number"
                    counter="5"
                    placeholder="GNode Gain"


                    />
                </td>
                <td>
                    <v-text-field
                    label="Tx Cable Losses"
                    v-model="Tx_Cable_Losses"
                    @change="calculate"
                    type="number"
                    counter="5"
                    placeholder="Tc Cable Losses"


                    />
                </td>
            </tr>
        </tbody>
        
    </v-simple-table>
    <v-divider></v-divider>
    <h1> {{$t('Receiver')}} </h1>
    <v-simple-table>
        <tbody>
            <tr>
                <td>
                    <v-text-field
                    label="gNodeB Power"
                    v-model="gNodeB_Power"
                    @change="calculate"
                    type="number"
                    counter="5"
                    placeholder="gNodeB Power"


                    />
                </td>
                <td>
                    <v-text-field
                    label="gNode Gain"
                    v-model="gNodeGain"
                    @change="calculate"
                    type="number"
                    counter="5"
                    placeholder="GNode Gain"


                    />
                </td>
                <td>
                    <v-text-field
                    label="Tx Cable Losses"
                    v-model="Tx_Cable_Losses"
                    @change="calculate"
                    type="number"
                    counter="5"
                    placeholder="Tc Cable Losses"


                    />
                </td>
            </tr>
        </tbody>
    </v-simple-table>

     <v-divider></v-divider>
    <h1> {{$t('Additional_losses')}} </h1>
    <v-simple-table>
        <tbody>
            <tr>
                <td>
                    <v-text-field
                    label="gNodeB Power"
                    v-model="gNodeB_Power"
                    @change="calculate"
                    type="number"
                    counter="5"
                    placeholder="gNodeB Power"


                    />
                </td>
                <td>
                    <v-text-field
                    label="gNode Gain"
                    v-model="gNodeGain"
                    @change="calculate"
                    type="number"
                    counter="5"
                    placeholder="GNode Gain"


                    />
                </td>
                <td>
                    <v-text-field
                    label="Tx Cable Losses"
                    v-model="Tx_Cable_Losses"
                    @change="calculate"
                    type="number"
                    counter="5"
                    placeholder="Tc Cable Losses"


                    />
                </td>
            </tr>
        </tbody>
    </v-simple-table>
     <v-divider></v-divider>
     
    <h1> {{$t('Output')}} </h1>
    <v-simple-table>
        <tbody>
            <tr>
              
                <td>
                    <v-text-field
                    disabled
                    label="Maximum Path Loss"
                    v-model="maxPathloss"
                   
                    type="number"
                    counter="5"
                   


                    />
                </td>
                <td>
                    <v-text-field
                    disabled
                    label="Maximum Distance"
                    v-model="maxDistance"
                    
                    type="number"
                    counter="5"
                    


                    />
                </td>
            </tr>
        </tbody>
    </v-simple-table>

</v-card>
    
</template>

<script>
export default {
    name : 'MaximumDistance',
    data(){
        return{
            msg:"hello",
            gNodeB_Power:0,
            gNodeGain:0,
            maxPathloss:0,
            maxDistance:0,


        }
    },
    methods:{
        calculate(){
            this.maxPathloss = this.maxPathloss +1;
             this.maxDistance = this.maxDistance +1;

        }
    }


  
}
</script>
