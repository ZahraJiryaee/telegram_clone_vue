<template>
  <div class="container">
    <div v-for="user in users" :key="user.id" class="flexWrapper">
      <div class="columnLeft">
        <div class="imgContainer">
          <img :src="user.avatar" :alt="user.name" width="52" height="52" />
        </div>
        <div class="nameAndBioContainer">
          <p>
            <span class="name">
              {{ user.name }}
            </span>
            <br />
            <span class="bio"> {{ user.bio }} ... </span>
          </p>
        </div>
      </div>
      <div class="columnRight">12:45</div>
    </div>
  </div>
</template>

<script>
import mockData from "@/mock/db.mock.json";

export default {
  name: "ChatList",
  data: () => ({
    users: [],
  }),
  methods: {
    loadUsers() {
      const { users } = mockData;
      this.users = users;
    },
  },
  created() {
    this.loadUsers();
  },
};
</script>

<style lang="scss" scoped>
.container {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 1rem;

  .flexWrapper {
    display: flex;
    justify-content: space-between;
    align-items: center;

    padding: 0 1rem;

    .columnLeft {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 1rem;

      .imgContainer img {
        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
      }

      .nameAndBioContainer {
        text-align: left;

        // .name {}

        .bio {
          font-size: 15px;
          color: gray;
        }
      }
    }

    // .columnRight {}
  }
}
</style>
