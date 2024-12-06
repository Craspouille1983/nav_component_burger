<template>
    <div :class="{ open: isOpen }" class="burger-panel">
        <ul>
            <li v-for="item in items" :key="`item-${item.id}`">
                <a :href="item.menuUrl">{{ item.menu }}</a>
            </li>
        </ul>
    </div>
</template>
<script>
export default {
    name: "burgerPanelMenu",
    props: {
        items: {
            type: Array,
            required: true
        },
        isOpen: {
            type: Boolean,
            required: true,
        },
    }, watch: {
        items(newItems) {
            this.$nextTick(() => {
                // Ici, tu attends la mise à jour du DOM avant d'agir sur les nouveaux items
                console.log('Les items ont été mis à jour:', newItems);
            });
        },
        isOpen(newIsOpen) {
            this.$nextTick(() => {
                console.log('isOpen a été mis à jour:', newIsOpen);
            });
        }
    },
    mounted() {
        console.log("Propriétés passées à l'enfant:", this.$props);
    }

}
</script>
<style lang="scss" scoped>
.burger-panel {
    /* Variable */
    $fs: 2.5rem;
    $padd: 6rem;
    /* End variable */
    height: 100vh;
    width: 100vw;
    position: fixed;
    top: 0;
    left: 0;
    margin-top: 8.5ex;
    transform-origin: right;
    transform: translateX(-150%);
    transition: ease-in-out .5s;
    padding: $padd;
    background-image: linear-gradient(rgba(255, 53, 75, .95), rgba(255, 53, 75, .95));
    background-size: 0;
    background-repeat: no-repeat;
    z-index: 1;
    ul {
        text-align: left;
        margin: auto;

        li {
            list-style: none;

            a {
                font-family: 'Pangolin';
                font-size: $fs;
                line-height: calc($fs * 1.55);
                text-decoration: none;
                color: #fff;
            }
        }
    }

    &.open {
        transform: translateX(0);
        background-size: 95%;
    }
}
</style>