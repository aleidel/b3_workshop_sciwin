<script setup lang="ts">
interface Segment { text: string; class?: string }

interface Line {
  type: 'cmd' | 'info' | 'output' | 'success' | 'table' | 'divider' | 'diff' | 'yaml'
  icon?: string
  text?: string
  segments?: Segment[]
  headers?: string[]
  rows?: (string | number)[][]
  lines?: string[]
}

defineProps<{
  cwd?: string
  lines: Line[]
}>()

function isSeparator(text: string) {
  return /^-{5,}$/.test(text.trim())
}

function diffClass(text: string) {
  const pipeIdx = text.indexOf('|')
  const rest = (pipeIdx >= 0 ? text.slice(pipeIdx + 1) : text).trimStart()
  if (rest.startsWith('+')) return 'text-green-600'
  if (rest.startsWith('-')) return 'text-red-600'
  return 'text-gray-500'
}
</script>

<template>
  <div class="w-full h-full bg-white text-gray-800 rounded-lg shadow-2xl overflow-hidden border border-gray-300 text-left flex flex-col">
    <!-- header -->
    <div class="bg-gray-100 px-4 py-2 flex items-center gap-2 text-xs text-gray-500 shrink-0 border-b border-gray-300">
      <span class="w-3 h-3 bg-red-500 rounded-full" />
      <span class="w-3 h-3 bg-yellow-500 rounded-full" />
      <span class="w-3 h-3 bg-green-500 rounded-full" />
      <span class="ml-auto font-mono">{{ cwd ?? '~/sciwin-demo' }}</span>
    </div>

    <!-- content -->
    <div class="p-5 font-mono text-base leading-6 space-y-1.5 flex-1 min-h-0 overflow-y-auto">
      <div v-for="(line, i) in lines" :key="i" v-click>

        <template v-if="line.type === 'cmd'">
          <span class="text-green-600 font-semibold">$</span>
          <span class="text-gray-900"> {{ line.text }}</span>
        </template>

        <template v-else-if="line.type === 'info'">
          <span v-if="line.icon" class="mr-1">{{ line.icon }}</span>
          <template v-if="line.segments">
            <span
              v-for="(seg, j) in line.segments"
              :key="j"
              :class="seg.class ?? 'text-gray-600'"
            >{{ seg.text }}</span>
          </template>
          <span v-else class="text-gray-600 whitespace-pre-wrap">{{ line.text }}</span>
        </template>

        <template v-else-if="line.type === 'yaml'">
          <pre class="text-base leading-6 text-gray-700 whitespace-pre-wrap bg-gray-50 rounded px-3 py-2 border border-gray-200">{{ line.text }}</pre>
        </template>

        <template v-else-if="line.type === 'table'">
          <table class="text-base md:text-lg border-collapse mt-1 mb-2">
            <thead>
              <tr>
                <th
                  v-for="(h, hi) in line.headers"
                  :key="hi"
                  class="px-3 py-1 text-left text-gray-500 border-b border-gray-300 font-normal"
                >{{ h }}</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(row, ri) in line.rows" :key="ri">
                <td
                  v-for="(cell, ci) in row"
                  :key="ci"
                  class="px-3 py-0.5 text-gray-700 whitespace-nowrap"
                >{{ cell }}</td>
              </tr>
            </tbody>
          </table>
        </template>

        <template v-else-if="line.type === 'output'">
          <span class="text-gray-500 pl-4 whitespace-pre-wrap">{{ line.text }}</span>
        </template>

        <template v-else-if="line.type === 'diff'">
          <div class="text-base leading-6 whitespace-pre">
            <template v-for="(dline, di) in line.lines" :key="di">
              <div
                v-if="isSeparator(dline)"
                class="border-t border-dotted border-gray-400 my-2"
              />
              <div v-else :class="diffClass(dline)">{{ dline }}</div>
            </template>
          </div>
        </template>

        <template v-else-if="line.type === 'divider'">
          <div class="flex items-center gap-3 my-3 text-gray-400">
            <div class="flex-1 h-px bg-gray-300" />
            <span class="text-xs uppercase tracking-wide">{{ line.text }}</span>
            <div class="flex-1 h-px bg-gray-300" />
          </div>
        </template>

        <template v-else>
          <span class="text-green-600 font-semibold">{{ line.text }}</span>
        </template>

      </div>
    </div>
  </div>
</template>