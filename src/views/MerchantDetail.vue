<template>
    <div class="detail" :style="{ top: (  this.$store.state.headerH + 46 + 44) + 'px', height: innerH - (this.$store.state.headerH + 46 + 44) + 'px'}">
        <SideMenu />
        <div class="shop-information py-3" v-for="shop in shops" :key="shop.uuid">
            <p>店家名稱： {{ shop.name }} </p>
            <p>店家電話： {{ shop.telephone }} </p>
            <p>店家地址： {{ shop.address }} </p>
            <a :href="shop.OEXPOURL" target="_blank" v-if="shop.qrcode && shop.OEXPOURL.includes('oexpo')" class="gotoOexpo text-decoration-none border-0 rounded-pill py-2 px-3">進入店家攤位</a>
            <!-- <button v-if="shop.qrcode && shop.OEXPOURL.includes('oexpo')" class="gotoOexpo border-0 rounded-pill py-2 px-3" @click="oexpoBtn(shop)">
                進入店家攤位
            </button> -->
            <div v-if="!shop.qrcode" class="text-white increase">
            目前尚未新增廠商攤位哦!
            </div>
        </div>
    </div>
</template>

<script>
import SideMenu from '@/components/SideMenu.vue'
export default {
  data () {
    return {
      innerH: '',
      stores: []
    }
  },
  components: {
    SideMenu
  },
  computed: {
    shops () {
      return this.stores.filter(item => {
        if (item.uuid === this.$route.query.merchantUUID) {
          return item
        }
      })
    }
  },
  mounted () {
    this.innerH = window.innerHeight
    // console.log(window.innerHeight)
    this.stores = this.$store.getters['storesData/storesData']
  }
}

</script>

<style lang="scss" scoped>
    .detail{
        position: relative;
        width: 100%;
        overflow: hidden;
    }
    .shop-information{
        width: 90%;
        margin: auto;
        p{
            color: #81CFF7;
        }
        .gotoOexpo{
            color: #C99000;
            background: linear-gradient(180deg, #FFF4B3 0%, #DED07B 50.21%, #FFF4B3 100%);
            font-size: 16px;
            font-weight: 600;
        }
    }
</style>
