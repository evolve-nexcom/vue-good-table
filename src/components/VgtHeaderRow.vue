<template>
<tr>
  <th
    class="vgt-row-header vgt-row-header-toggle"
    v-if="childrenVisibilityToggle">
    <button
      class="vgt-children-visibility-toggle"
      @click="toggleChildrenVisibility">
      {{headerRow.childrenVisible ? '-' : '+'}}
    </button>
  </th>
  <th
    v-if="headerRow.mode === 'span'"
    class="vgt-left-align vgt-row-header"
    :colspan="fullColspan">
    <slot
      :row="headerRow"
      name="table-header-row">
      <span v-if="headerRow.html" v-html="headerRow.label">
      </span>
      <span v-else>
        {{ headerRow.label }}
      </span>
    </slot>
  </th>
  <!-- if the mode is not span, we display every column -->
  <th
    class="vgt-row-header"
    v-if="headerRow.mode !== 'span' && lineNumbers"></th>
  <th
    class="vgt-row-header"
    v-if="headerRow.mode !== 'span' && selectable"></th>
  <th
    v-if="headerRow.mode !== 'span' && !column.hidden"
    v-for="(column, i) in columns"
    :key="i"
    class="vgt-row-header"
    :class="getClasses(i, 'td')">
    <slot
      :row="headerRow"
      :column="column"
      :formattedRow="formattedRow(headerRow, true)"
      name="table-header-row">
      <span v-if="!column.html">
        {{ collectFormatted(headerRow, column, true) }}
      </span>
      <span v-if="column.html" v-html="collectFormatted(headerRow, column, true)">
      </span>
    </slot>
  </th>
</tr>
</template>

<script>
export default {
  name: 'VgtHeaderRow',
  props: {
    headerRow: {
      type: Object,
    },
    columns: {
      type: Array,
    },
    lineNumbers: {
      type: Boolean,
    },
    selectable: {
      type: Boolean,
    },
    collectFormatted: {
      type: Function,
    },
    formattedRow: {
      type: Function,
    },
    getClasses: {
      type: Function,
    },
    fullColspan: {
      type: Number,
    },
    childrenVisibilityToggle: {
      type: Boolean
    }
  },
  data() {
    return {
    };
  },
  computed: {
  },
  methods: {
    toggleChildrenVisibility() {
      this.$emit('childrenVisibilityToggled')
    }
  },
  mounted() {
  },
  components: {
  },
};
</script>

<style lang="scss">

</style>
