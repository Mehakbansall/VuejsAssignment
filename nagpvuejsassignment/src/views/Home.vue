<template>
    <div class="home-page">
      <!-- <div class="banner">
        <div class="container">
          <h1 class="logo-font">Buzzle</h1>
          <p>share your knowledge by sharing your articles.</p>
        </div>
      </div> -->

      <div class="container page">
        <div class="row">
          <div class="col-md-9">
              <div class="feed-toggle">
                <ul class="nav nav-pills outline-active">
                  <li class="nav-item">
                    <a class="nav-link">Your Feed</a>
                  </li>
                  <li class="nav-item">
                    <router-link
                  :to="{ name: 'home' }"
                  exact
                  class="nav-link"
                  active-class="active"
                >
                  Global Feed
                </router-link>
                  </li>
                </ul>
              </div>

              <ArticlePreview
              v-for="article in feed" :article="article" :key="article.slug"></ArticlePreview>
          </div>
          <div class="col-md-3">
            <div class="sidebar">
              <p>Popular Tags</p>
              <div class="tag-list">
                <a href="" class="tag-pill tag-default">programming</a>
                <a href="" class="tag-pill tag-default">javascript</a>
                <a href="" class="tag-pill tag-default">emberjs</a>
                <a href="" class="tag-pill tag-default">angularjs</a>
                <a href="" class="tag-pill tag-default">react</a>
                <a href="" class="tag-pill tag-default">mean</a>
                <a href="" class="tag-pill tag-default">node</a>
                <a href="" class="tag-pill tag-default">rails</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
import ArticlePreview from '@/components/ArticlePreview.vue';
import articles from '@/store/modules/articles';
import { Article } from '../store/models';

@Component({
  components: {
    ArticlePreview,
  },
})

export default class extends Vue {
  feed: Article[] = [];

  created() {
    articles.refreshFeed('global').then(() => {
      this.feed = articles.feed;
    });
  }
}

</script>
