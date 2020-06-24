<template>
  <div>
    <div class="top-row">
      <div class="top part">
        <img :src="selectedRobot.head.src" title="head" />
        <button @click="selectPreviosHead()" class="prev-selector">&#9668;</button>
        <button @click="selectNextHead()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img :src="selectedRobot.leftArm.src" title="left arm" />
        <button @click="selectPreviosLeftArm()" class="prev-selector">&#9650;</button>
        <button @click="selectNextLeftArm()" class="next-selector">&#9660;</button>
      </div>
      <div class="center part">
        <img :src="selectedRobot.torso.src" title="left arm" />
        <button @click="selectPreviosTorso()" class="prev-selector">&#9668;</button>
        <button @click="selectNextTorso()" class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img :src="selectedRobot.rightArm.src" title="left arm" />
        <button @click="selectPreviosRightArm()" class="prev-selector">&#9650;</button>
        <button @click="selectNextRightArm()" class="next-selector">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img :src="selectedRobot.base.src" title="left arm" />
        <button @click="selectPreviosBase()" class="prev-selector">&#9668;</button>
        <button @click="selectNextBase()" class="next-selector">&#9658;</button>
      </div>
    </div>
  </div>
</template>

<script>
import availabelParts from "../data/parts";

var getNextValidIndex = function(index, length) {
  const nextIndex = (index += 1);
  return nextIndex > length - 1 ? 0 : nextIndex;
};

var getPreviosValidIndex = function(index, length) {
  const nextIndex = (index -= 1);
  return nextIndex < 0 ? length - 1 : nextIndex;
};

export default {
  name: "RobotBuilder",
  data() {
    return {
      availabelParts,
      selectNextHeadIndex: 0,
      selectNextLeftArmIndex: 0,
      selectNextRightArmIndex: 0,
      selectNextTorsoIndex: 0,
      selectNextBaseIndex: 0
    };
  },
  computed: {
    selectedRobot() {
      return {
        head: availabelParts.heads[this.selectNextHeadIndex],
        leftArm: availabelParts.arms[this.selectNextLeftArmIndex],
        torso: availabelParts.torsos[this.selectNextTorsoIndex],
        rightArm: availabelParts.arms[this.selectNextRightArmIndex],
        base: availabelParts.bases[this.selectNextBaseIndex]
      };
    }
  },
  methods: {
    //Head
    selectNextHead() {
      this.selectNextHeadIndex = getNextValidIndex(
        this.selectNextHeadIndex,
        availabelParts.heads.length
      );
    },
    selectPreviosHead() {
      this.selectNextHeadIndex = getPreviosValidIndex(
        this.selectNextHeadIndex,
        this.availabelParts.heads.length
      );
    },
    //Left Arm
    selectPreviosLeftArm() {
      this.selectNextLeftArmIndex = getPreviosValidIndex(
        this.selectNextLeftArmIndex,
        this.availabelParts.arms.length
      );
    },
    selectNextLeftArm() {
      this.selectNextLeftArmIndex = getPreviosValidIndex(
        this.selectNextLeftArmIndex,
        this.availabelParts.arms.length
      );
    },
    //Right Arm
    selectPreviosRightArm() {
      this.selectNextRightArmIndex = getPreviosValidIndex(
        this.selectNextRightArmIndex,
        this.availabelParts.arms.length
      );
    },
    selectNextRightArm() {
      this.selectNextRightArmIndex = getPreviosValidIndex(
        this.selectNextRightArmIndex,
        this.availabelParts.heads.length
      );
    },
    //Torso
    selectPreviosTorso() {
      this.selectNextTorsoIndex = getPreviosValidIndex(
        this.selectNextTorsoIndex,
        this.availabelParts.torsos.length
      );
    },
    selectNextTorso() {
      this.selectNextTorsoIndex = getPreviosValidIndex(
        this.selectNextTorsoIndex,
        this.availabelParts.torsos.length
      );
    },
    //Base
    selectPreviosBase() {
      this.selectNextBaseIndex = getPreviosValidIndex(
        this.selectNextBaseIndex,
        this.availabelParts.heads.length
      );
    },
    selectNextBase() {
      this.selectNextBaseIndex = getPreviosValidIndex(
        this.selectNextBaseIndex,
        this.availabelParts.bases.length
      );
    }
  }
};
</script>

<style>
.part {
  position: relative;
  width: 165px;
  height: 165px;
  border: 3px solid #aaa;
}
.part img {
  width: 165px;
}
.top-row {
  display: flex;
  justify-content: space-around;
}
.middle-row {
  display: flex;
  justify-content: center;
}
.bottom-row {
  display: flex;
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
  z-index: 1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector,
.center .next-selector {
  opacity: 0.8;
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
</style>