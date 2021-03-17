<template>
  <div class="item" v-bind:class="{active: activeMessage}">
    <div class="title is-6">{{username}}</div>
    <div class="subtitle is-6">{{lastMessage}}</div>
  </div>
</template>

<script>
export default {
  name: 'Item',
  props:['username','lastMessage','activeMessage'],
}
</script>

<style>
  .item {
    border-bottom: 1px solid #f2f2f2;
    padding: 15px 30px;
    margin-bottom: 0 !important;
  }

  .subtitle {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    color: gray;
  }

  .item:hover{
    background: #f5f5f5;
    cursor: pointer;
  }

  .item.active{
    background: rgb(235, 235, 235);
  }
</style>