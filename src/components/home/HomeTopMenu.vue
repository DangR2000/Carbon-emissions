<template>
  <el-row>
    <el-col :span="8">
      <div class="grid-content">
        <div class="logo">
          <img src="@/assets/imgs/home/logo/Basement Logo1.png" />
        </div>
        <div class="font">城区组团碳排放与用地布局关系模拟平台</div>
      </div>
    </el-col>
    <el-col :span="8">
      <div class="grid-content menu-main">
        <ul>
          <li
            v-for="(item,index) in menus"
            :class="index == currentIndex ? '' + 'on':''"
            @click="tabSelect(index,$event)"
            :key="index"
          >{{item.name}}</li>
        </ul>
      </div>
    </el-col>
    <el-col :span="8">
      <div class="grid-content top-end">
        <div class="zy-btn">
          <button :class="value == 'zh-CN' ? '' + 'br on':''" @click="switchLanguage('zh-CN')">zh</button>
          <button :class="value == 'en-US' ? '' + 'br on':''" @click="switchLanguage('en-US')">en</button>
        </div>
        <div class="login-btn">
          <router-link to="/login">
            <span v-show="login">登录</span>
          </router-link>
        </div>
      </div>
    </el-col>
  </el-row>
</template>

<script>
export default {
  name: "homeTopMenu",
  data() {
    return {
      logo: "",
      menus: [
        {
          name: "首页"
        },
        {
          name: "产品定位"
        },
        {
          name: "产品功能"
        },
        // {
        //   name: "关于我们"
        // }
      ],
      currentIndex: 0,
      login: true,
      value: this.$i18n.locale //为了把下拉框的默认值和全局变量的值一致，以此实现载入页面时显示的语言和数据配置一致
    };
  },
  mounted: function() {},
  methods: {
    tabSelect(index, e) {
      this.currentIndex = index;
      this.$emit("change", index);
    },
    switchLanguage(value) {
      this.value = value;
      if (value == "zh-CN") {
        this.$i18n.locale = "zh-CN";
      } else {
        this.$i18n.locale = "en-US";
      }
      this.$cookie.set(
        "DefaultLanguage",
        value, //
        {
          //
          expires: "30m" //默认cookie有效时间为30分钟
        }
      );
    }
  }
};
</script>

<style scoped lang="scss">
.grid-content {
  min-height: 36px;
}
.menu-main {
  ul {
    margin-top: 5px;
    display: block;
    overflow: hidden;
    li {
      float: left;
      margin: 0 50px;
      font-size: 16px;
      cursor: pointer;
    }
    li.on {
      color: #3c86d8;
    }
  }
}
.top-end {
  display: flex;
  justify-content: center;
  .zy-btn {
    display: flex;
    justify-content: center;
    height: 30px;
    width: 80px;
    border: 1px solid #3c86d8;
    border-radius: 4px;
    margin-right: 40px;
  }
  .zy-btn button {
    width: 40px;
    border-radius: 4px;
    text-align: center;
    font-size: 14px;
    color: #3c86d8;
    line-height: 30px;
  }
  .zy-btn button.on {
    background-color: #3c86d8;
    color: #fff;
  }
  .br {
    border-right: 1px solid #3c86d8;
  }
}
.login-btn {
  font-size: 16px;
  line-height: 30px;
  .el-icon-user-solid {
    font-size: 30px;
    color: #666;
  }
}
.grid-content {
  margin-left: 63px;
}
.logo img {
  float: left;
  width:40px
}
.font {
  float: left;
  font-size: 14px;
  padding-left: 7px;
  padding-top: 5.5px;
  color: #3c86d8;
  font-weight: bold;
}
</style>
