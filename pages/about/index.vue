<template>
  <div class="about flexc">
    <img :src="outerwilds" alt="bg" />
    <div class="flexc paragraphs">
      <p v-for="p in paragraphs">{{ p }}</p>
    </div>
    <div class="status">
      Last build &lt;
      <a target="_blank" :href="commitUrl">{{ sha }}</a>&gt; successed at
      <time>{{ buildTime }}</time>
    </div>
  </div>
</template>

<script>
import outerwilds from "~/assets/image/outerwilds.jpg";
import config from "@/config";
import { inBrowser } from "~/utils/utils";

export default {
  name: "index",
  head() {
    return {
      title: "关于",
    };
  },
  asyncData({ env }) {
    return {
      sha: env.NUXT_ENV_CURRENT_GIT_SHA || "Unknown",
    };
  },
  async created() {
    if (inBrowser) {
      this.buildTime = await (await fetch("/timestamp.txt")).text();
    }
  },
  computed: {
    commitUrl() {
      return `https://github.com/${config.githubName}/${config.githubRepo}/commit/${this.sha}`;
    },
  },
  data() {
    return {
      outerwilds,
      buildTime: "Unkown",
      paragraphs: [
        "再次联系是高三因病休学",
        "你的语气依然灵动可爱",
        "许久不见想看你的照片",
        "于是无聊就翻你的朋友圈",
        "第一句话是回答我的问题",
        "你还是迟疑着问了我的目的",
        "我一句带过其实只是想你",
        "因为思念开始发酵彻夜难熬",
        "甚至身上开始出现许多病状",
        "我从不后悔再次爱你的决定",
        "但是如果再次回到那年夏天",
        "我依旧会等到现在再去爱你",
        "——2022.10.12",
      ],
    };
  },
};
</script>

<style lang="scss">
@import "assets/style/var";
.in-about {
  #header {
    background: rgba($background, 0.1);
    backdrop-filter: blur(1px);
  }
  #body {
    padding-top: 0;
    .about {
      width: 100vw;
      height: calc(100vh - #{$footer-height});
      padding-bottom: $footer-height;
      position: relative;
      font-family: $font-source-han-sans;
      img {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
        object-position: right;
        z-index: 1;
      }
      .paragraphs {
        position: relative;
        z-index: 2;
        padding-top: 100px + $header-height;
        justify-content: center;
        p {
          font-size: 16px;
          letter-spacing: 0.8px;
          color: white;
          font-weight: 300;
          &:not(:last-of-type) {
            margin-bottom: 20px;
          }
        }
      }
      .status {
        color: #eeeeee;
        opacity: 0.5;
        font-size: 13px;
        position: absolute;
        bottom: 10px;
        right: 10px;
        z-index: 1;
        transition: $common-transition;
        &:hover {
          opacity: 1;
        }
        time {
          color: #ffb350;
        }
      }
    }
  }
  #footer {
    position: fixed;
    width: 100%;
    left: 0;
    bottom: 20px;
    z-index: 2;
    .middle {
      color: #a1a1a1;
    }
    &:hover {
      .middle {
        color: #e7e7e7;
      }
    }
  }
  #footer,
  #body .about {
    a[href] {
      color: #49b6a3;
      transition: $common-transition;
      &:hover {
        color: #50e5d4;
      }
    }
  }
}
</style>
