<template>
 <v-container grid-list-md text-xs-center>
   <v-layout row wrap>
      <v-flex sm12>
        <h1>Import CSV/Xcel file</h1>
        <h3 class="title-import">Import file</h3>
        <v-text-field 
          label="Select Image" 
          v-model='filename'
          @click='pickFile'  
          solo
          >
        </v-text-field>
        <input 
          id="fileInput"
          style="display: none"
					ref="image"
          type="file"
          @change="upload">
        <!-- <a
          @click='save'
          type='button'
          download >
          Save
        </a> -->
      </v-flex>
      <v-flex xs12 sm12>
        <h3 class="title-import">Filtter data</h3>
        <v-select
          v-model="value"
          :items="headers"
          @change="filter"
          chips
          label="Chips"
          multiple
          solo
          ></v-select>
      </v-flex>
      <v-flex xs12 sm12>
            <v-data-table
              :headers="headers"
              :items="doc"
            >
            <template slot="items" slot-scope="props">
              <td  v-for=" item in props.item" :key="item.id">
                {{ item }}
              </td>
            </template>
            <template slot="pageText" slot-scope="{ pageStart, pageStop }">
              From {{ pageStart }} to {{ pageStop }}
            </template>
            </v-data-table>
      </v-flex>
      <!-- <v-snackbar v-model="snack" :timeout="3000" :color="snackColor">
              {{ snackText }}
        <v-btn flat @click="snack = false">Close</v-btn>
      </v-snackbar> -->
   </v-layout>
  </v-container>
</template>

<script>
  import Papa from 'papaparse'
  import Blob from 'blob'
  import FileSaver from 'file-saver'
  export default {
    name: 'parse',
    data () {
      return {
        doc: null,
        headers: [],
        value: [],
        filename: ''
      }
    },
    methods: {
      pickFile () {
        this.$refs.image.click ()
      },
      upload () {
        const that = this
        const fileToLoad = event.target.files[0]
        const reader = new FileReader()
        that.filename = fileToLoad.name
        reader.onload = fileLoadedEvent => {
          Papa.parse(fileLoadedEvent.target.result, {
            header: true,
            complete (results) {
              console.log('complete', results)
              that.doc = results.data
              var keys = Object.keys(that.doc[0]);
              console.log(keys)
              var h = []
              for(var key in keys){
                // console.log(value)
                h.push({ text: keys[key], value: keys[key] })
              }
              console.log(h)
              that.headers = h
              that.value = h
            },
            error (errors) {
              console.log('error', errors)
            }
          })
        }
        reader.readAsText(fileToLoad)
      },
      save () {
        const blob = new Blob([this.parseJSONtoCSV()], { type: 'text/csv' })
        FileSaver.saveAs(blob, 'test.csv')
      },
      parseJSONtoCSV () {
        return Papa.unparse(this.doc)
      },
      savetable () {
        this.snack = true
        this.snackColor = 'success'
        this.snackText = 'Data saved'
      },
      cancel () {
        this.snack = true
        this.snackColor = 'error'
        this.snackText = 'Canceled'
      },
      open () {
        this.snack = true
        this.snackColor = 'info'
        this.snackText = 'Dialog opened'
      },
      close () {
        console.log('Dialog closed')
      },
      filter () {
        console.log('filter array')        
      },
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.title-import{
  text-align: left;
  margin-bottom: 8px;
}
</style>