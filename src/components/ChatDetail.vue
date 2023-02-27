<template>
  <div
    v-for="msg in messages"
    key="msg.id"
    class="container"
    :class="msg.sent ? 'msgSentWrapper' : 'msgRecievedWrapper'"
  >
    <div class="msg" :class="msg.sent ? 'msgSent' : 'msgRecieved'">
      <p>
        {{ msg.message }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "ChatDetail",
  props: {
    messages: Array,
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: column;
  margin-bottom: 1rem;

  width: 100%;
  &.msgSentWrapper {
    color: white;
    width: 100%;

    align-items: flex-start;
    .msgSent {
      background-color: #39004a;
      margin-left: 1rem;
    }
  }

  &.msgRecievedWrapper {
    width: 100%;
    align-items: flex-end;

    .msgRecieved {
      background-color: #803d93;
      margin-right: 1rem;
    }
  }
  .msg {
    border: 1px solid black;
    width: 80%;
    border-radius: 10px;
    padding: 1rem;
  }
}
</style>
