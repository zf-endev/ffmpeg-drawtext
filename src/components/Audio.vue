<template>
  <div>
    <b-form-group label="Audio Codec:" label-for="audio-codec">
      <b-form-select
        class="u-full-width"
        v-bind:value="value.codec"
        @input="update('codec', $event)"
      >
        <option :value="null" disabled>-- Please select an option --</option>
        <option v-for="o in filteredAudioCodecs" :key="o.id" :value="o.value">{{o.name}}</option>
      </b-form-select>
    </b-form-group>
  </div>
</template>

<script>
import config from '@/config';

const {
  codecs,
} = config;

export default {
  name: 'Audio',
  props: ['value', 'container'],
  data() {
    return {
      codecs,
    };
  },
  computed: {
    filteredAudioCodecs() {
      return this.codecs.audio.filter(
        o => !o.supported || o.supported.includes(this.container),
      );
    },
  },
  methods: {
    update(key, value) {
      this.$emit('input', { ...this.value, [key]: value });
    },
  },
};
</script>
