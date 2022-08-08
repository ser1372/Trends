
<template>

    <div class="accordion">
        <div class="accordion-item">
            <h2 class="accordion-header" @click="test(index)">
                <button class="accordion-button" type="button">
                    <slot name="title"></slot>
                </button>
            </h2>
            <div class="accordion-collapse collapse" :class="{ 'show': isShow }">

                <div class="accordion-body">
                    <slot name="content"></slot>
                </div>
            </div>
        </div>
    </div>

</template>
<script>

export default {
    props: [
        'isShow',
        'index',
    ],
    emit: [
        'onclickAccordion',
        'oncloseAccordion',
    ],

    data() {
        return {
            activeIndex: null,
        }
    },

    methods: {
        test(i){
            this.$emit('onclickAccordion', i);
            this.activeIndex = i;
            if(this.activeIndex === i){
                this.$emit('oncloseAccordion');
            }
            else{
                this.$emit('onclickAccordion', i);
            }
        }
    },

    created(){
        /*console.log(this.activeIndex);
        console.log(this.index);*/
    }

    



}
</script>