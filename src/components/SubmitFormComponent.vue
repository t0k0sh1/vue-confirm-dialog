<template>
  <form @submit.prevent="handleSubmit">
    <input type="submit" value="サブミット" />
    <confirm-dialog-component
      :is-visible="isDialogVisible"
      @confirm="handleConfirm"
      @cancel="handleCancel"
    ></confirm-dialog-component>
  </form>
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
      resolveDialog: null,
    };
  },
  methods: {
    showDialog() {
      this.isDialogVisible = true;
      return new Promise((resolve, reject) => {
        this.resolveDialog = resolve;
      });
    },
    handleConfirm() {
      console.log("confirmed");
      if (this.resolveDialog) {
        this.resolveDialog(true);
      }
      this.isDialogVisible = false;
    },
    handleCancel() {
      console.log("canceled");
      if (this.resolveDialog) {
        this.resolveDialog(false);
      }
      this.isDialogVisible = false;
    },
    async handleSubmit(e) {
      // show confirm dialog
      const confirmed = await this.showDialog();
      if (confirmed) {
        e.target.submit();
      }
    },
  },
};
</script>
