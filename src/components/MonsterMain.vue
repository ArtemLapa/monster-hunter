<template>
  <b-container>
    <b-row class="mb-4">
      <div class="monster__health-wrapper">
        <b-col>
          <h3 class="text-center">{{ userData.character }}</h3>
          <b-progress-bar
            show-value
            :value="userData.hp"
            variant="success"
          ></b-progress-bar>
        </b-col>

        <b-col>
          <h3 class="text-center">
            {{ monsterData.character }}
          </h3>
          <b-progress-bar
            show-value
            :value="monsterData.hp"
            variant="success"
          ></b-progress-bar>
        </b-col>
      </div>
    </b-row>

    <b-row class="justify-content-md-center mb-5">
      <b-col cols="8">
        <div class="monster__btns-group">
          <button type="button" class="btn btn-primary mr-3" @click="commonHit">
            Hit!
          </button>
          <button type="button" class="btn btn-warning mr-3" @click="superHit">
            Super Hit!
          </button>
          <button type="button" class="btn btn-success mr-3" @click="heal">
            Heal
          </button>
          <button type="button" class="btn btn-danger mr-3">Surrend</button>
        </div>
      </b-col>
    </b-row>

    <b-row class="justify-content-md-center">
      <b-col cols="8">
        <h4 class="text-center mb-2">Fight Log</h4>
        <div class="monster__fight-log">
          <div
            class="monster__log-message monster__log-message--start-game"
            v-for="(log, index) in gameLogs"
            :key="index"
          >
            {{ log }}
          </div>
        </div>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  name: "MonsterMain",
  data: () => ({
    userData: {
      character: "User",
      hp: 100,
      minAttackRange: 7,
      maxAttackRange: 14,
      // healthPotion: 3,
    },
    monsterData: {
      character: "Monster",
      hp: 100,
      minAttackRange: 9,
      maxAttackRange: 16,
    },
    gameLogs: [],
  }),
  methods: {
    startGame() {
      this.userData.hp = 100;
      this.monsterData.hp = 100;
      this.userData.healthPotion = 3;
      this.gameLogs.push("Game Start");
    },

    commonHit() {
      this.userAttack();
      this.monsterAttack();
    },

    superHit() {
      this.userSuperAttack();
      this.monsterAttack();
    },

    heal() {
      if (this.monsterData.hp !== 0) {
        if (this.userData.hp < 100 && this.userData.hp > 0) {
          let health = this.calculateDamage(5, 20);
          this.userData.hp += health;
          this.gameLogs.push(`Player health on ${health} HP`);
        }
      }
    },

    userAttack() {
      let damage = this.calculateDamage(
        this.userData.minAttackRange,
        this.userData.maxAttackRange
      );
      this.monsterData.hp -= damage;
      this.gameLogs.push(`Player hit a monster ${damage} damage`);
    },

    monsterAttack() {
      let damage = this.calculateDamage(
        this.monsterData.minAttackRange,
        this.monsterData.maxAttackRange
      );
      this.userData.hp -= damage;
      this.gameLogs.push(`Monster hit a player ${damage} damage`);
    },

    userSuperAttack() {
      let damage = this.calculateDamage(9, 20);
      this.monsterData.hp -= damage;
      this.gameLogs.push(
        `Player made a Super Hit and deal ${damage} to damage`
      );
    },
    calculateDamage(min, max) {
      return Math.max(Math.floor(Math.random() * max + 1), min);
    },
  },
  created() {
    this.startGame();
  },
};
</script>

<style scoped lang="scss">
@mixin box-shadow() {
  -webkit-box-shadow: 0px 5px 10px 2px rgba(34, 60, 80, 0.2);
  -moz-box-shadow: 0px 5px 10px 2px rgba(34, 60, 80, 0.2);
  box-shadow: 0px 5px 10px 2px rgba(34, 60, 80, 0.2);
}

$monster: "monster";
.#{$monster} {
  &__health-wrapper {
    display: flex;
    width: 100%;
    padding: 20px;
    @include box-shadow();
  }

  &__btns-group {
    @include box-shadow();
    padding: 20px;
    display: flex;
    justify-content: center;
  }

  &__fight-log {
    @include box-shadow();
    padding: 10px 10px 20px 10px;
    height: auto;
    max-height: 400px;
    overflow-y: auto;
  }

  &__log-message {
    width: 100%;
    text-align: center;
    margin-bottom: 15px;
    &:last-child {
      margin-bottom: 0;
    }
    &--start-game {
      background-color: var(--info);
      color: var(--white);
    }
    &--user-hit {
      background-color: var(--blue);
    }
    &--user-superhit {
      background-color: var(--yellow);
    }
    &--user-heal {
      background-color: var(--green);
    }
    &--monster-hit {
      background-color: var(--red);
    }
  }
}
</style>
