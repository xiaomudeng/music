<!--  -->
<template>
  <div class="music-content">
    <div class="music-content-left">
      <div class="content-left-list">
        <div class="left-list-item" v-for="item in songList" :key="item.id">
          <div class="list-item-left" @click="getSong(item.id)"></div>
          <div class="list-item-mid">{{ item.name }}</div>
          <div
            :class="[
              'list-item-right',
              { hidden: item.mvid === 0 ? true : false },
            ]"
          ></div>
        </div>
      </div>
    </div>
    <div class="music-content-mid"></div>
    <div class="music-content-right"></div>
  </div>
</template>

<script>
//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）
//例如：import 《组件名称》 from '《组件路径》';

export default {
  props: {
    songList: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  //import引入的组件需要注入到对象中才能使用
  components: {},
  data() {
    //这里存放数据
    return {};
  },
  //监听属性 类似于data概念
  computed: {},
  //监控data中的数据变化
  watch: {},
  //方法集合
  methods: {
    getSong: function (id) {
      this.$http
        .get("song/url", {
          params: {
            id: id,
          },
        })
        .then((res) => {
          console.log(res);
          let songUrl = res.data.data[0].url;
          this.$emit("geturl", songUrl);
        });
    },
  },
  //生命周期 - 创建完成（可以访问当前this实例）
  created() {},
  //生命周期 - 挂载完成（可以访问DOM元素）
  mounted() {},
  beforeCreate() {}, //生命周期 - 创建之前
  beforeMount() {}, //生命周期 - 挂载之前
  beforeUpdate() {}, //生命周期 - 更新之前
  updated() {}, //生命周期 - 更新之后
  beforeDestroy() {}, //生命周期 - 销毁之前
  destroyed() {}, //生命周期 - 销毁完成
  activated() {}, //如果页面有keep-alive缓存功能，这个函数会触发
};
</script>
<style lang='less' scoped>
.music-content {
  display: flex;
  .music-content-left {
    width: 200px;
    border-right: 1px dotted var(--themeColor);
    height: 480px;
    .content-left-list {
      overflow-y: scroll;
      height: 480px;
      .left-list-item:nth-child(odd) {
        background-color: rgba(224, 217, 217, 0.5);
      }
      .left-list-item {
        display: flex;
        align-items: center;
        justify-content: space-between;
        height: 50px;
        .list-item-left {
          width: 25px;
          height: 25px;
          background: url(/static/imgs/table.png) -18px -18px;
        }

        .list-item-mid {
          overflow: hidden;
          text-overflow: ellipsis;
          height: 30px;
          line-height: 30px;
          color: white;
          width: 150px;
          text-align: center;
        }
        .hidden {
          visibility: hidden;
        }
        .list-item-right {
          width: 30px;
          height: 20px;
          background: url(/static/imgs/table.png) left -45px;
        }
      }
    }
  }

  .music-content-mid {
    width: 400px;
    border-right: 1px dotted var(--themeColor);
    height: 480px;
  }

  .music-content-right {
    width: 200px;
    height: 480px;
  }
}
</style>