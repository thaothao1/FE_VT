<template>
    <div class="list-product" style="background: teal; height: 100%;">
        <v-navigation-drawer app width="300">
            <v-sheet color="grey lighten-4" class="pa-4">
                <v-avatar class="mb-4" color="grey darken-1" size="64"></v-avatar>
                <div>Web Compass</div>
            </v-sheet>
            <v-list shaped>
                <strong style="font-size: 25px; color: darksalmon;">{{CATEGORY_PHONE.name}}</strong>
                <v-list class="pl-14" shaped>
                    <v-list-item v-for="(item, index) in CATEGORY_PHONE.label" :key="index">
                        <v-list-item-content>
                            <v-list-item-title @click="setDataFilter(item)" style=" font-family:Impact Charcoal; font-size: 15px;text-transform: uppercase "><a style="color: black">{{ item.name }}</a></v-list-item-title>
                        </v-list-item-content>
                    </v-list-item>
                </v-list>
                <strong style="font-size: 25px; color: darksalmon;">{{CATEGORY_LAPTOP.name}}</strong>
                <v-list class="pl-14" shaped>
                    <v-list-item v-for="(item, index) in CATEGORY_LAPTOP.label" :key="index">
                        <v-list-item-content>
                            <v-list-item-title @click="setDataFilter(item)" style=" font-family:Impact Charcoal; font-size: 15px;text-transform: uppercase "><a style="color: black">{{ item.name }}</a></v-list-item-title>
                        </v-list-item-content>
                    </v-list-item>
                </v-list>
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
                >
                    <v-card>
                        <div class="product">
                            <span class="image">
                                <v-col
                                cols="12"
                                >
                                <v-img :src="item.image"></v-img>
                                </v-col>
                            </span>
                            <span class="product-name" style=""><a :href=item.link style="color: black;">
                                {{item.name}}</a>
                            </span><br />
                            <span class="product-price"><img src="../assets/images-icon-money.png" style="height: 20px ;  margin-left: 12px;"/>
                                {{item.price}}
                            </span><br/>
                            <span class="product-rating"><img src="../assets/images-star.png" style="height: 50px ;  margin-left: 12px;"/>
                                {{item.rating}}
                            </span>
                        </div>
                    </v-card>
                </v-col>
            </v-row>
        </v-container>
        <!-- <DetailProduct :showDialog="showDialog" @close-dialog-detail="created()" /> -->
        </v-main>
    </div>
        <!-- <paginate
            :page-count="10"
            :page-range="3"
            :margin-pages="2"
            :click-handler="clickCallback"
            :prev-text="'Prev'"
            :next-text="'Next'"
            :container-class="'pagination'"
            :page-class="'page-item'">
    </paginate> -->
</template>
<script>
import axios from 'axios';
export default {
    data() {
        return{
            DATA: [],
            CATEGORY_LAPTOP: [],
            CATEGORY_PHONE: [],
            errors: [],
            id_phone: null,
            id_laptop: null
        }
    },
    created() {
        this.getDataProduct();
        this.getDataCategoryPhone();
        this.getDataCategoryLapTop();
    },
    methods: {
        async getDataProduct() {
            let response = await  axios.get(`http://localhost:8000/api/api/randomProducts`);
            this.DATA = response.data.data;
        },
        async getDataCategoryPhone() {
            let response = await  axios.get(`http://localhost:8000/api/api/LabelByCategory?id=1`);
            this.CATEGORY_PHONE = response.data.data;
        },
        async getDataCategoryLapTop() {
            let response = await  axios.get(`http://localhost:8000/api/api/LabelByCategory?id=2`);
            this.CATEGORY_LAPTOP = response.data.data;
        },
        async setDataFilter(item) {
            // const params = {
            //     label: item.id,
            //     shop: 1
            // };
            console.log("  ", item.name);
            let response = await axios.get(`http://127.0.0.1:8000/api/api/allProduct?size=20&label=${item.id}&page=1&shop=1`);
            this.DATA = response.data.data.product.data;
            console.log("aloooooooo", this.DATA ,item)
        },
        async clickCallback (pageNum){
            console.log(pageNum)
            }
    }
}
</script>
<style lang="scss">
    .product {
        .product-name {
            text-align: center;
            margin-left: 12px; 
            margin-right: 5px; 
            color : black ; 
            font-size: 22px;
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