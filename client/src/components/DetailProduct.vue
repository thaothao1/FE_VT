<template>
  <v-row justify="center">
    <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition" :retain-focus="false">
      <v-card>
        <v-toolbar dark color="primary">
          <v-btn icon dark @click="close()">
            <v-icon>mdi-close</v-icon>
          </v-btn>
          <v-toolbar-title>{{ DATA.name }}</v-toolbar-title>
        </v-toolbar>
        <v-row>
          <v-sheet color="white" elevation="1" height="300" width="300" class="mt-6 ml-10">
            <v-row cols="12">
              <v-col row="2" class="mt-10">
                <v-img :src="selectedImage === null ? DATA.image : selectedImage"></v-img>
              </v-col>
              <v-col cols="6">
                <span class="ml-4">
                  Lượi xem: {{DATA.view}}
                </span>
              </v-col>
              <v-col cols="6">
                <span>
                  Giá: {{DATA.price}} đ
                </span>
              </v-col>
            </v-row>
          </v-sheet>
          <v-sheet color="white" elevation="1" height="300" width="250" class="mt-6 ml-10" v-if="DATA_TGDD != null">
            <div class="product">
              <v-row cols="12">
                <v-col row="1" cols="6">
                  <v-img src="https://cdn.haitrieu.com/wp-content/uploads/2021/11/Logo-The-Gioi-Di-Dong-MWG-Y-H.png" max-heigt="30"></v-img>
                </v-col>
                <v-col row="2" cols="12" class="mt-10">
                  <v-img :src="DATA_TGDD.image"></v-img>
                </v-col>
                <v-col cols="6">
                  <span class="ml-4">
                    <v-btn depressed color="primary" :href="DATA_TGDD.link">
                      Xem ngay
                    </v-btn>
                  </span>
                </v-col>
                <v-col cols="6">
                  <span>
                    Giá:{{ DATA_TGDD.price }}
                  </span>
                </v-col>
              </v-row>
            </div>
          </v-sheet>
          <v-sheet color="white" elevation="1" height="300" width="250" class="mt-6 ml-10" v-if="DATA_FPT != null">
            <div class="product">
              <v-row cols="18" row="4">
                <v-col row="1" cols="6">
                  <v-img src="https://fpthcm.com.vn/wp-content/uploads/2021/01/logo-fpt-shop.jpg" max-heigt="30"></v-img>
                </v-col>
                <v-col row="1" cols="8">
                  <v-img :src="DATA_FPT.image" width="100"></v-img>
                </v-col>
                <v-col row="1" cols="8">
                  <v-btn depressed color="primary" :href="DATA_FPT.link">
                    Xem ngay
                  </v-btn>
                </v-col>
                <v-col row="1" cols="8">
                  {{ DATA_FPT.price }}
                </v-col>
              </v-row>
            </div>
          </v-sheet>
          <v-sheet color="white" elevation="1" height="300" width="250" class="mt-6 ml-10" v-if="DATA_LAZADA != null">
            <div class="item-shop">
              <v-col cols="6">
                <v-img
                  src="https://inkythuatso.com/uploads/thumbnails/800/2021/09/lazada-logo-inkythuatso-14-11-39-50.jpg" max-heigt="30">
                </v-img>
              </v-col>
              <v-col cols="8">
                <v-img :src="DATA_LAZADA.image" width="100"></v-img>
              </v-col>
              <v-col cols="8">
                <v-btn depressed color="primary" :href="DATA_LAZADA.link">
                  Xem ngay
                </v-btn>
              </v-col>
              <v-col cols="8">
                {{ DATA_LAZADA.price }}
              </v-col>
            </div>
          </v-sheet>
          <v-sheet color="white" elevation="1" height="300" width="250" class="mt-6 ml-10" v-if="DATA_SHOPEE != null">
            <div class="item-shop">
                <v-col cols="5">
                  <v-img
                    src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/fe/Shopee.svg/1200px-Shopee.svg.png" max-heigt="30">
                  </v-img>
                </v-col>
                <v-col cols="8">
                  <v-img :src="DATA_SHOPEE.image" width="100"></v-img>
                </v-col>
                <v-col cols="8">
                  <v-btn depressed color="primary" :href="DATA_SHOPEE.link">
                    Xem ngay
                  </v-btn>
                </v-col>
                <v-col cols="8">
                  {{ DATA_SHOPEE.price }}
                </v-col>
            </div>
          </v-sheet>
        </v-row>
      </v-card>
    </v-dialog>
  </v-row>
</template>
<script>
import axios from 'axios';

export default {
  data() {
    return {
      DATA: [],
      DATA_FPT: [],
      DATA_TGDD: [],
      DATA_LAZADA: [],
      DATA_SHOPEE: [],
      notifications: false,
      sound: true,
      widgets: false,
      dialog: false,
      selectedImage: null,
    }
  },
  props: {
    showDialog: Boolean,
    idDetail: Number,
  },
  watch: {
    showDialog(newValue) {
      this.dialog = newValue;
      this.getItem();
    }
  },
  methods: {
    async getItem() {
      let response = await axios.get(`http://localhost:8000/api/api/detailProduct/${this.idDetail}`);
      this.DATA = response.data.data.data;
      this.DATA_FPT = response.data.data.product1;
      this.DATA_SHOPEE = response.data.data.product2;
      this.DATA_TGDD = response.data.data.product3;
      this.DATA_LAZADA = response.data.data.product4;
    },
    close() {
      this.$emit("close-dialog-detail");
    },
    zoom(url) {
      this.selectedImage = url;
    }
  }
}
</script>
<style>
.item-shop {
  text-align: center;
  margin: auto;
}
</style>