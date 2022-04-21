<template>
  <div id="top">
    <main>
      <h2>nekozuki.meブログパーツ</h2>
      <div class="input_area">
        <input
          type="text"
          name="url"
          id="input_url"
          placeholder="URLを入力してください"
          v-model="url"
        />
        <button type="submit" @click="url_submit()">実行</button>
      </div>
      <div class="result_area">
        <div class="item">
          <iframe
            width="100%"
            height="120px"
            src=""
            scrolling="no"
            style="border: solid 1px #ccc"
            frameborder="0"
          ></iframe>
          <button class="copybut" @click="copy">コピーする</button>
        </div>
      </div>
    </main>
    <footer>
      <small>&copy; 2022 AyumuNekozuki</small>
    </footer>
  </div>
</template>

<script>
export default {
  methods: {
    url_submit() {
      var input_url = this.url;

      document
        .querySelector(".item iframe")
        .setAttribute("src", "https://embed.nekozuki.me/thumb?url="+input_url);
    },
    copy(){
      var item = document.querySelector(".item iframe").outerHTML;
      navigator.clipboard.writeText(item);
    }
  },
};
</script>

<style lang="scss">
#top {
  min-height: 100vh;
  background: repeating-linear-gradient(
    -45deg,
    transparent,
    transparent 15px,
    #efefff 0,
    #efefff 30px
  );

  main {
    min-height: calc(100vh - 30px);
    padding: 3rem 0;

    h2 {
      text-align: center;
    }

    div {
      background: white;
      border-radius: 10px;
      margin: 1rem auto;
      padding: 1.5rem 2rem;
      max-width: 600px;
      width: calc(100% - 20px);
      box-shadow: 0 0 3px #7f7fff;

      &.input_area {
        display: flex;
        flex-direction: column;
        align-items: center;

        input {
          width: 100%;
          text-align: center;
          padding: 10px;
          border-radius: 10px;
          border: 1px solid #ccc;
          font-size: 18px;
        }
        button {
          margin-top: 0.5rem;
          padding: 3px 10px;
          background-color: #0080ff;
          color: white;
          font-weight: bold;
          border: none;
          border-radius: 5px;
          opacity: 1;
          transition: opacity ease 0.1s;
          cursor: pointer;

          &:hover {
            opacity: 0.8;
          }
        }
      }
    }
  }

  footer {
    display: flex;
    align-items: center;
    justify-content: center;

    background: #7f7fff;
    color: white;
    height: 30px;
    text-align: center;
  }
}
</style>