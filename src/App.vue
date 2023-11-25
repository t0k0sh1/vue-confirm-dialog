<template>
  <div>
    <h3>クリックバージョン</h3>
    <input type="button" value="CLICK" @click="handleClick" />
    <confirm-dialog-component
      :is-visible="isDialogVisibleForSubmit"
      @confirm="handleConfirmForSubmit"
      @cancel="handleCancelForSubmit"
    ></confirm-dialog-component>
  </div>
  <div>
    <h3>フォームバージョン</h3>
    <form id="myForm" @submit.prevent="handleSubmit">
      <input type="text" name="name" v-model="value" />
      <input type="submit" value="SUBMIT" />
      <confirm-dialog-component
        :is-visible="isDialogVisibleForClick"
        @confirm="handleConfirmForClick"
        @cancel="handleCancelForClick"
      ></confirm-dialog-component>
    </form>
  </div>
</template>

<script>
import ConfirmDialogComponent from "./components/ConfirmDialogComponent.vue";

export default {
  components: {
    ConfirmDialogComponent,
  },
  data() {
    return {
      value: "",
      isDialogVisibleForSubmit: false,
      isDialogVisibleForClick: false,
      resolveDialog: null,
    };
  },
  methods: {
    handleConfirmForClick() {
      alert("CLICKED CONFIRM");
      this.isDialogVisibleForClick = false;
    },
    handleCancelForClick() {
      alert("CLICKED CANCEL");
      this.isDialogVisibleForClick = false;
    },
    handleClick(e) {
      e.preventDefault();
      this.isDialogVisibleForClick = true;
    },
    showDialog() {
      this.isDialogVisibleForSubmit = true;
      return new Promise((resolve, reject) => {
        this.resolveDialog = resolve;
      });
    },
    handleConfirmForSubmit() {
      if (this.resolveDialog) {
        this.resolveDialog(true);
      }
      this.isDialogVisibleForSubmit = false;
    },
    handleCancelForSubmit() {
      if (this.resolveDialog) {
        this.resolveDialog(false);
      }
      this.isDialogVisibleForSubmit = false;
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
