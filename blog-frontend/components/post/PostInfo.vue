<template>
    <div class="post-info">
        <div class="info">
            <h1 class="title">{{title}}</h1>
            <div class="tags" v-if="tags" >
                <div class="tag" v-for="tag in tags" :key="tag">
                    <nuxt-link :to="{name: 'index', query: {tag: tag}}">#{{tag}}</nuxt-link>
                </div>
            </div>
            <div class="date" v-if="date !== 'Invalid date'">{{date}}</div>
        </div>
    </div>
</template>

<script>
import moment from "moment";
export default {
  props: ["title", "tags", "publishedDate"],
  computed: {
    date: {
      get() {
        return moment(this.$props.publishedDate).format("ll");
      }
    }
  }
};
</script>

<style lang="scss" scoped>
@import "@/assets/styles/utils.scss";

.post-info {
  background: $oc-blue-5;
  height: 24rem;
  display: flex;
  align-items: center;
  justify-content: center;

  .info {
    margin-top: -5rem; // 헤더 크기 만큼 위로
    width: 1024px;
    padding: 1rem;
    color: white;

    .title {
      font-weight: 300;
      font-size: 3rem;
      margin: 0;
      word-wrap: break-word; // 내용이 너무 길면 다음 줄에 작성
    }
    .tags {
      display: flex;
      margin-top: 1rem;
      font-size: 1.25rem;
      font-weight: 500;
      a {
        &:hover {
          text-decoration: underline;
        }
      }
      .tag + .tag {
        margin-left: 0.25rem; // 사이 여백
      }
    }
    .date {
      text-align: right;
      opacity: 0.75;
      font-style: italic;
      font-size: 1.25rem;
    }
  }

  @include media("<large") {
    .info {
      .title {
        font-size: 2rem;
      }
      .tags,
      .date {
        font-size: 1rem;
      }
      width: 100%;
    }
  }

  @include media("<medium") {
    height: auto;
    padding-bottom: 4rem;
    .info {
      padding-top: 0;
      margin: 0;

      .tags {
        margin-top: 0.25rem;
      }
      .tags,
      .date {
        font-size: 0.85rem;
      }
    }
  }
}
</style>