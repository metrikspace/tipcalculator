<template>
  <form id="container">
    <h1 id="title">Tip Calculator</h1>

    <div id="bill">
      <label for="billInput">
        How much was your bill?
      </label>
      <div>
        <span>
          $
        </span>
        <input
          id="billInput"
          placeholder="Bill Amount"
          ref="billInputRef"
          type="text"
        />
      </div>
    </div>

    <div id="service">
      <label for="serviceSelect">
        How much was your service
      </label>
      <div>
        <select id="serviceSelect" ref="serviceSelectRef">
          <option disabled selected value="0">
            -- Choose an Option --
          </option>
          <option value="0.3">
            30&#37; &#45; Outstanding
          </option>
          <option value="0.2">
            20&#37; &#45; Good
          </option>
          <option value="0.15">
            15&#37; &#45; It was OK
          </option>
          <option value="0.1">
            10&#37; &#45; Bad
          </option>
          <option value="0.05">
            5&#37; &#45; Terrible
          </option>
        </select>
      </div>
    </div>

    <div id="people">
      <label for="peopleInput">
        How many people are sharing the bill?
      </label>
      <div>
        <input
          id="peopleInput"
          ref="peopleInputRef"
          type="text"
        />
        <span>
          people
        </span>
      </div>
    </div>

    <button
      id="calc"
      type="submit"
      v-on:click.prevent="handleSubmit"
    >
      Calculator
    </button>

    <div v-show="tip !== 0 ? true : false">
      <h1 id="text">TIP AMOUNT</h1>
      <h2 id="text">{{ tip }}</h2>
      <h2 id="text">each</h2>
    </div>
  </form>
</template>
<script>
  export default {
    data() {
      return {
        tip: 0
      };
    },
    methods: {
      handleSubmit: function() {
        const amount = parseInt(
          this.$refs.billInputRef.value
        );
        const service = parseFloat(
          this.$refs.serviceSelectRef.value
        );
        const people = parseInt(
          this.$refs.peopleInputRef.value
        );
        this.$data.tip = (amount * service) / people;
        this.$data.tip =
          Math.round(this.$data.tip * 100) / 100;
        this.$data.tip = this.$data.tip.toFixed(2);
      }
    }
  };
</script>
<style lang="scss">
  body {
    align-items: center;
    background: linear-gradient(
      to bottom,
      rgba(65, 15, 15, 1),
      rgba(14, 32, 45, 1),
      rgba(43, 45, 45, 1)
    );
    background-repeat: no-repeat;
    box-sizing: border-box;
    display: flex;
    height: 100vh;
    justify-content: center;
    margin: 0;
    padding: 0;
    width: 100vw;
  }
  #container {
    -moz-border-radius: 1rem;
    -webkit-border-radius: 1rem;
    background: #f7f7f7;
    border-radius: 1rem;
    box-shadow: 0 0 3px rgba(0, 0, 0, 0.1);
    height: max-content;
    text-align: center;
    padding: 0 2rem;
    width: max-content;
  }
  #title {
    padding-top: 0.3rem;
  }
  #bill {
    margin: 2rem 0;
  }
  #service {
    margin: 2rem 0;
  }
  #people {
    margin: 2rem 0;
  }
  #calc {
    -moz-border-radius: 1rem;
    -webkit-border-radius: 1rem;
    border-radius: 1rem;
    box-shadow: 0.1rem 0.2rem 0.2rem black;
    margin-bottom: 1rem;
    border: 0.1rem solid black;
    padding: 1rem;
    width: 100%;
  }
  #text {
    padding: 0;
    margin: 0;
  }
</style>
