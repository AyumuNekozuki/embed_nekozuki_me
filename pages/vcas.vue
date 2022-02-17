<template>
  <div id="vcastop">
    <main>
      <h2>バーチャルキャスト非公式ブログパーツ</h2>
      <div class="input_area">
        <input
          type="text"
          name="url"
          id="input_url"
          placeholder="URLを入力してください"
        />
        <button type="submit" @click="url_submit()">実行</button>
      </div>
      <div class="result_area">
        <div class="item">
          <iframe width="312" height="176" src="https://embed.nekozuki.me/thumb/vcas?url=" scrolling="no" style="border:solid 1px #ccc;" frameborder="0"></iframe>
        </div>  
        <div class="item">
          <iframe width="312" height="176" src="https://embed.nekozuki.me/thumb/seed?url=" scrolling="no" style="border:solid 1px #ccc;" frameborder="0"></iframe>
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
    url_submit(){
      
    }
  }
};
</script>

<style lang="scss">
#vcastop {
  min-height: 100vh;
  background: repeating-linear-gradient(
    -45deg,
    transparent,
    transparent 15px,
    #E6F4FF 0,
    #E6F4FF 30px
  );

  main {
    min-height: calc(100vh - 30px);
    padding: 3rem 0;

    h2 {
      text-align: center;
    }

    &> div {
      background: white;
      border-radius: 10px;
      margin: 1rem auto;
      padding: 1.5rem 2rem;
      max-width: 700px;
      width: calc(100% - 20px);
      box-shadow: 0 0 3px #3079de;

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

      &.result_area{
        display: flex;
        justify-content: space-between;
      }
    }
  }

  footer {
    display: flex;
    align-items: center;
    justify-content: center;

    background: #3079de;
    color: white;
    height: 30px;
    text-align: center;
  }
}
</style>