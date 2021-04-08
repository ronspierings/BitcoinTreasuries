<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="images/logo.png"
          transition="scale-transition"
          width="40"
        />

           <h1>
                Herberts Bitcoin Treasuries  
          </h1>
          
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/ronspierings/BitcoinTreasuries"
        target="_blank"
        text
      >
          
    <span class="mr-2">Open Source</span>
        <v-icon>mdi-github</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <TreasuryList></TreasuryList>
    </v-main>
  </v-app>
</template>

<script>

import TreasuryList from './components/TreasuryList';

export default 
{
  name: 'App',

  components: {
    TreasuryList,
  },

  data: () => ({
    //
  }),
};
</script>
