<template>
    <section>
        <div class="container">
            <div class="row">
                <h1 class="order-page__title">{{ textThanksPageTitle }}</h1>

                <div class="order-page__text">
                    <p>{{ textThanksPageDescription }}</p>
                </div>

                <div class="order-page__text" v-if="orderId">
                    {{ textThanksPageOrderId }} {{ orderId }}
                </div>

            </div>
            <loader v-if="isLoading"></loader>
            <div v-if="!isLoading">
                <div class="special" v-if="activeSpecialOffer">
                    <div class="row">
                        <div class="timer">
                            <div class="timer__text">{{ textThanksPageSpecials }}</div>
                            <div class="timer__items">
                                <div class="timer__item timer__hours">{{ timer.hours }}</div>
                                <div class="timer__item timer__minutes">{{ timer.mins }}</div>
                                <div class="timer__item timer__seconds">{{ timer.secs }}</div>
                            </div>
                        </div>
                    </div>
                    <div class="row">
                        <div class="product-list">
                            <div class="col-6 col-md-3 card__product"  v-for="(product,i) in products" :key="i">
                                <div class="card__image">
                                    <a class="text-decoration-none" :href="productRoute + '/' + product.id">
                                        <img :src="'/storage/products/350/' + product.preview" :alt="product.h1.ru"
                                             v-if="lang === 'ru'">
                                        <img :src="'/storage/products/350/' + product.preview" :alt="product.h1.ua"
                                             v-if="lang === 'ua'">
                                    </a>
                                </div>
                                <div class="card__body">
                                    <h5 class="card__label" v-if="lang === 'ru'">{{ product.h1.ru }}</h5>
                                    <h5 class="card__label" v-if="lang === 'ua'">{{ product.h1.ua }}</h5>
                                    <div class="card__price">
                                        <div v-if="!product.discount_price"
                                             class="card__price-without-discount">{{ product.price }} грн.
                                        </div>

                                        <div v-if="product.discount_price" class="card__discount_price">
                                            <div class="card__old-price">{{ product.price }} грн.</div>
                                            <div class="card__actual-price">{{ product.discount_price }} грн.</div>
                                        </div>
                                    </div>
                                    <span class="card__button"
                                          @click="addItemToOrder(product.id,product.discount_price)">
                                    {{ textThanksPageAddItem }}
                                </span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div v-else class="order-page__text my-5">
                    <p>{{ textThanksPageSpecialsEnds }}</p>
                </div>
            </div>
            <response-modal :is-active-response-modal="response.isActive"
                            :response="response"
                            @sendForm="response.icon !== 'success' ? isActiveModal = true : isActiveModal = false;"
                            text-send="Зрозуміло"
            ></response-modal>
        </div>
    </section>
</template>

<script>
export default {
    props: {
        lang: String,
        productRoute: String,
        textGoToProductCard: String,
        textThanksPageTitle: String,
        textThanksPageDescription: String,
        textThanksPageOrderId: String,
        textThanksPageSpecialsEnds: String,
        textThanksPageSpecials: String,
        textThanksPageAddItemToOrder: String,
        textThanksPageAddItemToOrderError: String,
        textThanksPageAddItem: String,
    },
    data() {
        return {
            orderId: null,
            isLoading: true,
            products: [],
            activeSpecialOffer: false,
            timer: {
                hours: null,
                mins: null,
                secs: null,
            },
            response: {
                isActive: false,
                icon: null,
                text: null,
                title: null
            }
        }
    },
    mounted() {
        this.orderId = new URLSearchParams(window.location.search).get('order');
        axios.get('/api/v1/order/special/' + this.orderId)
            .then(({data}) => {
                if (data.result) {
                    const self = this;
                    setInterval(function () {
                        let t = new Date(data.result.end_time).getTime() - new Date().getTime();
                        if (t >= 0) {
                            self.timer.hours = ('0' + Math.floor((t % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))).slice(-2);
                            self.timer.mins = ('0' + Math.floor((t % (1000 * 60 * 60)) / (1000 * 60))).slice(-2);
                            self.timer.secs = ('0' + Math.floor((t % (1000 * 60)) / 1000)).slice(-2);
                            self.activeSpecialOffer = true;
                            self.products = data.result.products;
                            self.isLoading = false;
                        } else {
                            self.activeSpecialOffer = false;
                            self.isLoading = false;
                        }
                    }, 1000);
                } else {
                    this.isLoading = false;
                    this.activeSpecialOffer = false;
                }
            })
    },
    methods: {
        clearResponse() {
            this.response = {
                isActive: false,
                icon: null,
                text: null,
                title: null
            }
        },
        addItemToOrder(id, price) {
            this.clearResponse();
            axios.post('/api/v1/order/add-item/' + this.orderId, {
                'id': id,
                'price': price,
            })
                .then(() => this.response = {
                    isActive: true,
                    icon: 'success',
                    title: 'Додано!',
                    text: 'Товар успішно додано до вашого замовлення',
                })
                .catch((response) => {
                    console.log(response);
                    this.response = {
                        isActive: true,
                        icon: 'error',
                        title: 'Виникла помилка',
                        text: 'Зверніться до адміністратора',
                    }
                })
        }
    }
}
</script>