<script setup>
const props = defineProps(['profile'])

const addExperience = () => {
  props.profile.experiences.push({
    title: '',
    company: ''
  })
}
</script>

<template>
  <div class="space-y-4">
    <h2 class="text-xl font-bold">Editor</h2>

    <!-- Name -->
    <input
      type="text"
      placeholder="Name"
      v-model="props.profile.name"
      class="border p-2 w-full"
    />

    <!-- Bio -->
    <textarea
      placeholder="Bio"
      v-model="props.profile.bio"
      class="border p-2 w-full"
    ></textarea>

    <!-- Experience -->
    <div>
      <h3 class="font-semibold">Experience</h3>

      <button @click="addExperience" class="bg-blue-500 text-white px-3 py-1 mt-2">
        Add Experience
      </button>

      <div
        v-for="(exp, index) in props.profile.experiences"
        :key="index"
        class="mt-3 border p-2"
      >
        <input
          placeholder="Title"
          v-model="exp.title"
          class="border p-1 w-full mb-2"
        />

        <input
          placeholder="Company"
          v-model="exp.company"
          class="border p-1 w-full"
        />
      </div>
    </div>
  </div>
</template>