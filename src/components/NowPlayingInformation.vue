<template>
    <div>
        <div id="titleHolder">
            <transition mode="out-in"><div v-if='showTitle' key='real' id="title">{{nowPlayInfo.title}}</div></transition>
        </div>
        <div id="textHolder">
            <transition mode="out-in">
                <div v-if="showTitle" id="album-artist">
                    <transition mode="out-in">
                        <div v-if="carousel" key="album">{{nowPlayInfo.album}}</div>
                        <div v-else key="artist">{{nowPlayInfo.artist}}</div>
                    </transition>
                </div>
            </transition>
        </div>
    </div>
</template>

<script>
export default {
  props: {
    nowPlayInfo: {
      type: Object
    },
    progress: {
      type: Object
    }
  },
  data() {
    return {
      show: false,
      carousel: false
    };
  },
  computed: {
    showTitle: function() {
      return !(this.progress.remaining < 3);
    }
  },
  created() {
    setInterval(() => {
      this.carousel = !this.carousel;
    }, 5000);
  }
};
</script>

<style scoped>
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s;
}
.v-enter,
.v-leave-to {
  opacity: 0;
}
.v-enter-to,
.v-leave {
  opacity: 1;
}
div {
  text-align: center;
  color: #3a3a45;
  font-size: 1.2em;
}
div#textHolder {
  min-height: 1.3em;
}
div#album-artist {
  min-height: 1em;
  font-weight: 100;
  white-space: nowrap;
  font-size: 0.8em;
  color: #999999;
}
div#title {
  white-space: nowrap;
  font-weight: normal;
  min-height: 1.3em;
}
div#titleHolder {
  min-height: 1.7em;
}
</style>
