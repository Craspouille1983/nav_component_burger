<template>
    <div class="header-container"
        :style="{ backgroundImage: `url(${imgBgSrc})` }">
    </div>
</template>

<script>
export default {
    name: "headerImg",
    props: {
        bgSrc: {
            type: String,
        },
    },
    computed: {
        imgBgSrc() {
            return require(`@/assets/${this.bgSrc}`);
        }
    }
}
</script>
<style scoped>
.header-container {
    width: 100vw;
    height: 100vh;
    margin-top: 8.5ex;
    background-repeat: no-repeat;
    background-position: center;
    background-size: 100% 100%;
    overflow: hidden;
}
</style>