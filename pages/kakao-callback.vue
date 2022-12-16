<template>
  <div>로그인 중...</div>
</template>

<script>
export default {
  name: "KakaoCallback",
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
  async mounted() {
    try {
      if (!this.$route.query.code) {
        return this.$route.push("/");
      }

      const body = {
        code: this.$route.query.code,
        domain: window.location.origin,
      };

      const response = await this.$axios.$post("/auth/kakao-login", body, {});
      console.log("response>>", response);
    } catch (error) {
      console.error(error);
    }
  },
};
</script>
