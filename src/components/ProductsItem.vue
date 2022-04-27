<template>

    <div class="product ">


        <div class="product__info">
            <div class="product__photo">
                <a href="#" class="product__link">
                    <img :src='product.primaryImageUrl'>
                </a>
            </div>

            <div class="product__description">
                <div class="product__status-container">
                    <div class="product__code">Код: {{productCode}}</div>
                    <span class="product__status">Наличие</span>
                </div>


                <h2 class="product__title">
                    <a href="#" class="product__link">{{product.title}}</a>
                </h2>

                <div class="product__tags">
                    <span class="product__tags-title">Могут понадобиться:</span>
                    <a href="#" class="product__tags-item" v-for="item in getAssocProducts" :key="item">{{item}},</a>

                </div>
            </div>
        </div>


        <div class="product__purchase">

            <div class="product__price">
                <div class="product__price-club">
                    <p class="product__price-club-text">По карте<br>клуба</p>
                    <p class="product__goldPrice">{{priceDiscount}} ₽</p>
                </div>

                <div class="product__price-default">
                    <p class="product__retailPrice">{{price}} ₽</p>
                </div>

                <div class="product__price-points">
                    Можно купить за 231,75 балла
                </div>
            </div>

            <div v-if="this.product.unit!=this.product.unitAlt">
                <div class="product__units">
                    <div class="product__units-item " :class="{'active':priceType=='perMeter' }"
                        @click="priceType='perMeter'">
                        За м. кв.
                    </div>
                    <div class="product__units-item " :class="{'active':priceType=='perPackage' }"
                        @click="priceType='perPackage'">
                        За упаковку
                    </div>
                </div>

                <div class="product__unit-info">
                    <div class="product__unit-i"><img src="../assets/images//i.png" alt="info"></div>
                    <div class="product__unit-desc">
                        <p>Продается упаковками:</p>
                        <p>1 упак. = {{this.product.unitRatioAlt.toFixed(2)}} м. кв. </p>
                    </div>
                </div>
            </div>

            <div class="order-wrapper">

                <div class="order-wrapper__count">
                    <input class="stepper-input" type="number" v-model="productAmount">
                    <div class="stepper">
                        <div class="stepper-arrow" @click="productAmountIncrease"><img
                                src="../assets/images//arrow-up.svg" alt="arrow-up"></div>
                        <div class="stepper-arrow" @click="productAmountDecrease"><img
                                src="../assets/images//arrow-down.svg" alt="arrow-up"></div>
                    </div>
                </div>

                <div class="order-wrapper__btn " data-url="/cart/" :data-product-id="this.product.productId">
                    <div class="basket-image"><img src="../assets/images//cart.png" alt="basket"></div>
                    <p class="order-wrapper__btn-text">В корзину</p>
                </div>

            </div>
        </div>
    </div>

</template>


<script>
    export default {
        props: {
            product: {
                type: Object,
                required: true
            },
        },
        data() {
            return {
                productCode: +this.product.code,
                productAmount: 1,
                priceType: 'perMeter'

            }
        },
        methods: {
            productAmountIncrease() {
                this.productAmount = this.productAmount + 1;
            },
            productAmountDecrease() {
                if (this.productAmount > 1) {
                    this.productAmount = this.productAmount - 1;
                }

            },

        },
        computed: {
            getAssocProducts() {
                return this.product.assocProducts.split(';')
            },
            price() {
                if (this.priceType == 'perMeter') {
                    return this.product.priceRetailAlt.toFixed(2)
                } else {
                    return this.product.priceRetail.toFixed(2)
                }
            },
            priceDiscount() {
                if (this.priceType == 'perMeter') {
                    return this.product.priceGoldAlt.toFixed(2)
                } else {
                    return this.product.priceGold.toFixed(2)
                }
            }
        }
    }
</script>

<style scoped lang="scss">
    .product {
        margin: 30px auto;
        border: 1px solid #e0e0e0;
        padding: 10px 18px;
        max-width: 990px;
        display: flex;
        justify-content: space-between;
        background-color: #fff;

        &__info {
            display: flex;
            margin-right: 25px;
        }

        &__photo {
            margin-right: 10px;
        }

        &__photo img {
            width: 220px;
            height: 220px;
        }

        &__status-container {
            display: flex;
            margin-bottom: 25px;
        }

        &__code {
            font-size: 12px;
            color: #666;
            margin-right: 20px;
        }

        &__status {
            font-size: 14px;
            color: #093;
            cursor: pointer;
            border-bottom: #093 1px dotted;
        }

        &__status:hover {
            border-bottom: none;
        }

        &__description {

            max-width: 505px;
        }

        &__title {
            font-size: 16px;
            font-weight: 700;
            padding-bottom: 19px;
        }

        &__title:hover {
            text-decoration: underline;
        }

        &__tags-item {
            color: #666;
            font-size: 13px;
        }

        &__tags-item:hover {
            text-decoration: underline;
        }

        &__tags-title {
            font-size: 13px;
            font-weight: 700;
            color: #545454
        }

        &__purchase {
            display: flex;
            flex-direction: column;
            align-items: end;
        }

        &__price-points {
            font-size: 12px;
            color: #999;
            padding-bottom: 5px;
        }

        &__units {
            display: flex;
            align-items: center;
            margin-bottom: 8px;
            justify-content: flex-end;
        }

        &__units-item {
            margin-right: 20px;
            color: #707070;
            font-size: 13px;
            border-bottom: #707070 1px dotted;
            cursor: pointer;
        }

        &__units-item:hover {
            border-bottom: none;
        }

        &__price-club {
            display: flex;
            align-items: end;
        }

        &__price-club-text {
            font-size: 14px;
            margin-right: 16px;
        }

        &__goldPrice {
            font-size: 25px;
            color: #000;
            font-weight: 700;
        }

        &__retailPrice {
            font-size: 25px;
            color: #a7a7a7;
            padding-left: 70px;
            padding-bottom: 15px;
        }

        &__unit-info {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
            width: 222px;
            border: 1px solid #ccc;
            padding: 5px 10px;
        }

        &__unit-i {
            margin-right: 10px;
        }

        &__unit-i img {
            width: 15px;
            height: 15px;
        }

        &__unit-desc {
            position: relative;
        }

        &__unit-desc:after,
        &__unit-desc:before {
            content: '';
            position: absolute;
            bottom: -12px;
            border-top: 8px solid;
            display: block;
            width: 0;
            height: 0;
        }

        &__unit-desc:after {
            border-color: #fff;
            left: -21px;
            border-left: 7px solid transparent !important;
            border-right: 7px solid transparent !important;

        }

        &__unit-desc:before {
            margin-bottom: -1px;
            border-color: #ccc;
            color: #ccc;
            left: -22px;
            border-left: 8px solid transparent !important;
            border-right: 8px solid transparent !important;
        }



    }

    .order-wrapper {
        display: flex;

        &__count {
            display: flex;
            margin-right: 10px;
            border: solid 1px #ccc;
        }

        &__btn {
            display: flex;
            background-color: #f90;
            width: 148px;
            align-items: center;
            padding: 10px;
            cursor: pointer;
        }

        &__btn:hover {
            background-color: #707070;
        }

        &__btn-text {
            margin-left: 15px;
            color: #fff;
            text-transform: uppercase;
        }
    }

    .stepper-input {
        width: 40px;
        padding: 0 3px;
        font-size: 13px;
        text-align: center;
        outline: none;
    }

    .stepper-arrow {
        border: solid 1px #ccc;
        cursor: pointer;
        padding: 0 5px;
        height: 50%;
    }

    .stepper-arrow:hover {
        background-color: #707070;
    }

    .stepper-arrow img {
        width: 10px;
        height: 10px;
    }

    .active {
        background-color: #000;
        color: #fff;
        padding: 3px;
        border-bottom: none;
    }

    .basket-image img {
        width: 20px;
        height: 20px;
        color: #fff
    }

    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
        -webkit-appearance: none;
    }
</style>