<template>
  <button class="searchbtndef">{{searchtxt}}</button>
</template>

<script>
export default {
    props:{
        searchtxt: String
    }
}
</script>

<style scoped>
.searchbtndef {
  background: var(--background-btn-color);
  box-shadow: 0px 8px 16px rgba(0, 0, 0, 0.15);
  border-radius: 68px;
  padding: 12px 30px;
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 21px;
  color: #ffffff;
  border: none;
}
</style>