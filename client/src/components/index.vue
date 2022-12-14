<template>
    <div class="list-product" style="height: 95%;">
        <Loading v-if="isLoading" />
        <v-navigation-drawer app width="250">
            <v-sheet color="grey lighten-4" class="pa-4">
                <v-avatar class="mb-4" color="grey darken-1" size="64"><v-img src="@/assets/log-web-1.png"
                        alt=""></v-img></v-avatar>
                <div>BestPrice</div>
            </v-sheet>
            <v-list shaped :disabled="check_labels">
                <v-card class="mx-auto" max-width="250" tile>
                    <v-list>
                        <v-col>
                            <v-icon>mdi-cellphone</v-icon>
                            <span class="name-category">{{ CATEGORY_PHONE.name }}</span>
                        </v-col>
                        <v-list-item-group v-model="selectedItem" color="primary">
                            <v-list-item v-for="(item, index) in CATEGORY_PHONE.label" :key="index">
                                <v-list-item-icon>
                                    <v-icon v-text="item.icon"></v-icon>
                                </v-list-item-icon>
                                <v-list-item-content>
                                    <v-list-item-title class="name-product" @click="setDataFilter(item)">{{ item.name
                                    }}</v-list-item-title>
                                </v-list-item-content>
                            </v-list-item>
                        </v-list-item-group>
                    </v-list>
                </v-card>
                <v-card class="mx-auto" max-width="250" tile>
                    <v-list>
                        <v-col>
                            <v-icon>mdi-laptop</v-icon>
                            <span class="name-category">{{ CATEGORY_LAPTOP.name }}</span>
                        </v-col>
                        <v-list-item-group v-model="selectedItem" color="primary">
                            <v-list-item v-for="(item, index) in CATEGORY_LAPTOP.label" :key="index">
                                <v-list-item-icon>
                                    <v-icon v-text="item.icon"></v-icon>
                                </v-list-item-icon>
                                <v-list-item-content>
                                    <v-list-item-title @click="setDataFilter(item)">{{ item.name }}</v-list-item-title>
                                </v-list-item-content>
                            </v-list-item>
                        </v-list-item-group>
                    </v-list>
                </v-card>
            </v-list>
        </v-navigation-drawer>
        <div v-if="(DATA.length == 0)" style="margin: auto; text-align: center; color: red; font-size: 30px; ">
            No Data!
        </div>
        <v-row>
            <v-col v-for="(item, index) in DATA" :key="index" cols="3" @click="openDialog(item)">
                <v-sheet color="white" elevation="1" height="320px" width="280px" class="mt-6 ml-2">
                    <div class="product">
                        <span class="image">
                            <v-col cols="12">
                                <v-img :src="item.image" max-height="200"></v-img>
                            </v-col>
                        </span>
                        <v-toolbar-title class="product-name">
                            <a :href=item.link>
                                {{ item.name }}</a>
                        </v-toolbar-title>
                        <span :class="{khac_shop: selectedTab, shop: !selectedTab}">
                            Giá: {{ item.price }}
                        </span><br />
                        <span class="product-price-sale" v-if="selectedTab !== 0">
                            Sale: {{ item.priceSale }}
                        </span><br />
                        <span  v-if="selectedTab == 0">View:{{item.view}}</span>
                        <div class="text-center" v-if="selectedTab !== 0">
                            <v-rating background-color="orange lighten-3" color="orange" size="16"
                                v-if="(Object.keys(item) != 0)"
                                :value="item.rating">
                            </v-rating>
                        </div>
                    </div>
                </v-sheet>
            </v-col>
            <DetailProduct :DATASS="DATA" :idDetail="idDetail" :showDialog="showDialog" @close-dialog-detail="closeModel()" />
        </v-row>
        <div class="mt-10 mb-4">
            <Pagination v-if="Object.keys(DATA) != 0" :current="paramsPagination?.current" :total="paramsPagination?.total"
                @pageUpdate="pageUpdate" />
        </div>
    </div>
</template>
<script>
import axios from 'axios';
import DetailProduct from './DetailProduct.vue';
import Pagination from './Pagination.vue';
import Loading from './Loading.vue'
export default {
    data() {
        return {
            paramsPagination: {
                current: 1,
                total: 1
            },
            DATA: [],
            CATEGORY_LAPTOP: [],
            CATEGORY_PHONE: [],
            errors: [],
            id_phone: null,
            id_laptop: null,
            showDialog: false,
            idDetail: null,
            selectedItem: null,
            id_shop: null,
            isLoading: null,
            check_labels: false,
        };
    },
    props: {
        selectedTab: {
            type: Number
        },
        search_name: {
            type: String
        }
    },
    created() {
        this.getDataAllShop();
        this.getDataCategoryPhone();
        this.getDataCategoryLapTop();
    },
    watch: {
        selectedTab() {
            this.isLoading = true;
            if (this.selectedTab == 0) {
                this.getDataAllShop();
                this.id_shop = null;
                this.check_labels = false;
            }
            else if (this.selectedTab == 1) {
                this.getDataTGDD();
                this.id_shop = 3;
                this.check_labels = false;
            }
            else if (this.selectedTab == 2) {
                this.getDataSHOPEE();
                this.id_shop = 1;
                this.check_labels = true;
            }
            else if (this.selectedTab == 3) {
                this.getDataLAZADA();
                this.id_shop = 2;
                this.check_labels = true;
            }
            else if (this.selectedTab == 4) {
                this.getDatFPT();
                this.id_shop = 4;
                this.check_labels = false;
            }
        },
        search_name() {
            if (this.search_name) {
                this.searchName();
            }
            else {
                this.getDataAllShop();
                this.id_shop = null;
            }
        }
    },
    methods: {
        async getDataAllShop() {
            let response = await axios.get(`http://103.150.124.193:8000/api/api/allShowProduct?size=20&page=${this.paramsPagination.current}`);
            this.DATA = response.data.data.data.data;
            this.paramsPagination.total = response.data.data.data.total / response.data.data.data.count;
            this.paramsPagination.total = Math.round(this.paramsPagination.total);
            this.isLoading = false;
        },
        async getDataTGDD() {
            let response = await axios.get(`http://103.150.124.193:8000/api/api/allProduct?size=20&page=${this.paramsPagination.current}&shop=3`);
            this.DATA = response.data.data.product.data;
            this.paramsPagination.total = response.data.data.product.total / response.data.data.product.count;
            this.paramsPagination.total = Math.round(this.paramsPagination.total);
            this.isLoading = false;
            
        },
        async getDataSHOPEE() {
            let response = await axios.get(`http://103.150.124.193:8000/api/api/allProduct?size=20&page=${this.paramsPagination.current}&shop=1`);
            this.DATA = response.data.data.product.data;
            this.paramsPagination.total = response.data.data.product.total / response.data.data.product.count;
            this.paramsPagination.total = Math.round(this.paramsPagination.total);
            this.isLoading = false;
        },
        async getDataLAZADA() {
            let response = await axios.get(`http://103.150.124.193:8000/api/api/allProduct?size=20&page=${this.paramsPagination.current}&shop=2`);
            this.DATA = response.data.data.product.data;
            this.paramsPagination.total = response.data.data.product.total / response.data.data.product.count;
            this.paramsPagination.total = Math.round(this.paramsPagination.total);
            this.isLoading = false;
        },
        async getDatFPT() {
            let response = await axios.get(`http://103.150.124.193:8000/api/api/allProduct?size=20&page=${this.paramsPagination.current}&shop=4`);
            this.DATA = response.data.data.product.data;
            this.paramsPagination.total = response.data.data.product.total / response.data.data.product.count;
            this.paramsPagination.total = Math.round(this.paramsPagination.total);
            this.isLoading = false;
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
            this.isLoading = true;
            if (this.selectedTab != 0) {
                let response = await axios.get(`http://103.150.124.193:8000/api/api/allProduct?size=20&label=${item.id}&page=1&shop=${this.id_shop}`);
                if(response.status == 200) {
                    this.DATA = response.data.data.product.data;
                    this.isLoading = false;
                }
            }
            else {
                let response = await axios.get(`http://103.150.124.193:8000/api/api/allShowProduct?size=10&label=${item.id}&page=1`);
                if(response.status == 200) {
                    this.DATA = response.data.data.data.data;
                    this.isLoading = false;
                }
            }
        },
        async searchName() {
            this.isLoading = true;
            let response = await axios.get(`http://103.150.124.193:8000/api/api/search?query=${this.search_name}`);
            if(!response.hasError) {
                this.DATA = response.data.data;
                this.isLoading = false;
            }
        },
        openDialog(item) {
            if (this.selectedTab === 0) {
                this.showDialog = true;
                this.idDetail = item.id;
            }
        },
        pageUpdate(n) {
            this.paramsPagination.current = n;
            if (this.selectedTab == 0) {
                this.getDataAllShop(n);
                this.id_shop = null;
            }
            else if (this.selectedTab == 1) {
                this.getDataTGDD(n);
                this.id_shop = 3;
            }
            else if (this.selectedTab == 2) {
                this.getDataSHOPEE(n);
                this.id_shop = 1;
            }
            else if (this.selectedTab == 3) {
                this.getDataLAZADA(n);
                this.id_shop = 2;
            }
            else if (this.selectedTab == 4) {
                this.getDatFPT(n);
                this.id_shop = 4;
            }
        },
        closeModel() {
            this.showDialog = false;
        }
    },
    components: { DetailProduct, Pagination, Loading }
}
</script>
<style lang="scss">
.product {
    text-align: center;

    .product-name {
        text-align: center;
        color: black;
        font-size: 16px;
        margin: auto;
    }

    .khac_shop {
        font-size: 16px;
        text-decoration: line-through;
    }
    .shop {
        font-size: 20px;
        color: red;
    }
    .product-price-sale {
        font-size: 20px;
        color: red;
    }

    .product-rating {
        font-size: 25px;
        color: yellowgreen;
        margin-bottom: 20px;
    }
}

.name-category {
    color: black;
    font-weight: 600;
    font-size: 16px;
    padding-left: 10px;
}
</style>