<template>
  <section class="section is-fullheight">
    <b-tabs v-model="activeTab" type="is-boxed" expanded position="is-centered">
      <form>

        <b-tab-item label="1. Pilih Profil Karton">
          <div class="columns is-mobile">
            <div class="column is-half is-offset-one-quarter">
              <h1 class="title">Karton Box</h1>
              <b-field label="Profil Karton Box">
                <b-select v-model="selectedCartonProfile" placeholder="Select a name" expanded>
                  <option
                  v-for="cartonProfile in cartonProfiles"
                  :value="cartonProfile.id"
                  :key="cartonProfile.id">
                      {{ cartonProfile.name }}
                  </option>
                </b-select>
              </b-field>
              <b-field label="Kode Karton Box">
                <b-input :value="cartonCode" v-model="cartonCode">
                </b-input>
              </b-field>
              <button @click="activeTab = 1" class="button btn-long is-medium is-primary" type="button">Lanjut</button>
            </div>
          </div>
        </b-tab-item>
        <b-tab-item label="2. Inputkan Inner Box" disabled>
          <div class="container is-fluid">
            <div class="columns">
              <div class="column is-3 side-view">
                <div class="box">
                  <section class="section">
                    <p class="is-size-7">Profil</p>
                    <p class="is-size-5 has-text-weight-bold">{{ selectedCartonProfile }} </p>
                  </section>
                  <section class="section">
                    <p class="is-size-7">Kode Box</p>
                    <p class="is-size-5 has-text-weight-bold">{{ cartonCode }}</p>
                  </section>
                  <section class="section">
                    <b-field label="Kode Produk">
                      <b-input v-model="itemAdded.type">
                      </b-input>
                    </b-field>
                    <b-field label="Kode Unik">
                      <b-input v-model="itemAdded.code">
                      </b-input>
                    </b-field>
                    <button @click="onItemAdded" :disabled="isAddBtnDisabled" class="button is-primary is-fullwidth" type="button">Tambah Sepatu</button>
                  </section>
                  <section class="section has-text-centered">
                    <p class="is-size-5">Sudah Diinputkan</p>
                    <p class="is-size-1">{{ itemsAdded }}</p>
                  </section>
                </div>
              </div>
              <div class="column is-9">
                <div class="box">
                  <button @click="clearItem()" class="button is-danger" type="button">Kosongkan Inputan</button>
                  <table-input :item="item" :is-loading="isLoading"></table-input>

                </div>
                <button class="button btn-long is-primary is-medium is-pulled-right">Simpan</button>
              </div>
            </div>
          </div>
        </b-tab-item>

      </form>
    </b-tabs>
  </section>
</template>

<script>
import TableInput from './TableInput.vue'

export default {
  components: {
    TableInput
  },
  data() {
    return {
      // dummy
      isLoading: false,
      isAddBtnDisabled: false,
      activeTab: 0,
      cartonCode: "hesoyam",
      selectedCartonProfile: '',
      itemAdded: {
        type: 'asd',
        size: 39,
        code: 'dsa'
      },
      item: [
      ],
      cartonProfiles: [
        { id: 1, name: "solid - 12" },
        { id: 2, name: "solid - 6" }
      ]
    }
  },
  computed: {
    itemsAdded() {
      return this.item.length
    }
  },
  methods: {
    onItemAdded () {
      this.item.push({type: this.itemAdded.type, size: this.itemAdded.size, code: this.itemAdded.code})
    },
    clearItem() {
      this.item = []
    }
  }
};
</script>

<style scoped>
.is-fullheight {
  min-height: 90vh;
  padding-top: 1rem;
}
.box {
  margin: 2rem;
  border: 1.5px solid;
  box-shadow: none;
  min-height: 50vh;
}
.side-view .box {
  border: 0;
  margin-right: 0;
  padding: 0 !important;
}
.side-view .section {
  padding: 1rem 0 !important;
  padding-top: 0 !important;
}
.btn-long {
  margin-right: 2rem;
  padding-left: 2rem;
  padding-right: 2rem;
}
</style>
