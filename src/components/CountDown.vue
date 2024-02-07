<template>
    <div class="count-down">
        <h1>im testing props: <span>{{ myProps }}</span></h1>
        <h2>Countdown</h2>
        <p :class="{ low: isLow }">{{ targetTimeFormatted ? targetTimeFormatted : targetTime }}</p>
    </div>
</template>

<script>

import alarmSoundFile from '@/assets/audio/done.wav'

export default {
    props: ['myProps', 'targetTime'],
    data() {
        return {
            myText: this.myProps,
            currentTime: Date.now(),
            isLow: false,
            alarmSound: new Audio(alarmSoundFile),
        }
    },
    mounted() {
        this.intervalId = setInterval(() => {
            this.currentTime = Date.now()
            const countdownTime = this.targetTime - this.currentTime
            this.isLow = countdownTime <= 11000
        }, 1000)
    },
    beforeUnmount() {
        clearInterval(this.intervalId)
    },
    methods: {
        playAlarm() {
            if (this.alarmSound) {
                this.alarmSound.play()
            }
        },
    },
    computed: {
        targetTimeFormatted() {
            const countdownTime = this.targetTime - this.currentTime
            if (countdownTime <= 0) {
                clearInterval(this.intervalId)
                this.playAlarm()
                this.$emit('due')
                return '00:00'
            }
            const minutes = Math.floor((countdownTime % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((countdownTime % (1000 * 60)) / 1000);
            return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
        }
    }
}
</script>

<style scoped>
div {
    display: flex;
    flex-flow: column;
    align-items: center;

    margin-top: 20px;
    border: 2px solid red;
}

.low {
    color: red;
}
</style>