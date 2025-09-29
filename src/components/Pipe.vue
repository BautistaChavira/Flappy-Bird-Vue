<template>
  <div>
    <!-- Tubo superior -->
    <div
      class="pipe"
      :style="{ left: x + 'px', top: '0px', height: gapY - gapSize / 2 + 'px' }"
    ></div>

    <!-- Tubo inferior -->
    <div
      class="pipe"
      :style="{ left: x + 'px', top: gapY + gapSize / 2 + 'px', height: '600px' }"
    ></div>
  </div>
</template>

<script>
export default {
    props: ['x', 'gapY'],
    data() {
        return {
            gapSize: 160 // antes era 100, ahora más amplio
        }
    }
}
</script>

<style scoped>
.pipe {
  position: absolute;
  width: 50px;
  background-color: green;
}
</style>