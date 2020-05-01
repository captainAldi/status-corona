<template>
  <div>
    <v-row>
      <v-col>
        <h2>Data Indo</h2>
        <v-card
          hover
        >
          <div class="d-flex flex-no-wrap justify-space-between">
            <div v-if="dataIndo.length > 0">
              <v-card-title
                class="headline"
                v-text="dataIndo[0].name"
              ></v-card-title>

              <v-card-text>
                Positif: <strong>{{ dataIndo[0].positif }}</strong> <br>
                Sembuh: <strong>{{ dataIndo[0].sembuh }}</strong> <br>
                Meninggal: <strong>{{ dataIndo[0].meninggal }}</strong>
              </v-card-text>

            </div>

            <v-avatar
              class="ma-3"
              size="125"
              tile
            >
              <v-img alt="tes"></v-img>
            </v-avatar>
          </div>
        </v-card>
      </v-col>
    </v-row>

    <v-row>
      <v-col>
        <h2>Data Prov</h2>
        <v-card>
          <v-card-title>
            Indo
            <v-spacer></v-spacer>
            <v-text-field
              v-model="searchDataProv"
              append-icon="mdi-magnify"
              label="Search"
              single-line
              hide-details
            ></v-text-field>
          </v-card-title>
          <v-data-table
            :headers="headersDataProv"
            :items="itemDataProv"
            :search="searchDataProv"
          ></v-data-table>
        </v-card>
      </v-col>
    </v-row>

    <v-row>
      <v-col>
        <h2>Data Dunia</h2>
        <v-card>
          <v-card-title>
            World
            <v-spacer></v-spacer>
            <v-text-field
              v-model="searchDataDunia"
              append-icon="mdi-magnify"
              label="Search"
              single-line
              hide-details
            ></v-text-field>
          </v-card-title>
          <v-data-table
            :headers="headersDataDunia"
            :items="itemDataDunia"
            :search="searchDataDunia"
          ></v-data-table>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      dataIndo: [],
      dataProv: [],
      dataDunia: [],
      searchDataProv: '',
      searchDataDunia: '',
      headersDataProv: [
        { text: 'Provinsi', value: 'Provinsi' },
        { text: 'Positif', value: 'Kasus_Posi' },
        { text: 'Sembuh', value: 'Kasus_Semb' },
        { text: 'Meninggal', value: 'Kasus_Meni' },
      ],
      headersDataDunia: [
        { text: 'Negara', value: 'Country_Region' },
        { text: 'Positif', value: 'Confirmed' },
        { text: 'Sembuh', value: 'Recovered' },
        { text: 'Meninggal', value: 'Deaths' },
      ]
    }
  },
  computed: {
    itemDataProv() {
      const dataBaru = this.dataProv.map(attr => {
        return attr.attributes
      })

      return dataBaru
    },
    itemDataDunia() {
      const dataBaru = this.dataDunia.map(attr => {
        return attr.attributes
      })

      return dataBaru
    }
  },
  created () {
    this.getIndo()
    this.getProv()
    this.getWorld()
  },
  methods: {
    async getIndo() {
      try {
        let res = await axios.get('https://api.kawalcorona.com/indonesia/')
        this.dataIndo = res.data
      } catch (error) {
        console.log(error) 
      }
    },
    async getProv() {
      try {
        let res = await axios.get('https://api.kawalcorona.com/indonesia/provinsi/')
        this.dataProv = res.data
      } catch (error) {
        console.log(error) 
      }
    },
    async getWorld() {
      try {
        let res = await axios.get('https://api.kawalcorona.com/')
        this.dataDunia = res.data
      } catch (error) {
        console.log(error) 
      }
    }
  }
}
</script>

<style>

</style>