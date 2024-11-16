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
<style scoped>
.burger-panel {
    z-index: 1;
    width: 100vw;
    height: 100vh;
    position: fixed;
    top: 0;
    left: 0;
    padding-top: 8.5ex;
    background: #fff;
    transform-origin: left;
    transform: translateX(-100%);
    transition: ease-in-out 1s;
    &::after {
        content: "";
        position: absolute;
        width: 50%;
        height: 100%;
        background: deeppink;
        top: 0;
        z-index: -1;
    }
    &::before {
        content: "";
        position: absolute;
        width: 50%;
        height: 50%;
        background: darkgreen;
        bottom: 0;
        left: 0;
        z-index: -1;
    }

    &.open {
        transform: translateX(0);
    }
}
</style>