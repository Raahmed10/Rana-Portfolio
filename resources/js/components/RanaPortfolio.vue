<template>
  <div :dir="dir" :lang="lang" class="min-h-screen">
    <!-- Header -->
    <header
      id="site-header"
      class="fixed top-0 w-full z-50 flex justify-between items-center px-6 py-4
             text-[#5c6c7d] bg-[#C3D3E4]
             shadow-[0_8px_18px_rgba(191,219,243,0.2)]"
    >
      <div class="flex items-center gap-4">
        <button id="menu-open" class="text-2xl text-[#4e545c]" @click="openMenu" aria-label="Open menu">
          <i class="fa-solid fa-bars"></i>
        </button>

        <button
          class="cursor-pointer text-xl text-[#4e545c]"
          @click.stop="toggleLang"
          aria-label="Toggle language"
        >
          <i class="fa-solid fa-globe"></i>
        </button>
      </div>
    </header>

    <!-- Overlay (menu) -->
    <div
      id="menu-overlay"
      class="fixed inset-0 bg-black/40 z-40 transition-opacity duration-300"
      :class="isMenuOpen ? 'opacity-100 pointer-events-auto' : 'opacity-0 pointer-events-none'"
      @click="closeMenu"
    ></div>

    <!-- Navigation -->
    <nav
      id="menu"
      class="fixed top-0 h-full w-64 z-50 bg-[#C3D3E4] shadow-lg transition-transform duration-300"
      :class="[menuSideClass, isMenuOpen ? 'translate-x-0' : menuHiddenClass]"
    >
      <ul class="flex flex-col p-6 space-y-4 text-[#5c6c7d]">
        <li class="flex">
          <button
            id="menu-close"
            class="text-[#4e545c] text-2xl focus:outline-none ms-auto"
            aria-label="Close menu"
            @click="closeMenu"
          >
            ✕
          </button>
        </li>

        <li>
          <a href="#about" class="block px-4 py-2 rounded hover:bg-[#E0E6EB]" @click="closeMenu">
            {{ t("about") }}
          </a>
        </li>
        <li>
          <a href="#certificates" class="block px-4 py-2 rounded hover:bg-[#E0E6EB]" @click="closeMenu">
            {{ t("certificates") }}
          </a>
        </li>
        <li>
          <a href="#services" class="block px-4 py-2 rounded hover:bg-[#E0E6EB]" @click="closeMenu">
            {{ t("skills") }}
          </a>
        </li>
        <li>
          <a href="#portfolio" class="block px-4 py-2 rounded hover:bg-[#E0E6EB]" @click="closeMenu">
            {{ t("projects") }}
          </a>
        </li>
        <li>
          <a href="#contact" class="block px-4 py-2 rounded hover:bg-[#E0E6EB]" @click="closeMenu">
            {{ t("contact") }}
          </a>
        </li>
      </ul>
    </nav>

    <!-- Page -->
   <main class="pt-14 md:pt-16">
      <!-- Profile Section -->
        <div class="bg-gradient-to-b from-[#E5EDF3] via-[#F6FAFB] to-[#F6FAFB] py-14 md:py-20">
        <div
          class="bg-white rounded-[40px] shadow-2xl p-10 md:p-14 mt-12
                 flex flex-col md:flex-row items-center gap-10
                 max-w-5xl mx-auto"
        >
          <div class="flex flex-col md:flex-row items-center gap-8">
            <!-- Image -->
            <div class="relative group shrink-0">
              <img
                :src="assets.photo"
                alt="profile"
                class="w-44 h-44 md:w-56 md:h-56 rounded-full object-cover object-[50%_15%]
                       shadow-xl border-4 border-white
                       transition-transform duration-500 group-hover:scale-105"
              />
              <div
                class="absolute inset-0 rounded-full
                       bg-gradient-to-t from-transparent via-white/30 to-transparent
                       opacity-50 pointer-events-none"
              ></div>
            </div>

            <!-- Text -->
            <div class="max-w-xl text-center md:text-left" :class="dir === 'rtl' ? 'md:text-right text-right' : ''">
              <p class="text-[#5c6c7d] text-lg mb-2 font-medium tracking-wide">
                {{ t("role") }}
              </p>

              <h1 class="text-[#C3D3E4] text-4xl md:text-5xl font-bold mb-2 leading-snug">
                {{ t("name") }}
              </h1>

              <h2 class="text-2xl md:text-3xl font-normal text-[#5c6c7d] mb-3">
                {{ t("major") }}
              </h2>

              <p class="text-gray-600 text-base md:text-lg mt-2 leading-relaxed">
                {{ t("headline") }}
              </p>
            </div>
          </div>
        </div>
      </div>

      <!-- About Me -->
      <section id="about" class="bg-[#F6FAFB] py-16">
        <div class="max-w-7xl mx-auto px-6 md:px-12">
          <h1 class="text-[#5c6c7d] text-4xl font-bold mb-8">
            {{ t("about") }}
          </h1>

          <p class="text-gray-700 text-lg mb-12">
            {{ t("aboutText") }}
          </p>

          <!-- Tabs -->
          <div class="w-full border rounded-lg bg-white shadow-md overflow-hidden mb-6 flex">
            <button
              class="flex-1 text-center px-6 py-3 font-semibold transition-all duration-200"
              :class="tabClass('skills')"
              @click="activeTab = 'skills'"
            >
              {{ t("tabSkills") }}
            </button>

            <button
              class="flex-1 text-center px-6 py-3 font-semibold transition-all duration-200"
              :class="tabClass('experience')"
              @click="activeTab = 'experience'"
            >
              {{ t("tabExperience") }}
            </button>

            <button
              class="flex-1 text-center px-6 py-3 font-semibold transition-all duration-200"
              :class="tabClass('education')"
              @click="activeTab = 'education'"
            >
              {{ t("tabEducation") }}
            </button>
          </div>

          <!-- Tab content -->
          <div class="w-full">
            <div v-show="activeTab === 'skills'">
              <ul class="space-y-4 text-gray-700">
                <li class="p-4 rounded-lg hover:bg-gray-50 transition-colors">
                  <span class="font-semibold text-[#1e2022] text-lg">{{ t("skill1Title") }}</span>
                  <p class="text-gray-600 mt-1">{{ t("skill1Desc") }}</p>
                </li>
                <li class="p-4 rounded-lg hover:bg-gray-50 transition-colors">
                  <span class="font-semibold text-[#1e2022] text-lg">{{ t("skill2Title") }}</span>
                  <p class="text-gray-600 mt-1">{{ t("skill2Desc") }}</p>
                </li>
                <li class="p-4 rounded-lg hover:bg-gray-50 transition-colors">
                  <span class="font-semibold text-[#1e2022] text-lg">{{ t("skill3Title") }}</span>
                  <p class="text-gray-600 mt-1">{{ t("skill3Desc") }}</p>
                </li>
              </ul>
            </div>

            <div v-show="activeTab === 'experience'">
              <ul class="space-y-4 text-gray-700">
                <li class="p-4 rounded-lg hover:bg-gray-50 transition-colors">
                  <span class="font-semibold text-[#1e2022] text-lg">{{ t("exp1Title") }}</span>
                  <p class="text-gray-600 mt-1">{{ t("exp1Desc") }}</p>
                </li>
                <li class="p-4 rounded-lg hover:bg-gray-50 transition-colors">
                  <span class="font-semibold text-[#1e2022] text-lg">{{ t("exp2Title") }}</span>
                  <p class="text-gray-600 mt-1">{{ t("exp2Desc") }}</p>
                </li>
                <li class="p-4 rounded-lg hover:bg-gray-50 transition-colors">
                  <span class="font-semibold text-[#1e2022] text-lg">{{ t("exp3Title") }}</span>
                  <p class="text-gray-600 mt-1">{{ t("exp3Desc") }}</p>
                </li>
              </ul>
            </div>

            <div v-show="activeTab === 'education'">
              <ul class="space-y-4 text-gray-700">
                <li class="p-4 rounded-lg hover:bg-gray-50 transition-colors">
                  <span class="font-semibold text-[#1e2022] text-lg">{{ t("edu1Title") }}</span>
                  <p class="text-gray-600 mt-1">{{ t("edu1Desc") }}</p>
                </li>
                <li class="p-4 rounded-lg hover:bg-gray-50 transition-colors">
                  <span class="font-semibold text-[#1e2022] text-lg">{{ t("edu2Title") }}</span>
                  <p class="text-gray-600 mt-1">{{ t("edu2Desc") }}</p>
                </li>
                <li class="p-4 rounded-lg hover:bg-gray-50 transition-colors">
                  <span class="font-semibold text-[#1e2022] text-lg">{{ t("edu3Title") }}</span>
                  <p class="text-gray-600 mt-1">{{ t("edu3Desc") }}</p>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </section>

      <!-- Certificates -->
      <section id="certificates" class="bg-[#F6FAFB] py-16">
        <div class="max-w-7xl mx-auto px-6 md:px-12">
          <h1 class="text-[#5c6c7d] text-4xl font-bold mb-12">
            {{ t("certificates") }}
          </h1>

          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
            <button
              type="button"
              class="bg-white shadow-md rounded-lg overflow-hidden cursor-pointer transform hover:scale-105 transition duration-300 text-left"
              @click="openCert({ src: assets.c1, title: t('c1Title') })"
            >
              <img :src="assets.c1" alt="Certificate 1" class="w-full h-60 object-cover" />
              <div class="p-4">
                <h3 class="text-[#5c6c7d] font-semibold text-lg">
                  {{ t("c1Title") }}
                </h3>
              </div>
            </button>

            <button
              type="button"
              class="bg-white shadow-md rounded-lg overflow-hidden cursor-pointer transform hover:scale-105 transition duration-300 text-left"
              @click="openCert({ src: assets.c2, title: t('c2Title') })"
            >
              <img :src="assets.c2" alt="Certificate 2" class="w-full h-60 object-cover" />
              <div class="p-4">
                <h3 class="text-[#5c6c7d] font-semibold text-lg">
                  {{ t("c2Title") }}
                </h3>
              </div>
            </button>

            <button
              type="button"
              class="bg-white shadow-md rounded-lg overflow-hidden cursor-pointer transform hover:scale-105 transition duration-300 text-left"
              @click="openCert({ src: assets.c3, title: t('c3Title') })"
            >
              <img :src="assets.c3" alt="Certificate 3" class="w-full h-60 object-cover" />
              <div class="p-4">
                <h3 class="text-[#5c6c7d] font-semibold text-lg">
                  {{ t("c3Title") }}
                </h3>
              </div>
            </button>
          </div>
        </div>
      </section>

      <!-- Certificates Modal -->
      <div
        v-if="certModalOpen"
        class="fixed inset-0 z-[60] bg-black/60 flex items-center justify-center p-4"
        @click="closeCert"
      >
        <div class="bg-white rounded-2xl max-w-4xl w-full overflow-hidden shadow-2xl" @click.stop>
          <div class="flex items-center justify-between px-5 py-4 border-b">
            <p class="font-semibold text-[#4e545c]">{{ certModal?.title }}</p>
            <button class="text-2xl text-[#4e545c]" @click="closeCert" aria-label="Close">✕</button>
          </div>
          <div class="p-4 bg-[#F6FAFB]">
            <img :src="certModal?.src" alt="Certificate" class="w-full h-auto rounded-xl" />
          </div>
        </div>
      </div>

      <!-- My Skills -->
      <section id="services" class="bg-[#F6FAFB] py-16">
        <div class="max-w-7xl mx-auto px-6 md:px-12">
          <h1 class="text-4xl font-bold text-[#5c6c7d] mb-12">
            {{ t("skills") }}
          </h1>

          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
            <div
              class="bg-white p-6 rounded-lg shadow-md flex flex-col items-center text-center cursor-pointer
                     transition-transform transform hover:scale-105 active:scale-95 active:shadow-inner"
            >
              <i class="fa-solid fa-globe text-4xl text-[#4e545c] mb-4"></i>
              <h2 class="text-xl font-semibold text-[#c3d3e4] mb-2">
                {{ t("skillCard1Title") }}
              </h2>
              <p class="text-gray-600">
                {{ t("skillCard1Desc") }}
              </p>
            </div>

            <div
              class="bg-white p-6 rounded-lg shadow-md flex flex-col items-center text-center cursor-pointer
                     transition-transform transform hover:scale-105 active:scale-95 active:shadow-inner"
            >
              <i class="fa-solid fa-mobile-screen-button text-4xl text-[#4e545c] mb-4"></i>
              <h2 class="text-xl font-semibold text-[#c3d3e4] mb-2">
                {{ t("skillCard2Title") }}
              </h2>
              <p class="text-gray-600">
                {{ t("skillCard2Desc") }}
              </p>
            </div>

            <div
              class="bg-white p-6 rounded-lg shadow-md flex flex-col items-center text-center cursor-pointer
                     transition-transform transform hover:scale-105 active:scale-95 active:shadow-inner"
            >
              <i class="fa-solid fa-brush text-4xl text-[#4e545c] mb-4"></i>
              <h2 class="text-xl font-semibold text-[#c3d3e4] mb-2">
                {{ t("skillCard3Title") }}
              </h2>
              <p class="text-gray-600">
                {{ t("skillCard3Desc") }}
              </p>
            </div>
          </div>
        </div>
      </section>

      <!-- My Projects -->
      <section id="portfolio" class="py-[180px] bg-[#F6FAFB]">
        <div class="max-w-7xl mx-auto px-6 md:px-12">
          <h1 class="text-3xl md:text-4xl font-bold text-left text-[#5c6c7d]">
            {{ t("projects") }}
          </h1>

          <div class="grid [grid-template-columns:repeat(auto-fit,minmax(250px,1fr))] gap-10 mt-[50px]">
            <div class="group relative overflow-hidden rounded-[10px]">
              <div class="flex flex-col md:flex-row justify-center items-center gap-4">
                <img
                  :src="assets.project1"
                  alt="Project Image 1"
                  class="w-[45%] rounded-[12px] transition-transform duration-500 group-hover:scale-[1.04]"
                />
                <img
                  :src="assets.project2"
                  alt="Project Image 2"
                  class="w-[45%] rounded-[12px] transition-transform duration-500 group-hover:scale-[1.04]"
                />
              </div>

              <div
                class="absolute inset-0 flex flex-col items-center justify-center p-5 text-center
                       bg-gradient-to-t from-[rgba(195,211,228,0.75)] to-[rgba(195,211,228,0.25)]
                       opacity-0 transition-opacity duration-[400ms] group-hover:opacity-100"
              >
                <h3 class="m-0 text-[32px] md:text-[40px] font-bold text-[#4e545c]">
                  {{ t("projectTitle") }}
                </h3>
                <p class="mt-4 text-[16px] md:text-[20px] max-w-full text-[#5c6c7d]">
                  {{ t("projectDesc") }}
                </p>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Contact -->
      <section class="bg-[#F6FAFB] py-16">
        <div id="contact" class="max-w-7xl mx-auto px-6 md:px-12">
          <h1 class="text-3xl font-bold text-left mb-10 text-[#5c6c7d]">
            {{ t("contact") }}
          </h1>

          <div class="grid grid-cols-1 md:grid-cols-4 gap-6 md:gap-8">
            <a
              :href="assets.emailHref"
              class="bg-white p-6 rounded-xl shadow-md hover:shadow-xl transition duration-300 flex flex-col items-center text-center"
              target="_blank"
              rel="noreferrer"
            >
              <div class="flex flex-col items-center gap-3">
                <i class="fa-regular fa-paper-plane text-3xl text-[#5c6c7d]"></i>
                <span class="text-lg font-semibold text-[#5c6c7d]">{{ t("email") }}</span>
              </div>
            </a>

            <a
              :href="assets.phoneHref"
              class="bg-white p-6 rounded-xl shadow-md hover:shadow-xl transition duration-300 flex flex-col items-center text-center"
              target="_blank"
              rel="noreferrer"
            >
              <div class="flex flex-col items-center gap-3">
                <i class="fa-solid fa-phone text-3xl text-[#5c6c7d]"></i>
                <span class="text-lg font-semibold text-[#5c6c7d]">{{ t("phone") }}</span>
              </div>
            </a>

            <a
              :href="assets.cv"
              class="bg-white p-6 rounded-xl shadow-md hover:shadow-xl transition duration-300 flex flex-col items-center text-center"
              target="_blank"
              rel="noreferrer"
            >
              <div class="flex flex-col items-center gap-3">
                <i class="fa-regular fa-file-lines text-3xl text-[#5c6c7d]"></i>
                <span class="text-lg font-semibold text-[#5c6c7d]">{{ t("cv") }}</span>
              </div>
            </a>

            <div class="bg-white p-6 rounded-xl shadow-md flex flex-col items-center text-center">
              <div class="flex flex-col items-center gap-3 mb-4">
                <i class="fa-solid fa-share-nodes text-3xl text-[#5c6c7d]"></i>
                <span class="text-lg font-semibold text-[#5c6c7d]">{{ t("social") }}</span>
              </div>
              <div class="flex gap-4">
                <a
                  :href="assets.instagram"
                  target="_blank"
                  rel="noreferrer"
                  aria-label="Instagram"
                  class="text-[#5c6c7d] hover:text-pink-500 transition"
                >
                  <i class="fa-brands fa-instagram text-2xl"></i>
                </a>
                <a
                  :href="assets.linkedin"
                  target="_blank"
                  rel="noreferrer"
                  aria-label="LinkedIn"
                  class="text-[#5c6c7d] hover:text-blue-600 transition"
                >
                  <i class="fa-brands fa-linkedin-in text-2xl"></i>
                </a>
                <a
                  :href="assets.whatsapp"
                  target="_blank"
                  rel="noreferrer"
                  aria-label="WhatsApp"
                  class="text-[#5c6c7d] hover:text-green-500 transition"
                >
                  <i class="fa-brands fa-whatsapp text-2xl"></i>
                </a>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Footer / Copyright -->
      <div class="bg-[#F6FAFB] py-6">
        <p class="text-sm text-[#5c6c7d] text-center px-6">
          {{ t("copyright") }}
        </p>
      </div>

      <!-- Back to top -->
      <a
        href="#"
        class="fixed bottom-5 right-5 z-50 w-9 h-9 rounded-full
       bg-[#5c6c7d] text-white
       flex items-center justify-center
       shadow-md
       hover:bg-[#F6FAFB] hover:text-[#5c6c7d]
       transition-all duration-300"

        :class="showBackToTop ? 'opacity-100 visible scale-100' : 'opacity-0 invisible scale-90'"
        aria-label="Back to top"
        @click.prevent="scrollTop"
      >
        <i class="fa-solid fa-arrow-up text-sm"></i>
      </a>
    </main>
  </div>
</template>

<script setup>
import { computed, onBeforeUnmount, onMounted, ref } from "vue";


const assets = {
  photo: "/image/Photo.png",
  c1: "/image/C1.jpg",
  c2: "/image/C2.jpg",
  c3: "/image/C3.jpg",
  project1: "/image/image0.png",
  project2: "/image/image00.png",
  cv: "/image/Rana Ahmed Nasser Abuhaimed  1.pdf",

  emailHref: "mailto:ranaalh728@gmail.com",
  phoneHref: "tel:+966553180111",
  instagram: "https://instagram.com/raabuhaimed",
  linkedin: "https://linkedin.com/in/rana-abuhaimed",
  whatsapp: "https://wa.me/966553180111",
};

/** Language */
const lang = ref(localStorage.getItem("lang") || "en");
const dir = computed(() => (lang.value === "ar" ? "rtl" : "ltr"));

const dict = {
  en: {
    about: "About Me",
    certificates: "Certificates",
    skills: "My Skills",
    projects: "My Projects",
    contact: "Contact Me",

    role: "UI/UX Designer",
    name: "Rana Ahmed Abuhaimed",
    major: "Software Engineering Majer",
    headline: "Passionate about crafting beautiful UI/UX and building smart software solutions.",

    aboutText:
      "I am Rana Abuhaimed, an advanced Software Engineering student. I have a strong academic and practical background in software development, system design, and requirements analysis. I am passionate about building scalable technical solutions that improve efficiency and deliver real value, and I enjoy designing seamless user experiences through UI/UX and making data-driven decisions.",

    tabSkills: "Skills",
    tabExperience: "Experience",
    tabEducation: "Education",

    skill1Title: "UI/UX",
    skill1Desc: "Designing web/App interfaces",
    skill2Title: "Web development",
    skill2Desc: "Web app development",
    skill3Title: "App development",
    skill3Desc: "Building Android/iOS apps",

    exp1Title: "COOP Trainee",
    exp1Desc: "Enterprise Architecture & Data | Solutions by STC (Sep 2026)",
    exp2Title: "Graduation Project",
    exp2Desc: "WJHATAK | Al Yamamah University (Dec 2025)",
    exp3Title: "Summer Training Program",
    exp3Desc: "Corporate & Institutional Banking | Bank AlJazira (Jul 2025)",

    edu1Title: "SQL Fundamentals for Data Analysts",
    edu1Desc: "Corporate Finance Institute (CFI) via Coursera",
    edu2Title: "Financial Statements in Power BI",
    edu2Desc: "Corporate Finance Institute (CFI) via Coursera",
    edu3Title: "Project Management Professional (PMP)",
    edu3Desc: "On-Campus University",

    c1Title: "SQL Fundamentals for Data Analysts",
    c2Title: "Financial Statements in Power BI",
    c3Title: "Project Management Professional (PMP)",

    skillCard1Title: "Web Development",
    skillCard1Desc:
      "I develop responsive web pages using HTML, CSS, and JavaScript to build clean and functional websites.",
    skillCard2Title: "UI/UX Development",
    skillCard2Desc:
      "I create user-friendly interfaces and improve user experience through research, wireframes, and prototypes.",
    skillCard3Title: "Web Design",
    skillCard3Desc:
      "I design modern and responsive websites with clean layouts that provide a great user experience.",

    projectTitle: "Graduation Project | WJHATAK",
    projectDesc:
      "A smart tourist guide was developed to help users explore Riyadh's landmarks and discover new places effortlessly. The project included designing UI/UX screens in Figma and implementing the web interface with HTML and CSS, focusing on ease of use, multilingual support, and a smooth user experience.",

    email: "Email",
    phone: "Phone",
    cv: "CV",
    social: "Social Media",

    copyright: "Made with ❤️ © 2026 Rana Abuhaimed. All rights reserved.",
  },
  ar: {
    about: "نبذة عني",
    certificates: "الشهادات",
    skills: "مهاراتي",
    projects: "مشاريعي",
    contact: "تواصل معي",

    role: "مصممة واجهات وتجربة مستخدم",
    name: "رنا أحمد أبوحيمد",
    major: "تخصص هندسة برمجيات",
    headline: "شغوفة بتصميم واجهات مستخدم جذابة وبناء حلول برمجية ذكية.",

    aboutText:
      "أنا رنا أبوحيمد، طالبة هندسة برمجيات متقدمة. أمتلك خلفية أكاديمية وعملية في تطوير البرمجيات، وتصميم الأنظمة، وتحليل المتطلبات. شغوفة ببناء حلول تقنية قابلة للتوسع تسهم في تحسين الكفاءة وتقديم قيمة حقيقية، كما أستمتع بتصميم تجارب مستخدم سلسة من خلال UI/UX، واتخاذ قرارات مدعومة بالبيانات.",

    tabSkills: "المهارات",
    tabExperience: "الخبرة",
    tabEducation: "التعليم",

    skill1Title: "تصميم واجهات المستخدم",
    skill1Desc: "تصميم واجهات المواقع والتطبيقات",
    skill2Title: "تطوير الويب",
    skill2Desc: "تطوير تطبيقات الويب",
    skill3Title: "تطوير التطبيقات",
    skill3Desc: "بناء تطبيقات أندرويد و iOS",

    exp1Title: "التدريب التعاوني",
    exp1Desc: "هندسة المؤسسات والبيانات | حلول STC (سبتمبر 2026)",
    exp2Title: "مشروع التخرج",
    exp2Desc: "WJHATAK | جامعة اليمامة (ديسمبر 2025)",
    exp3Title: "برنامج التدريب الصيفي",
    exp3Desc: "الخدمات المصرفية للشركات والمؤسسات | بنك الجزيرة (يوليو 2025)",

    edu1Title: "أساسيات SQL لمحللي البيانات",
    edu1Desc: "معهد التمويل المؤسسي (CFI) عبر كورسيرا",
    edu2Title: "البيانات المالية في Power BI",
    edu2Desc: "معهد التمويل المؤسسي (CFI) عبر كورسيرا",
    edu3Title: "محترف إدارة المشاريع (PMP)",
    edu3Desc: "جامعة داخل الحرم الجامعي",

    c1Title: "أساسيات SQL لمحللي البيانات",
    c2Title: "البيانات المالية في Power BI",
    c3Title: "محترف إدارة المشاريع (PMP)",

    skillCard1Title: "تطوير الويب",
    skillCard1Desc:
      "أقوم بتطوير صفحات ويب متجاوبة باستخدام HTML وCSS وJavaScript لبناء مواقع نظيفة وعملية.",
    skillCard2Title: "تطوير واجهات وتجربة المستخدم",
    skillCard2Desc:
      "أقوم بإنشاء واجهات سهلة الاستخدام وتحسين تجربة المستخدم من خلال البحث والنماذج الأولية.",
    skillCard3Title: "تصميم الويب",
    skillCard3Desc:
      "أقوم بتصميم مواقع حديثة ومتجاوبة بتنسيقات نظيفة توفر تجربة مستخدم ممتازة.",

    projectTitle: "مشروع التخرج | WJHATAK",
    projectDesc:
      "تم تطوير دليل سياحي ذكي يساعد المستخدمين على استكشاف معالم الرياض وأماكن جديدة بسهولة. شمل المشروع تصميم شاشات UI/UX في Figma وتنفيذ واجهة الويب باستخدام HTML وCSS، مع التركيز على سهولة الاستخدام ودعم تعدد اللغات وتجربة مستخدم سلسة.",

    email: "البريد الإلكتروني",
    phone: "الهاتف",
    cv: "السيرة الذاتية",
    social: "وسائل التواصل",

    copyright: "تم الإنشاء بحب ❤️ © 2026 رنا أبوحيمد. كل الحقوق محفوظة.",
  },
};

function t(key) {
  return dict[lang.value]?.[key] ?? key;
}

function toggleLang() {
  lang.value = lang.value === "en" ? "ar" : "en";
  localStorage.setItem("lang", lang.value);
  closeMenu();
}

/** Menu */
const isMenuOpen = ref(false);
const menuSideClass = computed(() => (dir.value === "rtl" ? "right-0" : "left-0"));
const menuHiddenClass = computed(() => (dir.value === "rtl" ? "translate-x-full" : "-translate-x-full"));
function openMenu() {
  isMenuOpen.value = true;
}
function closeMenu() {
  isMenuOpen.value = false;
}

/** Tabs */
const activeTab = ref("skills");
function tabClass(tab) {
  return {
    "bg-[#E5EDF3] text-[#5c6c7d]": activeTab.value === tab,
    "text-gray-500 hover:text-[#5c6c7d]": activeTab.value !== tab,
  };
}

/** Back to top */
const showBackToTop = ref(false);
function onScroll() {
  showBackToTop.value = window.scrollY > 300;
}
function scrollTop() {
  window.scrollTo({ top: 0, behavior: "smooth" });
}

/** Certificates modal */
const certModalOpen = ref(false);
const certModal = ref(null);
function openCert(payload) {
  certModal.value = payload;
  certModalOpen.value = true;
}
function closeCert() {
  certModalOpen.value = false;
  certModal.value = null;
}

onMounted(() => {
  window.addEventListener("scroll", onScroll, { passive: true });
  onScroll();
});
onBeforeUnmount(() => {
  window.removeEventListener("scroll", onScroll);
});
</script>
