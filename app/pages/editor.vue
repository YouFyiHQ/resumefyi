
<script setup>
import { ref } from 'vue'
import ResumePreview from '~/components/ResumePreview.vue'

const profile = ref({
  name: 'YOUR NAME',
  role: 'The role you are applying for?',
   email: '',
  linkedin: '',
  location: '',
  summary: "Briefly explain why you're a great fit for the role...",

  experiences: [
    {
      title: 'Title',
      company: 'Company Name',
      meta: 'Date period    Location',
      description: 'Highlight your accomplishments, using numbers if possible.'
    }
  ],

  languages: [
    {
      name: 'Language',
      level: 'Beginner'
    }
  ],

  showSkills: false,
  showEducation: false,
  showTraining: false,
  showInterests: false,
  showAchievements: false,
  showLanguages: true,

  skills: ['Frontend', 'Vue', 'Nuxt'],
  educationTitle: 'Degree and Field of Study',
  educationSchool: 'School or University',
  trainingTitle: 'Course Title',
  interestsText: 'Career Interest / Passion',
  achievementText: 'Describe what you did and the impact it had.'
})

const toggleSection = (section) => {
  if (section === 'skills') profile.value.showSkills = !profile.value.showSkills
  if (section === 'education') profile.value.showEducation = !profile.value.showEducation
  if (section === 'training') profile.value.showTraining = !profile.value.showTraining
  if (section === 'interests') profile.value.showInterests = !profile.value.showInterests
  if (section === 'achievements') profile.value.showAchievements = !profile.value.showAchievements
}

const addExperience = () => {
  profile.value.experiences.push({
    title: 'Title',
    company: 'Company Name',
    meta: 'Date period    Location',
    description: 'Highlight your accomplishments, using numbers if possible.'
  })
}

const removeExperience = (index) => {
  profile.value.experiences.splice(index, 1)
}

const addLanguage = () => {
  if (!profile.value.showLanguages) {
    profile.value.showLanguages = true
  }

  profile.value.languages.push({
    name: 'Language',
    level: 'Beginner'
  })
}

const removeLanguage = (index) => {
  profile.value.languages.splice(index, 1)
}

const removeSection = (section) => {
  if (section === 'skills') profile.value.showSkills = false
  if (section === 'education') profile.value.showEducation = false
  if (section === 'training') profile.value.showTraining = false
  if (section === 'interests') profile.value.showInterests = false
  if (section === 'achievements') profile.value.showAchievements = false
  if (section === 'languages') profile.value.showLanguages = false
}

const downloadPdf = () => {
  window.print()
}
</script>

<template>
  <div class="min-h-screen bg-[#ececec] py-10">
    <div class="max-w-[1100px] mx-auto px-3">
      <div class="flex items-center justify-between mb-4  print:hidden">
        <div class="flex items-center gap-3 flex-wrap">
          <h2 class="text-[16px] font-medium text-[#2d3748]">Resume Editor</h2>

          <div class="flex items-center gap-2 text-sm flex-wrap">
            <span class="text-gray-500">Restore:</span>

            <button
              class="px-3 py-1 bg-white border border-gray-300 rounded text-[14px]"
              @click="toggleSection('skills')"
            >
              + Skills
            </button>

            <button
              class="px-3 py-1 bg-white border border-gray-300 rounded text-[14px]"
              @click="toggleSection('education')"
            >
              + Education
            </button>

            <button
              class="px-3 py-1 bg-white border border-gray-300 rounded text-[14px]"
              @click="toggleSection('training')"
            >
              + Training / Courses
            </button>

            <button
              class="px-3 py-1 bg-white border border-gray-300 rounded text-[14px]"
              @click="toggleSection('interests')"
            >
              + Interests
            </button>

            <button
              class="px-3 py-1 bg-white border border-gray-300 rounded text-[14px]"
              @click="toggleSection('achievements')"
            >
              + Key Achievements
            </button>

            <button
              class="px-3 py-1 bg-white border border-gray-300 rounded text-[14px]"
              @click="addExperience"
            >
              + Experience
            </button>

            <button
              class="px-3 py-1 bg-white border border-gray-300 rounded text-[14px]"
              @click="addLanguage"
            >
              + Language
            </button>
          </div>
        </div>

        <button
          class="bg-[#4c6fff] hover:bg-[#3f5fe0] text-white px-2 py-2 rounded-md text-[12px] font-medium"
          @click="downloadPdf"
        >
          Download PDF
        </button>
      </div>

      <ResumePreview
        :profile="profile"
        :remove-experience="removeExperience"
        :remove-language="removeLanguage"
        :remove-section="removeSection"
      />
    </div>
  </div>
</template>