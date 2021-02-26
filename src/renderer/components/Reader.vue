<!--
 * @Date: 2021-02-20 18:27:52
 * @LastEditors: Jecosine
 * @LastEditTime: 2021-02-21 20:22:41
-->
<template>
  <el-container id="reader-container">
    <el-main id="reader-main">
      <Word word="currentWord"/>
      <div id="unfold-button">
        <font-awesome-icon :icon="['fas',unfold ? 'arrow-right' : 'arrow-right']"></font-awesome-icon>
      </div>
      <div id="reader-aside" v-show="unfold">
        
      </div>
      <!-- catalog -->
      

    </el-main>
    
  </el-container>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      currentWord: '',
      unfold: true,
      notebookData: {}
    }
  },
  methods: {
    async fetchNotebook () {
      let that = this
      if (this.name) {
        this.notebookData = await this.$db.models.Notebook.findOne({
          where: {
            name: that.name
          },
          attributes: ['id', 'name', 'count']
        })
      }
    }
  },
  watch: {
    $route (to, from) {
      if (to.path !== from.path) {
        this.fetchNotebook()
      }
    }
  },
  mounted () {
    // todo render aside catalog
    // ...
    // test
  },
  created () {
    let that = this
    // todo get notebook data
    this.fetchNotebook()
    // todo get last record
    // ...
  }
}
</script>

<style scoped>
#reader-container {
  width: 100%;
  height: 100%;
}
#reader-main {
  background-color: aqua;
  padding: 0;
  margin: 0;

}
#unfold-button {
  width: 0.5rem;
  height: 5rem;

}
#reader-aside {
  width: 10rem;
  height: 100%;
  background-color: beige;
}
.catalog-container {
  
  height: 100%;
}
</style>