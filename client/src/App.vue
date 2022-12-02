<template>
  <v-app id="inspire">
    <v-app-bar app class="navig-app">
      <v-toolbar-title class="title-app">Web Compass</v-toolbar-title>
      <v-tabs   
      v-model="selectedTab"
      background-color="primary"
      dark >
        <v-tab v-for="item in SHOP"
        :key="item.id">
        {{ item.name}}
      </v-tab>
      </v-tabs>
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
    </v-app-bar>
    <v-navigation-drawer
      v-model="drawer"
      fixed
      temporary
    >
    </v-navigation-drawer>
    <v-carousel :show-arrows="false" class="slider" cycle>
      <v-carousel-item
        v-for="(item,i) in items"
        :key="i"
        :src="item.src"
      ></v-carousel-item>
    </v-carousel>
    <index :selectedTab="selectedTab" />
    <v-main>
      <v-footer
        dark
        padless
      >
        <v-card
          class="flex"
          flat
          tile
        >
          <v-card-title class="teal">
            <strong class="subheading">Get connected with us on social networks!</strong>
  
            <v-spacer></v-spacer>
  
            <v-btn
              v-for="icon in icons"
              :key="icon"
              class="mx-4"
              dark
              icon
            >
              <v-icon size="24px">
                {{ icon }}
              </v-icon>
            </v-btn>
          </v-card-title>
  
          <v-card-text class="py-2 white--text text-center">
            {{ new Date().getFullYear() }} — <strong>Vuetify</strong>
          </v-card-text>
        </v-card>
      </v-footer>
    </v-main>
  </v-app>
</template>

<script>
import index from '@/components/index.vue'
  export default {
    data: () => ({ 
      drawer: null,
      selectedTab: 0,
      icons: [
        'mdi-facebook',
        'mdi-twitter',
        'mdi-linkedin',
        'mdi-instagram',
      ],
      items: [
          {
            src: 'https://cdnmedia.baotintuc.vn/Upload/cVJiASFv9S8nriO7eNwA/files/2021/01/18-1/Lazada%20(2).png',
          },
          {
            src: 'https://intphcm.com/data/upload/mau-banner-shopee.jpg',
          },
          {
            src: 'https://genk.mediacdn.vn/139269124445442048/2022/4/28/photo-1-1651119706627901243837-1651129623433-16511296237011271681052.jpg',
          },
          {
            src: 'https://cdn.tgdd.vn/Files/2019/10/06/1205627/hotsale1010_800x450.jpg',
          },
        ],
      SHOP: [
        {id: '0', name: 'So sánh giá'},
        {id: '1', name: 'Thế giới di động' },
        {id: '2', name: 'Shopee' },
        {id: '3', name: 'Lazada' },
        {id: '4', name: 'FPT Shop' },

      ]
    }),
    components: {
      index
    },
  }
</script>
<style lang="scss">
#inspire {
  .navig-app {
    background: rgb(211, 120, 16);
    .title-app {
      width: 200px;
      color: rgb(53, 14, 161);
    }
  }
  .slider {
    width: 70%;
    margin-top: 100px;
    margin-top: 100px;
    margin-bottom: 20px;
    border-radius: 20px;
    margin-left: 380px;
  }
  .container-content {
    width: 90%;
    border-radius: 10px;
    margin: auto;
  }
}

</style>