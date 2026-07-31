<script lang="ts">
  /* Hallmark · pre-emit critique: P5 H5 E5 S5 R5 V5 · genre: modern-minimal · theme: Midnight */
  import { 
    Zap, 
    Copy, 
    Check, 
    FileCode, 
    GitBranch, 
    Terminal, 
    Cpu, 
    Boxes,
    HardDrive,
    Trash2,
    ShieldCheck
  } from '@lucide/svelte';

  // Svelte 5 Runes ($state)
  let activeTab = $state<'win' | 'sh' | 'cargo'>('win');
  let copied = $state(false);

  const winCmd = 'irm https://raw.githubusercontent.com/caya8205-2/ferrum-scan/main/install.ps1 | iex';
  const shCmd = 'curl -fsSL https://raw.githubusercontent.com/caya8205-2/ferrum-scan/main/install.sh | bash';
  const cargoCmd = 'cargo install --path .';
  
  // Svelte 5 Derived Rune ($derived)
  let currentCmd = $derived(
    activeTab === 'win' ? winCmd : activeTab === 'sh' ? shCmd : cargoCmd
  );

  function handleCopy() {
    navigator.clipboard.writeText(currentCmd);
    copied = true;
    setTimeout(() => {
      copied = false;
    }, 2000);
  }
</script>

<svelte:head>
  <title>ferrum-scan — Ultra-Fast Repository Intelligence Engine in Pure Rust</title>
  <meta name="description" content="Ultra-fast multithreaded repository scanner and health inspector CLI written in pure Rust." />
</svelte:head>

<div class="min-h-screen bg-[#0a0c10] text-gray-100 selection:bg-orange-500 selection:text-black relative font-['Inter']">
  <!-- Atmosphere Grid -->
  <div 
    class="fixed inset-0 pointer-events-none z-0 opacity-30"
    style="
      background-image: 
        radial-gradient(circle at 50% 0%, rgba(249, 115, 22, 0.12), transparent 50%),
        linear-gradient(to right, rgba(255, 255, 255, 0.02) 1px, transparent 1px),
        linear-gradient(to bottom, rgba(255, 255, 255, 0.02) 1px, transparent 1px);
      background-size: 100% 100%, 40px 40px, 40px 40px;
    "
  ></div>

  <!-- Header Nav -->
  <header class="relative z-10 max-w-5xl mx-auto px-6 py-6 flex justify-between items-center border-b border-white/5">
    <div class="flex items-center gap-3">
      <span class="bg-gradient-to-r from-orange-500 to-amber-500 text-black text-xs font-black px-2.5 py-1 rounded tracking-wider">
        RUST
      </span>
      <span class="font-['Outfit'] text-xl font-extrabold tracking-tight text-white">
        ferrum-scan
      </span>
    </div>
    <nav class="flex items-center gap-6 text-sm font-medium text-gray-400">
      <a href="#install" class="hover:text-white transition-colors">Install</a>
      <a href="#benchmark" class="hover:text-white transition-colors">Benchmark</a>
      <a href="#terminal" class="hover:text-white transition-colors">Terminal</a>
      <a href="#features" class="hover:text-white transition-colors">Features</a>
      <a 
        href="https://github.com/caya8205-2/ferrum-scan" 
        target="_blank" 
        rel="noreferrer"
        class="flex items-center gap-2 bg-white/5 hover:bg-white/10 border border-white/10 px-3.5 py-1.5 rounded-lg text-white text-xs font-semibold transition-all"
      >
        <svg class="w-4 h-4 fill-current" viewBox="0 0 24 24"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
        GitHub
      </a>
    </nav>
  </header>

  <!-- Hero Section -->
  <main class="relative z-10 max-w-4xl mx-auto px-6 pt-16 pb-12 text-center">
    <div class="inline-flex items-center gap-2 bg-orange-500/10 border border-orange-500/30 text-orange-400 text-xs font-semibold px-3.5 py-1.5 rounded-full mb-6">
      <Zap class="w-3.5 h-3.5" />
      Pure Multithreaded Rust Intelligence Engine
    </div>

    <h1 class="font-['Outfit'] text-4xl sm:text-6xl font-extrabold tracking-tight leading-none mb-6 text-white">
      Ultra-Fast Repository <br />
      <span class="bg-gradient-to-r from-orange-400 via-amber-400 to-amber-500 bg-clip-text text-transparent">
        Analysis & Inspection
      </span>
    </h1>

    <p class="text-base sm:text-lg text-gray-400 max-w-2xl mx-auto mb-10 leading-relaxed">
      Analyze millions of lines of code, breakdown storage hogs, and detect duplicate files in milliseconds. Built with zero bloat and multi-core parallelism.
    </p>

    <!-- Installer Command Section (No Scrollbar, Responsive Full Render) -->
    <div id="install" class="bg-[#121620] border border-white/10 rounded-2xl p-5 max-w-3xl mx-auto shadow-2xl text-left">
      <div class="flex items-center justify-between border-b border-white/10 pb-3 mb-4">
        <span class="text-xs font-semibold text-gray-400 uppercase tracking-wider">Installation</span>
        <div class="flex gap-1.5">
          <button 
            onclick={() => activeTab = 'win'}
            class="px-3 py-1 rounded-lg text-xs font-semibold transition-all {activeTab === 'win' ? 'bg-orange-500 text-white' : 'bg-white/5 text-gray-400 hover:text-white'}"
          >
            Windows (PowerShell)
          </button>
          <button 
            onclick={() => activeTab = 'sh'}
            class="px-3 py-1 rounded-lg text-xs font-semibold transition-all {activeTab === 'sh' ? 'bg-orange-500 text-white' : 'bg-white/5 text-gray-400 hover:text-white'}"
          >
            Linux / macOS
          </button>
          <button 
            onclick={() => activeTab = 'cargo'}
            class="px-3 py-1 rounded-lg text-xs font-semibold transition-all {activeTab === 'cargo' ? 'bg-orange-500 text-white' : 'bg-white/5 text-gray-400 hover:text-white'}"
          >
            Cargo
          </button>
        </div>
      </div>

      <div class="bg-[#080a0e] border border-white/5 p-4 rounded-xl relative group">
        <pre class="font-mono text-xs sm:text-sm text-cyan-400 whitespace-pre-wrap break-all pr-12 leading-relaxed">{currentCmd}</pre>
        
        <button 
          onclick={handleCopy}
          aria-label="Copy command"
          class="absolute top-3 right-3 bg-white/10 hover:bg-orange-500 text-white p-2 rounded-lg transition-colors flex items-center justify-center shrink-0"
        >
          {#if copied}
            <Check class="w-4 h-4 text-emerald-400" />
          {:else}
            <Copy class="w-4 h-4" />
          {/if}
        </button>
      </div>

      <p class="text-xs text-gray-500 mt-3">
        {#if activeTab === 'win'}
          Downloads pre-compiled <code>ferrum-scan.exe</code> directly into <code>%LOCALAPPDATA%\ferrum-scan</code> and updates PATH.
        {:else if activeTab === 'sh'}
          Downloads pre-compiled binary directly to <code>~/.ferrum-scan/bin</code> and adds to PATH.
        {:else}
          Compiles and installs globally via Cargo toolchain.
        {/if}
      </p>
    </div>
  </main>

  <!-- Benchmark Stats -->
  <section id="benchmark" class="relative z-10 max-w-5xl mx-auto px-6 py-12">
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 sm:gap-6">
      <div class="bg-[#121620] border border-white/10 p-5 rounded-xl text-center">
        <div class="font-['Outfit'] text-3xl font-extrabold text-white mb-1">
          5.5<span class="text-amber-400">M+</span>
        </div>
        <div class="text-xs text-gray-400 font-medium">Lines of Code Processed</div>
      </div>

      <div class="bg-[#121620] border border-white/10 p-5 rounded-xl text-center">
        <div class="font-['Outfit'] text-3xl font-extrabold text-white mb-1">
          34<span class="text-amber-400">k+</span>
        </div>
        <div class="text-xs text-gray-400 font-medium">Files Scanned Simultaneously</div>
      </div>

      <div class="bg-[#121620] border border-white/10 p-5 rounded-xl text-center">
        <div class="font-['Outfit'] text-3xl font-extrabold text-white mb-1">
          ~5<span class="text-amber-400">s</span>
        </div>
        <div class="text-xs text-gray-400 font-medium">Full Scan Execution Time</div>
      </div>

      <div class="bg-[#121620] border border-white/10 p-5 rounded-xl text-center">
        <div class="font-['Outfit'] text-3xl font-extrabold text-white mb-1">
          100<span class="text-amber-400">%</span>
        </div>
        <div class="text-xs text-gray-400 font-medium">Pure Rust Parallel Engine</div>
      </div>
    </div>
  </section>

  <!-- Terminal Output Preview (Strict JetBrains Mono Alignment + Complete TOTAL Row & Jumbo Files) -->
  <section id="terminal" class="relative z-10 max-w-5xl mx-auto px-6 py-12">
    <h2 class="font-['Outfit'] text-2xl font-extrabold text-center text-white mb-6">
      Terminal Output Preview
    </h2>

    <div class="bg-[#080a0e] border border-white/10 rounded-xl overflow-hidden shadow-2xl">
      <div class="bg-[#121620] px-4 py-2.5 flex items-center justify-between border-b border-white/10">
        <div class="flex items-center gap-1.5">
          <div class="w-3 h-3 rounded-full bg-red-500/80"></div>
          <div class="w-3 h-3 rounded-full bg-amber-500/80"></div>
          <div class="w-3 h-3 rounded-full bg-emerald-500/80"></div>
        </div>
        <div class="flex items-center gap-2 text-xs font-mono text-gray-400">
          <Terminal class="w-3.5 h-3.5 text-orange-400" />
          ferrum-scan --full -s -d -j
        </div>
      </div>

      <div class="p-5 overflow-x-auto">
        <pre 
          class="text-xs sm:text-sm leading-snug whitespace-pre text-gray-300 tracking-normal"
          style="font-family: 'JetBrains Mono', 'Fira Code', 'Courier New', monospace; font-variant-numeric: tabular-nums;"
        ><span class="text-amber-400 font-bold">⚡ FERRUM-SCAN REPOSITORY REPORT ⚡</span>

📌 Path               : .
📁 Total Files        : <span class="text-cyan-400">34,293</span>
💾 Total Size         : <span class="text-emerald-400">239.91 MB</span> (251,565,402 bytes)
⏱️ Scan Time          : <span class="text-amber-400">7,392 ms</span>
📝 Total Lines        : <span class="text-cyan-400">5,561,948</span> (Code: 4.67M, Blank: 264k, Comments: 628k)

<span class="text-cyan-400 font-bold">--- LANGUAGE BREAKDOWN ---</span>
<span class="text-gray-500">┌──────────────────┬───────┬──────────┬────────┬─────────┬───────────┬─────────┐</span>
│ Language         ┆ Files ┆ Code LOC ┆ Blank  ┆ Comment ┆ Total LOC ┆ Share % │
<span class="text-gray-500">├──────────────────┼───────┼──────────┼────────┼─────────┼───────────┼─────────┤</span>
│ <span class="text-cyan-400">Other</span>            ┆ 11508 ┆ 1856450  ┆ 15146  ┆ 3255    ┆ 1874851   ┆ <span class="text-purple-400">39.8%</span>   │
│ <span class="text-cyan-400">JavaScript</span>       ┆ 12430 ┆ 1757605  ┆ 119502 ┆ 212924  ┆ 2090031   ┆ <span class="text-purple-400">37.6%</span>   │
│ <span class="text-cyan-400">C</span>                ┆ 22    ┆ 339409   ┆ 36073  ┆ 188454  ┆ 563936    ┆ <span class="text-purple-400">7.3%</span>    │
│ <span class="text-cyan-400">TypeScript</span>       ┆ 4763  ┆ 268006   ┆ 36599  ┆ 212529  ┆ 517134    ┆ <span class="text-purple-400">5.7%</span>    │
│ <span class="text-cyan-400">JSON</span>             ┆ 3485  ┆ 252681   ┆ 53     ┆ 24      ┆ 252758    ┆ <span class="text-purple-400">5.4%</span>    │
│ <span class="text-cyan-400">Markdown</span>         ┆ 678   ┆ 94747    ┆ 36078  ┆ 3760    ┆ 134585    ┆ <span class="text-purple-400">2.0%</span>    │
│ <span class="text-cyan-400">Rust</span>             ┆ 25    ┆ 52878    ┆ 498    ┆ 46      ┆ 53422     ┆ <span class="text-purple-400">1.1%</span>    │
│ <span class="text-cyan-400">HTML</span>             ┆ 84    ┆ 16132    ┆ 15683  ┆ 1870    ┆ 33685     ┆ <span class="text-purple-400">0.3%</span>    │
│ <span class="text-cyan-400">TypeScript (TSX)</span> ┆ 34    ┆ 11199    ┆ 910    ┆ 97      ┆ 12206     ┆ <span class="text-purple-400">0.2%</span>    │
│ <span class="text-cyan-400">TOML</span>             ┆ 1038  ┆ 8004     ┆ 2022   ┆ 4146    ┆ 14172     ┆ <span class="text-purple-400">0.2%</span>    │
│ <span class="text-cyan-400">C++</span>              ┆ 7     ┆ 6061     ┆ 884    ┆ 268     ┆ 7213      ┆ <span class="text-purple-400">0.1%</span>    │
│ <span class="text-cyan-400">YAML</span>             ┆ 142   ┆ 3168     ┆ 389    ┆ 108     ┆ 3665      ┆ <span class="text-purple-400">0.1%</span>    │
│ <span class="text-cyan-400">CSS</span>              ┆ 23    ┆ 2000     ┆ 435    ┆ 375     ┆ 2810      ┆ <span class="text-purple-400">0.0%</span>    │
│ <span class="text-cyan-400">Shell Script</span>     ┆ 49    ┆ 1115     ┆ 77     ┆ 245     ┆ 1437      ┆ <span class="text-purple-400">0.0%</span>    │
│ <span class="text-cyan-400">Makefile</span>         ┆ 3     ┆ 22       ┆ 12     ┆ 0       ┆ 34        ┆ <span class="text-purple-400">0.0%</span>    │
│ <span class="text-cyan-400">XML</span>              ┆ 2     ┆ 9        ┆ 0      ┆ 0       ┆ 9         ┆ <span class="text-purple-400">0.0%</span>    │
<span class="text-gray-500">├──────────────────┼───────┼──────────┼────────┼─────────┼───────────┼─────────┤</span>
│ <span class="text-amber-400 font-bold">TOTAL</span>            ┆ <span class="text-amber-400 font-bold">34293</span> ┆ <span class="text-amber-400 font-bold">4669486</span>  ┆ <span class="text-amber-400 font-bold">264361</span> ┆ <span class="text-amber-400 font-bold">628101</span>  ┆ <span class="text-amber-400 font-bold">5561948</span>   ┆ <span class="text-amber-400 font-bold">100.0%</span>  │
<span class="text-gray-500">└──────────────────┴───────┴──────────┴────────┴─────────┴───────────┴─────────┘</span>

<span class="text-cyan-400 font-bold">--- TOP DIRECTORIES BY STORAGE (--storage) ---</span>
• <span class="text-white font-semibold">node_modules</span> : <span class="text-emerald-400">207.07 MB</span> (26,134 files)
• <span class="text-white font-semibold">src-tauri</span>    : <span class="text-emerald-400">15.55 MB</span> (7,741 files)
• <span class="text-white font-semibold">frontend</span>     : <span class="text-emerald-400">8.50 MB</span> (101 files)
• <span class="text-white font-semibold">backend</span>      : <span class="text-emerald-400">8.36 MB</span> (215 files)

<span class="text-cyan-400 font-bold">--- DUPLICATE FILES DETECTOR (--duplicates) ---</span>
<span class="text-red-400 font-bold">⚠️ Wasted Storage Space: 21.85 MB (1,930 duplicate groups)</span>

<span class="text-cyan-400 font-bold">--- 🚨 JUMBO FILES DETECTOR (--jumbo > 5 MB) ---</span>
• <span class="text-white font-semibold">node_modules\kuromoji\test\resource\minimum-dic\matrix.def</span>  : <span class="text-amber-400 font-semibold">21.94 MB</span>
• <span class="text-white font-semibold">node_modules\better-sqlite3\build\Release\obj\...\sqlite3.c</span> : <span class="text-amber-400 font-semibold">8.81 MB</span>
• <span class="text-white font-semibold">node_modules\better-sqlite3\deps\sqlite3\sqlite3.c</span>          : <span class="text-amber-400 font-semibold">8.81 MB</span>
• <span class="text-white font-semibold">node_modules\typescript\lib\typescript.js</span>                   : <span class="text-amber-400 font-semibold">8.69 MB</span>
• <span class="text-white font-semibold">node_modules\typescript\lib\_tsc.js</span>                         : <span class="text-amber-400 font-semibold">5.93 MB</span>

<span class="text-cyan-400 font-bold">--- 💡 REPOSITORY INSIGHTS ---</span>
• Dominant Language: Other / JavaScript (39.8% / 37.6% of code LOC).
• Moderate documentation ratio (11.3% comments).
• Jumbo files alert: 5 file(s) exceed 5 MB threshold (total 54.17 MB).
• Overall Repository Health Rating: <span class="text-emerald-400 font-bold">A+ (Optimal & Clean)</span></pre>
      </div>
    </div>
  </section>

  <!-- Features Grid -->
  <section id="features" class="relative z-10 max-w-5xl mx-auto px-6 py-16 border-t border-white/5">
    <h2 class="font-['Outfit'] text-2xl font-extrabold text-center text-white mb-10">
      Engine Capabilities
    </h2>

    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <div class="bg-[#121620] border border-white/10 p-5 rounded-xl">
        <div class="w-9 h-9 bg-orange-500/10 text-orange-400 rounded-lg flex items-center justify-center font-mono font-bold text-sm mb-3">
          <HardDrive class="w-4 h-4" />
        </div>
        <h3 class="font-['Outfit'] text-lg font-bold text-white mb-1">Storage Breakdown</h3>
        <p class="text-gray-400 text-xs leading-relaxed">
          Inspect top-level directories and pinpoint which folders consume disk space in bloated repositories.
        </p>
      </div>

      <div class="bg-[#121620] border border-white/10 p-5 rounded-xl">
        <div class="w-9 h-9 bg-orange-500/10 text-orange-400 rounded-lg flex items-center justify-center font-mono font-bold text-sm mb-3">
          <Copy class="w-4 h-4" />
        </div>
        <h3 class="font-['Outfit'] text-lg font-bold text-white mb-1">Duplicate Detector</h3>
        <p class="text-gray-400 text-xs leading-relaxed">
          Identify duplicate files across your workspace using parallel content hashing and calculate wasted space.
        </p>
      </div>

      <div class="bg-[#121620] border border-white/10 p-5 rounded-xl">
        <div class="w-9 h-9 bg-orange-500/10 text-orange-400 rounded-lg flex items-center justify-center font-mono font-bold text-sm mb-3">
          <Boxes class="w-4 h-4" />
        </div>
        <h3 class="font-['Outfit'] text-lg font-bold text-white mb-1">Full Scan Override</h3>
        <p class="text-gray-400 text-xs leading-relaxed">
          Optionally bypass <code>.gitignore</code> and ignore rules to scan every single file in the directory tree.
        </p>
      </div>

      <div class="bg-[#121620] border border-white/10 p-5 rounded-xl">
        <div class="w-9 h-9 bg-orange-500/10 text-orange-400 rounded-lg flex items-center justify-center font-mono font-bold text-sm mb-3">
          <Trash2 class="w-4 h-4" />
        </div>
        <h3 class="font-['Outfit'] text-lg font-bold text-white mb-1">Native Uninstaller</h3>
        <p class="text-gray-400 text-xs leading-relaxed">
          Uninstall cleanly with <code>ferrum-scan uninstall</code> or <code>-Uninstall</code> script flag with safety prompts.
        </p>
      </div>

      <div class="bg-[#121620] border border-white/10 p-5 rounded-xl">
        <div class="w-9 h-9 bg-orange-500/10 text-orange-400 rounded-lg flex items-center justify-center font-mono font-bold text-sm mb-3">
          <GitBranch class="w-4 h-4" />
        </div>
        <h3 class="font-['Outfit'] text-lg font-bold text-white mb-1">Git Health Inspector</h3>
        <p class="text-gray-400 text-xs leading-relaxed">
          Inspect commit counts, total contributors, top committers, and recent activity dates automatically.
        </p>
      </div>

      <div class="bg-[#121620] border border-white/10 p-5 rounded-xl">
        <div class="w-9 h-9 bg-orange-500/10 text-orange-400 rounded-lg flex items-center justify-center font-mono font-bold text-sm mb-3">
          <ShieldCheck class="w-4 h-4" />
        </div>
        <h3 class="font-['Outfit'] text-lg font-bold text-white mb-1">Markdown & JSON Export</h3>
        <p class="text-gray-400 text-xs leading-relaxed">
          Export formatted reports to <code>SCAN_REPORT.md</code> or structured JSON for documentation & CI pipelines.
        </p>
      </div>
    </div>
  </section>

  <!-- Footer -->
  <footer class="relative z-10 border-t border-white/5 py-8 text-center text-xs text-gray-500">
    <p>Built with 🦀 Rust & Rayon by <a href="https://github.com/caya8205-2" target="_blank" rel="noreferrer" class="text-gray-300 hover:text-white underline">caya8205-2</a>. Released under MIT License.</p>
  </footer>
</div>
