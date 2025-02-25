<template>
  <section :class="mergeClass">
    <div
      class="text-inherit relative z-10 flex flex-col tablet-wide:flex-row w-full"
    >
      <div
        class="tablet-wide:flex-[1_1_50%] tablet-wide:w-1/2 tablet-wide:mr-8"
        :class="{'pb-10 tablet:py-10 tablet-wide:py-[100px]':fullImg || data.fullImg}"
      >
        <SectionHeader v-if="data.title" :title="data.title" class="relative z-20" :class="{ 'max-w-sm text-gray-darkest':fullImg || data.fullImg}" />
        <div class="relative z-20" :class="{'tablet:p-[50px]':fullImg || data.fullImg}">
          <div
            v-if="data.content"
            class="content-html text-inherit"
            v-html="data.content"
          ></div>
          <CustomLink
            v-if="data.button_url && data.button_text"
            class="flex items-center w-fit text-sm tablet:text-base text-white hover:text-white font-medium uppercase mt-5 tablet:mt-11 px-6 tablet:px-8 py-4 rounded-full duration-300 after:content-[''] after:block after:w-[25px] after:h-0.5 after:bg-white after:ml-5 after:transition after:duration-300 hover:after:translate-x-1 bg-blue-main hover:bg-blue-main-hover"
            :url="data.button_url"
            :title="data.button_text"
          />
          <List v-if="data.list" :data="data.list" />
        </div>
        <svg v-if="data.decoration && data.decoration !== 'none' " 
          class="absolute z-10 -left-40 max-w-full hidden tablet-wide:block"
          :class="[data.decoration == 'top' ? 'top-1' : 'bottom-10']"
        width="324" height="324" viewBox="0 0 324 324" fill="none" xmlns="http://www.w3.org/2000/svg">
          <circle cx="162" cy="162" r="61" stroke="#F4F6F7" stroke-width="2"/>
          <circle cx="162" cy="162" r="104.5" stroke="#F4F6F7"/>
          <circle opacity="0.75" cx="162" cy="162" r="161.5" stroke="#F4F6F7"/>
        </svg>

      </div>
      <div
        class="tablet-wide:flex-[1_1_50%] tablet-wide:w-1/2"
        :class="{'mb-5 tablet-wide:ml-8' :!fullImg || data.fullImg}"
      >
        <Globe v-if="globeImg" />
        <CustomLink
          v-else-if="data.image && data.image_url"
          :url="data.image_url"
          :isExternal="true"
        >
          <component
            :is="fullImg || data.fullImg ? 'HomepageImage' : 'SectionImage'"
            :url="data.image.url ? data.image.url : ''"
            :title="data.image.title ? data.image.title : ''"
            :alt="data.image.alt ? data.image.alt : ''"
            :imageDecoration="data.image_decoration"
            :class="{'!pl-0 mx-[-12.5%] tablet-wide:mx-0 tablet-wide:absolute inset-y-0 left-1/2 right-[-12.5%]':fullImg || data.fullImg}"
          />
        </CustomLink>
        <component
          v-else-if="data.image"
          :is="fullImg || data.fullImg ? 'HomepageImage' : 'SectionImage'"
          :url="data.image.url ? data.image.url : ''"
          :title="data.image.title ? data.image.title : ''"
          :alt="data.image.alt ? data.image.alt : ''"
          :imageDecoration="data.image_decoration"
          :class="{'!pl-0 mx-[-12.5%] tablet-wide:mx-0 tablet-wide:absolute inset-y-0 left-1/2 right-[-12.5%]':fullImg || data.fullImg}"
        />
      </div>
    </div>
  </section>
</template>

<script>
import SectionHeader from './section-header.vue'
import SectionImage from './section-image.vue'
import HomepageImage from './homepage-image.vue'
import List from './list.vue'
import Globe from './globe.vue'

export default {
  name: 'section_two_column',
  components: {
    SectionHeader,
    SectionImage,
    HomepageImage,
    List,
    Globe,
  },
  props: {
    data: {
      type: Object,
      required: false,
      default: () => {},
    },
    staticClass: {
      type: String,
      required: false,
      default: '',
    },
    fullImg: {
      type: Boolean,
      required: false,
      default: false,
    },
    globeImg: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
  computed: {
    mergeClass: function () {
      return (
        'bg-white relative w-full text-gray-dark' +
        ' ' +
        this.staticClass + ' ' +
        (this.fullImg || this.data?.fullImg ? ' ' : 'pb-5 tablet-wide:pb-1')
      )
    },
  },
}
</script>

<style scoped>
.content-html :deep( h1 ),
.content-html :deep( h2 ),
.content-html :deep( h3 ),
.content-html :deep( h4 ),
.content-html :deep( h5 ),
.content-html :deep( h6 ),
.content-html :deep( li ),
.content-html :deep( b ),
.content-html :deep( u ),
.content-html :deep( *:not(p):not(iframe)  ){
  width: auto !important;
  max-width: 100% !important;
}

.content-html :deep( .wp-caption-text ){
  width: 100% !important;
}
.content-html :deep( div ),
.content-html :deep( code ){
  @apply text-inherit font-lato;
}
.content-html :deep( h1 ){
  @apply text-4xl tablet:text-[50px] mb-5;
}
.content-html :deep( h2 ){
  @apply text-3xl tablet:text-4xl mb-5;
}
.content-html :deep( h3 ){
  @apply text-2xl tablet:text-3xl mb-5;
}
.content-html :deep( h4 ){
  @apply text-xl tablet:text-2xl mb-5;
}
.content-html :deep( h5 ){
  @apply text-lg tablet:text-xl mb-5;
}
.content-html :deep( h6 ){
  @apply text-base tablet:text-lg mb-5;
}
.content-html :deep( p ){
  @apply text-base inline-block mb-5 w-full text-justify text-inherit;
}

.content-html :deep( li ){
  @apply text-gray-dark;
}

.content-html :deep( ol li ){
  @apply list-disc ml-5;
}

.content-html :deep( ol ),
.content-html :deep( ul ) {
  @apply mb-5;
}
.content-html :deep(ul li::before) {
  background-size: contain;
  background-image: url("/list-icon.svg");  
  @apply content-[''] shrink-0 grow-0 w-6 h-6 tablet:w-10 tablet:h-10 bg-no-repeat inline-block relative mr-2 tablet:mr-5 tablet:-top-1
}
.content-html :deep(ul li) {
  @apply mb-[30px] text-lg tablet:text-xl desktop:text-2xl text-gray-darkest flex
}

.content-html :deep( hr ){
  @apply block mx-[10%] mt-5 mb-10;
}

.content-html :deep( code ){
  @apply block whitespace-pre-wrap max-w-2xl bg-gray-light p-2.5 tablet:p-5 rounded-md mb-10;
}

.content-html :deep( img ){
  @apply max-w-full w-auto h-auto;
}

.content-html :deep( iframe ){
  @apply max-w-full h-auto;
}

.content-html :deep( iframe[src*='www.youtu'] ){
  @apply w-full aspect-video;
}
</style>
