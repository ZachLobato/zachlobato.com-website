<template>
  <article
    role="article"
    @mouseenter="isHovered = true"
    @mouseleave="isHovered = false"
    @touchend="isHovered = !isHovered"
    class="card rounded-lg bg-cadet-gray-100 dark:bg-cadet-gray-900 w-80 h-64 lg:w-80"
  >
    <section class="w-full lg:w-full h-64 overflow-hidden rounded-lg">
      <header class="drop-shadow-[0_4px_8px_rgba(255,255,255,0.25)] dark:drop-shadow-[0_4px_8px_rgba(0,0,0,0.75)] relative">
        <div v-if="isWebPageMirror" class="relative w-full" :class="{ 'h-32': isHovered, 'h-48': !isHovered }">
          <iframe
            v-if="shouldRenderIframe"
            ref="iframeRef"
            :src="iframeSrc"
            title="Two-deep page mirror"
            class="absolute inset-0 w-full h-full rounded-lg"
            :style="scaledStyle"
            loading="lazy"
            :sandbox="mirrorSandbox"
            scrolling="no"
            aria-hidden
            tabindex="-1"
            @load="onIframeLoad"
          />

          <div v-if="showGhost" aria-hidden class="pointer-events-none fixed inset-0" :style="{ zIndex: 2147483646 }">
            <div
              ref="dotRef"
              :style="{
                position: 'fixed',
                top: 0,
                left: 0,
                width: '14px',
                height: '14px',
                borderRadius: '9999px',
                boxShadow: '0 0 0 2px rgba(0,0,0,.15)',
                background: 'white',
                mixBlendMode: 'difference',
                opacity: cursorVisible ? 0.9 : 0,
                transition: 'opacity 120ms linear',
                willChange: 'transform, opacity',
                transform: `translate(${Math.round(cursorX)}px, ${Math.round(cursorY)}px)`,
              }"
            />
          </div>
        </div>

        <div v-else>
          <img
            v-if="(resolvedBannerImageUrl || resolvedBannerDarkImageUrl) && !hasVideo"
            :aria-expanded="!isHovered"
            :alt="`Banner for ${title}`"
            :class="{
              'card-image': true,
              'object-center': true,
              'object-cover': true,
              'w-full': true,
              'h-32': isHovered,
              'h-48': !isHovered,
              'transition-all': true,
            }"
            :src="prefersDark ? resolvedBannerDarkImageUrl : resolvedBannerImageUrl"
          />
          <video
            v-if="hasVideo"
            :alt="`Video Banner for ${title}`"
            tabindex="-1"
            :class="{
              'card-video': true,
              'object-center': true,
              'object-cover': true,
              'w-full': true,
              'h-32': isHovered,
              'h-48': !isHovered,
              'transition-all': true,
            }"
            :src="prefersDark ? resolvedBannerDarkVideoUrl : resolvedBannerVideoUrl"
            loop
            autoplay
            muted
            playsinline
          ></video>
        </div>
      </header>

      <div
        :class="{
          'card-content': true,
          'px-4': true,
          'py-2': true,
          'flex': true,
          'flex-col': true,
          'transition-all': true,
          'justify-between': true,
          'h-32': true,
        }"
      >
        <div>
          <h3 class="card-title text-2xl font-semibold dark:text-pistachio-400 text-pistachio-600">{{ title }}</h3>
          <p class="card-subtitle text-xs text-cadet-gray-600 dark:text-cadet-gray-400">{{ subTitle }}</p>
        </div>
        <footer class="grid grid-cols-2 content-around content-end">
          <section class="icons flex gap-3 content-around">
            <span v-if="underConstruction" :title="`Under Construction (${title})`">
              <ConstructionWorker
                class="construction dark:text-cadet-gray-200 text-cadet-gray-800"
                tabindex="-1"
                @focus="isHovered = true"
                @blur="isHovered = false"
                :alt="`${title} is still under construction`"
                :aria-label="`${title} is still under construction`"
              />
            </span>
            <a
              class="inline-block dark:text-prussian-blue-200 text-prussian-blue-800 hover:text-mint-green-800 dark:hover:text-mint-green-200"
              v-if="launchUrl"
              :href="launchUrl"
              target="_blank"
              rel="noopener noreferrer"
              :alt="`Launch link to ${title} project`"
              :aria-label="`Launch link to ${title} project`"
              :title="`Launch (${title})`"
            >
              <MaterialRocketLaunchOutline class="launch" tabindex="0" @focus="isHovered = true" @blur="isHovered = false" />
            </a>
            <a
              class="inline-block dark:text-prussian-blue-200 text-prussian-blue-800 hover:text-mint-green-800 dark:hover:text-mint-green-200"
              v-if="githubUrl"
              :href="githubUrl"
              target="_blank"
              rel="noopener noreferrer"
              :alt="`GitHub link to ${title} project`"
              :aria-label="`GitHub link to ${title} project`"
              :title="`GitHub (${title})`"
            >
              <BiGithub class="github" tabindex="0" @focus="isHovered = true" @blur="isHovered = false" />
            </a>
            <a
              class="inline-block dark:text-prussian-blue-200 text-prussian-blue-800 hover:text-mint-green-800 dark:hover:text-mint-green-200"
              v-if="notionUrl"
              :href="notionUrl"
              target="_blank"
              rel="noopener noreferrer"
              :alt="`Notion link to ${title} project`"
              :aria-label="`Notion link to ${title} project`"
              :title="`Notion (${title})`"
            >
              <CibNotion class="notion" tabindex="0" @focus="isHovered = true" @blur="isHovered = false" />
            </a>
          </section>
          <div class="text-xs dark:text-cadet-gray-200 text-cadet-gray-800 place-self-end">{{ updatedAt }}</div>
        </footer>
      </div>
    </section>
  </article>
</template>

<script lang="ts" setup>
import { ref, watchEffect, onUnmounted, onMounted, onBeforeUnmount, computed, watch } from 'vue'
import CibNotion from './icons/IconCibNotion.vue'
import BiGithub from './icons/IconGithub.vue'
import MaterialRocketLaunchOutline from './icons/IconMaterialRocketLaunchOutline.vue'
import ConstructionWorker from './icons/IconEmConstructionWorker.vue'

// === Props ===
const props = withDefaults(defineProps<{
  title: string
  updatedAt: string
  subTitle?: string
  bannerImageUrl?: string
  bannerDarkImageUrl?: string
  bannerVideoUrl?: string
  bannerDarkVideoUrl?: string
  launchUrl?: string
  githubUrl?: string
  notionUrl?: string
  underConstruction?: boolean

  /** Enable the two-deep webpage mirror in the banner slot */
  isWebPageMirror?: boolean
  /** Scale of the mirror inside the header area */
  mirrorScale?: number
  /** Max depth to recurse (0 = none, 1 = one-deep, 2 = two-deep). Default 2. */
  mirrorMaxDepth?: number
  /** Sandbox attrs for the iframe */
  mirrorSandbox?: string
  /** Strict target origin for postMessage; default '*' but set your origin in prod. */
  mirrorTargetOrigin?: string

  /** Media caching controls */
  mediaCacheEnabled?: boolean
  mediaCacheName?: string
}>(), {
  isWebPageMirror: false,
  mirrorScale: 0.5,
  mirrorMaxDepth: 8,
  mirrorSandbox: 'allow-same-origin allow-scripts allow-forms allow-popups allow-pointer-lock',
  mirrorTargetOrigin: '*',
  mediaCacheEnabled: true,
  mediaCacheName: 'portfolio-media-cache-v1',
})

// === Hover/Dark Mode ===
const isHovered = ref(false)
const prefersDark = ref(window.matchMedia('(prefers-color-scheme: dark)').matches)
watchEffect(() => {
  const mq = window.matchMedia('(prefers-color-scheme: dark)')
  const handler = (e: MediaQueryListEvent) => { prefersDark.value = e.matches }
  mq.addEventListener('change', handler)
  onUnmounted(() => mq.removeEventListener('change', handler))
})

// === Media caching (images + videos) ===
const hasVideo = computed(() => !!(props.bannerVideoUrl || props.bannerDarkVideoUrl))

const resolvedBannerImageUrl = ref<string | undefined>(props.bannerImageUrl)
const resolvedBannerDarkImageUrl = ref<string | undefined>(props.bannerDarkImageUrl)
const resolvedBannerVideoUrl = ref<string | undefined>(props.bannerVideoUrl)
const resolvedBannerDarkVideoUrl = ref<string | undefined>(props.bannerDarkVideoUrl)

const blobUrls: string[] = []

async function getCachedAssetUrl(url?: string): Promise<string | undefined> {
  if (!url) return undefined
  if (!props.mediaCacheEnabled || !('caches' in window)) return url
  try {
    const cache = await caches.open(props.mediaCacheName)
    const cached = await cache.match(url)
    if (cached) {
      // If opaque (cross-origin without CORS), we can't read the body; fall back to direct URL.
      if (cached.type === 'opaque') return url
      const blob = await cached.blob()
      const obj = URL.createObjectURL(blob)
      blobUrls.push(obj)
      return obj
    } else {
      // Try CORS first so we can read the blob; if it fails, fall back to direct URL and still cache if possible.
      let resp: Response | undefined
      try {
        resp = await fetch(url, { mode: 'cors' })
      } catch {
        try { resp = await fetch(url, { mode: 'no-cors' }) } catch {}
      }
      if (!resp || !resp.ok) throw new Error(`Failed to fetch asset: ${url}`)
      try { await cache.put(url, resp.clone()) } catch {}
      // If opaque, we can't blob(); return original URL so the browser streams it.
      if (resp.type === 'opaque') return url
      const blob = await resp.blob()
      const obj = URL.createObjectURL(blob)
      blobUrls.push(obj)
      return obj
    }
  } catch (e) {
    console.warn('Media cache error', e)
    return url
  }
}

async function resolveMediaAssets() {
  // images
  resolvedBannerImageUrl.value = await getCachedAssetUrl(props.bannerImageUrl)
  resolvedBannerDarkImageUrl.value = await getCachedAssetUrl(props.bannerDarkImageUrl)
  // videos
  resolvedBannerVideoUrl.value = await getCachedAssetUrl(props.bannerVideoUrl)
  resolvedBannerDarkVideoUrl.value = await getCachedAssetUrl(props.bannerDarkVideoUrl)
}

onMounted(() => {
  resolveMediaAssets()
  // Idle pre-warm for whatever is not yet cached
  if (props.mediaCacheEnabled && 'requestIdleCallback' in window) {
    ;(window as any).requestIdleCallback(async () => {
      try {
        const cache = await caches.open(props.mediaCacheName)
        const urls = [
          props.bannerImageUrl,
          props.bannerDarkImageUrl,
          props.bannerVideoUrl,
          props.bannerDarkVideoUrl,
        ].filter(Boolean) as string[]
        for (const u of urls) {
          const match = await cache.match(u)
          if (!match) {
            try { await cache.add(u) } catch {}
          }
        }
      } catch {}
    })
  }
})

// Re-resolve when any media URL prop changes
watch(
  () => [props.bannerImageUrl, props.bannerDarkImageUrl, props.bannerVideoUrl, props.bannerDarkVideoUrl],
  () => resolveMediaAssets()
)

onUnmounted(() => {
  // Revoke blob: URLs to avoid memory leaks
  blobUrls.forEach(u => { try { URL.revokeObjectURL(u) } catch {} })
})

// === Mirror logic ===
function getDepthFromURL(): number {
  const usp = new URLSearchParams(window.location.search)
  const q = usp.get('embedDepth')
  const d = q ? parseInt(q, 10) : 0
  return Number.isNaN(d) ? 0 : d
}
const depth = getDepthFromURL()

const iframeRef = ref<HTMLIFrameElement | null>(null)
const frameReady = ref(false)
const cursorX = ref(0)
const cursorY = ref(0)
const cursorVisible = ref(true)

const shouldRenderIframe = computed(() => props.isWebPageMirror && depth < props.mirrorMaxDepth)
const showGhost = computed(() => props.isWebPageMirror && depth >= 1 && !prefersReducedMotion())

const iframeSrc = computed(() => {
  const url = new URL(window.location.href)
  url.searchParams.set('embedDepth', String(depth + 1))
  return url.toString()
})

function prefersReducedMotion(): boolean {
  return 'matchMedia' in window && window.matchMedia('(prefers-reduced-motion: reduce)').matches
}

const scaledStyle = computed(() => ({
  transform: `scale(${props.mirrorScale})`,
  transformOrigin: 'top left',
  width: `${100 / props.mirrorScale}%`,
  height: `${100 / props.mirrorScale}%`,
  overflow: 'hidden',
}))

function onIframeLoad() {
  const doc = iframeRef.value?.contentDocument;
  if (doc) {
    const style = doc.createElement('style');
    style.textContent = `
      html, body {
        overflow: hidden !important;
        scrollbar-width: none !important;
      }
      ::-webkit-scrollbar {
        display: none !important;
      }
    `;
    doc.head.appendChild(style);
  }
  frameReady.value = true;
}

function clamp01(n: number) { return Math.max(0, Math.min(1, n)) }

let rafId = 0
let mmX = 0, mmY = 0
let scX = 0, scY = 0
let needsSend = false

function startParentStreamer() {
  if (!props.isWebPageMirror || prefersReducedMotion() || depth !== 0) return
  const onMouseMove = (e: MouseEvent) => { mmX = e.clientX; mmY = e.clientY; needsSend = true }
  const onScroll = () => { scX = window.scrollX; scY = window.scrollY; needsSend = true }
  const onResize = () => { needsSend = true }

  const tick = () => {
    const iframe = iframeRef.value
    if (needsSend && iframe && iframe.contentWindow) {
      iframe.contentWindow.postMessage({
        type: 'mirror-state',
        cx: clamp01(mmX / window.innerWidth),
        cy: clamp01(mmY / window.innerHeight),
        w: window.innerWidth,
        h: window.innerHeight,
        scrollX: scX,
        scrollY: scY,
        showCursor: true,
      }, props.mirrorTargetOrigin)
      needsSend = false
    }
    rafId = requestAnimationFrame(tick)
  }

  window.addEventListener('mousemove', onMouseMove, { passive: true })
  window.addEventListener('scroll', onScroll, { passive: true })
  window.addEventListener('resize', onResize)
  rafId = requestAnimationFrame(tick)

  onBeforeUnmount(() => {
    window.removeEventListener('mousemove', onMouseMove as any)
    window.removeEventListener('scroll', onScroll as any)
    window.removeEventListener('resize', onResize as any)
    cancelAnimationFrame(rafId)
  })
}

// Embed (depth >= 1): receive + mirror; at depth 1 also forward to child
function startEmbedReceiver() {
  if (!props.isWebPageMirror || prefersReducedMotion() || depth < 1) return

  const onMessage = (ev: MessageEvent) => {
    if (!ev.data || ev.data.type !== 'mirror-state') return
    const { cx, cy, w, h, scrollX, scrollY, showCursor } = ev.data

    cursorVisible.value = !!showCursor
    cursorX.value = cx * w
    cursorY.value = cy * h

    try {
      if (typeof scrollX === 'number' && typeof scrollY === 'number') {
        window.scrollTo({ left: scrollX, top: scrollY, behavior: 'instant' as any })
      }
    } catch {}

    if (depth === 1) {
      const child = iframeRef.value?.contentWindow
      if (child) child.postMessage(ev.data, props.mirrorTargetOrigin)
    }
  }

  window.addEventListener('message', onMessage)
  onBeforeUnmount(() => window.removeEventListener('message', onMessage))
}

onMounted(() => {
  startParentStreamer()
  startEmbedReceiver()
})
</script>
