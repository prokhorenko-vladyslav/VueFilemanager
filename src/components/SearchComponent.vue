<template>
    <div class="search">
        <div class="search__icon" @click="search(query)">
            <transition name="fade">
                <svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px"
                     width="30" height="30"
                     viewBox="0 0 172 172"
                     style=" fill:#000000;"
                     v-if="!query.length"
                ><g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><path d="M0,172v-172h172v172z" fill="none"></path><g fill="#9f9f9f"><path d="M74.53333,17.2c-31.59642,0 -57.33333,25.73692 -57.33333,57.33333c0,31.59642 25.73692,57.33333 57.33333,57.33333c13.73998,0 26.35834,-4.87915 36.24766,-12.97839l34.23203,34.23203c1.43802,1.49778 3.5734,2.10113 5.5826,1.57735c2.0092,-0.52378 3.57826,-2.09284 4.10204,-4.10204c0.52378,-2.0092 -0.07957,-4.14458 -1.57735,-5.5826l-34.23203,-34.23203c8.09924,-9.88932 12.97839,-22.50768 12.97839,-36.24766c0,-31.59642 -25.73692,-57.33333 -57.33333,-57.33333zM74.53333,28.66667c25.39937,0 45.86667,20.4673 45.86667,45.86667c0,25.39937 -20.46729,45.86667 -45.86667,45.86667c-25.39937,0 -45.86667,-20.46729 -45.86667,-45.86667c0,-25.39937 20.4673,-45.86667 45.86667,-45.86667z"></path></g></g></svg>
            </transition>
            <transition name="fade">
                <svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px"
                     width="50" height="50"
                     viewBox="0 0 172 172"
                     style=" fill:#000000;"
                     v-if="query.length"
                     @click="clearQuery"
                ><g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><path d="M0,172v-172h172v172z" fill="none"></path><g fill="#9f9f9f"><path d="M43.14781,34.4l-44.23625,51.6l44.23625,51.6h115.09219c7.56531,0 13.76,-6.19469 13.76,-13.76v-75.68c0,-7.56531 -6.19469,-13.76 -13.76,-13.76zM46.29219,41.28h111.94781c3.84313,0 6.88,3.03688 6.88,6.88v75.68c0,3.84313 -3.03687,6.88 -6.88,6.88h-111.93437l-38.33719,-44.72zM78.11219,62.92781l-4.86437,4.86437l18.20781,18.20781l-18.20781,18.20781l4.86437,4.86437l18.20781,-18.20781l18.20781,18.20781l4.86437,-4.86437l-18.20781,-18.20781l18.20781,-18.20781l-4.86437,-4.86437l-18.20781,18.20781z"></path></g></g></svg>
            </transition>
        </div>
        <div class="search__input">
            <input
                    type="text"
                    placeholder="Search query"
                    v-model="query"
                    @keyup.enter="search(query)"
            >
        </div>
    </div>
</template>

<script>
    import {mapActions} from "vuex";

    export default {
        name: "SearchComponent",
        data() {
            return {
                query: ""
            }
        },
        methods: {
            ...mapActions(['search', 'fetchAll']),
            clearQuery() {
                this.query = '';
                this.fetchAll();
            }
        }
    }
</script>

<style lang="scss" scoped>
    .search {
        display: flex;
        align-items: center;
        width: 100%;

        .search__icon {
            width: 20px;
            height: 20px;

            svg {
                width: 100%;
                height: 100%;
            }

            .fade-enter-active {
                transition: opacity .5s;
            }
            .fade-enter, .fade-leave-active {
                opacity: 0;
            }
        }

        .search__input {
            width: 100%;
            padding: .5rem .8rem;
            transition: all .3s ease-in-out;

            input {
                width: 100%;
                height: 100%;
                border: 0;
                font-size: .9rem;
                font-weight: 300;
                
                &::placeholder {
                    color: #828D99;
                    font-size: .9rem;
                    font-weight: 300;
                }
            }
        }
    }
</style>