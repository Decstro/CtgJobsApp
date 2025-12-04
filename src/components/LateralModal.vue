<script setup>
import { ref } from 'vue';

const props = defineProps({
  isOpen: Boolean,
});

const emit = defineEmits(['close']);

const selectedAnswer = ref('');
const notes = ref('');

const closeModal = () => {
  emit('close');
};

const handleConfirm = () => {
  // Handle form submission here
  console.log('Answer:', selectedAnswer.value);
  console.log('Notes:', notes.value);
  closeModal();
};
</script>

<template>
  <!-- Backdrop -->
  <div
    v-if="isOpen"
    class="fixed inset-0 bg-black bg-opacity-50 z-40 transition-opacity"
    @click="closeModal"
  ></div>

  <!-- Lateral Modal -->
  <div
    :class="[
      'fixed top-0 right-0 h-full w-full md:w-[500px] bg-white shadow-2xl z-50 transform transition-transform duration-300 flex flex-col',
      isOpen ? 'translate-x-0' : 'translate-x-full'
    ]"
  >
    <!-- Scrollable Content Area -->
    <div class="flex-1 overflow-y-auto">
      <!-- Header -->
      <div class="px-8 pt-[6.5rem] pb-6 border-b border-gray-200">
        <div class="flex justify-between items-center mb-4">
          <h1 class="text-[#212529] font-['DM_Sans'] text-[22px] font-bold leading-[125%] tracking-[-0.44px] flex-1">
            Summit Group Action Items
          </h1>
          <button
            @click="closeModal"
            class="text-[#5C0CB8] font-['DM_Sans'] text-[14px] font-bold leading-[125%] tracking-[-0.44px] hover:underline ml-auto flex items-center gap-1 flex-shrink-0 pl-4"
            aria-label="Close panel"
          >
            <span>Close Panel</span>
            <span>✕</span>
          </button>
        </div>
        <button
          @click="closeModal"
          class="text-[#5C0CB8] pt-[1rem] text-right font-['DM_Sans'] text-[14px] font-bold leading-[130%] tracking-[-0.42px] hover:underline"
        >
          &lt; Back to Mark Requirements Complete
        </button>
      </div>

      <!-- Content -->
      <div class="pl-9 pt-1 pb-[8rem]">
        <!-- Title -->
        <h2 class="text-[#212529] font-['DM_Sans'] text-[20px] font-bold leading-[125%] tracking-[-0.4px] mb-4">
          Annual HIPAA Training
        </h2>

        <!-- Description -->
        <p class="text-[#495057] font-['DM_Sans'] text-[16px] font-normal leading-[130%] tracking-[-0.32px] mb-6">
          Let us know a few more details and lorem ipsum dolor sit amet lorem ipsum dolor sit amet.
        </p>

        <!-- Question -->
        <div class="mb-6">
          <p class="text-[#212529] font-['DM_Sans'] text-[14px] font-bold leading-[130%] tracking-[-0.28px] mb-3">
            Q1: Does the employer have any exposure to Protected Health Information...
          </p>

          <!-- Radio Options -->
          <div class="space-y-3">
            <label class="flex items-start cursor-pointer group">
              <input
                type="radio"
                v-model="selectedAnswer"
                value="self-insured-hands-on"
                class="mt-1 mr-3 w-4 h-4 text-[#5C0CB8] focus:ring-[#5C0CB8]"
              />
              <span class="text-[#212529] font-['DM_Sans'] text-[16px] font-bold leading-[130%] tracking-[-0.32px] group-hover:text-[#5C0CB8]">
                Yes - employer is self-insured and hands-on (self-insured med/Rx/den/vis, FSA, and/or HRA)
              </span>
            </label>

            <label class="flex items-start cursor-pointer group">
              <input
                type="radio"
                v-model="selectedAnswer"
                value="self-insured-hands-on"
                class="mt-1 mr-3 w-4 h-4 text-[#5C0CB8] focus:ring-[#5C0CB8]"
              />
              <span class="text-[#212529] font-['DM_Sans'] text-[16px] font-bold leading-[130%] tracking-[-0.32px] group-hover:text-[#5C0CB8]">
                Yes - employer is self-insured and hands-on (self-insured med/Rx/den/vis, FSA, and/or HRA)
              </span>
            </label>

            <label class="flex items-start cursor-pointer group">
              <input
                type="radio"
                v-model="selectedAnswer"
                value="self-insured-hands-off"
                class="mt-1 mr-3 w-4 h-4 text-[#5C0CB8] focus:ring-[#5C0CB8]"
              />
              <span class="text-[#212529] font-['DM_Sans'] text-[16px] font-normal leading-[130%] tracking-[-0.32px] group-hover:text-[#5C0CB8]">
                Yes - employer is self-insured but hands-off (level-funded with no FSA or HRA and no claims analytics drill-down)
              </span>
            </label>

                        <label class="flex items-start cursor-pointer group">
              <input
                type="radio"
                v-model="selectedAnswer"
                value="self-insured-hands-off"
                class="mt-1 mr-3 w-4 h-4 text-[#5C0CB8] focus:ring-[#5C0CB8]"
              />
              <span class="text-[#212529] font-['DM_Sans'] text-[16px] font-normal leading-[130%] tracking-[-0.32px] group-hover:text-[#5C0CB8]">
                Yes - employer is self-insured but hands-off (level-funded with no FSA or HRA and no claims analytics drill-down)
              </span>
            </label>
          </div>
        </div>

        <!-- Add Notes -->
        <div class="mb-6">
          <label class="text-[#5C0CB8] font-['DM_Sans'] text-[16px] font-bold leading-[130%] tracking-[-0.32px] block mb-3">
            Add Notes (optional)
          </label>

          <textarea
            v-model="notes"
            class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-[#5C0CB8] focus:border-transparent"
            rows="4"
            placeholder="Notes"
          ></textarea>
        </div>
      </div>
    </div>

    <!-- Fixed Footer with Grey Background -->
    <div class="bg-gray-200 px-3 py-14 border-t border-gray-300 shadow-lg flex justify-end items-start">
      <button
        @click="handleConfirm"
        class="bg-[#5C0CB8] text-white font-['DM_Sans'] text-[14px] font-medium leading-[130%] py-2 px-8 rounded-md hover:bg-[#4A0A96] transition-colors mr-4"
      >
        Confirm Complete
      </button>
    </div>
  </div>
</template>

<style scoped>
/* Custom radio button styling */
input[type="radio"] {
  accent-color: #5C0CB8;
}
</style>
