<template>
    <div class="properties">
        <div class="container">

            <div class="row">
                <div class="col-md-4 col-sm-12" v-for="(property,i) in propertiesData" :key="property.id">
                    <div class="properties__col">

                        <img :src="require(`../assets/layouts/images/${property.image}.png`)" :alt="property.desc.sqft"
                            class="properties__img">

                        <h4 class="properties__h4">{{ ` ${property.title}` }}</h4>

                        <p class="properties__sub properties__subDecor">{{ property.subtitle }}</p>
                        <p class="properties__price">{{ property.price }} </p>
                        <div class="block">
                            <div class="block__item">
                                <Accordion 
                                :index="i" 
                                @onclickAccordion="isShowAccordionFunction"
                                :isShow="isShowAccordion ===i"
                                @oncloseAccordion="isShowAccordion=null"
                                >
                                    <template #title>
                                        
                                        Опис

                                    </template>
                                    <template #content>
                                        {{property.description}}
                                    </template>
                                </Accordion>

                            </div>
                        </div>




                        <div id="popup" class="popup">
                            <a href="#header" class="popup__area"></a>
                            <div class="popup__body">
                                <div class="popup_content">
                                    <a href="#header" class="popup__close">X</a>
                                    <div class="popup__title">Після оформлення замовлення очікуйте дзвінок
                                        оператора для підтвердження!</div>
                                    <div class="popup__text">
                                        <p class="text-center">Все буде Україна!</p>


                                        <div class="mb-3">
                                            <label for="formGroupExampleInput" class="form-label">ПІБ</label>
                                            <input type="text" class="form-control" id="formGroupExampleInput">
                                        </div>



                                        <div class="mb-3">
                                            <label for="formGroupExampleInput" class="form-label">Телефон</label>
                                            <input type="text" class="form-control" id="formGroupExampleInput">
                                        </div>

                                        <div class="mb-3">
                                            <label for="formGroupExampleInput" class="form-label">Місто</label>
                                            <input type="text" class="form-control" id="formGroupExampleInput">
                                        </div>

                                        <div class="mb-3">
                                            <label for="formGroupExampleInput" class="form-label">Номер відділення Нової
                                                пошти</label>
                                            <input type="text" class="form-control" id="formGroupExampleInput">
                                        </div>

                                        <div class="mb-3">
                                            <label for="formGroupExampleInput" class="form-label">Коментар (Не
                                                обов'язково)</label>
                                            <input type="text" class="form-control" id="formGroupExampleInput">
                                        </div>

                                        <button type="button" class="btn btn-legacy bg-danger">Відправити
                                            замовлення!</button>


                                    </div>
                                </div>
                            </div>
                        </div>

                        <div class="size2">
                            <a href="#popup" class="popup-link"><button type="button"
                                    class="btn btn-danger btn-xs btn-block">
                                    <div class="text-center">Оформити замовлення</div>
                                </button></a>
                        </div>


                        <div class="size">
                            <button type="button" class="btn btn-danger btn-xs btn-block">
                                <div class="text-center"><i class="fa fa-shopping-cart"></i>Додати в кошик
                                </div>
                            </button>
                        </div>










                    </div>
                </div>
            </div>
        </div>
    </div>

</template>


<script>
import Accordion from './Accordion.vue';
export default {
    data(){
    return{
        isShowAccordion: null,
    }
},

    props: {
        propertiesData: {
            type: Array,
            default: () => [],
        }
    },
    components: { Accordion },

    methods:{

    isShowAccordionFunction(index){
            this.isShowAccordion = index;
            console.log(index);
            console.log(this.isShowAccordion);
        }
    }
}



</script>

<style lang = "scss">
.size {
    padding-top: 5px;
}

.accordion-button {
    left: 15px;
}
</style>




