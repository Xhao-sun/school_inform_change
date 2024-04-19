<template>
  <el-collapse-transition>
    <div v-show="show">
      <el-row type="flex" justify="center" align="middle">
        <el-col type="flex" justify="center">
          <section class="showcase">
            <video src="../assets/1.mp4" muted loop autoplay></video>
            <div class="overlay"></div>
            <div class="text">
              <h2>Zzuli</h2>
              <h1 style="display: inline-block">郑州轻工业大学</h1>
              &nbsp;
              <p style="display: inline-block">校园信息发布平台</p>
              <br /><br />
              <p>
                郑州轻工业大学创建于1977年，原隶属于国家轻工业部，1998年转隶河南省人民政府。学校是河南省人民政府和国家烟草专卖局共建高校、河南省特色骨干大学建设高校、河南省国际化特色试点高校。学校牢固坚持社会主义办学方向，秉承“为之则易、不为则难”的校训精神和“朴实、务实、扎实”的校风，扎根中原大地，发挥优势特色，为国家、地方和行业高质量发展作出了积极贡献。学校现有科学校区、东风校区和禹州实习实训基地，占地面积2200余亩。有教职工2300余人，全日制本科生、研究生30000余人。各类中外文纸质图书245万册，电子图书861万册，建有“全国示范数字档案室”，获评河南省智慧校园建设示范学校。
              </p>
              <el-button @click="login()">登录/注册</el-button>
              <el-button type="success" @click="guest()">游客登录</el-button>
            </div>
          </section>
        </el-col>
      </el-row>
    </div>
  </el-collapse-transition>
</template>

<script>
// fade/zoom 等
import "element-ui/lib/theme-chalk/base.css";
// collapse 展开折叠
import CollapseTransition from "element-ui/lib/transitions/collapse-transition";
import Vue from "vue";
Vue.component(CollapseTransition.name, CollapseTransition);
export default {
  data: () => ({
    show: true,
  }),

  methods: {
    getCookie(cname) {
      var name = cname + "=";
      var ca = document.cookie.split(";");
      for (var i = 0; i < ca.length; i++) {
        var c = ca[i].trim();
        if (c.indexOf(name) == 0) return c.substring(name.length, c.length);
      }
      return "";
    },

    checkuserno() {
      var userno = this.getCookie("user_no");
      if (userno != "") {
        if (userno == 0) {
          console.log("游客已登录");
        } else {
          this.$router.push({ path: "/Wtbhome" });
        }
      }
    },

    login() {
      this.show = !this.show;
      document.cookie = "user_no=0";
      setTimeout(() => {
        this.$router.push({ path: "/Login" });
      }, 500);
    },

    guest() {
      this.show = !this.show;
      document.cookie = "user_no=0";
      setTimeout(() => {
        this.$router.push({ path: "/Wtbhome" });
      }, 500);
    },
  },
  mounted() {
    this.checkuserno();
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.showcase {
  position: absolute;
  right: 0;
  width: 100%;
  min-height: 100vh;
  padding: 100px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #000;
  color: #fff;
  z-index: 2;
  transition: 0.5s;
}
.text {
  position: relative;
  z-index: 10;
}

.text h1 {
  font-size: 5em;
  font-weight: 800;
  line-height: 1em;
  text-transform: uppercase;
}

.text h2 {
  font-size: 4em;
  font-weight: 700;
  line-height: 1em;
  text-transform: uppercase;
}

.text p {
  font-size: 1.1em;
  margin: 20px 0;
  font-weight: 400;
  max-width: 700px;
}
@media (max-width: 991px) {
  .showcase {
    padding: 40px;
  }

  .text h1 {
    font-size: 3em;
  }

  .text h2 {
    font-size: 2em;
  }
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: darkkhaki;
  /* background: gold; */
  mix-blend-mode: overlay;
}

.showcase video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0.8;
  object-fit: cover;
}
</style>