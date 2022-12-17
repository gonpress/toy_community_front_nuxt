<template>
  <div>네이버 로그인 중...</div>
</template>

<script>
export default {
  name: "NaverCallback",
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

      const response = await this.$axios.$post("/auth/naver-login", body, {});
      console.log("response>>", response.access_token);
    } catch (error) {
      console.error(error);
    }
  },
};
</script>
