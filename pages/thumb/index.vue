<template>
  <a id="embed" :href="data.url" target="_blank" rel="noopener noreferrer">
    <header>
      <div class="wrap">
        <div class="head">
          {{data.url}}
        </div>
      </div>
    </header>
    <div class="body">
      <div class="thumb">
        <a target="_blank" rel="noopener noreferrer" :href="data.url">
          <img :src="data.image" :alt="data.title" srcset="" />
        </a>
      </div>
      <div class="text">
        <div>
          <a
            class="title"
            target="_blank"
            rel="noopener noreferrer"
            :href="data.url"
            >{{ data.title }}</a
          >
        </div>
        <p class="autor">{{ data.autor }}</p>
        <p
          class="description">
          {{ data.description }}
        </p>
      </div>
    </div>
  </a>
</template>

<script>
export default {
  layout: "thumb",
  async asyncData({ $axios, query }) {
    var data = await $axios
      .$get(`/api_nekozukiogp/ogp?url=${query.url}`)
      .catch((error) => {
        console.log(error);
      });

    data.url = query.url;

    return {
      data,
    };
  },
};
</script>

<style lang="scss" scoped>
#embed {
  display: block;
  background: white;
  color: #252525;
  text-decoration: none;

  header {
    background: white;
    width: 100%;
    height: 17px;
    font-weight: bold;
    margin-bottom: 5px;

    .wrap {
      width: 100%;
      height: 17px;
      display: flex;
      justify-content: space-between;

      .head {
        height: 17px;
        display: flex;
        justify-content: space-between;
        font-size: 12px;

        a {
          color: inherit;
          text-decoration: none;
          font-size: 11px;
          display: flex;
          align-items: center;
          position: relative;
        }

        img {
          min-height: 16px;
          min-width: 16px;
          height: 100%;
          aspect-ratio: 1 / 1;
          object-fit: contain;
          margin-right: 3px;
        }
      }

      a {
        color: inherit;
        text-decoration: none;
        font-size: 11px;
        display: flex;
        align-items: center;
      }
    }

    &::after {
      content: "";
      display: block;
      height: 2px;
      background: #7f7fff;
    }
  }
  div.body {
    display: flex;
    align-items: flex-start;
    color: inherit;
    text-decoration: none;
    padding: 4px 8px;

    .thumb {
      width: 160px;
      height: 90px;
      aspect-ratio: 16 / 9;

      img {
        width: 100%;
        height: 100%;
        object-fit: contain;
        border: 1px solid #999;
        background: white;
      }
    }

    .text {
      width: 212px;
      height: auto;
      flex: 1;
      padding-left: 5px;
      overflow: hidden;
      * {
        font-size: 14px;
      }

      .type {
        display: inline-block;
        font-size: 9px;
        font-weight: bold;
        padding: 2px 3px;
        margin: 0;

        &.vrm {
          background: #ee9c00;
          color: white;
        }
        &.vci {
          background: #3dc87c;
          color: white;
        }
        &.glb {
          background: #d36db6;
          color: white;
        }
        &.user {
          background: linear-gradient(to right, #48c8f5 0%, #3079de 100%);
          color: white;
        }
        &.error {
          background: #f00;
          color: white;
        }
      }

      .title {
        color: #0080ff;
        text-decoration: underline;
        font-weight: bold;

        &:not(.err):hover {
          background: #0080ff;
          color: white;
        }
      }

      .autor {
        font-size: 12px;
        font-weight: bold;
      }
      .description {
        margin-top: 3px;
        line-height: 14px;
        font-size: 10px;
        *{
          line-height: 14px;
          font-size: 10px;
        }
      }
    }
  }
}
</style>