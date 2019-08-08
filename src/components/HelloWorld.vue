<template>
  <div class="container">
    <div class="row">
      <div class="col mt-5 pt-5">
        <div ref="card" class="card shadow-lg p-5" style="border-radius: 50px"></div>
      </div>
    </div>

    <div class="row">
      <div class="col-7 mt-5 pt-5">
        <b-button block variant="dark" @click="purchase()">Purchase</b-button>
      </div>
    </div>
  </div>
</template>


<script>
let stripe = Stripe(`pk_test_yMq2Il8Mmm2oW7MO2tQtsEhB00YflXZMdE`),
  elements = stripe.elements(),
  card = undefined;

export default {
  methods: {
    purchase() {
      stripe.createToken(card).then(result => {
        if (result.error) {
          self.hasCardErrors = true;
          self.$forceUpdate(); // Forcing the DOM to update so the Stripe Element can update.
          return;
        }
        console.log(result)
        // Access the TOken with result.token
      });
    }
  },
  mounted() {
    card = elements.create("card");
    card.mount(this.$refs.card);
  }
};
</script>