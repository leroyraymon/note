<template>
  <a-layout>
    <a-layout-content>
      <div class="margin-bottom">
        <a-skeleton :loading="blogLoading" style="float: left;" active>
          <div class="markdown-body">
            <h3 class="title">{{blogData.title}}</h3>
            <div v-html="blogData.body_html">{{blogData.body_html}}</div>
          </div>
        </a-skeleton>
      </div>
    </a-layout-content>
  </a-layout>
</template>

<script>
import HomeAside from "@/components/HomeAside/index";
import github from "@/assets/js/github.js";

export default {
  name: 'Detailed',
  layout: 'index',
  components: { HomeAside },
  data() {
    return {
      blogData: {
        created_at: null,
        user: {
          avatar_url: null
        }
      },
      blogLoading: true,
    };
  },
  mounted() {
    this.getBlog();
  },
  methods: {
    async getBlog() {
      let { data: post } = await github.issues.get({
        owner: process.env.owner,
        repo: process.env.repo,
        issue_number: this.$route.query.number,
        headers: {
          Accept: 'application/vnd.github.v4.html'
        }
      });
      this.blogData = post;
      this.blogLoading = false;
    }
  }
}
</script>

<style scoped>
.markdown-body {
  min-height: 90px;
  /* padding: 20px; */
  width: 100%;
  font-size: 12px;
}
.markdown-body .title {
  text-align: center;
  font-size: 14px;
  font-weight: bold;
  margin-bottom: 10px;
}
::v-deep .markdown-body pre {
  padding: 16px;
  overflow: auto;
  line-height: 1.45;
  background-color: #f6f8fa;
  border-radius: 3px;
}
::v-deep .markdown-body code {
  border-radius: 3px;
  background-color: #f6f8fa;
}
::v-deep .markdown-body h3 {
  font-size: 16px;
  margin-top: 10px;
  margin-bottom: 16px;
  font-weight: 600;
  line-height: 1.25;
}
::v-deep .markdown-body ol,
::v-deep .markdown-body ul {
  padding-left: 2em;
  margin-top: 0;
  margin-bottom: 16px;
}
</style>
