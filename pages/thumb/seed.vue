<template>
  <div id="seed_embed">
    <header>
      <div class="wrap">
        <div class="head">
          <a
            class="logo"
            href="https://seed.online/"
            target="_blank"
            rel="noopener noreferrer"
          >
            <img src="~/assets/logo/tso_logo_icon_col.png" alt="" srcset="" />
            <span>THE SEED ONLINE</span>
          </a>
        </div>
        <a
          href="https://embed.nekozuki.me/vcas"
          target="_blank"
          rel="noopener noreferrer"
        >
          非公式ブログパーツ
        </a>
      </div>
    </header>
    <div class="body" v-if="data.contents !== 'error'">
      <div class="thumb">
        <a target="_blank" rel="noopener noreferrer" :href="data.url">
          <img :src="data.image" :alt="data.title" srcset="" />
        </a>
      </div>
      <div class="text">
        <p v-if="data.type == 'VRM'" class="type vrm">VRM</p>
        <p v-if="data.type == 'VCI'" class="type vci">VCI</p>
        <p v-if="data.type == 'GLB'" class="type glb">GLB</p>
        <p v-if="data.contents == 'users'" class="type user">ユーザー</p>
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
          class="description"
          v-if="data.contents == 'products' || data.contents == 'users'"
        >
          {{ data.description }}
        </p>
      </div>
    </div>
    <div class="body" v-if="data.contents === 'error'">
      <div class="text">
        <p class="type error">ERROR!</p>
        <p class="title err">エラーが発生しました。</p>
        <p class="description">
          ページが見つからないか、内部でエラーが発生した可能性があります。少し時間を空けて再度お試しください。<br>
          何度も表示される場合は <a href="https://twitter.com/nekozuki_dev" target="_blank" rel="noopener noreferrer">@nekozuki_dev</a>までご連絡ください。
        </p>
      </div>
    </div>
  </div>
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

    if (data) {
      data.url = query.url;

      if (data.url.indexOf("products") !== -1) {
        data.contents = "products";
      } else if (data.url.indexOf("users") !== -1) {
        data.contents = "users";
      } else if (data.url.indexOf("items") !== -1) {
        data.contents = "items";
      } else {
        // 対象外のとき
        data.contents = "error";
      }

      if (data.contents == "products" || data.contents == "items") {
        //タイトルの最後のSEED表示を消す
        data.title = data.title.substr(0, data.title.length - 18);

        // タイトル・投稿者・タイプを分ける
        var dataarr = data.title.split("/");

        //タイプの無駄なスペースを消して格納
        data.type = dataarr[dataarr.length - 1].replace(" ", "");
        dataarr.splice(-1, 1);

        //投稿者の無駄なスペースを消して格納
        data.autor = dataarr[dataarr.length - 1].substr(
          0,
          dataarr[dataarr.length - 1].length - 1
        );
        data.autor = data.autor.substr(1);
        dataarr.splice(-1, 1);

        //残りを結合してタイトルに&いらない空白とコンマを削除
        data.title = dataarr.toString();
        data.title = data.title.substr(0, data.title.length - 1);
        data.title = data.title.replace(",", "");

        //詳細分の文字数を削る
        data.description = data.description.substring(0, 49) + "…";

      } else if (data.contents == "users") {
        data.title = data.title.substr(0, data.title.length - 28);
        data.description = data.description.substring(0, 49) + "…";
      }
    } else {
      var data = {};
      data.contents = "error";
    }

    return {
      data,
    };
  },
};
</script>

<style lang="scss" scoped>
#seed_embed {
  background: #fafafa;
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
      background: linear-gradient(to right, #48c8f5 0%, #3079de 100%);
    }
  }
  div.body {
    display: flex;
    align-items: flex-start;
    color: inherit;
    text-decoration: none;
    padding: 4px 8px;

    .thumb {
      width: 100px;
      height: 100px;
      aspect-ratio: 1 / 1;

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