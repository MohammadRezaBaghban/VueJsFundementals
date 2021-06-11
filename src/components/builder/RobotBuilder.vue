<template>
  <div class="content">
    <button class="add-to-cart" @click="addToCart()">Add Cart</button>
    <div class="top-row">
      <div class="top part">
        <div class="robot-name">
          <br/>
            {{selectedRobot.head.title}}
            <span class="sale" v-if="selectedRobot.head.onSale">
              Sale
            </span>
          <br/>
        </div>
        <img :src="selectedRobot.head.src" title="head"/>
        <button @click="selectNextHead()" class="prev-selector">&#9668;</button>
        <button @click="selectPreviousHead()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img :src="selectedRobot.lArm.src" title="left arm"/>
        <button @click="selectNextLArm()" class="prev-selector">&#9650;</button>
        <button @click="selectPreviousLArm()" class="next-selector">&#9660;</button>
      </div>
      <div class="center part">
        <img :src="selectedRobot.body.src" title="left arm"/>
        <button @click="selectNextBody()" class="prev-selector">&#9668;</button>
        <button @click="selectPreviousBody()" class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img :src="selectedRobot.rArm.src" title="left arm"/>
        <button @click="selectNextRArm()" class="prev-selector">&#9650;</button>
        <button @click="selectPreviousRArm()" class="next-selector">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img :src="selectedRobot.Base.src" title="left arm"/>
        <button @click="selectNextBase()" class="prev-selector">&#9668;</button>
        <button @click="selectPreviousBase()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div>
      <table>
        <thead>
         <h1>Cart</h1>
          <tr>
            <th>Robot</th>
            <th class="cost">Cost</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(robot, index) in cart" :key="index">
            <td>{{robot.robot.head.title}}</td>
            <td>{{robot.cost}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import availableParts from '../data/data';

function getPreviousValidIndex(index, length) {
  const deprecatedIndex = index - 1;
  return deprecatedIndex < 0 ? length - 1 : deprecatedIndex;
}

function getNextValidIndex(index, length) {
  const incrementedIndex = index + 1;
  return incrementedIndex > length - 1 ? 0 : incrementedIndex;
}

export default {
  name: 'RobotBuilder',
  data() {
    return {
      availableParts,
      cart: [],
      maxNumberOfPictures: 4,
      selectedHeadIndex: 0,
      selectedRArmIndex: 0,
      selectedLArmIndex: 0,
      selectedBodyIndex: 0,
      selectedBasesIndex: 0,
    };
  },
  computed: {
    selectedRobot() {
      return {
        head: availableParts.heads[this.selectedHeadIndex],
        lArm: availableParts.arms[this.selectedLArmIndex],
        rArm: availableParts.arms[this.selectedRArmIndex],
        body: availableParts.torsos[this.selectedBodyIndex],
        Base: availableParts.bases[this.selectedBasesIndex],
      };
    },
  },
  methods: {
    addToCart() {
      const robot = this.selectedRobot;
      const cost = robot.head.cost + robot.lArm.cost
      + robot.rArm.cost + robot.body.cost + robot.Base.cost;
      const re = { robot, cost };
      this.cart.push(re);
      console.log(this.cart);
    },
    selectNextHead() {
      this.selectedHeadIndex = getNextValidIndex(
        this.selectedHeadIndex,
        this.maxNumberOfPictures,
      );
    },
    selectPreviousHead() {
      this.selectedHeadIndex = getPreviousValidIndex(
        this.selectedHeadIndex,
        this.maxNumberOfPictures,
      );
    },
    selectNextLArm() {
      this.selectedLArmIndex = getNextValidIndex(
        this.selectedLArmIndex,
        this.maxNumberOfPictures,
      );
    },
    selectPreviousLArm() {
      this.selectedLArmIndex = getPreviousValidIndex(
        this.selectedLArmIndex,
        this.maxNumberOfPictures,
      );
    },
    selectNextRArm() {
      this.selectedRArmIndex = getNextValidIndex(
        this.selectedRArmIndex,
        this.maxNumberOfPictures,
      );
    },
    selectPreviousRArm() {
      this.selectedRArmIndex = getPreviousValidIndex(
        this.selectedRArmIndex,
        this.maxNumberOfPictures,
      );
    },
    selectNextBody() {
      this.selectedBodyIndex = getNextValidIndex(
        this.selectedBodyIndex,
        this.maxNumberOfPictures,
      );
    },
    selectPreviousBody() {
      this.selectedBodyIndex = getPreviousValidIndex(
        this.selectedBodyIndex,
        this.maxNumberOfPictures,
      );
    },
    selectNextBase() {
      this.selectedBasesIndex = getNextValidIndex(
        this.selectedBasesIndex,
        this.maxNumberOfPictures,
      );
    },
    selectPreviousBase() {
      this.selectedBasesIndex = getPreviousValidIndex(
        this.selectedBasesIndex,
        this.maxNumberOfPictures,
      );
    },
  },
};
</script>

<style>
.part {
  position: relative;
  width:165px;
  height:165px;
  border: 3px solid #aaa;
}
.part img {
  width:165px;
}
.top-row {
  display:flex;
  justify-content: space-around;
}
.middle-row {
  display:flex;
  justify-content: center;
}
.bottom-row {
  display:flex;
  justify-content: space-around;
  border-top: none;
}
.head {
  border-bottom: none;
}
.left {
  border-right: none;
}
.right {
  border-left: none;
}
.left img {
  transform: rotate(-90deg);
}
.right img {
  transform: rotate(90deg);
}
.bottom {
  border-top: none;
}
.prev-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector, .center .next-selector {
  opacity:0.8;
}
.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  right: -3px;
}

.sale {

  color:Red
}

.robot-name {
  position: absolute;
  top: -25px;
  text-align: center;
  width:100%;
}
.content{
  position:relative
}
.add-to-cart{
  position: absolute;
  right:30px;
  width:220px;
  padding:3px;
  font-size:16px;
}
td, th{
  text-align:left;
  padding: 5px;
  padding-right: 20px;
}
.cost{
  text-align: right;
}
</style>
