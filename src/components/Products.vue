<template>
    <div id="products_section">
         <div class="products-page ">
              <ProductsItem
              v-for="elem of productsList"
              :key='elem'
              :product='elem'
              />
            </div>
         </div>
</template>

<script>
import ProductsItem from '@/components/ProductsItem.vue';
import productsList from '../../products.json'

export default{
    components:{
        ProductsItem,
    },
    data(){
        return{
            productsList,
        }
    }


}

</script>

<style scoped lang='scss'>

</style>