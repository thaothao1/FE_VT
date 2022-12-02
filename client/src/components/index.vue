<template>
    <div class="list-product" style="background: teal; height: 100%;">
        <v-navigation-drawer app width="300">
            <v-sheet color="grey lighten-4" class="pa-4">
                <v-avatar class="mb-4" color="grey darken-1" size="64"></v-avatar>
                <div>BestPrice</div>
            </v-sheet>
            <v-list shaped>
                <v-card
                class="mx-auto"
                max-width="300"
                tile
              >
                <v-list rounded>
                  <v-subheader>{{CATEGORY_PHONE.name}}</v-subheader>
                  <v-list-item-group
                    v-model="selectedItem"
                    color="primary"
                  >
                    <v-list-item
                    v-for="(item, index) in CATEGORY_PHONE.label" :key="index"
                    >
                      <v-list-item-icon>
                        <v-icon v-text="item.icon"></v-icon>
                      </v-list-item-icon>
                      <v-list-item-content>
                        <v-list-item-title @click="setDataFilter(item)">{{item.name}}</v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>
                  </v-list-item-group>
                </v-list>
              </v-card>
              <v-card
              class="mx-auto"
              max-width="300"
              tile
            >
              <v-list rounded>
                <v-subheader>{{CATEGORY_LAPTOP.name}}</v-subheader>
                <v-list-item-group
                  v-model="selectedItem"
                  color="primary"
                >
                  <v-list-item
                  v-for="(item, index) in CATEGORY_LAPTOP.label" :key="index"
                  >
                    <v-list-item-icon>
                      <v-icon v-text="item.icon"></v-icon>
                    </v-list-item-icon>
                    <v-list-item-content>
                      <v-list-item-title @click="setDataFilter(item)">{{item.name}}</v-list-item-title>
                    </v-list-item-content>
                  </v-list-item>
                </v-list-item-group>
              </v-list>
            </v-card>
                <!-- <strong style="font-size: 25px; color: darksalmon;" class="ml-4">{{CATEGORY_PHONE.name}}</strong>
                <v-list class="pl-14" shaped>
                    <v-list-item v-for="(item, index) in CATEGORY_PHONE.label" :key="index">
                        <v-list-item-content>
                            <v-list-item-title @click="setDataFilter(item)" style=" font-family:Impact Charcoal; font-size: 15px;text-transform: uppercase "><a style="color: black">{{ item.name }}</a></v-list-item-title>
                        </v-list-item-content>
                    </v-list-item>
                </v-list>
                <strong style="font-size: 25px; color: darksalmon;" class="ml-4">{{CATEGORY_LAPTOP.name}}</strong>
                <v-list class="pl-14" shaped>
                    <v-list-item v-for="(item, index) in CATEGORY_LAPTOP.label" :key="index">
                        <v-list-item-content>
                            <v-list-item-title @click="setDataFilter(item)" style=" font-family:Impact Charcoal; font-size: 15px;text-transform: uppercase "><a style="color: black">{{ item.name }}</a></v-list-item-title>
                        </v-list-item-content>
                    </v-list-item>
                </v-list> -->
            </v-list>
        </v-navigation-drawer>
        <v-main>
            <v-container fluid>
                <strong style="font-size: 25px; color: darksalmon;">All Product</strong>
                <v-row>
                <v-col
                    v-for="item in DATA"
                    :key="item"
                    cols="3"
                    @click="openDialog(item)"
                >
                    <v-sheet color="white" elevation="1" height="500px" width="250px" class="mt-6 ml-4">
                        <div class="product">
                            <span class="image">
                                <v-col
                                cols="12"
                                >
                                <v-img :src="item.image"  style="width : 300px ; heigth : 700px"></v-img>
                                </v-col>
                            </span>
                            <span class="product-name" style=""><a :href=item.link>
                                {{item.name}}</a>
                            </span><br />
                            <span class="product-price">
                               Giá: {{item.price}}
                            </span><br/>
                            <div class="text-center" v-if="selectedTab !== 0">
                                <v-rating
                                background-color="orange lighten-3"
                                color="orange"
                                size="16"
                                :value="item.rating"
                                ></v-rating>
                            </div>
                        </div>
                    </v-sheet>
                </v-col>
                <DetailProduct :idDetail="idDetail" :showDialog="showDialog" @close-dialog-detail="closeModel()" />
            </v-row>
        </v-container>
        </v-main>
    </div>
</template>
<script>
import axios from 'axios';
import DetailProduct from './DetailProduct.vue';
export default {
    data() {
        return {
            DATA: [],
            CATEGORY_LAPTOP: [],
            CATEGORY_PHONE: [],
            errors: [],
            id_phone: null,
            id_laptop: null,
            showDialog: false,
            idDetail: null,
        };
    },
    props: {
        selectedTab: {
            type: Number
        }
    },
    created() {
        this.getDataAllShop();
        this.getDataCategoryPhone();
        this.getDataCategoryLapTop();
    },
    watch: {
        selectedTab() {
            if (this.selectedTab == 0) {
                this.getDataAllShop();
            }
            else if (this.selectedTab == 1) {
                this.getDataTGDD();
            }
            else if (this.selectedTab == 2) {
                this.getDataSHOPEE();
            }
            else if (this.selectedTab == 3) {
                this.getDataLAZADA();
            }
            else if (this.selectedTab == 4) {
                this.getDatFPT();
            }
            console.log(this.selectedTab);
        }
    },
    methods: {
        async getDataAllShop() {
            let response = await axios.get("http://103.150.124.193:8000/api/api/allShowProduct?size=20&page=1");
            this.DATA = response.data.data.data.data;
            console.log(this.DATA);
        },
        async getDataTGDD() {
            let response = await axios.get("http://103.150.124.193:8000/api/api/allProduct?size=20&page=1&shop=1");
            this.DATA = response.data.data.product.data;
            console.log(this.DATA);
        },
        async getDataSHOPEE() {
            let response = await axios.get("http://103.150.124.193:8000/api/api/allProduct?size=20&page=1&shop=2");
            this.DATA = response.data.data.product.data;
            console.log(this.DATA);
        },
        async getDataLAZADA() {
            let response = await axios.get("http://103.150.124.193:8000/api/api/allProduct?size=20&page=1&shop=3");
            this.DATA = response.data.data.product.data;
            console.log(this.DATA);
        },
        async getDatFPT() {
            let response = await axios.get("http://103.150.124.193:8000/api/api/allProduct?size=20&page=1&shop=4");
            this.DATA = response.data.data.product.data;
            console.log(this.DATA);
        },
        async getDataCategoryPhone() {
            let response = await axios.get(`http://103.150.124.193:8000/api/api/LabelByCategory?id=1`);
            this.CATEGORY_PHONE = response.data.data;
        },
        async getDataCategoryLapTop() {
            let response = await axios.get(`http://103.150.124.193:8000/api/api/LabelByCategory?id=2`);
            this.CATEGORY_LAPTOP = response.data.data;
        },
        async setDataFilter(item) {
            // const params = {
            //     label: item.id,
            //     shop: 1
            // };

            console.log("  ", item);
            let response = await axios.get(`http://103.150.124.193:8000/api/api/allProduct?size=20&label=${item.id}&page=1&shop=1`);
            this.DATA = response.data.data.product.data;
        },
        async clickCallback(pageNum) {
            console.log(pageNum);
        },
        openDialog(item) {
            if(this.selectedTab === 0) {
                this.showDialog = true;
                this.idDetail = item.id;
            }
        },
        closeModel() {
            this.showDialog = false;
        }
    },
    components: { DetailProduct }
}
</script>
<style lang="scss">
    .product {
        text-align: center;
        .product-name {
            text-align: center; 
            color : black ; 
            font-size: 16px;
            margin: auto;
        }
        width: 250px;

        .product-price {
            font-size :20px ; 
            color: red ;
        }
        .product-rating {
            font-size :25px ; 
            color: yellowgreen;
            margin-bottom: 20px;
        }
        
    }
</style>