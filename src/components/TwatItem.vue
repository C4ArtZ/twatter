<template>
  <div class="twat-item" @click="fovouriteTwat(twat.id)">
    <div class="user-profile__twat">
      <div class="twat-item__user">
        @{{username}}
      </div>
      <div class="twat-item__content">
        {{twat.content}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TwatItem",
  props: {
    username: {
      type: String,
      required: true
    },
    twat: {
      type: Object,
      required: true
    }
  },
  methods: {
    fovouriteTwat(id) {
      this.$emit('favourite', id);
    }
  }
}
</script>

<style lang="scss" scoped>

.twat-item {
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;
  margin-bottom: 10px;

  &:hover {
    transform: scale(1.05, 1.05);
  }

  .twat-item__user {
    font-weight: bold;
  }
}





</style>