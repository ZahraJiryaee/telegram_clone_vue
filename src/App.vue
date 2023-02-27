<template>
  <div
    class="container"
    :class="{ showDetailFullScreen: isDetailShowedCompeltely }"
  >
    <div class="columnLeft">
      <label class="header">
        <!-- menu -->
        <div class="menuIcon">
          <div></div>
          <div></div>
          <div></div>
        </div>
        <!-- input -->
        <input
          type="search"
          class="searchInput"
          placeholder="Search"
          v-model="searchInput"
        />
      </label>
      <!-- chat list -->
      <ChatList />
      <button @click="showDetailCompeltely(true)">btn 1</button>
    </div>
    <div class="chatDetail">
      <!-- chat detail -->
      <p>chat detail</p>
      <button @click="showDetailCompeltely(false)">btn 2</button>
    </div>
  </div>
</template>

<script>
import ChatList from "@/components/ChatList";

export default {
  name: "App",
  components: { ChatList },
  data() {
    return {
      isDetailShowedCompeltely: false,
      searchInput: "",
    };
  },
  methods: {
    showDetailCompeltely(value) {
      this.isDetailShowedCompeltely = value;
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  width: 100%;
  min-width: 100%;
  max-width: 100%;
  height: 100%;
  min-height: 100vh;
  overflow: hidden;
  position: relative;

  opacity: 1;
  transition: opacity 0.3s cubic-bezier(0.4, 0, 0.2, 1);

  @media only screen and (max-width: 600px) {
    display: grid;
    grid-template-columns: 100%;
    grid-template-rows: 100%;
    min-width: 100%;
  }

  .columnLeft {
    display: flex;
    flex-direction: column;
    flex: 2;

    max-width: 420px;
    width: 420px;

    overflow: visible;

    border-right: 1px solid black;

    @media only screen and (min-width: 601px) and (max-width: 925px) {
      display: flex;
      position: fixed;
      left: 0;
      top: 0;
      width: 26.5rem;
      max-width: none;
      transition: transform 0.2s cubic-bezier(0.4, 0, 0.2, 1);
    }

    @media only screen and (max-width: 600px) {
      max-width: 100%;
      width: 100%;
    }

    .header {
      position: relative;
      background-color: transparent;
      padding: 1rem;

      display: flex;
      justify-content: center;
      align-items: center;
      gap: 1.4rem;

      .menuIcon > div {
        width: 25px;
        height: 2px;
        background-color: black;
        margin: 6px 0;
      }

      input {
        width: 100%;
        height: 44px;
        background-color: #ffffff25 !important;
        outline: none;
        border-radius: 22px;
        padding-left: 35px;
        padding-top: 4px;
        padding-bottom: 4px;
        color: #a39698;

        &::placeholder {
          color: #a39698;
        }
      }
    }
  }

  .chatDetail {
    // width: 60%;
    background-color: #e6ebee !important;
    overflow: hidden;
    flex: 3;
    position: relative;

    @media only screen and (max-width: 601px) {
      width: 100%;
    }

    @media only screen and (min-width: 601px) and (max-width: 925px) {
      transform: translate3d(26.5rem, 0, 0);
      transition: transform 0.2s cubic-bezier(0.4, 0, 0.2, 1);
    }
  }
}

.showDetailFullScreen.container {
  @media only screen and (max-width: 925px) {
    .columnLeft {
      transform: translate3d(-100%, 0, 0);
    }

    .chatDetail {
      transform: translate3d(0%, 0, 0);
    }
  }

  @media only screen and (max-width: 601px) {
    grid-template-rows: 0 100%;
    .columnLeft {
      transform: translate3d(-100%, 0, 0);
    }

    .chatDetail {
      transform: translate3d(0%, 0, 0);
    }
  }
}
</style>
