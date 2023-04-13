<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
    name: 'my-button'
}
</script>

<style>
    .btn {
        margin-top: 15px;
        margin-right: 5px;
        align-self: flex-end;
        padding: 10px;
        background: None;
        color: teal;
        border: 2px solid teal;
    }
</style>