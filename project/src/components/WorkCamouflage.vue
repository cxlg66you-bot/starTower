<script setup>
import { computed, ref } from 'vue'

const emit = defineEmits(['leave'])

const FILES = {
  'src/services/PaymentReconcileService.ts': {
    lang: 'TypeScript',
    lines: `import { LedgerClient } from '../api/ledger'
import type { SettlementBatch, ReconDiff } from '../types/recon'

const WINDOW_DAYS = 7
const TOLERANCE = 0.01

export class PaymentReconcileService {
  constructor(private readonly ledger: LedgerClient) {}

  async reconcile(batch: SettlementBatch): Promise<ReconDiff[]> {
    const range = this.ledger.rangeOf(batch.settledAt, WINDOW_DAYS)
    const [ours, theirs] = await Promise.all([
      this.ledger.listOutbound(range),
      this.ledger.listProvider(batch.provider, range),
    ])

    const byRef = new Map(theirs.map((row) => [row.reference, row]))
    const diffs: ReconDiff[] = []

    for (const item of ours) {
      const peer = byRef.get(item.reference)
      if (!peer) {
        diffs.push({ code: 'MISSING_PROVIDER', reference: item.reference, amount: item.amount })
        continue
      }
      const delta = Math.abs(item.amount - peer.amount)
      if (delta > TOLERANCE) {
        diffs.push({ code: 'AMOUNT_MISMATCH', reference: item.reference, amount: delta })
      }
      byRef.delete(item.reference)
    }

    for (const leftover of byRef.values()) {
      diffs.push({ code: 'UNMATCHED_PROVIDER', reference: leftover.reference, amount: leftover.amount })
    }
    return diffs
  }
}
`.trim().split('\n'),
  },
  'docs/本周需求评审.md': {
    lang: 'Markdown',
    lines: `# 支付对账模块 · 本周评审

## 目标

- 支持按结算批次核对渠道账单与内部流水
- 差异需在 15 分钟内进入待处理队列
- 月末出账窗口内，P95 查询时延小于 200ms

## 已确认

1. 对账窗口按结算日向前 7 天，避免跨日漏单
2. 金额容差 0.01，低于容差的记为匹配
3. 未匹配流水保留原单号，方便财务回查

## 待办

- [ ] 补齐渠道侧补单接口的超时重试
- [ ] 给异常队列加上处理人与状态流转
- [ ] 压测 11 月出账峰值，再决定是否加只读副本
`.trim().split('\n'),
  },
  'src/api/ledger.ts': {
    lang: 'TypeScript',
    lines: `export type DateRange = { from: string; to: string }

export class LedgerClient {
  constructor(private readonly baseUrl: string) {}

  rangeOf(settledAt: string, days: number): DateRange {
    const end = new Date(settledAt)
    const start = new Date(end)
    start.setDate(start.getDate() - days)
    return { from: start.toISOString(), to: end.toISOString() }
  }

  listOutbound(range: DateRange) {
    return this.get('/v1/ledger/outbound', range)
  }

  listProvider(provider: string, range: DateRange) {
    return this.get('/v1/ledger/providers/' + encodeURIComponent(provider), range)
  }

  private async get(path: string, query: DateRange) {
    const url = new URL(path, this.baseUrl)
    url.searchParams.set('from', query.from)
    url.searchParams.set('to', query.to)
    const res = await fetch(url)
    if (!res.ok) throw new Error('ledger request failed: ' + res.status)
    return res.json()
  }
}
`.trim().split('\n'),
  },
}

const fileNames = Object.keys(FILES)
const active = ref(fileNames[0])
const current = computed(() => FILES[active.value])

function onTitleBarDblClick() {
  emit('leave')
}
</script>

<template>
  <div class="ide" role="dialog" aria-label="工作台" @keydown.stop>
    <header class="titlebar" @dblclick="onTitleBarDblClick">
      <div class="traffic" aria-hidden="true"><i></i><i></i><i></i></div>
      <div class="win-title">payment-recon — Visual Studio Code</div>
    </header>

    <div class="body">
      <aside class="activity" aria-hidden="true">
        <span class="act on">&#x2630;</span>
        <span class="act">&#x1F50D;</span>
        <span class="act">&#x2387;</span>
        <span class="act">&#x2713;</span>
      </aside>

      <aside class="sidebar">
        <div class="side-label">资源管理器</div>
        <div class="root">PAYMENT-RECON</div>
        <button
          v-for="name in fileNames"
          :key="name"
          class="file"
          :class="{ on: name === active }"
          type="button"
          @click="active = name"
        >{{ name }}</button>
      </aside>

      <section class="editor">
        <div class="tabs">
          <div class="tab on">{{ active.split('/').pop() }}</div>
        </div>
        <pre class="code"><span
          v-for="(line, i) in current.lines"
          :key="i"
          class="ln"
        ><span class="no">{{ i + 1 }}</span><span class="tx">{{ line || ' ' }}</span></span></pre>
      </section>
    </div>

    <footer class="statusbar">
      <span>main*</span>
      <span>UTF-8</span>
      <span>{{ current.lang }}</span>
      <span class="grow">Ln {{ current.lines.length }}, Col 1</span>
    </footer>
  </div>
</template>

<style scoped>
.ide {
  position: fixed;
  inset: 0;
  z-index: 9999;
  display: flex;
  flex-direction: column;
  background: #1e1e1e;
  color: #d4d4d4;
  font-family: "Segoe UI", "PingFang SC", "Noto Sans SC", sans-serif;
  font-size: 13px;
  user-select: none;
}
.titlebar {
  height: 36px;
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 0 12px;
  background: #323233;
  cursor: default;
}
.traffic { display: flex; gap: 6px; }
.traffic i {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  display: block;
}
.traffic i:nth-child(1) { background: #ff5f57; }
.traffic i:nth-child(2) { background: #febc2e; }
.traffic i:nth-child(3) { background: #28c840; }
.win-title {
  flex: 1;
  text-align: center;
  color: #cccccc;
  font-size: 12px;
}
.body { flex: 1; display: flex; min-height: 0; }
.activity {
  width: 48px;
  background: #333333;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 10px;
  gap: 16px;
  color: #858585;
}
.act { font-size: 16px; }
.act.on { color: #ffffff; }
.sidebar {
  width: min(260px, 42vw);
  background: #252526;
  padding: 8px 0;
  overflow: auto;
}
.side-label, .root {
  padding: 4px 16px;
  letter-spacing: 0.08em;
  font-size: 11px;
  color: #bbbbbb;
}
.root { color: #cccccc; font-weight: 600; margin-top: 8px; letter-spacing: 0; }
.file {
  display: block;
  width: 100%;
  text-align: left;
  border: 0;
  background: transparent;
  color: #cccccc;
  padding: 6px 16px 6px 24px;
  font: inherit;
  cursor: pointer;
}
.file:hover { background: #2a2d2e; }
.file.on { background: #37373d; }
.editor { flex: 1; display: flex; flex-direction: column; min-width: 0; background: #1e1e1e; }
.tabs { height: 35px; background: #252526; display: flex; }
.tab {
  padding: 0 16px;
  display: flex;
  align-items: center;
  background: #1e1e1e;
  border-right: 1px solid #252526;
  color: #ffffff;
}
.code {
  flex: 1;
  margin: 0;
  padding: 8px 0 32px;
  overflow: auto;
  font-family: "Menlo", "Consolas", "Source Code Pro", monospace;
  font-size: 13px;
  line-height: 1.55;
  user-select: text;
}
.ln { display: flex; }
.no {
  width: 48px;
  flex: none;
  text-align: right;
  padding-right: 16px;
  color: #858585;
}
.tx { white-space: pre; color: #d4d4d4; }
.statusbar {
  height: 22px;
  background: #007acc;
  color: #ffffff;
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 0 10px;
  font-size: 11px;
}
.grow { margin-left: auto; }
</style>
