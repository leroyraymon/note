<template>
  <a-config-provider :locale="locale">
    <a-layout>
      <a-layout-header>
        <home-head></home-head>
      </a-layout-header>
      <a-layout class="content">
        <a-layout-content class="container">
          <nuxt></nuxt>
          <a-back-top />
        </a-layout-content>
      </a-layout>
      <!-- <a-layout-footer>
        <home-footer></home-footer>
      </a-layout-footer> -->
    </a-layout>
  </a-config-provider>
</template>

<script>
import HomeHead from "@/components/HomeHead/index";
import HomeFooter from "@/components/HomeFooter/index";
import jaJP from 'ant-design-vue/es/locale/ja_JP';
export default {
  transition: "page",
  components: { HomeHead, HomeFooter },
  data() {
    return {
      locale: jaJP,
    };
  }
};
</script>

<style scoped>
.content {
  background: #fff;
  padding: 60px 0 0 0;
  min-height: 90em;
}
.ant-layout-header {
  position: fixed;
  z-index: 1009;
  padding: 0;
  width: 100%;
  height: 50px;
}
.ant-back-top {
  bottom: 120px;
}
::v-deep .ant-back-top-content {
  height: 40px;
  width: 40px;
  line-height: 40px;
  border-radius: 4px;
}
.ant-layout-footer {
  background-color: #455a64;
}
</style>
