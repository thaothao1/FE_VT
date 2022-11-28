<template>
    <div class="list-product" style="background: teal; height: 100%;">
        <v-navigation-drawer app width="300">
            <v-sheet color="grey lighten-4" class="pa-4">
                <v-avatar class="mb-4" color="grey darken-1" size="64"></v-avatar>
                <div>john@vuetifyjs.com</div>
            </v-sheet>
            <strong style="font-size: 25px; color: darksalmon;">Category</strong>
            <v-list shaped>
                <v-list-item v-for="n in 5" :key="n" link>
                    <v-list-item-content>
                        <v-list-item-title>Item {{ n }}
                            <v-list class="pl-14" shaped>
                                <v-list-item v-for="n in 5" :key="n" link>
                                    <v-list-item-content>
                                        <v-list-item-title>Item {{ n }}</v-list-item-title>
                                    </v-list-item-content>
                                </v-list-item>
                            </v-list>
                        </v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>
        <v-main>
            <v-container fluid>
                <strong style="font-size: 25px; color: darksalmon;">All Product</strong>
                <v-row>
                <v-col
                    v-for="item in DATA.data.product.data"
                    :key="item"
                    cols="3"
                >
                    <v-card>
                        <div class="product" @click="showDialog = true">
                            <span class="image">
                                <v-col
                                cols="12"
                                >
                                <v-img :src="item.image"></v-img>
                                </v-col>
                            </span>
                            <span class="product-name">
                                {{item.name}}
                            </span><br />
                            <span class="product-price">
                                {{item.price}}
                            </span>
                        </div>
                    </v-card>
                </v-col>
            </v-row>
        </v-container>
        <DetailProduct :showDialog="showDialog" @close-dialog-detail="closeDialog()" />
        </v-main>
    </div>
</template>
<script>
import DetailProduct from "../components/DetailProduct.vue"
export default {
    components: {
        DetailProduct
    },
    data() {
        return {
            DATA:
            {
                "data": {

                    "shop": {
                        "changed_at": "2022-11-27T11:26:43.179219",
                        "name": "fpt",
                        "id": 1,
                        "created_at": "2022-11-27T11:26:43.179219",
                        "link": "https://fptshop.com.vn"
                    },
                    "product": {
                        "data": [
                            {
                                "created_at": "2022-11-27T11:27:23.208017",
                                "id": 1,
                                "link": "https://fptshop.com.vn/dien-thoai/iphone-13-pro-max",
                                "price": "33.990.000đ",
                                "rating": "5",
                                "shopId": 1,
                                "categoryId": 1,
                                "name": "iPhone 13 Pro Max 128GB",
                                "changed_at": "2022-11-27T11:27:23.208017",
                                "image": "https://images.fpt.shop/unsafe/fit-in/585x390/filters:quality(90):fill(white)/fptshop.com.vn/Uploads/Originals/2022/4/19/637859778843241685_iphone-13-pro-max-vang-1.jpg",
                                "priceSale": "27.990.000đ",
                                "labelId": 1
                            },
                            {
                                "created_at": "2022-11-27T11:27:42.783270",
                                "id": 2,
                                "link": "https://fptshop.com.vn/dien-thoai/samsung-galaxy-z-flip4-flex-mode-collection",
                                "price": "25.990.000đ",
                                "rating": "5",
                                "shopId": 1,
                                "categoryId": 1,
                                "name": "Samsung Galaxy Z Flip4 5G Flex Mode Collection",
                                "changed_at": "2022-11-27T11:27:42.783270",
                                "image": "https://images.fpt.shop/unsafe/fit-in/585x390/filters:quality(90):fill(white)/fptshop.com.vn/Uploads/Originals/2022/9/13/637986875399707328_samsung-galaxy-z-flip4-flex-mode-collection-1.jpg",
                                "priceSale": "20.990.000đ",
                                "labelId": 2
                            },
                            {
                                "created_at": "2022-11-27T11:27:50.606464",
                                "id": 3,
                                "link": "https://fptshop.com.vn/dien-thoai/xiaomi-redmi-10?dung-luong=128-gb",
                                "price": "4.290.000đ",
                                "rating": "5",
                                "shopId": 1,
                                "categoryId": 1,
                                "name": "Xiaomi Redmi 10 4GB-128GB 2021",
                                "changed_at": "2022-11-27T11:27:50.606464",
                                "image": "https://images.fpt.shop/unsafe/fit-in/585x390/filters:quality(90):fill(white)/fptshop.com.vn/Uploads/Originals/2021/8/19/637649622568371405_xiaomi-redmi-10-trang-1.jpg",
                                "priceSale": "3.590.000đ",
                                "labelId": 3
                            },
                            {
                                "created_at": "2022-11-27T11:27:50.630369",
                                "id": 4,
                                "link": "https://fptshop.com.vn/dien-thoai/iphone-11-64gb",
                                "price": "14.999.000đ",
                                "rating": "4",
                                "shopId": 1,
                                "categoryId": 1,
                                "name": "iPhone 11 64GB",
                                "changed_at": "2022-11-27T11:27:50.630369",
                                "image": "https://images.fpt.shop/unsafe/fit-in/585x390/filters:quality(90):fill(white)/fptshop.com.vn/Uploads/Originals/2019/9/11/637037652457717299_11-den.png",
                                "priceSale": "11.199.000đ",
                                "labelId": 1
                            },
                            {
                                "created_at": "2022-11-27T11:28:05.222252",
                                "id": 5,
                                "link": "https://fptshop.com.vn/dien-thoai/oppo-reno8",
                                "price": "8.990.000đ",
                                "rating": "5",
                                "shopId": 1,
                                "categoryId": 1,
                                "name": "OPPO Reno8 4G 8GB - 256GB",
                                "changed_at": "2022-11-27T11:28:05.222252",
                                "image": "https://images.fpt.shop/unsafe/fit-in/585x390/filters:quality(90):fill(white)/fptshop.com.vn/Uploads/Originals/2022/8/5/637952897277145731_oppo-reno8-4g-vang-5.jpg",
                                "priceSale": "8.690.000đ",
                                "labelId": 4
                            },
                            {
                                "created_at": "2022-11-27T11:28:13.840347",
                                "id": 6,
                                "link": "https://fptshop.com.vn/dien-thoai/vivo-y22s",
                                "price": "5.990.000đ",
                                "rating": "5",
                                "shopId": 1,
                                "categoryId": 1,
                                "name": "Vivo Y22s 8GB-128GB",
                                "changed_at": "2022-11-27T11:28:13.840347",
                                "image": "https://images.fpt.shop/unsafe/fit-in/585x390/filters:quality(90):fill(white)/fptshop.com.vn/Uploads/Originals/2022/9/9/637983398316214932_vivo-y22s-xanh-7.jpg",
                                "priceSale": "5.590.000đ",
                                "labelId": 5
                            },
                            {
                                "created_at": "2022-11-27T11:28:13.861224",
                                "id": 7,
                                "link": "https://fptshop.com.vn/dien-thoai/samsung-galaxy-s22-bora-purple",
                                "price": "21.990.000đ",
                                "rating": "5",
                                "shopId": 1,
                                "categoryId": 1,
                                "name": "Samsung Galaxy S22 Bora Purple",
                                "changed_at": "2022-11-27T11:28:13.861224",
                                "image": "https://images.fpt.shop/unsafe/fit-in/585x390/filters:quality(90):fill(white)/fptshop.com.vn/Uploads/Originals/2022/7/23/637941779749495327_samsung-galaxy-s22-bora-purple-1.jpg",
                                "priceSale": "12.990.000đ",
                                "labelId": 2
                            },
                            {
                                "created_at": "2022-11-27T11:28:20.812259",
                                "id": 8,
                                "link": "https://fptshop.com.vn/dien-thoai/xiaomi-redmi-note-11-4g",
                                "price": "4.990.000₫",
                                "rating": "5",
                                "shopId": 1,
                                "categoryId": 1,
                                "name": "Xiaomi Redmi Note 11 4GB - 128GB",
                                "changed_at": "2022-11-27T11:28:20.812259",
                                "image": "https://images.fpt.shop/unsafe/fit-in/585x390/filters:quality(90):fill(white)/fptshop.com.vn/Uploads/Originals/2022/1/27/637788717449466537_xiaomi-redmi-note-11-xam-1.jpg",
                                "priceSale": "4.790.000₫",
                                "labelId": 3
                            },
                            {
                                "created_at": "2022-11-27T11:28:29.220549",
                                "id": 9,
                                "link": "https://fptshop.com.vn/dien-thoai/iphone-12?dung-luong=64gb",
                                "price": "19.999.000đ",
                                "rating": "5",
                                "shopId": 1,
                                "categoryId": 1,
                                "name": "iPhone 12 64GB",
                                "changed_at": "2022-11-27T11:28:29.220549",
                                "image": "https://images.fpt.shop/unsafe/fit-in/585x390/filters:quality(90):fill(white)/fptshop.com.vn/Uploads/Originals/2020/10/14/637382632990998957_ip-12-xanhla-1.png",
                                "priceSale": "16.499.000đ",
                                "labelId": 1
                            },
                            {
                                "created_at": "2022-11-27T11:28:35.812879",
                                "id": 10,
                                "link": "https://fptshop.com.vn/dien-thoai/samsung-galaxy-a53",
                                "price": "10.990.000đ",
                                "rating": "5",
                                "shopId": 1,
                                "categoryId": 1,
                                "name": "Samsung Galaxy A53 5G 256GB",
                                "changed_at": "2022-11-27T11:28:35.812879",
                                "image": "https://images.fpt.shop/unsafe/fit-in/585x390/filters:quality(90):fill(white)/fptshop.com.vn/Uploads/Originals/2022/3/10/637825310288115049_samsung-galaxy-a53-den-4.jpg",
                                "priceSale": "9.990.000đ",
                                "labelId": 2
                            }
                        ],
                        "total": 235,
                        "count": 10
                    }
                }
            },
            showDialog: false,
            recent: [
                {
                    active: true,
                    avatar: 'https://cdn.vuetifyjs.com/images/lists/1.jpg',
                    title: 'Jason Oner',
                },
                {
                    active: true,
                    avatar: 'https://cdn.vuetifyjs.com/images/lists/2.jpg',
                    title: 'Mike Carlson',
                },
                {
                    avatar: 'https://cdn.vuetifyjs.com/images/lists/3.jpg',
                    title: 'Cindy Baker',
                },
                {
                    avatar: 'https://cdn.vuetifyjs.com/images/lists/4.jpg',
                    title: 'Ali Connors',
                },
            ],
            previous: [{
                title: 'Travis Howard',
                avatar: 'https://cdn.vuetifyjs.com/images/lists/5.jpg',
            }],
            LIST_CATEGORY: [
                { id: 1, name: "Iphone" },
                { id: 2, name: "Samsung" },
                { id: 3, name: "Oppo" },
                { id: 4, name: "Nokia" },
            ]
        }
    },
    created() {
        console.log(this.DATA.data.product.data);
    },
    methods: {
        closeDialog() {
            this.showDialog = false;
        }
    }
}
</script>
<style lang="scss">
    .product {
        .product-name {
            color: brown;
            font-size: 20px;
            text-align: center;
            margin: 5px;
        }
    }
</style>