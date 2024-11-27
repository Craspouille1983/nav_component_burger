<template>
    <div class="header-container">
        <img alt="" :src="imgBgSrc" />
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
<style lang="scss" scoped>
.header-container {
    width: 100vw;
    height: 100vh;
    margin-top: 8.5ex;
    /* background-repeat: no-repeat;
    background-position: center;
    background-size: 100% 100%; */
    overflow: hidden;
    img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        object-position: top center;
    }
}
</style>