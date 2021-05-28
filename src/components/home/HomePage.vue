<template>
  <div class="home">
    <div>
      <img class="robot" src="../../assets/robot-home.png" aria-hidden="true">
    </div>
    <div>
      <a href="">Get Started</a>
      Building your first robot!
    </div>
    <div>
      <br/>
      <RobotBuilder/>
    </div>
  </div>
</template>

<script>

import RobotBuilder from '../builder/RobotBuilder.vue';

export default {
  components: {
    RobotBuilder,
  },
  name: 'HomePage',
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.home{
  text-align: center;

}
.robot{
  height: 300px;
}
</style>
