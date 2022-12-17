<template>
  <div>
    <a @click="loginWithKakao">
      <img src="/kakao-login.png" />
    </a>
    <a @click="loginWithNaver">
      <img src="http://static.nid.naver.com/oauth/small_g_in.PNG" />
    </a>
  </div>
</template>

<script>
export default {
  name: "IndexPage",
  methods: {
    initKakao() {
      if (!Kakao.isInitialized()) {
        Kakao.init(process.env.KAKAO_LOGIN_JAVASCRIPT_KEY);
      }

      Kakao.isInitialized();
    },

    async loginWithKakao() {
      await Kakao.Auth.authorize({
        redirectUri: `${window.location.origin}/kakao-callback`,
      });
    },

    async loginWithNaver() {
      const clientId = "_HgrTuzxqgIF3Fxt5fbi";
      const redirectUri = `${window.location.origin}/naver-callback`;
      const state = "NAVER_LOGIN_TEST";
      const api_url = `https://nid.naver.com/oauth2.0/authorize?response_type=code&client_id=${clientId}&redirect_uri=${redirectUri}&state=${state}`;

      window.location.replace(api_url);
    },
  },
  mounted() {
    this.initKakao();
  },
};
</script>
