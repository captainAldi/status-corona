<template>
  <div>
    <section
      v-if="statusAllData == true"
    >
      <center>
        <v-progress-circular
          :size="70"
          :width="7"
          color="purple"
          indeterminate
        ></v-progress-circular>
        <h2>Fetching All Data..</h2>
        <h4>Please Wait..</h4>
      </center>
    </section>
    
    <section
      v-else
    >
      <v-row>
        <v-col>
          <center>
            <h4>Sumber Data: API Kawal Corona</h4>
            <h5
              v-if="itemDataDunia.length > 0"
            >
              Last Update: {{ new Date().toString(itemDataDunia[0].Last_Update) }}
            </h5>
          </center>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <h2>Indonesia Summary</h2>
        </v-col>
      </v-row>
      <v-row>
        <v-col
          cols="12"
          lg="4"
          md="6"
        >
          <v-card
            hover
            color="yellow"
          >
            <div class="d-flex flex-no-wrap justify-space-between">
              <div v-if="dataIndo.length > 0">
                <v-card-title
                  class="headline"
                >Positif</v-card-title>

                <v-card-text>
                  Jumlah: <strong>{{ dataIndo[0].positif }}</strong> <br>
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

        <v-col
          cols="12"
          lg="4"
          md="6"
        >
          <v-card
            hover
            class="green"
          >
            <div class="d-flex flex-no-wrap justify-space-between">
              <div v-if="dataIndo.length > 0">
                <v-card-title
                  class="headline"
                >Sembuh</v-card-title>

                <v-card-text>
                  Jumlah: <strong>{{ dataIndo[0].sembuh }}</strong> <br>
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

        <v-col
          cols="12"
          lg="4"
          md="6"
        >
          <v-card
            hover
            class="red lighten-1"
          >
            <div class="d-flex flex-no-wrap justify-space-between">
              <div v-if="dataIndo.length > 0">
                <v-card-title
                  class="headline"
                >Meninggal</v-card-title>

                <v-card-text>
                  Jumlah: <strong>{{ dataIndo[0].meninggal }}</strong>
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
          <h2>World Summary</h2>
        </v-col>
      </v-row>
      <v-row>
        <v-col
          cols="12"
          lg="4"
          md="6"
        >
          <v-card
            hover
            color="yellow"
          >
            <div class="d-flex flex-no-wrap justify-space-between">
              <div v-if="dataDunia.length > 0">
                <v-card-title
                  class="headline"
                >Positif</v-card-title>

                <v-card-text>
                  Jumlah: <strong>{{ confirmedWorld | ribuanSeparator }}</strong> <br>
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

        <v-col
          cols="12"
          lg="4"
          md="6"
        >
          <v-card
            hover
            class="green"
          >
            <div class="d-flex flex-no-wrap justify-space-between">
              <div v-if="dataDunia.length > 0">
                <v-card-title
                  class="headline"
                >Sembuh</v-card-title>

                <v-card-text>
                  Jumlah: <strong>{{ recoveredWorld | ribuanSeparator }}</strong> <br>
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

        <v-col
          cols="12"
          lg="4"
          md="6"
        >
          <v-card
            hover
            class="red lighten-1"
          >
            <div class="d-flex flex-no-wrap justify-space-between">
              <div v-if="dataDunia.length > 0">
                <v-card-title
                  class="headline"
                >Meninggal</v-card-title>

                <v-card-text>
                  Jumlah: <strong>{{ deathsWorld | ribuanSeparator }}</strong>
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
          <h2>Data Provinsi</h2>
          <v-card>
            <v-card-title>
              Indonesia
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
            >
              <template v-slot:item.Kasus_Posi="{ item }">
                {{ item.Kasus_Posi | ribuanSeparator }}
              </template>
              <template v-slot:item.Kasus_Semb="{ item }">
                {{ item.Kasus_Semb | ribuanSeparator }}
              </template>
              <template v-slot:item.Kasus_Meni="{ item }">
                {{ item.Kasus_Meni | ribuanSeparator }}
              </template>
            </v-data-table>
          </v-card>
        </v-col>

        <v-col>
          <h2>Data Dunia</h2>
          <v-card>
            <v-card-title>
              Worldwide
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
            >
              <template v-slot:item.Confirmed="{ item }">
                {{ item.Confirmed | ribuanSeparator }}
              </template>
              <template v-slot:item.Recovered="{ item }">
                {{ item.Recovered | ribuanSeparator }}
              </template>
              <template v-slot:item.Deaths="{ item }">
                {{ item.Deaths | ribuanSeparator }}
              </template>
            </v-data-table>
          </v-card>
        </v-col>
      </v-row>
    </section>
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
    },
    confirmedWorld() {
      const dataBaru = this.itemDataDunia.map(confirm => {
        return confirm.Confirmed
      })

      const jumlahDataBaru = dataBaru.reduce((a,b) => a + b, 0)

      return jumlahDataBaru
    },
    recoveredWorld() {
      const dataBaru = this.itemDataDunia.map(recover => {
        return recover.Recovered
      })

      const jumlahDataBaru = dataBaru.reduce((a,b) => a + b, 0)

      return jumlahDataBaru
    },
    deathsWorld() {
      const dataBaru = this.itemDataDunia.map(death => {
        return death.Deaths
      })

      const jumlahDataBaru = dataBaru.reduce((a,b) => a + b, 0)

      return jumlahDataBaru
    },
    statusAllData() {
      let status = true;

      if((this.dataIndo.length > 0 && this.dataProv.length > 0) && this.dataDunia.length > 0) {
        
        status = false;
      
      } else {
        status = true
      }

      return status

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
  },
  filters: {
    ribuanSeparator (jumlah) {
      return jumlah.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }
  }
}
</script>

<style>

</style>