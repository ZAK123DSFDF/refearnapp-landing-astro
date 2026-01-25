<template>
  <section id="how-it-works" class="bg-slate-50/50 px-4 py-20 sm:px-6 lg:py-32">
    <div class="container mx-auto max-w-6xl">
      <div class="mb-20 text-center">
        <h2
          class="mb-4 text-4xl font-extrabold tracking-tight text-slate-900 md:text-6xl"
        >
          How <span class="text-blue-600">It Works</span>
        </h2>
        <p class="text-xl text-slate-500">
          Launch your program in six simple steps.
        </p>
      </div>

      <div
        class="grid grid-cols-1 items-start gap-y-16 lg:grid-cols-12 lg:gap-16"
      >
        <div class="space-y-[35vh] py-10 lg:col-span-5 lg:pb-[60vh]">
          <div
            v-for="(step, index) in steps"
            :key="index"
            :id="'step-trigger-' + index"
            class="step-item group cursor-pointer transition-all duration-700"
            :class="[
              activeStep === index
                ? 'scale-100 opacity-100 lg:scale-105'
                : 'opacity-20 blur-[1px] grayscale',
            ]"
            @click="scrollToStep(index)"
          >
            <div class="flex items-start gap-4 sm:gap-6">
              <div
                class="flex h-12 w-12 shrink-0 items-center justify-center rounded-2xl text-lg font-black shadow-lg transition-all duration-500 sm:h-14 sm:w-14 sm:text-xl"
                :class="
                  activeStep === index
                    ? 'bg-blue-600 text-white ring-4 ring-blue-600/10 sm:ring-8'
                    : 'bg-slate-200 text-slate-500'
                "
              >
                {{ step.number }}
              </div>
              <div class="flex-1">
                <h3
                  class="mb-3 text-2xl font-bold transition-colors duration-500 sm:mb-4 sm:text-3xl"
                  :class="
                    activeStep === index ? 'text-slate-900' : 'text-slate-400'
                  "
                >
                  {{ step.title }}
                </h3>
                <Transition name="fade-slide">
                  <p
                    v-if="activeStep === index"
                    class="text-base leading-relaxed text-slate-600 sm:text-lg"
                  >
                    {{ step.description }}
                  </p>
                </Transition>
              </div>
            </div>

            <div v-if="activeStep === index" class="mt-8 w-full lg:hidden">
              <div
                class="overflow-hidden rounded-2xl border border-slate-200 bg-white shadow-2xl"
              >
                <video
                  controls
                  playsinline
                  class="aspect-video w-full object-cover"
                  poster="/opengraph-update.png"
                >
                  <source :src="step.video" type="video/mp4" />
                </video>
              </div>
            </div>
          </div>
        </div>

        <div class="sticky top-1/4 hidden lg:col-span-7 lg:block">
          <div class="mb-6 flex w-full gap-3 px-2">
            <div
              v-for="(_, i) in steps"
              :key="i"
              class="relative h-2 flex-1 overflow-hidden rounded-full bg-slate-200 transition-all duration-500"
              :class="{ 'ring-2 ring-blue-600/20': activeStep === i }"
            >
              <div
                class="absolute inset-0 bg-blue-600 shadow-[0_0_10px_rgba(37,99,235,0.5)] transition-transform duration-700 ease-out"
                :style="{
                  transform:
                    activeStep >= i ? 'translateX(0)' : 'translateX(-100%)',
                }"
              ></div>
            </div>
          </div>
          <div
            class="group relative overflow-hidden rounded-[2.5rem] border border-white bg-white p-3 shadow-[0_50px_100px_-20px_rgba(0,0,0,0.15)]"
          >
            <div
              class="relative overflow-hidden rounded-[1.8rem] border border-slate-200 bg-slate-900"
            >
              <div
                class="flex items-center justify-between border-b border-slate-100 bg-slate-50 px-6 py-4"
              >
                <div class="flex items-center gap-2">
                  <div class="h-3 w-3 rounded-full bg-[#FF5F56]"></div>
                  <div class="h-3 w-3 rounded-full bg-[#FFBD2E]"></div>
                  <div class="h-3 w-3 rounded-full bg-[#27C93F]"></div>
                </div>
                <div
                  class="rounded-full bg-slate-200/50 px-4 py-1 font-mono text-[10px] font-bold tracking-widest text-slate-400 uppercase"
                >
                  Step {{ activeStep + 1 }} of 6
                </div>
              </div>
              <div class="relative aspect-video overflow-hidden bg-black">
                <Transition name="fade" mode="out-in">
                  <video
                    :key="activeStep"
                    autoplay
                    muted
                    loop
                    playsinline
                    class="h-full w-full object-cover"
                    poster="/opengraph-update.png"
                  >
                    <source :src="steps[activeStep].video" type="video/mp4" />
                  </video>
                </Transition>
              </div>
            </div>
          </div>
          <div
            class="absolute -top-20 -right-20 -z-10 h-80 w-80 bg-blue-400/10 blur-[100px]"
          ></div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const activeStep = ref(0);

const steps = [
  {
    number: '01',
    title: 'Create Your Organization',
    description:
      'Configure settings and flexible commission tiers tailored for your SaaS.',
    video: 'https://assets.refearnapp.com/Step-1.mp4',
  },
  {
    number: '02',
    title: 'Connect Your Web App',
    description:
      'Add our script to your frontend. Drop it in and start tracking instantly.',
    video: 'https://assets.refearnapp.com/Step-2.mp4',
  },
  {
    number: '03',
    title: 'Connect Payment Provider',
    description:
      'Link Stripe or Paddle to sync conversions and rewards securely.',
    video: 'https://assets.refearnapp.com/Step-3.mp4',
  },
  {
    number: '04',
    title: 'Integrate Tracking',
    description:
      'Pass tracking IDs to your checkout flow to attribute sales automatically.',
    video: 'https://assets.refearnapp.com/Step-4.mp4',
  },
  {
    number: '05',
    title: 'Share Affiliate Portal',
    description:
      'Give affiliates a branded portal to generate links and view progress.',
    video: 'https://assets.refearnapp.com/Step-5.mp4',
  },
  {
    number: '06',
    title: 'Track Performance',
    description: 'Monitor real-time analytics as your affiliates drive growth.',
    video: 'https://assets.refearnapp.com/Step-6.mp4',
  },
];

const scrollToStep = (index) => {
  const el = document.getElementById('step-trigger-' + index);
  if (el) {
    window.scrollTo({
      top: el.offsetTop - window.innerHeight / 3,
      behavior: 'smooth',
    });
  }
};

onMounted(() => {
  const observerOptions = {
    root: null,
    rootMargin: '-30% 0% -30% 0%', // Trigger closer to middle
    threshold: 0.2,
  };

  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        const index = parseInt(entry.target.id.split('-').pop());
        activeStep.value = index;
      }
    });
  }, observerOptions);

  document.querySelectorAll('.step-item').forEach((el) => observer.observe(el));
});
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.4s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.fade-slide-enter-active {
  transition: all 0.5s ease-out;
}
.fade-slide-enter-from {
  opacity: 0;
  transform: translateX(-20px);
}
.fade-slide-enter-active {
  transition: all 0.5s ease-out;
  width: 100%;
}
.sticky {
  will-change: transform;
}
</style>
