<template>
  <a @click="loginWithKakao">
    <img src="/kakao-login.png" />
  </a>
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
  },
  mounted() {
    this.initKakao();
  },
};
</script>
