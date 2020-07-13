<template>
  <div class="drawer-container">
    <div class="drawer-button">
      <el-button @click="drawer=true" icon="el-icon-caret-bottom" circle></el-button>
    </div>
    <el-drawer :with-header="false" :visible.sync="drawer" :direction="direction">
      <div class="button-div">
        <div v-for="color in colors" :key="color">
          <div class="theme-container">
            <i :class="getIcon(color)"></i>
            <div>
              <div>
                <el-button
                  size="mini"
                  :style="{width:'100%', marginBottom:'2%'}"
                  @click.stop="changeTheme(color)"
                  type="primary"
                >Apply Theme</el-button>
              </div>
              <div>
                <el-button
                  @click.stop="modal=true"
                  size="mini"
                  :style="{width:'100%'}"
                  type="secondary"
                >Customize Theme</el-button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </el-drawer>
    <el-dialog title="Tips" :visible.sync="modal" width="30%">
      <span>This is a message</span>
      <span slot="footer" class="dialog-footer">
        <el-button @click="modal = false">Cancel</el-button>
        <el-button type="primary" @click="modal = false">Confirm</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      drawer: false,
      modal: false,
      direction: "ttb",
      colors: ["system", "light", "dark", "sepia"],
      currentTheme: this.$colorMode.preference
    };
  },
  mounted() {
    var allCSS = [].slice
      .call(document.styleSheets)
      .reduce(function(prev, styleSheet) {
        if (styleSheet.cssRules) {
          return (
            prev +
            [].slice.call(styleSheet.cssRules).reduce(function(prev, cssRule) {
              if (cssRule.selectorText == ".dark-mode") {
                var css = cssRule.cssText.split("{");
                css = css[1].replace("}", "").split(";");
                for (var i = 0; i < css.length; i++) {
                  var prop = css[i].split(":");
                  if (prop.length == 2 && prop[0].indexOf("--") == 1) {
                    console.log("Property name: ", prop[0]);
                    console.log("Property value:", prop[1]);
                  }
                }
              }
            }, "")
          );
        }
      }, "");

    let para = document.getElementsByClassName(
      this.$colorMode.value + "-mode"
    )[0];
    // para.style.setProperty("--bg", "pink");
    // let para = document.getElementsByClassName(
    //   this.$colorMode.value + "-mode"
    // )[0];
    // console.log(window.getComputedStyle(para), "*** parta");
    // console.log(
    //   window.getComputedStyle(para).getPropertyValue("--color-primary"),
    //   "*** colo r mde"
    // );
    // console.log(this.$colorMode.value, "*** pre");
  },
  methods: {
    getIcon(color) {
      let colorIcon = {
        light: "el-icon-sunny",
        dark: "el-icon-moon",
        sepia: "el-icon-coffee-cup",
        system: "el-icon-monitor"
      };
      return colorIcon[color];
    },
    previewTheme(mode, color) {
      setTimeout(() => {
        let colorChosen = mode === 1 ? color : this.currentTheme;
        this.$colorMode.preference = colorChosen;
      }, 500);
    },
    changeTheme(color) {
      this.$colorMode.preference = color;
      this.currentTheme = color;
      setTimeout(() => {
        this.drawer = false;
      }, 500);
    }
  }
};
</script>
<style>
i {
  font-size: 40px;
}
.theme-container {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 200px;
  justify-content: space-around;
  border-radius: 5%;
  cursor: pointer;
}
.drawer-button {
  display: flex;
  width: 100%;
  justify-content: center;
}
.button-div {
  display: flex;
  padding: 2%;
  justify-content: space-between;
  height: 100%;
}
.button-nuxt {
  width: 200px;
}
</style>
