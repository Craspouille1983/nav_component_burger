<template>
    <nav>
        <figure><img :src="require(`@/assets/${src}`)" :alt="altText"></figure>
        <ul v-show="isWideScreen">
            <li v-for="item in items" :key="`item-${item.id}`"><a :href="item.menuUrl">{{ item.menu }}</a></li>
        </ul>
        <div :class="{ burger: true, open: burger }"
            v-show="!isWideScreen" @click="openBurger">
            <span></span><span></span><span></span></div>
        <!-- Le composant enfant BurgerMenu -->
    </nav>
    <burgerPanelMenu :items="items" :isOpen="burger" />
    <div :class="{ open: burger }" class="volets"></div>
</template>
<script>
import burgerPanelMenu from './burgerPanelMenu.vue';
import { ref, onMounted, onUnmounted } from "vue";

export default {
    name: "navComponent",
    components: {
        burgerPanelMenu,
    },
    data() {
        return {
            burger: false,
            show: false,
        }
    },
    props: {
        src: {
            type: String,
            default: "crasp_2_logo.png"
        },
        altText: {
            type: String,
            default: "Logo Craspouille"
        },
        items: {
            type: Array,
            default: () => [],
        }
    },
    methods: {
        openBurger: function () {
            // console.log(e)
            this.burger = !this.burger;
            this.$nextTick(() => {
                // Après la mise à jour du DOM, tu peux exécuter des actions ici
                console.log('Le menu a été mis à jour, burger:', this.burger);
            });
        }
    },
    setup() {
        const isWideScreen = ref(window.innerWidth > 768); // Initialise selon la taille actuelle de l'écran

        const updateScreenSize = () => {
            isWideScreen.value = window.innerWidth > 768;
        };

        onMounted(() => {
            window.addEventListener("resize", updateScreenSize); // Écoute les changements de taille
        });

        onUnmounted(() => {
            window.removeEventListener("resize", updateScreenSize); // Nettoie l'écouteur
        });

        return { isWideScreen };
    },
}
</script>
<style scoped>
.volets {
    width: 100vw;
    height: 100vh;
    /* margin-top: 8.5ex; */
    overflow: hidden;
    position: fixed;
    left: 0;
    z-index: 1;

    &.open {

        &::after {
            transform-origin: top right;
            transform: translateX(0);
        }

        &::before {
            transform: scaleY(1);
        }
    }

    &::after {
        z-index: 0;
        content: "";
        position: absolute;
        width: 43vw;
        right: 0;
        height: 100vh;
        background: rgba(1, 1, 1, .95);
        top: 0;
        transition: transform .75s ease-in-out allow-discrete;
        transform-origin: top right;
        transform: translateX(100vw);
    }

    &::before {
        content: "";
        position: absolute;
        width: 15vw;
        height: 100vh;
        background: rgb(139, 0, 0, .5);
        top: -8.5ex;
        left: calc(50% - calc(15vw/2));
        z-index: 1;
        transition: transform .75s;
        transform-origin: top;
        transform: scaleY(0);
    }
}

nav {
    background: rgba(3, 3, 3, .95);
    position: fixed;
    display: flex;
    justify-content: space-between;
    align-items: center;
    top: 0;
    width: 100vw;
    height: 8.5ex;
    padding: .75rem 4rem;
    z-index: 10;

    .burger {
        width: 100%;
        max-width: 3em;
        display: inline-flex;
        flex-direction: column;
        align-items: flex-end;
        row-gap: .5em;
        cursor: pointer;
        position: relative;

        &.open {
            span {
                &:nth-of-type(1) {
                    width: 2em;
                    transform: rotateZ(-45deg) translateX(-30%);
                }

                &:nth-of-type(2) {
                    position: absolute;
                    transform: translateX(100vw);
                }

                &:nth-of-type(3) {
                    width: 2em;
                    transform: rotateZ(45deg) translateX(-30%);
                }
            }
        }

        span {
            position: relative;
            display: inline-block;
            height: .6ex;
            width: 3em;
            left: 0;
            background-color: #fff;
            transform-origin: center;
            transition: .5s ease-in-out;

            &:nth-of-type(1) {
                width: 2em;
                transform: rotateZ(0) translate(0);
            }

            &:nth-of-type(2) {
                transform-origin: left;
                transform: translateX(0);
            }

            &:nth-of-type(3) {
                width: 1em;
                transform: rotateZ(0) translate(0);
            }
        }
    }

    figure {
        max-width: 3em;
        height: 100%;
        filter: contrast(1.75);

        img {
            height: 100%;
            object-fit: cover;
        }
    }

    ul {
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: space-around;

        li {
            list-style: none;

            a {
                font-family: "Climate Crisis", sans-serif;
                font-variation-settings: "YEAR" 2012;
                font-weight: bold;
                font-optical-sizing: auto;
                color: #fff;
                text-decoration: none;
            }
        }
    }
}
</style>
