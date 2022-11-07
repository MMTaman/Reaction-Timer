<template>
      <div class="res">
            <slot></slot>
            <slot name="failed"></slot>
      </div>
</template>
<script>
export default {
      data() {},
};
</script>
<style lang="scss">
$bgColor: #5cdb95;
$textColor: #05386b;
$fancy: #edf5e1;
.res {
      color: $textColor;
      background-color: $fancy;
      width: 160px;
      height: 70px;
      font-weight: 600;
      font-size: 25px;
      border-radius: 5px;
}
</style>
