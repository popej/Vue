<template>
  <div class="claimWrapper">
    <h1 class="claim">SPACE WALK</h1>
    <p class="subclaim">
      Begin your jurney throught our amazing galaxy,
      and discover places you never even heard of.
    </p>
    <p class="subclaim">Type anything space-related to start</p>
  </div>
</template>
<script>
export default {
  name: "Claim"
};
</script>
<style lang="scss" scoped>
.claimWrapper {
  color: #fff;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.claim {
  font-size: 35px;
  margin: 0;

  @media (min-width: 768px) {
    font-size: 80px;
  }

  @media (min-width: 1024px) {
    font-size: 100px;
  }
}

.subclaim {
  margin: 20px 0 0;
  font-size: 13px;
  min-width: 300px;

  @media (min-width: 768px) {
    font-size: 23px;
    padding: 0 50px;
    letter-spacing: 1px;
  }
  @media (min-width: 1024px) {
    width: 770px;
  }
}
</style>
