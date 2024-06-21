<script>
import { store } from '../store.js';
export default {
    name: "AppHeader",
    data() {
        return {
            store,
        }
    },
}
</script>

<template>
    <header>
        <div class="header-container">
            <div class="items-container">
                <div class="title">IP Address Tracker</div>
                <div>
                    <div class="relative">

                        <span class="arrow-button" @click="$emit('button_search')" >
                            <img src="../../public/imgs/icon-arrow.svg" alt="">
                        </span>

                        <input class="input-text" type="text" name="ipAddress" id="ipAddress" placeholder="Search for any IP address or domanin" v-model="store.searchText">
                    </div>
                </div>
                
            </div>
        </div>
    </header>
</template>

<style lang="scss" scoped>
.header-container{
    @apply bg-[url('/public/imgs/pattern-bg-desktop.png')] bg-cover bg-center bg-no-repeat h-[300px] lg:h-[200px];

    .items-container{
        @apply h-[100%] flex flex-col items-center pt-5;

        .title{
            @apply text-3xl font-semibold text-white mb-5;
        }

        .arrow-button{
            @apply absolute right-0 h-[100%] flex items-center bg-black rounded-r-xl px-4 hover:cursor-pointer;
        }

        .input-text{
            @apply min-w-[350px] sm:w-[450px] text-lg p-2 rounded-xl;
        }
    }
} 
</style>