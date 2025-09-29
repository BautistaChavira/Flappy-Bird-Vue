<template>
    <div class="bird" :style="{ top: y + 'px' }"></div>
</template>

<script>
    export default {
        props: ['y']
    }
</script>

<style scoped>
.bird {
    width: 30px;
    height: 30px;
    background: yellow;
    position: absolute;
    left: 50px;
    border-radius: 50%;
}
</style>