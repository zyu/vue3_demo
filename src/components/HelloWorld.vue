<template>
<h1>{{ msg }}</h1>
<Son propsA='hh' propsB=4></Son>

<button @click="increment">count is: {{ t }} </button>
<button @click="btnclick">Clear</button>
<h1 :style="{ background:color }">x : {{position.x}} y: {{position.y}}</h1>
</template>

<script>
import {
    ref,
    computed,
    reactive,
    watch,
    provide,
    unref,
    watchEffect
} from 'vue'

import Son from './Son.vue'

export default {
    name: 'HelloWorld',
    components: {
        Son
    },
    props: {
        msg: String
    },
    setup() {
        const t = ref(0)

        //      const i = inject('datas', 0)

        // 创建响应式数据
        const position = reactive({});
        // 设置不断变化的数据
        window.addEventListener("mousemove", (e) => {
            //  console.log("mousemove:", e.pageX, e.pageY);
            position.x = e.pageX;
            position.y = e.pageY;
        });

        const color = computed(() => {
            const hex = (num) => (num % 255).toString(16);
            return `#${hex(position.x) + hex(position.x) + '00'}`;
        });

        const time = ref(0)
        setInterval(() => {
            time.value = Date.now()
        }, 1000)

        watch(
            time,
            (val, prev) => {
                console.log(`watch ${val}`);
            }
        )

        //响应式副作⽤
        watchEffect(() => {
            //  console.log("time", time.vlaue, unref(time));
        });

        const btnclick = () => {
            time.value = 0;
        };

        provide('location', time)
        provide('geolocation', {
            longitude: 90,
            latitude: 135
        })

        return {
            t,
            time,
            position,
            btnclick,
            color
        }

    },
    methods: {
        increment() {
            this.t++
        }
    }
}
</script>
