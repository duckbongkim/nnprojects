<template>
<div>
    <div class="d-flex justify-content-center sub-container grid gap-3">
    <div>
        <!-- {{selectedProduct.product_image}} // url 바인딩 -->
        <img :src="selectedProduct.product_image" alt="">
    </div>

    <div class="product-price"> 
        <h1>{{selectedProduct.product_name}}</h1>
        <p>{{selectedProduct.product_name}}</p>
            <div>
                <p>배송예정일</p>
                <p>택배사</p>
                
            </div>
        <!-- <p><span>가격</span>{{selectedProduct.product_price}}</p> -->
        <p><span>가격</span>{{selectedProduct.product_price}}</p>
        <div>
            <button @click="minusQ">-</button>
            <input type="number" v-model="orderQuantity">
            <button @click="plusQ">+</button>
            <p><span>총 가격</span>{{selectedProduct.product_price * orderQuantity}}</p>
        </div>
        <div>
            <button @click="addLikes">찜</button>
            <button @click="addCarts">장바구니</button> 
            <button @click="dirOrder">바로구매</button> 
        </div>
        </div>
    </div>
        <br> 라인으로 섹션 나누기

    <div>
        <h1>추천상품</h1>
    </div>
    <div>
        <div>
            <연관제품1 대표이미지>
            <연관제품1 가격>
        </div>
        <div>
            <연관제품2 대표이미지>
            <연관제품2 가격>
        </div>
        <div>
            <연관제품3 대표이미지>
            <연관제품3 가격>
        </div>
        <div>
            <연관제품4 대표이미지>
            <연관제품4 가격>
        </div>
    </div>
    

    <!-- <hr class="product-line">


    <div>
        <ul class="product-info">
            <li>
                <a href="#">상품상세정보</a>
            </li> 
            <li><a href="#">배송안내</a></li> 
            <li><a href="#">교환 및 상품</a></li>
            <li><a href="#">상품후기</a></li> 
                                                
        </ul>
    </div>

    <hr> -->

<footer>
    <productInfoVue />
</footer>  

</div>
</template>


<script>
import axios from 'axios'; 
import productInfoVue from '../components/productInfo.vue';
export default{ 
    name:'',
    components:{
      productInfoVue
    },
    data(){
        return{
            selectedProduct : {
                product_name : '발렌타인20년산',
                product_price : 300000,
                product_description:'발렌타인 20년산',
                product_stock:20,
                product_image:'/emg.png',
            },
            orderQuantity : 1,
        };
    },
    setup(){},
    created(){},
    mounted(){
        this.getProducts()
    },
    unmounted(){},
    methods:{

        

        // Product 정보 가져오기
        async getProducts() {
            try {
                //도메인 요청, 돌아오는 response 잡기
                const response = await axios.get(`http://localhost:3000/products/${product_id}`);
                // product_id에 해당하는 제품 data object를 받아온다.
                this.selectedProduct = response.data ; 
            }catch(err) {
                console.error(err);
            }
        },

        plusQ() {
            this.orderQuantity += 1;
        },
        minusQ() {
            if(this.orderQuantity > 1){
                this.orderQuantity -= 1;
            }
        },

        async addLikes() {
            try {
                //1. selectedProduct.id 를 likes DB에 추가
                await axios.post(`http://localhost:3000/orders/like`, this.selectedProduct.id);
                    // 사용자 아이디는 뭐 어떻게 알더라? 세션에서 가져오나. ?
                    //await axios.post(`http://localhost:3000/orders/like`, this.selectedProduct.id, 세션정보)

                // 2. 찜에 추가되었습니다. 모달 띄우기

            } catch(err) {
                console.error(err);
            }
        },

        async addCarts() {
            try{
                await axios.post(`http://localhost:3000/mypage/carts/`,this.product.id);
            }catch(err){
                console.error(err)
            }
            // selectedProduct.id 와 orderQuantity 를 carts DB에 추가. 
            // "장바구니 갈래? y/n" 모달창 띄우기
        },

        async dirOrder() {
            // selectedProduct.id 와 orderQuantity 를 orders DB에 추가. 
            // 주문 페이지로 이동
        }        
    }
}

</script>

<style scoped>
/* .sub-container {
    display: flex;
    justify-content: center;
    gap:10%;
}
.text-box {
    margin: auto 0;
}

.text-box div {
    padding: 30px 0;
} */

.product-price {
    margin: auto 0;
}



</style>

