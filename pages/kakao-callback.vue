<template>
  <div>카카오 로그인 중...</div>
</template>

<script>
export default {
  name: "KakaoCallback",
  methods: {},
  async mounted() {
    try {
      if (!this.$route.query.code) {
        return this.$router.push("/");
      }

      const body = {
        code: this.$route.query.code,
        domain: window.location.origin,
      };

      const response = await this.$axios.$post("/auth/kakao-login", body, {});
      console.log("response>>", response.access_token);
    } catch (error) {
      console.error(error);
    }
  },
};
</script>
