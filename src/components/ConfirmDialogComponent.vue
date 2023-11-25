<template>
  <div v-if="isVisible" class="dialog">
    <div class="dialog-content">
      <!-- ダイアログの内容 -->
      <button @click="submit" class="button ok">OK</button>
      <button @click="cancel" class="button cancel">キャンセル</button>
    </div>
  </div>
</template>

<style>
.dialog {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: white;
  border: 1px solid #ccc;
  padding: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  z-index: 1000;
}

.dialog-content {
  text-align: center;
}

.button {
  margin: 10px;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.ok {
  background-color: #4caf50;
  color: white;
}

.ok:hover {
  background-color: #45a049;
}

.cancel {
  background-color: #f44336;
  color: white;
}

.cancel:hover {
  background-color: #d73829;
}
</style>

<script>
export default {
  props: ["isVisible"],
  methods: {
    submit() {
      this.$emit("confirm");
    },
    cancel() {
      this.$emit("cancel");
    },
  },
};
</script>
