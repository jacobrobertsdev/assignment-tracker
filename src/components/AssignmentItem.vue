<script setup>
import { nextTick, ref } from "vue";

const props = defineProps({
  course: String,
  title: String,
  due: String,
  id: String,
});

const emit = defineEmits(["deleteAssignment", "editAssignment"]);

let inputRef = ref(null);
const readOnly = ref(true);
const editedTitle = ref(props.title);

const toggleEdit = async () => {
  readOnly.value = !readOnly.value;

  if (!readOnly.value) {
    await nextTick();
    inputRef.value.focus();
  }
};

const preventFocus = (event) => {
  event.preventDefault();
};

function deleteAssignment() {
  emit("deleteAssignment", props.id);
}

function handleEditTitle(value) {
  editedTitle.value = value;
}

function saveEdit() {
  toggleEdit();
  emit("editAssignment", { id: props.id, newTitle: editedTitle.value });
}

function cancelEdit() {
  editedTitle.value = props.title;
  toggleEdit();
}
</script>

<template>
  <li class="assignment">
    <textarea
      rows="1"
      name="assignment title"
      ref="inputRef"
      :readonly="readOnly"
      :value="editedTitle"
      :onmousedown="readOnly ? preventFocus : null"
      @change="handleEditTitle($event.target.value)"
    >
    </textarea>

    <span class="course-name">{{ props.course }}</span>
    <span class="due-date">Due: {{ props.due }}</span>

    <button class="delete" @click="deleteAssignment">Delete</button>
    <button v-if="readOnly" class="edit" @click="toggleEdit">Edit</button>

    <div v-else class="edit-buttons">
      <button class="save" @click="saveEdit">Save</button>
      <button class="cancel" @click="cancelEdit">Cancel</button>
    </div>
  </li>
</template>

<style scoped>
.assignment {
  background-color: #122034;
  position: relative;
  padding: 2.8rem 1rem;
  width: 90%;
  border-radius: 5px;
  word-break: break-all;
}

textarea {
  width: 100%;
  background-color: transparent;
  color: var(--text);
  font-size: 0.9rem;
  border: none;
  resize: none;
}

textarea::-webkit-scrollbar {
  width: 0.6rem;
}

textarea::-webkit-scrollbar-track {
  background-color: var(--background);
  border-radius: 3px;
}

textarea::-webkit-scrollbar-thumb {
  background-color: #8390a3;
  border-radius: 3px;
}
span {
  font-size: 0.8rem;
}

.course-name {
  position: absolute;
  top: 0;
  left: 0;
  padding: 0.2rem 0.4rem;
  background-color: #495057;
  border-bottom-right-radius: 5px;
  border-top-left-radius: 5px;
}
.due-date {
  position: absolute;
  top: 0;
  right: 0;
  padding: 0.2rem 0.4rem;
  background-color: #495057;
  border-bottom-left-radius: 5px;
  border-top-right-radius: 5px;
}

.delete {
  font-size: 0.9rem;
  position: absolute;
  bottom: 0;
  right: 0;
  padding: 0.2rem 0.4rem;
  background-color: transparent;
  border: none;
  border-top-left-radius: 5px;
  border-bottom-right-radius: 5px;
  color: red;
}
.edit {
  font-size: 0.8rem;
  position: absolute;
  bottom: 0;
  left: 0;
  padding: 0.2rem 0.4rem;
  background-color: #1864ab;
  border: none;
  border-top-right-radius: 5px;
  border-bottom-left-radius: 5px;
}

.edit-buttons {
  position: absolute;
  bottom: 0;
  left: 0;
  display: flex;
  gap: 1rem;
}

.edit-buttons button {
  padding: 0.2rem 0.4rem;
  font-size: 0.8rem;
  background-color: #1864ab;
  border: none;
}

.save {
  border-top-right-radius: 5px;
  border-bottom-left-radius: 5px;
}

.cancel {
  border-top-right-radius: 5px;
  border-top-left-radius: 5px;
}

button:hover {
  background-color: hsl(220, 20%, 30%);
}
</style>
