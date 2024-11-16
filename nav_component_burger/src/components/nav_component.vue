<template>
    <nav>
        <figure><img :src="require(`@/assets/${src}`)" :alt="altText"></figure>
        <ul>
            <li v-for="item in items" :key="`item-${item.id}`"><a :href="item.menuUrl">{{ item.menu }}</a></li>
        </ul>
        <div :class="{ burger: true, open: burger }" @click="openBurger"><span></span><span></span><span></span></div>
    </nav>
    <!-- Le composant enfant BurgerMenu -->
    <burgerPanelMenu :items="items" :isOpen="burger" />
</template>
<script>
import burgerPanelMenu from './burgerPanelMenu.vue';

export default {
    name: "navComponent",
    components: {
        burgerPanelMenu,
    },
    data() {
        return {
            burger: false,
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
    }
}
</script>
<style scoped>
nav {
    .burger {
        max-width: 3em;
        display: inline-flex;
        flex-direction: column;
        align-items: flex-end;
        row-gap: .5em;

        &.open {
            span {
                background-color: deeppink;
            }
        }

        span {
            display: inline-block;
            height: .6ex;
            width: 3em;
            background-color: #fff;

            &:nth-of-type(1) {
                width: 2em;
            }

            &:nth-of-type(3) {
                width: 1em;
            }
        }
    }

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
