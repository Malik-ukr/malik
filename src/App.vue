<template>
  
    


 <!-- App.vue -->

<v-app  dark id="inspire">
  
 <v-navigation-drawer app>
         <v-navigation-drawer
        v-model="drawer"
        absolute
        bottom
        permanent
        
        
      >
        <v-list
          nav
          dense
        >
          <v-list-item-group
            v-model="group"
            active-class="deep-purple--text text--accent-4"
          >

          
            <v-list-item :to="formulas[0].link" link   > 
              <v-list-item-icon>
                <v-icon >mdi-home</v-icon>
              </v-list-item-icon>
              <v-list-item-title>Home</v-list-item-title>
            </v-list-item>

     
  
          
            <v-list-item :to="formulas[1].link" link>
              <v-list-item-icon>
                <v-icon>mdi-hammer-wrench</v-icon>
              </v-list-item-icon>
              <v-list-item-title>Formulas</v-list-item-title>
            </v-list-item>
          
          </v-list-item-group>
        </v-list>
      </v-navigation-drawer>
  </v-navigation-drawer>
  <v-app-bar app>
     <v-app-bar
        color="deep-purple"
        
      >
        <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>
  
        <v-toolbar-title>5G Calculator</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-switch
        v-model="isDarkTheme"
        :label="`Switch to: ${isDarkTheme? 'White':'Dark' }`"
        @click="changeTheme"
      ></v-switch>
        <localeChanger/>
      </v-app-bar>
  </v-app-bar>

  <!-- Sizes your content based upon application components -->
  <v-main dark>

    <!-- Provides the application the proper gutter -->
    <v-container fluid>
     

      <!-- If using vue-router -->
      <router-view></router-view>
    </v-container>
  </v-main>

  <v-footer app>
    <!-- -->
  </v-footer>
</v-app>
      

      
   

   
</template>

<script>
 import localeChanger from './components/localeChanger'


export default {
  name: 'App',
  components: {
    localeChanger,
    
  },


  data: () => ({
    //
    drawer: false,
    isDarkTheme:false,
    group: null,
    formulas: [{"name": "home", "link": "/"},
    {"name": "formulas", "link": "/formulas"}]
  }),
  methods:{
    changeTheme(){
      
      this.$vuetify.theme.dark=this.isDarkTheme;
    }
  },
  created(){
    this.$vuetify.theme.dark=this.isDarkTheme;
  },

  
};
</script>
