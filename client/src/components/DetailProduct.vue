<template>
  <v-row justify="center">
    <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition" :retain-focus="false">
      <v-card height="1000">
        <v-toolbar dark color="primary">
          <v-btn icon dark @click="close()">
            <v-icon>mdi-close</v-icon>
          </v-btn>
          <v-toolbar-title>{{ DATA.name }}</v-toolbar-title>
        </v-toolbar>
        <v-row>
          <v-sheet color="white" elevation="1" height="450" width="250" class="mt-6 ml-10">
            <v-row cols="12">
              <v-col row="2" class="mt-10">
                <v-img :src="selectedImage === null ? DATA.image : selectedImage"></v-img>
              </v-col>
              <v-col cols="12" class="mt-10" align="center">
                <span>
                  Giá: {{ DATA.price }} đ
                </span><br>
              </v-col>
              <v-col cols="12" align="center">
                <span>
                  Lượi xem: {{ DATA.view }}
                </span><br>
              </v-col>
            </v-row>
          </v-sheet>
          <v-card color="white" elevation="1" height="450" width="250" class="mt-6 ml-10" v-if="DATA_TGDD != null">
            <v-row class="fill-height" cols="12" row="5">
              <v-col row="1" cols="8" align="center">
                <v-img src="https://cdn.haitrieu.com/wp-content/uploads/2021/11/Logo-The-Gioi-Di-Dong-MWG-Y-H.png"
                  max-heigt="30"></v-img>
              </v-col>
                <v-col cols="12" row="1">
                  <v-img :src="DATA_TGDD.image"></v-img>
                </v-col>
                <v-col cols="12" row="1">
                  <v-toolbar-title align="center">
                      {{ DATA_TGDD.name }}
                  </v-toolbar-title>
                </v-col>
                <v-col cols="12" class="price-text" align="center" row="1">
                  Giá :{{ DATA_TGDD.price }}
                </v-col>
                <v-col cols="12" align="center" row="1">
                  Sale : {{ DATA_TGDD.priceSale }}
                </v-col>
                <v-col row="1" cols="12">
                  <v-btn target="_blank" depressed color="primary" :href="DATA_TGDD.link" style="margin-left: 71px;">
                    Xem ngay
                  </v-btn><br />
                </v-col>
              </v-row>
          </v-card>
          <v-card color="white" elevation="1" height="450" width="250" class="mt-6 ml-10" v-if="DATA_FPT != null">
            <v-row class="fill-height" cols="12" row="5">
              <v-col row="1" cols="6" align="center">
                <v-img src="https://fpthcm.com.vn/wp-content/uploads/2021/01/logo-fpt-shop.jpg"
                  max-heigt="30"></v-img>
              </v-col>
                <v-col cols="12" row="1">
                  <v-img :src="DATA_FPT.image" max-width="150"></v-img>
                </v-col>
                <v-col cols="12" row="1">
                  <v-toolbar-title align="center">
                      {{ DATA_FPT.name }}
                  </v-toolbar-title>
                </v-col>
                <v-col cols="12" class="price-text" align="center" row="1">
                  Giá :{{ DATA_FPT.price }}
                </v-col>
                <v-col cols="12" align="center" row="1">
                  Sale : {{ DATA_FPT.priceSale }}
                </v-col>
                <v-col row="1" cols="12">
                  <v-btn depressed color="primary" :href="DATA_FPT.link" style="margin-left: 71px;">
                    Xem ngay
                  </v-btn><br />
                </v-col>
              </v-row>
          </v-card>
          <v-card color="white" elevation="1" height="450" width="250" class="mt-6 ml-10"  v-if="DATA_SHOPEE != null">
            <v-row class="fill-height" cols="12" row="5">
              <v-col row="1" cols="6" align="center">
                <v-img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/fe/Shopee.svg/1200px-Shopee.svg.png"
                  max-heigt="30"></v-img>
              </v-col>
                <v-col cols="12" row="1">
                  <v-img :src="DATA_SHOPEE.image" max-width="150"></v-img>
                </v-col>
                <v-col cols="12" row="1">
                  <v-toolbar-title align="center">
                      {{ DATA_SHOPEE.name }}
                  </v-toolbar-title>
                </v-col>
                <v-col cols="12" class="price-text" align="center" row="1">
                  Giá :{{ DATA_SHOPEE.price }}
                </v-col>
                <v-col cols="12" align="center" row="1">
                  Sale : {{ DATA_SHOPEE.priceSale }}
                </v-col>
                <v-col row="1" cols="12">
                  <v-btn depressed color="primary" :href="DATA_SHOPEE.link" style="margin-left: 71px;">
                    Xem ngay
                  </v-btn><br />
                </v-col>
              </v-row>
          </v-card>
          <v-card color="white" elevation="1" height="450" width="250" class="mt-6 ml-10" v-if="DATA_LAZADA != null">
            <v-row class="fill-height" cols="12" row="5">
              <v-col row="1" cols="6" align="center">
                <v-img src="https://inkythuatso.com/uploads/thumbnails/800/2021/09/lazada-logo-inkythuatso-14-11-39-50.jpg"
                  max-heigt="30"></v-img>
              </v-col>
                <v-col cols="12" row="1">
                  <v-img :src="DATA_LAZADA.image" max-width="150"></v-img>
                </v-col>
                <v-col cols="12" row="1">
                  <v-toolbar-title align="center">
                      {{ DATA_LAZADA.name }}
                  </v-toolbar-title>
                </v-col>
                <v-col cols="12" class="price-text" align="center" row="1">
                  Giá :{{ DATA_LAZADA.price }}
                </v-col>
                <v-col cols="12" align="center" row="1">
                  Sale : {{ DATA_LAZADA.priceSale }}
                </v-col>
                <v-col row="1" cols="12">
                  <v-btn depressed color="primary" :href="DATA_LAZADA.link" style="margin-left: 71px;">
                    Xem ngay
                  </v-btn><br />
                </v-col>
              </v-row>
          </v-card>
        </v-row>
        <h2 class="mt-10 ml-8">Sản phẩm liên quan</h2>
        <v-sheet class="mx-auto ma-6" elevation="8" max-width="1430">
          <v-slide-group v-model="model" class="pa-4" active-class="success" show-arrows>
            <v-slide-item v-for="(item, index) in DATASS" :key="index" cols="12">
              <v-card class="ma-4" height="300" width="200" @click="changeData(item)">
                <v-row class="fill-height" align="center" justify="center" cols="12">
                    <v-col cols="12">
                      <v-img :src="item.image" max-height="200"></v-img>
                    </v-col>
                    <v-col cols="12">
                      <v-toolbar-title class="product-name" align="center">
                          {{ item.name }}
                      </v-toolbar-title>
                    </v-col>
                    <v-col cols="12" align="center">
                      Giá: {{ item.price }}
                    </v-col>
                  </v-row>
              </v-card>
            </v-slide-item>
          </v-slide-group>
        </v-sheet>
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
      model: null,
    }
  },
  props: {
    showDialog: Boolean,
    idDetail: Number,
    DATASS: {
      type: Array
    }
  },
  watch: {
    showDialog(newValue) {
      this.dialog = newValue;
      this.getItem();
    }
  },
  methods: {
    async getItem() {
      let response = await axios.get(`http://103.150.124.193:8000/api/api/detailProduct/${this.idDetail}`);
      this.DATA = response.data.data.data;
      this.DATA_FPT = response.data.data.product1;
      this.DATA_SHOPEE = response.data.data.product2;
      this.DATA_TGDD = response.data.data.product3;
      this.DATA_LAZADA = response.data.data.product4;
    },
    close() {
      this.$emit("close-dialog-detail");
    },
    async changeData(item) {
      let response = await axios.get(`http://103.150.124.193:8000/api/api/detailProduct/${item.id}`);
      this.DATA = response.data.data.data;
      this.DATA_FPT = response.data.data.product1;
      this.DATA_SHOPEE = response.data.data.product2;
      this.DATA_TGDD = response.data.data.product3;
      this.DATA_LAZADA = response.data.data.product4;
    }
  }
}
</script>
<style>
.item-shop {
  text-align: center;
  margin: auto;
}
.price-text {
  text-decoration: line-through;
}
</style>