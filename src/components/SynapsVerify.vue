<template>
  <iframe
    :src="url"
    :style="{
      'min-width': '400px',
      'min-height': '687px',
    }"
    class="root"
    allow="microphone; camera; midi; encrypted-media; usb; ethereum"
    allowfullscreen="true"
    frameBorder="none"
  />
</template>

<script>
const serviceUrl = {
  individual: "https://verify.synaps.io",
  corporate: "https://verify-v3.synaps.io",
};
export default {
  name: "SynapsVerify",
  props: {
    sessionId: {
      type: String,
    },
    service: {
      type: String,
    },
    onReady: {
      type: Function,
    },
    onFinish: {
      type: Function,
    },
    color: {
      type: Object,
    },
    lang: {
      type: String,
    },
    tier: {
      type: Number,
    },
    withFinishButton: {
      type: Boolean,
    },
  },
  computed: {
    url() {
      const { sessionId, service, color, lang, tier, withFinishButton } = this;
      const params = {
        service,
        session_id: sessionId,
        primary_color: color ? color.primary : undefined,
        secondary: color ? color.secondary : undefined,
        lang: lang ? lang : "en",
        tier: tier ? tier : undefined,
        with_finish_button: withFinishButton,
      };
      return `${serviceUrl[service]}?${Object.keys(params)
        .reduce((acc, key) => {
          if (params[key]) {
            acc.push(`${key}=${params[key]}`);
          }
          return acc;
        }, [])
        .join("&")}`;
    },
  },
  methods: {
    _listernerMessage({ data }) {
      if (data.type === "ready") {
        this.$emit(data.type);
      } else if (data.type === "finish") {
        this.$emit(data.type);
      }
    },
  },
  mounted() {
    window.addEventListener("message", this._listernerMessage);
  },
  unmounted() {
    window.removeEventListener("message", this._listernerMessage);
  },
};
</script>
