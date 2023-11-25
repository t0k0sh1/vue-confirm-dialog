<script>
import ConfirmDialogComponent from "./components/ConfirmDialogComponent.vue";

export default {
  components: {
    ConfirmDialogComponent,
  },
  data() {
    return {
      value: "",
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
      if (this.resolveDialog) {
        this.resolveDialog(true);
      }
      this.isDialogVisible = false;
    },
    handleCancel() {
      if (this.resolveDialog) {
        this.resolveDialog(false);
      }
      this.isDialogVisible = false;
    },
    async handleSubmit(e) {
      // form validation
      if (!this.validate()) {
        return;
      }

      // show confirm dialog
      const confirmed = await this.showDialog();
      if (confirmed) {
        e.target.submit();
      }
    },
    validate() {
      if (this.value === "") {
        alert("Input is empty!");
        return false;
      }
      return true;
    },
  },
};
</script>

<template>
  <form id="myForm" @submit.prevent="handleSubmit">
    <input type="text" name="name" v-model="value" />
    <input type="submit" value="SUBMIT" />
    <confirm-dialog-component
      :is-visible="isDialogVisible"
      @confirm="handleConfirm"
      @cancel="handleCancel"
    ></confirm-dialog-component>
  </form>
</template>
