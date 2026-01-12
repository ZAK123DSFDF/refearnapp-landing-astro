<script setup>
import { ref } from 'vue';

const activeIndex = ref(null);

const faqData = [
  {
    question: 'Can I try RefearnApp for free?',
    answer:
      'Yes! You can try RefearnApp completely free for 14 days. During your trial, you’ll have full access to all features—no credit card required. This allows you to explore the dashboard, set up your affiliate program, and understand how RefearnApp can help grow your SaaS.',
  },
  {
    question: 'Which platforms does RefearnApp support?',
    answer:
      'RefearnApp currently supports Stripe and Paddle for subscription tracking and payment reporting. We’re actively working on adding more integrations to support a wider range of billing platforms in the future.',
  },
  {
    question: 'How do I pay my affiliates?',
    answer:
      'At the moment, you can export a complete CSV payout file directly from your dashboard. This CSV contains all affiliate earnings for the selected period and can be used to send payments quickly and easily through PayPal. We plan to introduce additional payout options and automated payment flows in future updates to make the process even more seamless.',
  },
  {
    question: 'Can I set how long affiliates get paid?',
    answer:
      'Absolutely. RefearnApp allows you to define how long an affiliate should continue receiving commissions. You can configure both the duration value and the time unit—days, weeks, or months—giving you complete flexibility over your commission structure.',
  },
];

const toggle = (index) => {
  // If clicking the same one, close it. Otherwise, open the new one and close others.
  activeIndex.value = activeIndex.value === index ? null : index;
};
</script>

<template>
  <section id="faq" class="bg-white px-6 py-24">
    <div class="mx-auto mb-12 max-w-3xl text-center">
      <h2 class="text-3xl font-bold tracking-tight text-slate-900 md:text-5xl">
        Frequently Asked Questions
      </h2>
      <p class="mt-4 text-lg text-slate-500">
        Answers to the most common questions about RefearnApp.
      </p>
    </div>

    <div class="mx-auto max-w-3xl">
      <div class="space-y-2">
        <div
          v-for="(item, index) in faqData"
          :key="index"
          class="border-b border-slate-200"
        >
          <button
            @click="toggle(index)"
            class="hover:text-primary group flex w-full items-center justify-between py-6 text-left text-lg font-semibold transition-colors focus:outline-none"
          >
            <span
              :class="activeIndex === index ? 'text-primary' : 'text-slate-900'"
              >{{ item.question }}</span
            >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
              class="group-hover:text-primary text-slate-400 transition-transform duration-300 ease-in-out"
              :class="{ 'rotate-180': activeIndex === index }"
            >
              <path d="m6 9 6 6 6-6" />
            </svg>
          </button>

          <div
            class="overflow-hidden transition-all duration-300 ease-in-out"
            :style="{
              maxHeight: activeIndex === index ? '500px' : '0px',
              opacity: activeIndex === index ? '1' : '0',
            }"
          >
            <div class="pb-6 text-base leading-relaxed text-slate-500">
              {{ item.answer }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
