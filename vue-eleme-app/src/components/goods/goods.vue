<template >
  <div>
    <div class="goods">
      <!-- vue 少dom操作 this.refs.menuWrapper -->
      <div class="memu-wrapper" ref="menuWrapper">
      </div>   
      <div class="food-wrapper" ref="foodsWrapper"></div> 
      <shopcart>
      </shopcart>
    </div>
    <food></food>
  </div>
</template>
<script>
import food from '@/components/food/food'
import shopcart from '@/components/shopcart/shopcart'
const response = require('../../common/data/goods.json')
export default {
  mounted () {
    console.log(this.$refs.memuWrapper)
  },
  components: {
    food,
    shopcart
  }
}
</script>

<style lang="css">
</style>