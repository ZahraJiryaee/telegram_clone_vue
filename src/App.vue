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
      <ChatList
        :search="searchInput"
        :selectedItem="selectedItem"
        @getMessage="getMessageFromUser"
      />
    </div>
    <div class="columnRight">
      <!-- info -->
      <div class="header">
        <div class="info">
          <img
            src="https://img.icons8.com/fluency/48/null/long-arrow-up.png"
            alt="arrow"
            @click="showDetailCompeltely(false)"
            class="arrowIcon"
          />
          <img
            :src="userInfo.photoUrl"
            alt="avatar"
            class="avatarIcon"
            width="48"
            height="48"
          />
          <span>
            {{ userInfo.fullName }}
          </span>
        </div>
        <div>
          <img
            src="https://img.icons8.com/nolan/64/search-more.png"
            alt="search"
          />
        </div>
      </div>
      <!-- chat detail -->
      <ChatDetail :messages="filteredMessages" />
    </div>
  </div>
</template>

<script>
import ChatList from "@/components/ChatList";
import ChatDetail from "@/components/ChatDetail";

import mockData from "@/mock/db.mock.json";

export default {
  name: "App",
  components: { ChatList, ChatDetail },
  data() {
    return {
      isDetailShowedCompeltely: false,
      searchInput: "",
      messages: [],
      filteredMessages: "",
      userId: 1,
      selectedItem: 1,
      userInfo: {
        fullName: "",
        photoUrl: "",
        userName: "",
        phoneNumber: "",
        bio: "",
        lastAct: "",
      },
    };
  },
  methods: {
    showDetailCompeltely(value) {
      this.isDetailShowedCompeltely = value;
    },
    loadMessages() {
      const { messages } = mockData;
      this.messages = messages;
      this.getMessageFromUser(this.userId);
    },
    getMessageFromUser(id) {
      this.userId = id;
      this.selectedItem = id;
      this.showDetailCompeltely(true);
      this.filteredMessages = this.messages.filter(function (message) {
        return message.chat_id == id;
      });
    },
    getUserInfo(id) {
      const { users } = mockData;
      const selectedUser = users.filter(function (user) {
        return user.id == id;
      });

      this.userInfo.fullName = selectedUser[0].name;
      this.userInfo.photoUrl = selectedUser[0].avatar;
      this.userInfo.userName = selectedUser[0].username;
      this.userInfo.phoneNumber = selectedUser[0].phone;
      this.userInfo.bio = selectedUser[0].bio;
      this.userInfo.lastAct = selectedUser[0].activity;
    },
  },
  created() {
    this.loadMessages();
    this.getUserInfo(1);
  },
  watch: {
    userId: function (newVal) {
      this.getUserInfo(newVal);
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
  // min-height: 100vh;
  overflow: hidden;
  position: relative;

  opacity: 1;
  transition: opacity 0.3s cubic-bezier(0.4, 0, 0.2, 1);

  @media only screen and (max-width: 600px) {
    display: grid;
    grid-template-columns: 100%;
    // grid-template-rows: 100%;
    min-width: 100%;
  }

  .columnLeft {
    display: flex;
    flex-direction: column;
    flex: 2;

    max-width: 420px;
    width: 420px;

    overflow: visible;

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

  .columnRight {
    // width: 60%;
    background: url(./assets/bg.png);
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;

    overflow: hidden;
    flex: 3;
    position: relative;

    border-left: 1px solid black;

    min-height: 100vh;

    @media only screen and (max-width: 601px) {
      width: 100%;
      transform: translate3d(100%, 0, 0);
      display: none;
    }

    @media only screen and (min-width: 601px) and (max-width: 925px) {
      transform: translate3d(26.5rem, 0, 0);
      transition: transform 0.2s cubic-bezier(0.4, 0, 0.2, 1);
    }

    .header {
      background-color: white;
      margin-bottom: 2rem;

      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0 1rem;

      .info {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 1rem;

        .avatarIcon {
          border-radius: 50%;
        }

        .arrowIcon {
          transform: rotate(-90deg);
        }
      }
    }
  }
}

.showDetailFullScreen.container {
  @media only screen and (max-width: 925px) {
    .columnLeft {
      transform: translate3d(-100%, 0, 0);
    }

    .columnRight {
      transform: translate3d(0%, 0, 0);
    }
  }

  @media only screen and (max-width: 601px) {
    grid-template-rows: 0 100% !important;
    .columnLeft {
      transform: translate3d(-100%, 0, 0);
    }

    .columnRight {
      transform: translate3d(0%, 0, 0);
      display: block;
    }
  }
}
</style>
