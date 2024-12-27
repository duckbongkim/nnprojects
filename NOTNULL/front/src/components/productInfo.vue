<template>
<div>
    
    <hr class="product-line">


    <div>
        <ul class="info-list">
            <li @click="currentComponent = 'infoDetail'">
                <a>상품상세정보</a>
            </li> 
            <li  @click="currentComponent = 'infoDelivery'">
                <a>배송안내</a>
            </li> 
            <li @click="currentComponent = 'infoExchange'">
                <a>교환 및 상품</a>
            </li>
            <li @click="currentComponent = 'infoReview'">
                <a>상품후기</a>
            </li> 
                                                
        </ul>
    </div>

    <hr>
     <component :is="currentComponent" />
</div>
</template>
<script>
import infoDetail from './infoDetail.vue';
import infoDelivery from './infoDelivery.vue';
import infoExchange from './infoExchange.vue';
import infoReview from './infoReview.vue';

export default{ 
    name:'',
    components:{
        infoDelivery,
        infoDetail,
        infoExchange,
        infoReview
    },
    data(){
        return{
            currentComponent: 'infoDetail'
        };
    },
    setup(){},
    created(){},
    mounted(){},
    unmounted(){},
    methods:{}
}
</script>

<style scoped>
 .product-line {
    height: 5px;
 }

 .info-list {
    list-style: none;
    display: flex;
    gap: 10%;
    justify-content: center;
 }

 .info-list li {
    cursor: pointer;
 }
</style>