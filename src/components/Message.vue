<template>
  <div class="message" v-bind:class="{green: green}">
    {{ content }}
    <span>{{ time }}</span>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: ['content', 'time', 'green']
}
</script>

<style>
 .message {
  font-size: 14px;
  box-shadow: 0 1px 0.5px 0 rgba(0,0,0,.13);
  background: #ffffff;
  margin: 5px 100px;
  padding: 5px 10px;
  border-radius: 5px;
  width: fit-content;
 }

 .green {
  background: rgb(220, 248, 198) !important;
  align-self: flex-end;
 }

 .message span {
  margin-left: 25px;
  font-size: 11px;
  color: gray;
 }
</style>