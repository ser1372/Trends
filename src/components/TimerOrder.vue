<template>
    <div class="row">
        <div class="timer">
            <div class="timer__items">
                <div class="timer__item timer__hours">{{ timer.hours }}</div>
                <div class="timer__item timer__minutes">{{ timer.mins }}</div>
                <div class="timer__item timer__seconds">{{ timer.secs }}</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            timer: {
                hours: null,
                mins: null,
                secs: null,
            },
        }
    },
    mounted(){
        const self = this;
        let currentDate = new Date();
        setInterval(function () {
            
            let futureDate = new Date(currentDate.getTime() + 10*60000);
            let t = futureDate - currentDate ;
            self.timer.hours = ('0' + Math.floor((t % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))).slice(-2);
            self.timer.mins = ('0' + Math.floor((t % (1000 * 60 * 60)) / (1000 * 60))).slice(-2);
            self.timer.secs = ('0' + Math.floor((t % (1000 * 60)) / 1000)).slice(-2);

            console.log(currentDate);
            console.log(futureDate);
            console.log(t);
            
        }, 1000);
    },
}
</script>