<script setup>
import { ref } from "vue";

const showGame = ref(false);
const finalResult = ref();
const finalPlayer = ref();
const finalEnemy = ref();

const showBoard = () => {
  showGame.value = false;
}

const startGame = (value) => {
  showGame.value = true;
  const enemy = enemyTurn();
  finalPlayer.value = playerChose(value);
  finalEnemy.value = enemyChose(enemy);
  finalResult.value = whoWin(value, enemy);
  console.log(`player: ${value}, enemy ${enemy}`)
}

const enemyChose = (value) => {
  const cards = ['rock-enemy.svg', 'paper-enemy.svg', 'scissor-enemy.svg'];
  return cards[value];
}

const playerChose = (value) => {
  const cards = ['rock.svg', 'paper.svg', 'scissor.svg'];
  return cards[value];
}

const enemyTurn = () => {
  return Math.floor(Math.random() * 3);
}

const whoWin = (player, enemy) => {
  let result;

  // 0 = rock
  // 1 = paper
  // 2 = scissor

  if(player === enemy) {
    result = 'Draw';
  }
  else if(player === 0) {
    if(enemy === 2) {
      result = 'Player';
    }
    else if(enemy === 1) {
      result = 'Enemy';
    }
  }

  else if(player === 1) {
    if(enemy === 0) {
      result = 'Player';
    }
    else if(enemy === 2) {
      result = 'Enemy';
    }
  }

  else if(player === 2) {
    if(enemy === 1) {
      result = 'Player';
    }
    else if(enemy === 0) {
      result = 'Enemy';
    }
  }

  return result;
}
</script>

<template>
  <section class="section">
    <div class="title">
      <h1>Paper Rock Scissors Game</h1>
    </div>

    <div class="container">

      <div class="box">

        <div class="game" v-if="showGame">
          <div class="game__cards">
            <div class="game__card">
              <img :src="`/${finalPlayer}`" alt="player">
            </div>
            <div class="game__card">
              <img :src="`/${finalEnemy}`" alt="enemy">
            </div>
          </div>
          <h2 v-if="finalResult === 'Draw'">{{ finalResult }}</h2>
          <h2 v-else>{{ finalResult }} won</h2>
          <div class="game__btn" @click="showBoard">
            Again??
          </div>
        </div>

        <div class="board" v-else>
          <h2>Choose a card</h2>

          <div class="box__cards">
            <div class="box__card" @click="startGame(0)">
              <img src="/rock.svg" alt="rock">
            </div>
            <div class="box__card" @click="startGame(1)">
              <img src="/paper.svg" alt="paper">
            </div>
            <div class="box__card" @click="startGame(2)">
              <img src="/scissor.svg" alt="scissor">
            </div>
          </div>
        </div>
        </div>

    </div>
  </section>
</template>

<style scoped lang="scss">
.section {
  width: 100%;
}

.title {
  display: flex;
  width: 100%;
  justify-content: center;

  h1 {
    margin-top: 80px;
    font-size: 54px;
    letter-spacing: 1px;
    text-align: center;

    @media(max-width: 900px) {
      padding: 30px;
    }

    @media(max-width: 430px) {
      font-size: 44px;
    }
  }
}

.container {
  margin-top: 175px;
  display: flex;
  width: 100%;
  justify-content: center;

  @media(max-width: 900px) {
    padding: 30px 0 30px 0;
  }

  @media(max-width: 700px) {
    margin-top: 80px;
  }

  @media(max-width: 430px) {
    margin-top: 40px;
  }
}

.box {
  align-items: center;
  display: flex;
  flex-direction: column;

  .board {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  h2 {
    letter-spacing: 1px;
    font-size: 24px;
    font-weight: 400;
    margin-bottom: 50px;
  }

  &__cards {
    display: flex;
    justify-content: space-between;
    gap: 30px;
  }

  &__card {
    display: flex;
    border: 2px solid #2F2E41;
    border-radius: 13px;
    padding: 20px;
    justify-content: center;
    cursor: pointer;

    img {
      width: 30px;
    }
  }

  &__card:hover {
    background-color: #2F2E41;
  }

  .game {
    display: flex;
    flex-direction: column;
    align-items: center;

    &__btn {
      display: flex;
      border: 2px solid #2F2E41;
      border-radius: 13px;
      padding: 15px 25px;
      justify-content: center;
      cursor: pointer;
    }

    &__btn:hover {
      background-color: #2F2E41;
    }

    &__cards {
      display: flex;
      justify-content: center;
      gap: 30px;
    }

    &__card {
      display: flex;
      border: 2px solid #2F2E41;
      border-radius: 13px;
      padding: 20px;
      justify-content: center;

      img {
        width: 30px;
      }
    }
  }
}
</style>