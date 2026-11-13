<script setup>
const files = [
  { type: 'dir', name: 'bg', message: 'Initial commit: Star Dome Tower', ago: '2 days ago' },
  { type: 'dir', name: 'project', message: 'Add a work-camouflage overlay toggled with F2 or backtick.', ago: '1 hour ago' },
  { type: 'file', name: '.gitignore', message: 'Add a work-camouflage overlay toggled with F2 or backtick.', ago: '1 hour ago' },
  { type: 'file', name: 'LICENSE', message: 'Initial commit: Star Dome Tower', ago: '2 days ago' },
  { type: 'file', name: 'MANIFEST.sha256', message: 'Initial commit: Star Dome Tower', ago: '2 days ago' },
  { type: 'file', name: 'README.md', message: 'Document the Cloudflare Pages URL for this fork.', ago: '1 hour ago' },
  { type: 'file', name: 'SKILL.md', message: 'Initial commit: Star Dome Tower', ago: '2 days ago' },
]
</script>

<template>
  <div class="gh" aria-hidden="true">
    <header class="gh-top">
      <div class="gh-top-left">
        <span class="gh-mark" title="GitHub">
          <svg viewBox="0 0 16 16" width="32" height="32" fill="currentColor" aria-hidden="true">
            <path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82A7.7 7.7 0 0 1 8 4.84c.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.01 8.01 0 0 0 16 8c0-4.42-3.58-8-8-8Z" />
          </svg>
        </span>
        <nav class="gh-crumb">
          <span class="link">cxlg66you-bot</span>
          <span class="slash">/</span>
          <span class="link strong">starTower</span>
          <span class="badge">Public</span>
        </nav>
      </div>
      <div class="gh-top-right">
        <span class="search">Type <kbd>/</kbd> to search</span>
        <span class="pill">Watch <b>1</b></span>
        <span class="pill">Fork <b>1</b></span>
        <span class="pill">Star <b>0</b></span>
      </div>
    </header>

    <nav class="gh-tabs">
      <span class="tab on">Code</span>
      <span class="tab">Issues <i>0</i></span>
      <span class="tab">Pull requests <i>0</i></span>
      <span class="tab">Actions</span>
      <span class="tab">Projects</span>
      <span class="tab">Security</span>
      <span class="tab">Insights</span>
    </nav>

    <div class="gh-main">
      <div class="gh-code">
        <div class="toolbar">
          <span class="branch">main</span>
          <span class="muted">7 files</span>
          <span class="go">Go to file</span>
          <span class="code-btn">Code</span>
        </div>

        <div class="file-box">
          <div class="commit-row">
            <span class="avatar">c</span>
            <span class="who">cxlg66you-bot</span>
            <span class="msg">Hide the desktop intro panel and tidy the phone frame layout.</span>
            <span class="ago">a minute ago</span>
          </div>
          <div v-for="f in files" :key="f.name" class="file-row">
            <span class="ico" :class="f.type">{{ f.type === 'dir' ? '▸' : '📄' }}</span>
            <span class="name" :class="{ dir: f.type === 'dir' }">{{ f.name }}</span>
            <span class="fmsg">{{ f.message }}</span>
            <span class="fago">{{ f.ago }}</span>
          </div>
        </div>

        <article class="readme">
          <div class="readme-head">
            <span class="rm-icon">☰</span>
            <strong>README.md</strong>
          </div>
          <div class="readme-body">
            <h1>星穹塔 Star Dome Tower</h1>
            <p>一座从地底矿窟修到星空的 50 层观星塔，一段原创冒险。</p>
            <p>用 Vue 3 + Vite 制作的魔塔风格网页游戏。手机与电脑浏览器均可打开。</p>
            <h2>游戏特色</h2>
            <ul>
              <li>没有随机、没有经验。每层都是 11×11 的固定地图。</li>
              <li>战斗预判：与怪物相邻时显示预计损失与回合数。</li>
              <li>撤销最多 50 步，换层时自动存档。</li>
            </ul>
            <pre>cd project
npm install
npm run dev</pre>
          </div>
        </article>
      </div>

      <aside class="about">
        <h3>About</h3>
        <p class="desc">星穹塔 50 层游戏</p>
        <p class="meta"><span class="link">MIT license</span></p>
        <p class="meta">0 stars · 1 fork · 1 watching</p>
        <h3>Languages</h3>
        <div class="bar"><i class="js"></i><i class="vue"></i><i class="css"></i></div>
        <ul class="langs">
          <li><b class="dot js"></b> JavaScript 68.4%</li>
          <li><b class="dot vue"></b> Vue 24.1%</li>
          <li><b class="dot css"></b> CSS 7.5%</li>
        </ul>
      </aside>
    </div>
  </div>
</template>

<style scoped>
.gh {
  height: 100%;
  display: flex;
  flex-direction: column;
  background: #ffffff;
  color: #1f2328;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Noto Sans", Helvetica, Arial, sans-serif;
  font-size: 14px;
  line-height: 1.5;
  overflow: auto;
  border-right: 1px solid #d0d7de;
}
.gh-top {
  flex: none;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  padding: 16px 24px 12px;
  background: #ffffff;
  border-bottom: 1px solid #d0d7de;
}
.gh-top-left, .gh-top-right { display: flex; align-items: center; gap: 12px; min-width: 0; }
.gh-mark { color: #1f2328; display: flex; flex: none; }
.gh-crumb { display: flex; align-items: center; gap: 4px; min-width: 0; font-size: 14px; }
.link { color: #0969da; }
.strong { font-weight: 600; color: #0969da; }
.slash { color: #656d76; }
.badge {
  margin-left: 6px;
  font-size: 12px;
  padding: 0 7px;
  border: 1px solid #d0d7de;
  border-radius: 999px;
  color: #656d76;
  font-weight: 500;
}
.search {
  display: flex;
  align-items: center;
  gap: 8px;
  min-width: 160px;
  padding: 5px 12px;
  border: 1px solid #d0d7de;
  border-radius: 6px;
  color: #656d76;
  background: #f6f8fa;
  font-size: 13px;
}
.search kbd {
  font: 11px ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
  border: 1px solid #d0d7de;
  border-radius: 4px;
  padding: 0 5px;
  background: #fff;
}
.pill {
  border: 1px solid #d0d7de;
  border-radius: 6px;
  padding: 3px 10px;
  background: #f6f8fa;
  font-size: 12px;
  color: #1f2328;
  white-space: nowrap;
}
.pill b { font-weight: 600; }
.gh-tabs {
  flex: none;
  display: flex;
  gap: 4px;
  padding: 0 24px;
  border-bottom: 1px solid #d0d7de;
  overflow-x: auto;
  scrollbar-width: none;
}
.tab {
  padding: 12px 10px;
  color: #1f2328;
  font-size: 14px;
  border-bottom: 2px solid transparent;
  white-space: nowrap;
}
.tab.on { font-weight: 600; border-bottom-color: #fd8c73; }
.tab i {
  display: inline-block;
  min-width: 18px;
  padding: 0 6px;
  margin-left: 4px;
  border-radius: 999px;
  background: #f6f8fa;
  border: 1px solid #d0d7de;
  font-style: normal;
  font-size: 12px;
}
.gh-main {
  flex: 1;
  display: flex;
  gap: 24px;
  padding: 16px 24px 32px;
  min-height: 0;
}
.gh-code { flex: 1; min-width: 0; }
.about { width: 240px; flex: none; padding-top: 8px; }
.toolbar { display: flex; align-items: center; gap: 8px; margin-bottom: 12px; }
.branch, .go, .code-btn {
  border: 1px solid #d0d7de;
  border-radius: 6px;
  padding: 4px 12px;
  background: #f6f8fa;
  font-size: 13px;
  font-weight: 500;
}
.code-btn { margin-left: auto; background: #1f883d; color: #fff; border-color: #1f883d; }
.muted { color: #656d76; font-size: 12px; }
.file-box {
  border: 1px solid #d0d7de;
  border-radius: 6px;
  overflow: hidden;
  background: #fff;
}
.commit-row, .file-row {
  display: grid;
  grid-template-columns: 28px minmax(88px, 160px) 1fr auto;
  align-items: center;
  gap: 8px;
  padding: 8px 16px;
  border-top: 1px solid #d0d7de;
  font-size: 13px;
}
.commit-row {
  grid-template-columns: 22px auto 1fr auto;
  background: #f6f8fa;
  border-top: 0;
}
.avatar {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #0969da;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 11px;
  font-weight: 700;
}
.who { font-weight: 600; }
.msg, .fmsg { color: #1f2328; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
.ago, .fago { color: #656d76; white-space: nowrap; }
.ico { text-align: center; color: #656d76; }
.ico.dir { color: #54aeff; font-size: 14px; }
.name { color: #0969da; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
.name.dir { font-weight: 500; }
.readme {
  margin-top: 16px;
  border: 1px solid #d0d7de;
  border-radius: 6px;
  overflow: hidden;
}
.readme-head {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 16px;
  border-bottom: 1px solid #d0d7de;
  background: #fff;
  font-size: 13px;
}
.readme-body { padding: 16px 24px 24px; }
.readme-body h1 {
  margin: 0 0 12px;
  font-size: 28px;
  padding-bottom: 8px;
  border-bottom: 1px solid #d0d7de;
  color: #1f2328;
}
.readme-body h2 { font-size: 18px; margin: 20px 0 8px; color: #1f2328; }
.readme-body p, .readme-body li { color: #1f2328; margin: 0 0 8px; }
.readme-body ul { margin: 0 0 12px; padding-left: 20px; }
.readme-body pre {
  margin: 0;
  padding: 16px;
  background: #f6f8fa;
  border-radius: 6px;
  font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
  font-size: 12.5px;
  color: #1f2328;
}
.about h3 { margin: 16px 0 8px; font-size: 15px; color: #1f2328; }
.about h3:first-child { margin-top: 0; }
.desc { margin: 0 0 8px; color: #1f2328; }
.meta { margin: 0 0 6px; color: #656d76; font-size: 13px; }
.bar { display: flex; height: 8px; border-radius: 6px; overflow: hidden; margin: 8px 0; }
.bar i { display: block; height: 100%; }
.bar .js { width: 68.4%; background: #f1e05a; }
.bar .vue { width: 24.1%; background: #41b883; }
.bar .css { width: 7.5%; background: #563d7c; }
.langs { list-style: none; margin: 0; padding: 0; font-size: 12px; color: #1f2328; }
.langs li { margin: 4px 0; }
.dot { display: inline-block; width: 10px; height: 10px; border-radius: 50%; margin-right: 6px; vertical-align: -1px; }
.dot.js { background: #f1e05a; }
.dot.vue { background: #41b883; }
.dot.css { background: #563d7c; }

@media (max-width: 1100px) {
  .about { display: none; }
  .fmsg { display: none; }
  .commit-row, .file-row { grid-template-columns: 28px 1fr auto; }
}
</style>
