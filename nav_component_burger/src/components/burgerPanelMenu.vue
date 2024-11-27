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
    $padd: 8rem;
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
    &::before {
        content: "";
        background: rgba(139, 0, 0, .95);
        display: block;
        width: 45%;
        height: 100%;
        position: relative;
        left: -$padd;
        top: -$padd;
    }
    // display: flex;
    // justify-content: flex-end;
    // align-items: center;

    ul {
        text-align: left;
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        margin: auto;
        // padding-left: 8rem;
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
    }
}
</style>