<template>
    <div @click="toggleBgc" class="time-container" :class="{ dark: isDark }">
        <p class="icon">{{ currentSeasonIcon }}</p>
        <p>{{ formattedCurrentTime }}</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isDark: false,
            currentTime: new Date(),
        }
    },
    created() {
        this.interval = setInterval(() => {
            this.currentTime = new Date()
        }, 1000)
    },
    beforeUnmount() {
        clearInterval(this.interval)
    },
    computed: {
        formattedCurrentTime() {
            return this.currentTime.toLocaleTimeString()
        },
        currentSeasonIcon() {
            const month = this.currentTime.getMonth()
            if (month >= 2 && month <= 4) {
                return '🌸'
            } else if (month >= 5 && month <= 7) {
                return '☀️'
            } else if (month >= 8 && month <= 10) {
                return '🍂'
            } else {
                return '❄️'
            }
        }
    },
    methods: {
        toggleBgc() {
            this.isDark = !this.isDark
        }
    }
}
</script>

<style scoped>
div {
    display: flex;
    flex-flow: column;
    align-items: center;
    border: 2px solid blue;
}

.icon {
    font-size: 2rem;
}

.dark {
    background-color: darkgray;

    p {
        color: blue;
    }
}
</style>