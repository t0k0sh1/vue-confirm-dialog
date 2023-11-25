<template>
  <div>
    <ClickFormComponent />
  </div>
  <div>
    <SubmitFormComponent />
  </div>
</template>

<script>
import ClickFormComponent from "./components/ClickFormComponent.vue";
import SubmitFormComponent from "./components/SubmitFormComponent.vue";

export default {
  components: {
    ClickFormComponent,
    SubmitFormComponent,
  },
};
</script>
