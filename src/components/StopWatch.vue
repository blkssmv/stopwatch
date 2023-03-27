<template>
    <div :class="running ? 'watch running_watch' : 'watch'">
        <div id="clock">{{ time }}</div>
        <div class="actions">

            <div v-if="running">
                <button @click="pause">
                    <svg width="10" height="20" viewBox="0 0 10 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <rect x="7" width="3" height="20" fill="#9E9E9E" />
                        <rect width="3" height="20" fill="#9E9E9E" />
                    </svg>
                </button>
            </div>
            <div v-else>
                <button @click="start">
                    <svg width="17" height="20" viewBox="0 0 17 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M0 20V0L17 10L0 20Z" fill="#9E9E9E" />
                    </svg>
                </button>
            </div>

            <button @click="reset">
                <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <rect width="20" height="20" fill="#9E9E9E" />
                </svg>
            </button>
        </div>

    </div>
</template>
  
<script>
export default {
    data() {
        return {
            time: '00:00:00',
            timeBegan: null,
            timePaused: null,
            stoppedDuration: 0,
            started: null,
            running: false,
        };
    },
    methods: {

        // Старт секундомера

        start() {
            if (this.running) return;

            if (this.timeBegan === null) {
                this.reset();
                this.timeBegan = new Date();
            }

            if (this.timePaused !== null) {
                this.stoppedDuration += new Date() - this.timePaused;
            }

            this.started = setInterval(this.clockRunning, 10);
            this.running = true;
        },

        // Пауза секундомера

        pause() {
            this.running = false;
            this.timePaused = new Date();
            clearInterval(this.started);
        },

        // Сброс секундомера

        reset() {
            this.running = false;
            clearInterval(this.started);
            this.stoppedDuration = 0;
            this.timeBegan = null;
            this.timePaused = null;
            this.time = '00:00:00';
        },


        clockRunning() {
            const currentTime = new Date();
            const timeElapsed = new Date(currentTime - this.timeBegan - this.stoppedDuration);
            const hour = timeElapsed.getUTCHours();
            const min = timeElapsed.getUTCMinutes();
            const sec = timeElapsed.getUTCSeconds();


            // Не отображать если час или минута не прошли

            if (hour > 0) {
                this.time =
                    hour +
                    ':' +
                    min +
                    ':' +
                    sec;
            } else if (min > 0) {
                this.time = min + ':' + sec;
            } else {
                this.time = sec;
            }
        },
    },
};

</script>

<style scoped lang="scss">
.watch {
    width: 225px;
    height: 120px;
    background-color: #696969;
    text-align: center;

    #clock {
        height: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .actions {
        height: 50%;
        border-top: 1px solid #9E9E9E;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 15px;

        button {
            cursor: pointer;
            background: none;
            border: none;
            display: flex;
            align-items: center;
            justify-content: center;
            width: 20px;
            height: 20px;

            svg {

                path,
                rect {
                    transition: all .3s ease;
                }
            }

            &:hover svg {

                path,
                rect {
                    fill: #FFFFFF;
                }
            }
        }
    }
}

.running_watch {
    color: #FFFFFF;
    .actions {
        border-top: 1px solid #FFFFFF;

        button {

            svg {
                path,
                rect {
                    fill: #FFFFFF;
                }
            }

            &:hover svg {
                path,
                rect {
                    fill: #9E9E9E;
                }
            }
        }
    }
}

</style>
  