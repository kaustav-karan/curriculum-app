<template>
  <v-row>
    <v-col>
      <h1 class="hover-icon-container" v-if="editField !== 'name'">
        {{ curriculum_.name }}
        <v-icon v-if="canEdit()" color="gray lighten-1" class="togglable-icon" @click="toggleEdit('name')">
          mdi-pencil-box-outline
        </v-icon>
      </h1>
      <v-text-field data-test="name-edit-field" v-else-if="canEdit()" v-model="curriculum_.name">
        <template v-slot:append-outer>
          <v-btn small outlined color="primary" class="mr-1" @click="saveEdit('name')">
            Save
          </v-btn>
          <v-btn outlined small @click="cancelEdit">
            Cancel
          </v-btn>
        </template>
      </v-text-field>

      <div v-if="curriculum_.goal">
        <p class="hover-icon-container" v-if="editField !== 'goal'">
          Goal: {{ curriculum_.goal }}
          <v-icon v-if="canEdit()" color="gray lighten-1" class="togglable-icon" @click="toggleEdit('goal')" small>
            mdi-pencil-box-outline
          </v-icon>
        </p>
        <v-text-field v-else-if="canEdit()" v-model="curriculum_.goal">
          <template v-slot:append-outer>
            <v-btn small outlined color="primary" class="mr-1" @click="saveEdit('goal')">
              Save
            </v-btn>
            <v-btn outlined small @click="cancelEdit">
              Cancel
            </v-btn>
          </template>
        </v-text-field>
      </div>
      <div v-else>
        <!-- TODO: need to hook this button up -->
        <v-btn color="info" small text>Add Goal</v-btn>
      </div>

      <div>
        <p>
          Created By: {{ curriculum_.createdByName }}
        </p>
      </div>

      <p class="hover-icon-container" v-if="editField !== 'description'">
        {{ curriculum_.description }}
        <v-icon v-if="canEdit()" color="gray lighten-1" class="togglable-icon" @click="toggleEdit('description')" small>
          mdi-pencil-box-outline
        </v-icon>
      </p>
      <v-text-field v-else-if="canEdit()" v-model="curriculum_.description">
        <template v-slot:append-outer>
          <v-btn small outlined color="primary" class="mr-1" @click="saveEdit('description')">
            Save
          </v-btn>
          <v-btn outlined small @click="cancelEdit">
            Cancel
          </v-btn>
        </template>
      </v-text-field>
    </v-col>
  </v-row>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  editField: String,
  selectedCurriculum: Object,
  toggleEdit: Function,
  saveEdit: Function,
  cancelEdit: Function,
  canEdit: Function
})

const emit = defineEmits(['selectCurriculum:update'])

const curriculum_ = computed({
  get: () => props.selectedCurriculum,
  set: () => {
    emit('selectCurriculum:update', props.selectedCurriculum)
  }
})
</script>
