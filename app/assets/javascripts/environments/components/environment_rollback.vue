<script>
/**
 * Renders Rollback or Re deploy button in environments table depending
 * of the provided property `isLastDeployment`.
 *
 * Makes a post request when the button is clicked.
 */
import eventHub from '../event_hub';
import loadingIcon from '../../vue_shared/components/loading_icon.vue';

export default {
  props: {
    retryUrl: {
      type: String,
      default: '',
    },

    isLastDeployment: {
      type: Boolean,
      default: true,
    },
  },

  components: {
    loadingIcon,
  },

  data() {
    return {
      isLoading: false,
    };
  },

  methods: {
    onClick() {
      this.isLoading = true;

      eventHub.$emit('postAction', this.retryUrl);
    },
  },
};
</script>
<template>
  <button
    type="button"
    class="btn"
    @click="onClick"
    :disabled="isLoading">

    <span v-if="isLastDeployment">
      Re-deploy
    </span>
    <span v-else>
      Rollback
    </span>

    <loading-icon v-if="isLoading" />
  </button>
</template>
