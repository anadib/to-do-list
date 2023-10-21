<template>
  <li class="list-item-wrapper">
    <span class="list-item" @click="toggleCheckbox(item)">
      <input
        type="checkbox"
        :id="index"
        class="item-checkbox"
        @change="$emit('input', $event.target.checked)"
        :checked="item.checked"
      />
      <label :for="index" :class="getItemClass(item.checked)">{{
        item.label
      }}</label>
    </span>
    <span
      class="trash-icon"
      v-html="deleteIcon"
      @click="deleteFromList(index)"
    ></span>
  </li>
</template>

<script>
import feather from "feather-icons";

export default {
  name: "ListItem",
  props: {
    item: Object,
    index: Number,
  },
  computed: {
    deleteIcon() {
      return feather.icons.trash.toSvg();
    },
  },
  methods: {
    getItemClass(itemChecked) {
      return itemChecked ? "item-checked" : "";
    },
    deleteFromList(index) {
      this.$emit("delete-item", index);
    },
    toggleCheckbox(item) {
      item.checked = !item.checked;
      this.$emit("updateStore");
    },
  },
};
</script>

<style scoped>
.list-item-wrapper {
  display: flex;
  background-color: #20212c;
  padding: 12px 15px;
  border-radius: 10px;
  margin-bottom: 10px;
  align-items: center;
  justify-content: space-between;
}

.list-item {
  display: flex;
  align-items: center;
}

.item-checkbox {
  width: 20px;
  height: 20px;
  min-width: 20px;
  min-height: 20px;
  margin-right: 5px;
  cursor: pointer;
}

label {
  color: #ccc;
  text-decoration: initial;
  margin-left: 5px;
  word-wrap: break-word;
  padding-right: 8px;
}

.item-checked {
  text-decoration: line-through;
}

.trash-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  cursor: pointer;
  width: 20px;
  height: 20px;
}
</style>
