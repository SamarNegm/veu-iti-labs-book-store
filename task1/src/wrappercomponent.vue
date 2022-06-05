<template>
    <div class="container">
        <div class="row">
            <div class="col-12"><headcomponent /></div>
        </div>
        <div class="row">
            <div class="col-2">
                <linkscomponent />
            </div>
            <div class="col-10">
                <!-- <bodycomponent /> -->
                <lab1component />
                
            </div>
            <div class="col-12">
                <footercomponent />
            </div>
        </div>
    </div>
</template>


<script>
import headcomponent from './components/headcomponent.vue'
import linkscomponent from './components/linkscomponent.vue'
import bodycomponent from './components/bodycomponent.vue'
import footercomponent from './components/footercomponent.vue'
import lab1component from './components/lab1component.vue'
export default {
    data(){
        return {

        }
    },
    components:{
        headcomponent, linkscomponent, bodycomponent, footercomponent, lab1component,
    }

}
</script>