<template>
  <div class="claim-wrapper">
    <h1 class="claim">
      spacer journey
    </h1>
    <p class="subclaim">
      Let's begin amazing journey through our universe and discover places you never even seen.
    </p>
    <p class="subclaim">
      Type anything space-related to begin journey.
    </p>
  </div>
</template>

<script>
export default {
  name: 'Claim',
};
</script>

<style lang="scss" scoped>
  .claim-wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-items: center;
    text-align: center;
    color: #fff;

    .claim {
      font-size: 50px;
      margin: 0;
      text-transform: uppercase;
      line-height: 1;

      @media (min-width: 768px) {
        font-size: 72px;
      }
    }

    .subclaim {
      margin: 20px 0 0 0;
      font-size: 14px;
      font-weight: 300;

      @media (min-width: 768px) {
        font-size: 18px;
        margin-top: 30px;
      }

      @media (min-width: 1024px) {
        font-size: 22px;
        margin-top: 40px;
      }
    }
  }
</style>
