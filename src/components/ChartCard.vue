<script setup lang="ts">
import { computed } from 'vue'
import { Bar, Line } from 'vue-chartjs'
import {
  Chart as ChartJS,
  CategoryScale,
  LinearScale,
  BarElement,
  PointElement,
  LineElement,
  Filler,
  Tooltip,
  Legend,
} from 'chart.js'

ChartJS.register(CategoryScale, LinearScale, BarElement, PointElement, LineElement, Filler, Tooltip, Legend)

const props = defineProps<{
  title: string
  type?: 'bar' | 'line'
  data?: number[]
  labels?: string[]
  color?: string
  fill?: boolean
  ySuffix?: string
  yStepInteger?: boolean
}>()

const chartData = computed(() => ({
  labels: props.labels || ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
  datasets: [
    {
      data: props.data || [],
      backgroundColor: props.fill ? hexToRgba(props.color || '#4285f4', 0.15) : hexToRgba(props.color || '#4285f4', 0.7),
      borderColor: props.color || '#4285f4',
      borderWidth: props.type === 'line' ? 2.5 : 0,
      fill: props.fill ?? false,
      tension: 0.3,
      pointRadius: 4,
      pointBackgroundColor: props.color || '#4285f4',
      pointBorderColor: '#fff',
      pointBorderWidth: 2,
    },
  ],
}))

const chartOptions = computed(() => ({
  responsive: true,
  maintainAspectRatio: false,
  plugins: {
    legend: { display: false },
    tooltip: { enabled: true },
  },
  scales: {
    x: {
      grid: { display: false },
      ticks: { font: { size: 11 } },
    },
    y: {
      grid: { color: 'rgba(0,0,0,0.06)' },
      ticks: {
        font: { size: 11 },
        stepSize: props.yStepInteger ? 1 : undefined,
        callback: (value: number | string) => {
          const v = Number(value)
          if (props.ySuffix === '%') return v + '%'
          if (v >= 1000) return v.toLocaleString()
          return v
        },
      },
    },
  },
}))

function hexToRgba(hex: string, alpha: number): string {
  const named: Record<string, string> = {
    blue: '#4285f4', red: '#ea4335', green: '#34a853',
    orange: '#fbbc04', cyan: '#00bcd4', purple: '#9c27b0',
  }
  const h = named[hex] || hex
  const r = parseInt(h.slice(1, 3), 16)
  const g = parseInt(h.slice(3, 5), 16)
  const b = parseInt(h.slice(5, 7), 16)
  return `rgba(${r},${g},${b},${alpha})`
}
</script>

<template>
  <v-card flat class="rounded-lg pa-2" color="white">
    <v-card-title class="text-subtitle-1 font-weight-bold px-5 pt-5 pb-0">{{ title }}</v-card-title>
    <v-card-text class="px-5 pb-5 pt-4">
      <div class="chart-container">
        <Bar v-if="type === 'bar' && data?.length" :data="chartData" :options="chartOptions" />
        <Line v-else-if="data?.length" :data="chartData" :options="chartOptions" />
        <div v-else class="chart-placeholder">
          <span class="text-medium-emphasis text-body-2">No data</span>
        </div>
      </div>
    </v-card-text>
  </v-card>
</template>

<style scoped>
.chart-container {
  width: 100%;
  height: 220px;
  position: relative;
}

.chart-placeholder {
  width: 100%;
  height: 220px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgb(var(--v-theme-surface-variant));
  border-radius: 8px;
  border: 1px dashed rgba(var(--v-border-color), var(--v-border-opacity));
}
</style>
