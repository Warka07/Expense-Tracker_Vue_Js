<template>
  <div>
    <h3>Add new transition</h3>
    <form id="form" @submit.prevent="onSubmit">
      <div class="form-control">
        <label for="text">Text</label>
        <input
          type="text"
          id="text"
          v-model="text"
          placeholder="Enter Text..."
        />
      </div>
      <div class="form-control">
        <label for="amount"
          >Amount <br />

          (negative - expense, positive = income)
        </label>
        <input
          type="text"
          id="amount"
          v-model="amount"
          placeholder="Enter Amount..."
        />
      </div>
      <button class="btn">Add Transaction</button>
    </form>
  </div>
</template>
<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";

const text = ref("");
const amount = ref("");

const emit = defineEmits(["transactionSubmitted"]);

const toast = useToast();

const onSubmit = () => {
  if (!text.value || !amount.value) {
    toast.error("Both fields must be filled");
    return;
  }
  // console.log(text.value, amount.value);

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit("transactionSubmitted", transactionData);

  text.value = "";
  amount.value = "";
};
</script>
