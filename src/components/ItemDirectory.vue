<template>
  <div class="item-directory">
    <div
        :class="['item-directory__name', {'item-directory__name-open': showContent}]"
        @click="toggleShowLeave"
    >
      <slot name="directory-name" />
    </div>

    <div class="item-directory__content" v-if="showContent">
      <slot name="directory-content" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showContent: false
    }
  },

  methods: {
    toggleShowLeave() {
      this.showContent = !this.showContent
    }
  },
}
</script>

<style>
.item-directory {
  padding: 5px 0;
  cursor: pointer;
  width: fit-content;
}

.item-directory__content {
  margin-left: 20px;
}

.item-directory__name {
  padding-left: 30px;
  margin-bottom: 5px;
  position: relative;
}

.item-directory__name::before {
  content: '';
  width: 20px;
  height: 20px;
  position: absolute;
  background: red;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  background: url("../assets/iconDirectory.png") no-repeat center;
}

.item-directory__name-open::before {
  background: url("../assets/iconOpenDirectory.png") no-repeat center;
}
</style>