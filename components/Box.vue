<script setup lang="ts">
interface WhyItem {
  strong: string
  text: string
}

interface Props {
  label?: string
  items?: WhyItem[]
  accent?: string
  bgFrom?: string
  bgTo?: string
  borderColor?: string
  dashedColor?: string
  startClick?: number
}

const props = withDefaults(defineProps<Props>(), {
  label: 'Why Use This?',
  items: () => [],
  accent: '#0f9884',
  bgFrom: '#f2fbf9',
  bgTo: '#e6f7f3',
  borderColor: '#cdeee6',
  dashedColor: '#7fd0bf',
  startClick: 1,
})
</script>

<template>
  <div
    class="why-box"
    :style="{
      '--accent': accent,
      '--bg-from': bgFrom,
      '--bg-to': bgTo,
      '--border-color': borderColor,
      '--dashed-color': dashedColor,
    }"
    v-click="startClick"
  >
    <div class="why-box-outer">
      <span class="why-box-label">{{ label }}</span>

      <ul v-if="items.length" class="why-box-list">
        <li
          v-for="(item, i) in items"
          :key="i"
          v-click="startClick + i + 1"
        >
          <strong>{{ item.strong }}</strong> {{ item.text }}
        </li>
      </ul>

      <slot v-else />
    </div>
  </div>
</template>

<style scoped>
.why-box {
  margin-top: 1.5rem;
  border-radius: 14px;
  padding: 14px 16px 14px;
  background: linear-gradient(180deg, var(--bg-from) 0%, var(--bg-to) 100%);
  border: 1px solid var(--border-color);
  box-shadow: 0 2px 10px rgba(15, 152, 132, 0.08);
  width: 100%;
  box-sizing: border-box;
}

.why-box-outer {
  border: 1.5px dashed var(--dashed-color);
  border-radius: 12px;
  padding: 16px 16px 12px;
  background: #ffffff;
  position: relative;
}

.why-box-label {
  position: absolute;
  top: -9px;
  left: 12px;
  background: #ffffff;
  padding: 0 6px;
  font-size: 0.68rem;
  font-weight: 700;
  color: var(--accent);
  text-transform: uppercase;
  letter-spacing: .03em;
}

.why-box-list {
  margin: 0;
  padding-left: 1.3em;
  list-style-type: none;
}

.why-box-list li {
  position: relative;
  line-height: 1.6;
  margin-bottom: 0.4em;
  padding-left: 0.4em;
}

.why-box-list li strong {
  color: var(--accent);
}
</style>