<template>
<div class="user-profile">
  <div class="user-profile__user-panel">
    <h1 class="user-profile__username">@ {{user.username}}</h1>
    <div class="user-profile__admin-badge" v-if="user.isAdmin">
      Admin
    </div>
    <div class="user-profile__follower-count">
      <strong>Followers: </strong> {{followers}}
    </div>
    <form class="user-profile__create-twat" @submit.prevent="createNewTwat">
      <label for="newTwat"><strong>New Twat</strong></label>
      <textarea id="newTwat" rows="4" v-model="newTwatContent"></textarea>

      <div class="user-profile__create-twat-type">
        <label for="newTwatType"><strong>Type: </strong></label>
        <select id="newTwatType" v-model="selectedTwatType">
          <option :value="option.value" v-for="(option, index) in twatTypes" :key="index">
            {{option.name}}
          </option>
        </select>
      </div>

      <button>
        Twat!
      </button>
    </form>
  </div>
  <div class="user-profile__twats-wrapper">
    <TwatItem v-for="twat in user.twats"
              :key="twat.id"
              :username="user.username"
              :twat="twat"
              @favourite="toggleFavourite"></TwatItem>
  </div>
</div>
</template>

<script>

import TwatItem from "@/components/TwatItem";

export default {
  name: "UserProfile",
  components: {TwatItem},

  data() {
    return {
      newTwatContent: '',
      selectedTwatType: 'instant',
      twatTypes: [
        {value: 'draft', name: 'Draft'},
        {value: 'instant', name: 'Instant Twat'}
      ],
      followers: 0,
      user: {
        id: 1,
        username: 'c4artz',
        firstname: 'Christopher',
        lastname: 'Monje',
        email: 'twatter@c4rtz.de',
        isAdmin: true,
        twats: [
          {
            id: 1,
            content: 'Twatter is amazing!'
          },
          {
            id: 2,
            content: "Don't forget - Your're a twat!"
          }
        ]
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower`);
      }
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstname} ${this.user.lastname}`;
    }
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id) {
      console.log(`Favourited Twat #${id}`);
    },
    createNewTwat() {
      if (this.newTwatContent && this.selectedTwatType !== 'draft') {
        this.user.twats.unshift({
          id: this.user.twats.length + 1,
          content: this.newTwatContent
        })
        this.newTwatContent = ''
      }
    }
  },
  mounted() {
    this.followUser();
  }
}
</script>

<style>

h1 {
  margin: 0 0 10px 0;
}

.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}

.user-profile__admin-badge {
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}

.user-profile__create-twat {
  display: flex;
  flex-direction: column;
  margin-top: 10px;
}

</style>