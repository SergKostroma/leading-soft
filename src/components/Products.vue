<template>
    <div id="products_section">
         <div class="products-page ">
              <ProductsItem
              v-for="elem of ProductsList"
              :key='elem'
              :product='elem'
              />
            </div>
         </div>
</template>

<script>
import ProductsItem from '@/components/ProductsItem.vue';
import ProductsList from '../../products.json'

export default{
    components:{
        ProductsItem,
    },
    data(){
        return{
            ProductsList,
        }
    }


}

</script>

<style scoped lang='scss'>

</style>