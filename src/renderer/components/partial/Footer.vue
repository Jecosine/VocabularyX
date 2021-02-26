<!--
 * @Date: 2021-02-06 20:59:43
 * @LastEditors: Jecosine
 * @LastEditTime: 2021-02-26 20:46:48
-->
<template>
  <div id="footer-container">
    <div id="clock-container" class="widget-container">
      <font-awesome-icon :icon="['far','clock']" class="widget-icon"></font-awesome-icon>
      <!-- todo 24h / 12h settings -->
      <div class="widget-content-container">{{timeStr}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'footerbar',
  props: {
    widgetList: {
      type: Object,
      required: false,
      default: () => {
        return {
          'clock': true
        }
      }
    }
  },
  computed: {
    // timeStr () {
    //   return this.currentTime.toLocaleTimeString('en', {hour12: true})
    // }
  },
  data () {
    return {
      // timer
      // calibration: false,
      currentTime: new Date(),
      timeStr: '',
      timer: -1,
      // config get from settings
      // all the other settings inherit from default
      scopeMapper: {
        'default': {
          'clock': true,
          'today': true,
          'overview': true
        },
        'main': {

        },
        'word': {
          'wordStatus': true
        },
        'notebook': {
          'notebookStatus': true
        }
      }
    }
  },
  watch: {
    $route (to, from) {
      if (to.widgetScope !== from.widgetScope) {
        // todo change widget
      }
    }
  },
  mounted () {

  },
  created () {
    let that = this
    this.$nextTick(() => {
      // todo more accuracy
      that.timer = setInterval(() => {
        if (that.currentTime) {
          that.currentTime.setTime(Date.now())
          that.timeStr = that.currentTime.toLocaleTimeString('en', {hour12: true})
        }
      }, 1000)
    })
  }
}
</script>

<style scoped>
@import '../../theme/base.css';
#footer-container {
  position: relative;
  width: 100%;
  height: 100%;
}
.widget-container {
  position: relative;
  box-sizing: border-box;
  height:100%;
  line-height: 100%;
  padding: 0.1rem 0.6rem;
  user-select: none;
}
.widget-container {
  position: relative;
  width: 10rem;
  height: 100%;
  display: flex;
  flex-direction: row;
  align-items: center;
}
.widget-content-container {
  color: var(--color-text-secondary);
  font-size: 1rem;
  font-weight: regular;
  line-height: 100%;
  margin-left: 1rem;
}
.widget-icon {
  color: var(--color-text-secondary );
}
#clock-container {
  float: right;
}
</style>