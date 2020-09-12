<template>
<p style="width:30px;height:40px;background-color:#ccc">{{ propsA }}</p>

<p style="width:30px;height:40px;background-color:#ccc">{{ userLocation }}</p>

<button @click="show = !show">
    Toggle
</button>

<transition name="fade">
    <p v-if="show">hello</p>
</transition>
</template>

<script>
import {
    toRefs,
    inject
} from "vue"

export default {
    name: 'Son',
    data() {
        return {
            show: true
        }
    },
    props: {
        propsA: String,
    },
    setup(props) {

        const {
            propsA
        } = toRefs(props)

        console.log('son:', propsA, propsA.value)

        const userLocation = inject('location', 'The Universe')
        const userGeolocation = inject('geolocation')
        const tt = inject('tt', 'null is true')
        return {
            userLocation,
            tt,
            userGeolocation
        }

    }

}
</script>

<style>
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>
