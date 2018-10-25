<template>
  <v-app>
  <div>
    <template>
      <v-toolbar
        color="rgb(64, 170, 132)"
        dark
        extended
        flat
        class="toolbar-high"
      >
        <v-toolbar-side-icon></v-toolbar-side-icon>
        <v-flex xs10>
          <h1 class="name-project">Datawow</h1>
          <div class="image-title">
            <v-list-tile avatar>
              <v-list-tile-avatar color="teal">
                <span class="white--text headline">C</span>
              </v-list-tile-avatar>


              <v-list-tile-content>
                <v-list-tile-title>CPE412 Shoping</v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
          </div>
        </v-flex>
        <v-flex xs2>
          <v-text-field
          hide-details
          prepend-icon="search"
          single-line
          ></v-text-field>
        </v-flex>
      </v-toolbar>
    </template>
    <v-layout row>
        <v-flex xs2 class="navigation-menu">
          <v-navigation-drawer
            floating
            permanent
            stateless
            value="true"
            color="grey lighten-1"
          >
            <v-list dense>
              <v-list-tile
                v-for="item in items"
                :key="item.title"
                @click=""
              >
                <v-list-tile-action>
                  <v-icon>{{ item.icon }}</v-icon>
                </v-list-tile-action>

                <v-list-tile-content>
                  <v-list-tile-title>{{ item.title }}</v-list-tile-title>
                </v-list-tile-content>
              </v-list-tile>
            </v-list>
          </v-navigation-drawer>
        </v-flex>
        <v-flex xs12 sm10>
          <v-container class="card--flex-toolbar">
            <template>
            <v-layout row>
              <v-flex xs12>
                <v-card >
                 <importcsv/>
                  
                </v-card>
              </v-flex>
            </v-layout>
          </template>
          </v-container>
        </v-flex>
    </v-layout> 
  </div>
  </v-app>
</template>

<script>
import Importcsv from "@/components/Importcsv"
export default {
  name: "app",
  components: {
    Importcsv,
  },
  data () {
    return {
      items: [
        { title: 'Home', icon: 'dashboard' },
        { title: 'About', icon: 'question_answer' }
      ],
      right: null
    }
  }
}
</script>

<style scoped>
.border{
  border-radius: 3px;
  color: white;
  box-shadow: 10px 10px 60px 4px rgba(0,0,0,0.1);
}
.toolbar-high {
  height: 25vh;
  margin-bottom: -15vh; 
  background-color: rgb(64, 170, 132)
}
.name-project{
  margin-top: 120px;
  margin-bottom: 65px;
}
.image-title{
  margin-left: -50px;
}
.navigation-menu{
  margin-top: 17vh;
}
.theme--light.v-list {
  background: rgb(250, 250, 250);
  color: rgba(0,0,0,0.87);
}
.theme--light.v-navigation-drawer {
    background-color: rgb(250, 250, 250);
}
</style>
