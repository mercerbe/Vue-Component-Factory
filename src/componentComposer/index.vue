<script>
import Vue from "vue";
import _ from "lodash";
/**
 * Create component is a recursive function that takes a DOM structure
 * and a rendering function (of vue.js) and returns a Vuejs component.
 */
const createComponent = (dNode, h) => {
  // Handle empty elements and return empty array in case the dNode passed in is empty
  if (_.isEmpty(dNode)) {
    return [];
  }

  // if the el is array call createComponent for all elements
  if (_.isArray(dNode)) {
    return dNode.map(child => createComponent(child, h));
  }

  let children = [];

  if (dNode.children && dNode.children.length > 0) {
    dNode.children.forEach(c => {
      if (_.isString(c)) {
        children.push(c);
      } else {
        children.push(createComponent(c, h));
      }
    });
  }
  // Need to clone
  const properties = _.cloneDeep(dNode.properties);
  return h(
    dNode.tagName,
    properties,
    children.length > 0 ? children : dNode.textNode
  );
};

export default {
  name: "ComponentFactory",
  props: {
    name: { type: String, required: true },
    nodes: { type: Object, required: true }
  },
  data() {
    return {
      component: Vue.component(this.name, {
        render: function(h) {
          return createComponent(this.nodes, h);
        },
        props: {
          nodes: {
            type: Object,
            required: true
          }
        }
      })
    };
  }
};
</script>

<template>
  <component :is="component" :nodes="nodes" />
</template>
