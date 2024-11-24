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
    /* End variable */
    width: 45vw;
    height: 100vh;
    position: fixed;
    top: 0;
    left: 0;
    margin-top: 8.5ex;
    padding: 1rem;
    background: rgba(139, 0, 0, .95);
    transform-origin: right;
    transform: translateX(-150%);
    transition: ease-in-out .5s;
    
    ul {
        text-align: left;
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