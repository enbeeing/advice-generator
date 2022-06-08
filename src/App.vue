<template>
  <div class="advice-wrapper">
    <div v-if="advice">
      <p class="advice-num">Advice # {{ advice.id }}</p>
      <p class="advice-quote">‘‘{{ advice.advice }}’’</p>
    </div>
    <div v-else>
      <p class="advice-num">Advice</p>
      <p class="advice-quote">{{ loadingSymbol }}</p>
    </div>

    <span class="separator" v-if="mobile">
      <svg width="295" height="16" xmlns="http://www.w3.org/2000/svg">
        <g fill="none" fill-rule="evenodd">
          <path fill="#4F5D74" d="M0 8h122v1H0zM173 8h122v1H173z" />
          <g transform="translate(138)" fill="#CEE3E9">
            <rect width="6" height="16" rx="3" />
            <rect x="14" width="6" height="16" rx="3" />
          </g>
        </g>
      </svg>
    </span>
    <span class="separator" v-else>
      <svg width="444" height="16" xmlns="http://www.w3.org/2000/svg">
        <g fill="none" fill-rule="evenodd">
          <path fill="#4F5D74" d="M0 8h196v1H0zM248 8h196v1H248z" />
          <g transform="translate(212)" fill="#CEE3E9">
            <rect width="6" height="16" rx="3" />
            <rect x="14" width="6" height="16" rx="3" />
          </g>
        </g>
      </svg>
    </span>
  </div>

  <div class="dice-button" @click="rollNewAdvice">
    <img
      src="./assets/icon-dice.svg"
      alt="dice img, click and roll for new advice"
    />
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      advice: null,
      loadingSymbol: "...",
      mobile: window.innerWidth < 380,
    };
  },
  methods: {
    rollNewAdvice() {
      fetch("https://api.adviceslip.com/advice")
        .then((res) => res.json())
        .then((data) => {
          this.advice = data.slip;
        })
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Manrope:wght@500&display=swap");

:root {
  --main-font: "Manrope", sans-serif;

  --main-bg-color: hsl(218, 23%, 16%);
  --advice-wrapper-bg-color: hsl(217, 19%, 24%);
  --main-text-color: hsl(193, 38%, 86%);
  --accent-color: hsl(150, 100%, 66%);
  --shadow-color: hsla(218, 23%, 11%);
}

* {
  margin: 0;
  padding: 0;
}

body {
  height: 100vh;
  background: var(--main-bg-color);
  color: var(--main-text-color);
  text-align: center;
  font-family: var(--main-font);
  font-weight: 800;
  font-size: 1rem;
}

#app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.advice-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: var(--advice-wrapper-bg-color);
  border-radius: 10px;
  padding: 1rem 1.5rem;
  margin: 0 2rem;
  box-shadow: 0 0 5px var(--shadow-color);
}
p,
svg {
  margin-top: 1.5rem;
}
.advice-num {
  color: var(--accent-color);
  text-transform: uppercase;
  letter-spacing: 0.2rem;
  font-weight: normal;
  font-size: small;
}
.advice-quote {
  font-size: 28px;
}
.separator {
  margin-bottom: 3rem;
}

.dice-button {
  background: var(--accent-color);
  display: inline-flex;
  justify-content: center;
  align-items: center;
  padding: 1.2rem;
  border-radius: 50%;
  transform: translateY(-50%);
  transition: 0.2s;
}

/* active and hover */
.dice-button:hover,
.dice-button:active {
  box-shadow: 0 0 10px var(--accent-color);
  cursor: pointer;
}

/* desktop */
@media only screen and (min-width: 380px) {
  .advice-wrapper {
    max-width: 450px;
    padding: 1.2rem 2.5rem;
  }
  p {
    margin-top: 30px;
  }
  svg {
    margin-top: 40px;
  }
}
</style>
