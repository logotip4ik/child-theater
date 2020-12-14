<template>
  <nav>
    <h1>Дитячий театр</h1>

    <div class="navigation">
      <p @click="currTab = 0">1 Сторінка</p>
      <p @click="currTab = 1">2 Сторінка</p>
      <p @click="currTab = 2">3 Сторінка</p>
    </div>
    <div class="icon" @click="menu = !menu">
      <div class="top"></div>
      <div class="middle"></div>
      <div class="bottom"></div>
    </div>
  </nav>
  <div :class="{ menu: true, show: menu }">
    <h2 @click="setTab(0)">1 Сторінка</h2>
    <h2 @click="setTab(1)">2 Сторінка</h2>
    <h2 @click="setTab(2)">3 Сторінка</h2>
  </div>
  <transition mode="out-in" name="fade">
    <div class="tab" v-if="currTab === 0">
      <h2>Івасик телесик</h2>
      <video src="./assets/Івасик-Телесик(1989).mp4" controls></video>
    </div>
    <div class="tab" v-else-if="currTab === 1">
      <h2>Капітошка</h2>
      <video src="./assets/Капітошка(1980).mp4" controls></video>
    </div>
    <div class="tab" v-else-if="currTab === 2">
      <div class="item" v-for="(item, idx) in music" :key="idx">
        <h2>{{ item.name }}</h2>
        <audio :src="item.src" controls></audio>
      </div>
    </div>
  </transition>
</template>

<script>
import { ref } from 'vue';
import vovkIBusel from './assets/Вовк-і-бусел.mp3';
import vovkIKit from './assets/Вовк-і-Кіт.mp3';
import zayazHolod from './assets/Заячий-холодок.mp3';
import lisizaIZapUYami from './assets/Лисиця-і-Цап-у-ямі.mp3';
import svatIDisvchina from './assets/Сват-і-кмітлива-дівчина.mp3';
import simLozin from './assets/Сім-лозин.mp3';
import voronaUkralaKorovu from './assets/Як-ворона-украла-корову.mp3';

export default {
  name: 'App',
  setup() {
    const currTab = ref(0);
    const menu = ref(false);

    const music = ref([
      {
        name: 'Вовк і бусел',
        src: vovkIBusel,
      },
      {
        name: 'Вовк і Кіт',
        src: vovkIKit,
      },
      {
        name: 'Заячий холодок',
        src: zayazHolod,
      },
      {
        name: 'Лисиця і Цап у ямі',
        src: lisizaIZapUYami,
      },
      {
        name: 'Сват і кмітлива дівчина',
        src: svatIDisvchina,
      },
      {
        name: 'Сім лозин',
        src: simLozin,
      },
      {
        name: 'Як ворона украла корову',
        src: voronaUkralaKorovu,
      },
    ]);

    function setTab(tab) {
      currTab.value = tab;
      menu.value = false;
    }

    return {
      currTab,
      menu,
      music,
      setTab,
    };
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell,
    'Open Sans', 'Helvetica Neue', sans-serif;
  min-height: 100vh;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  overflow-x: hidden;
  position: relative;

  nav {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #18181e;
    padding: 0.75rem 1rem;
    color: white;
    box-shadow: 0 10px 10px rgba($color: #000000, $alpha: 0.2);

    .navigation {
      display: flex;
      gap: 2rem;

      p {
        cursor: pointer;
      }
    }
    .icon {
      display: none;
      height: 1.4rem;
      position: relative;
      width: 1.9rem;
      transform: rotateZ(0);
      z-index: 1000;

      div {
        background-color: whitesmoke;
        height: 2px;
        left: 0;
        position: absolute;
        width: 100%;

        &.middle {
          top: 50%;
          transform: translateY(-50%);
        }

        &.bottom {
          bottom: 0;
        }
      }
    }
  }

  .menu {
    display: none;
    position: absolute;
    z-index: 100;
    top: 0;
    bottom: 0;
    right: 0;
    background: #18181e;
    width: 150px;
    color: whitesmoke;
    padding-top: 3rem;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    box-shadow: -10px 0 10px rgba($color: #000000, $alpha: 0.2);
    transform: translateX(150px);
    transition: transform 150ms ease-out;

    &.show {
      transform: translateX(0);
    }

    h2 {
      cursor: pointer;
      font-weight: 200;
      margin-bottom: 1rem;
    }
  }

  .tab {
    max-width: 800px;
    margin: 2rem auto;
    display: flex;
    flex-direction: column;
    padding: 1rem;
    box-shadow: 0 0 10px rgba($color: #000000, $alpha: 0.2);
    border-radius: 0.25rem;

    .item audio {
      width: 100%;
      margin-bottom: 2rem;
    }

    h2 {
      margin-bottom: 1rem;
    }
    video {
      margin-bottom: 1rem;
    }
  }
}

@media (max-width: 580px) {
  nav > .navigation {
    display: none !important;
  }
  .menu {
    display: flex !important;
  }
  .icon {
    display: block !important;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
