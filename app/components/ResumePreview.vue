<script setup>
import {
  Mail,
  Linkedin,
  MapPin,
  GripVertical
} from 'lucide-vue-next';
import RichTextEditor from '~/components/RichTextEditor.vue'
const props = defineProps([
  'profile',
  'removeExperience',
  'removeLanguage',
  'removeSection',
  'moveExperienceUp',
  'moveExperienceDown',
  'moveLanguageUp',
  'moveLanguageDown'
])
</script>

<template>
  <div class="resume-container max-w-[760px] mx-auto bg-white min-h-[900px] px-[56px] py-[48px] shadow-sm print:shadow-none print:min-h-100">
  <!-- <div class="max-w-[760px] mx-auto bg-white min-h-[900px] px-[56px] py-[48px] shadow-sm"> -->
    <!-- Header -->
     
    <div>
      <input
        v-model="props.profile.name"
        class="w-full bg-transparent outline-none border-none p-0
               text-[56px] leading-none font-semibold tracking-[-1px]
               text-[#1f2f4a] uppercase"
        style="font-family: Georgia, 'Times New Roman', serif;"
      />

      <input
        v-model="props.profile.role"
        class="w-full bg-transparent outline-none border-none p-0 mt-3
               text-[18px] italic text-[#9aa3b2]"
        style="font-family: Georgia, 'Times New Roman', serif;"
      />

     <div class="flex items-center gap-4 mt-4 text-[14px] text-[#5a78ff]">
      <div class="flex items-center gap-1">
        <Mail class="w-4 h-4" />
        <input
          v-model="props.profile.email"
          placeholder="Email"
          class="bg-transparent outline-none border-none w-[100] placeholder:text-[#5a78ff]"
        />
      </div>

      <div class="flex items-center gap-1">
        <Linkedin class="w-4 h-4" />
        <input
          v-model="props.profile.linkedin"
          placeholder="LinkedIn"
          class="bg-transparent outline-none border-none w-[100] placeholder:text-[#5a78ff]"
        />
      </div>

      <div class="flex items-center gap-1">
        <MapPin class="w-4 h-4" />
        <input
          v-model="props.profile.location"
          placeholder="Location"
          class="bg-transparent outline-none border-none w-[100] placeholder:text-[#5a78ff]"
        />
      </div>
    </div>
      
    </div>

    <div class="border-t border-gray-300 mt-6 mb-5"></div>

    <!-- Summary -->
    <section class="mb-10 relative">
      <button
        class="absolute -left-4 top-0 text-[#d66] text-[18px] leading-none print:hidden"
        title="Remove section"
        @click="props.profile.summary = ''" 
      >
        ×
      </button>

      <div class="mb-2">
        <span
          class="text-[13px] font-bold tracking-wide uppercase text-[#222]"
          style="font-family: Georgia, 'Times New Roman', serif;"
        >
          Summary
        </span>
        <div class="border-t-2 border-[#1f2f4a] mt-2 w-full print-line"></div>
      </div>

    <textarea
        v-model="props.profile.summary"
        class="w-full mt-3 bg-transparent outline-none border-none resize-none p-0
               text-[16px] leading-7 text-[#4b5563] min-h-[70px]"
        style="font-family: Georgia, 'Times New Roman', serif;"
      />
  
    </section>

    <!-- Experience -->
    <section class="relative">
      <button
        class="absolute -left-4 top-0 text-[#d66] text-[18px] leading-none print:hidden"
        title="Remove section"
        @click="props.profile.experiences = []" 
      >
        ×
      </button>

      <div class="mb-2">
        <span
          class="text-[13px] font-bold tracking-wide uppercase text-[#222]"
          style="font-family: Georgia, 'Times New Roman', serif;"
        >
          Experience
        </span>
        <div class="border-t-2 border-[#1f2f4a] mt-2 w-full print-line"></div>
      </div>

      <div
          v-for="(exp, index) in props.profile.experiences"
          :key="index"
          class="mt-4 relative pl-6 print-block"
        >
        <button
          class="absolute -left-4 top-0 text-[#d66] text-[18px] leading-none print:hidden"
          title="Remove experience"
          @click="props.removeExperience(index)" 
        >
          ×
        </button>

        <input
          v-model="exp.title"
          class="w-full bg-transparent outline-none border-none p-0
                 text-[18px] font-semibold text-[#1f1f1f]"
          style="font-family: Georgia, 'Times New Roman', serif;"
        />

        <input
          v-model="exp.company"
          class="w-full bg-transparent outline-none border-none p-0 mt-2
                 text-[18px] text-[#5673ff]"
          style="font-family: Georgia, 'Times New Roman', serif;"
        />

        <input
          v-model="exp.meta"
          class="w-full bg-transparent outline-none border-none p-0 mt-1
                 text-[14px] text-[#9ca3af]"
          style="font-family: Georgia, 'Times New Roman', serif;"
        />

        <textarea
          v-model="exp.description"
          class="w-full mt-3 bg-transparent outline-none border-none resize-none p-0
                 text-[16px] leading-7 text-[#4b5563] min-h-[90px]"
          style="font-family: Georgia, 'Times New Roman', serif;"
        />
      </div>
    </section>

    <!-- Languages -->
    <section v-if="props.profile.showLanguages" class="mt-10 relative page-safe">
      <button
        class="absolute -left-4 top-0 text-[#d66] text-[18px] leading-none print:hidden"
        title="Remove section"
        @click="props.removeSection('languages')" 
      >
        ×
      </button>

      <div class="mb-2">
        <span
          class="text-[13px] font-bold tracking-wide uppercase text-[#222]"
          style="font-family: Georgia, 'Times New Roman', serif;"
        >
          Languages
        </span>
        <div class="h-[2px] border-t-2 border-[#1f2f4a] mt-2 w-[100%]"></div>
      </div>

      <div
        v-for="(lang, index) in props.profile.languages"
        :key="index"
        class="mt-4 flex items-start justify-between relative pl-6 print-block"
      >
        <button
          class="absolute -left-4 top-0 text-[#d66] text-[18px] leading-none print:hidden"
          title="Remove language"
          @click="props.removeLanguage(index)" 
        >
          ×
        </button>

        <div>
          <input
            v-model="lang.name"
            class="w-full bg-transparent outline-none border-none p-0
                   text-[18px] text-[#1f1f1f]"
            style="font-family: Georgia, 'Times New Roman', serif;"
          />

          <input
            v-model="lang.level"
            class="w-full bg-transparent outline-none border-none p-0 mt-1
                   text-[14px] text-[#9ca3af]"
            style="font-family: Georgia, 'Times New Roman', serif;"
          />
        </div>

        <div class="flex gap-1 mt-2">
          <span class="w-4 h-4 rounded-sm bg-[#5a78ff]"></span>
          <span class="w-4 h-4 rounded-sm bg-[#5a78ff]"></span>
          <span class="w-4 h-4 rounded-sm bg-gray-200"></span>
          <span class="w-4 h-4 rounded-sm bg-gray-200"></span>
          <span class="w-4 h-4 rounded-sm bg-gray-200"></span>
        </div>
      </div>
    </section>

    <!-- Key Achievements -->
    <section v-if="props.profile.showAchievements" class="mt-10 relative">
      <button
        class="absolute -left-4 top-0 text-[#d66] text-[18px] leading-none print:hidden"
        title="Remove section"
        @click="props.removeSection('achievements')"  
      >
        ×
      </button>

      <div class="mb-2">
        <span
          class="text-[13px] font-bold tracking-wide uppercase text-[#222]"
          style="font-family: Georgia, 'Times New Roman', serif;"
        >
          Key Achievements
        </span>
        <div class="h-[2px] border-t-2 border-[#1f2f4a] mt-2 w-[100%]"></div>
      </div>

      <textarea
        v-model="props.profile.achievementText"
        class="w-full mt-3 bg-transparent outline-none border-none resize-none p-0
               text-[16px] leading-7 text-[#4b5563] min-h-[80px]"
        style="font-family: Georgia, 'Times New Roman', serif;"
      />
    </section>

    <!-- Skills -->
    <section v-if="props.profile.showSkills" class="mt-10 relative">
      <button
        class="absolute -left-4 top-0 text-[#d66] text-[18px] leading-none  print:hidden"
        title="Remove section"
        @click="props.removeSection('skills')" 
      >
        ×
      </button>

      <div class="mb-2">
        <span
          class="text-[13px] font-bold tracking-wide uppercase text-[#222]"
          style="font-family: Georgia, 'Times New Roman', serif;"
        >
          Skills
        </span>
        <div class="h-[2px] border-t-2 border-[#1f2f4a]  mt-2 w-[100%]"></div>
      </div>

      <div class="mt-4 flex flex-wrap gap-2">
        <span
          v-for="(skill, index) in props.profile.skills"
          :key="index"
          class="px-3 py-1 text-[14px] bg-gray-100 rounded"
        >
          {{ skill }}
        </span>
      </div>
    </section>

    <!-- Education -->
    <section v-if="props.profile.showEducation" class="mt-10 relative">
      <button
        class="absolute -left-4 top-0 text-[#d66] text-[18px] leading-none  print:hidden"
        title="Remove section"
        @click="props.removeSection('education')"  
      >
        ×
      </button>

      <div class="mb-2">
        <span
          class="text-[13px] font-bold tracking-wide uppercase text-[#222]"
          style="font-family: Georgia, 'Times New Roman', serif;"
        >
          Education
        </span>
        <div class="h-[2px] border-t-2 border-[#1f2f4a]  mt-2 w-[100%]"></div>
      </div>

      <input
        v-model="props.profile.educationTitle"
        class="w-full bg-transparent outline-none border-none p-0 mt-4
               text-[18px] font-semibold text-[#1f1f1f]"
        style="font-family: Georgia, 'Times New Roman', serif;"
      />

      <input
        v-model="props.profile.educationSchool"
        class="w-full bg-transparent outline-none border-none p-0 mt-2
               text-[18px] text-[#5673ff]"
        style="font-family: Georgia, 'Times New Roman', serif;"
      />
    </section>

    <!-- Training / Courses -->
    <section v-if="props.profile.showTraining" class="mt-10 relative">
      <button
        class="absolute -left-4 top-0 text-[#d66] text-[18px] leading-none  print:hidden"
        title="Remove section"
        @click="props.removeSection('training')" 
      >
        ×
      </button>

      <div class="mb-2">
        <span
          class="text-[13px] font-bold tracking-wide uppercase text-[#222]"
          style="font-family: Georgia, 'Times New Roman', serif;"
        >
          Training / Courses
        </span>
        <div class="h-[2px] border-t-2 border-[#1f2f4a] mt-2 w-[100%]"></div>
      </div>

      <input
        v-model="props.profile.trainingTitle"
        class="w-full bg-transparent outline-none border-none p-0 mt-4
               text-[18px] font-semibold text-[#1f1f1f]"
        style="font-family: Georgia, 'Times New Roman', serif;"
      />
    </section>

    <!-- Interests -->
    <section v-if="props.profile.showInterests" class="mt-10 relative">
      <button
        class="absolute -left-4 top-0 text-[#d66] text-[18px] leading-none print:hidden"
        title="Remove section"
        @click="props.removeSection('interests')" 
      >
        ×
      </button>

      <div class="mb-2">
        <span
          class="text-[13px] font-bold tracking-wide uppercase text-[#222]"
          style="font-family: Georgia, 'Times New Roman', serif;"
        >
          Interests
        </span>
        <div class="h-[2px] border-t-2 border-[#1f2f4a] mt-2 w-[100%]"></div>
      </div>

      <textarea
        v-model="props.profile.interestsText"
        class="w-full mt-3 bg-transparent outline-none border-none resize-none p-0
               text-[16px] leading-7 text-[#4b5563] min-h-[70px]"
        style="font-family: Georgia, 'Times New Roman', serif;"
      />
    </section>
  </div>
</template>