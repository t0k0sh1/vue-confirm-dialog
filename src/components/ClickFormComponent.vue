<template>
  <input type="button" value="クリック" @click.prevent="handleClick" />
  <confirm-dialog-component
    :is-visible="isDialogVisible"
    @confirm="handleConfirm"
    @cancel="handleCancel"
  ></confirm-dialog-component>
</template>

<script>
import ConfirmDialogComponent from "./ConfirmDialogComponent.vue";

export default {
  components: {
    ConfirmDialogComponent,
  },
  data() {
    return {
      isDialogVisible: false,
    };
  },
  methods: {
    handleConfirm() {
      console.log("confirmed");
      this.isDialogVisible = false;
    },
    handleCancel() {
      console.log("canceled");
      this.isDialogVisible = false;
    },
    handleClick(e) {
      this.isDialogVisible = true;
    },
  },
};
</script>
