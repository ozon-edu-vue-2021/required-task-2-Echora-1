<template>
  <div :class="leaveClasses" @click="pick">
    <template v-if="type === 'file'">
      <div class="item-leave__file">
        <slot />
      </div>
    </template>

    <template v-else>
      <div class="item-leave__link">
        <slot />
      </div>
    </template>
  </div>
</template>

<script>
export default {
  props: {
    type: {
      type: String,
      required: true,
      validator: v => ['file', 'link'].includes(v),
    },

    name: {
      type: String,
      required: true,
    },

    selectedLeave: {
      type: String,
    }
  },

  data() {
   return {
     uid: ''
   }
  },


  methods: {
    pick() {
      this.$emit('onSelectedLeave', this.id)
    }
  },

  computed: {
    id() {
      return `${this.name}-${this.uid}`
    },

    leaveClasses() {
      return ['item-leave', {'item-leave--selected': this.selectedLeave === this.id}]
    }
  },

  mounted () {
    this.uid = Math.random()
  }
}
</script>

<style>

.item-leave {
  width: fit-content;
  border-radius: 5px;
}

.item-leave--selected {
  background-color: rgba(0,0,0,0.20);
}

.item-leave__file,
.item-leave__link {
  position: relative;
  padding: 5px 5px 5px 30px;
  width: fit-content;
}

.item-leave__file::before,
.item-leave__link::before {
  content: '';
  width: 20px;
  height: 20px;
  position: absolute;
  background: red;
  left: 5px;
  top: 50%;
  transform: translateY(-50%);
}

.item-leave__file::before {
  background: url("../assets/iconFile.png") no-repeat center;
}

.item-leave__link::before {
  background: url("../assets/iconLink.png") no-repeat center;
}

</style>