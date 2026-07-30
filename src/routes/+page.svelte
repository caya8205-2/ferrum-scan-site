<script lang="ts">
  import { 
    Zap, 
    Copy, 
    Check, 
    FileCode, 
    GitBranch, 
    Terminal, 
    Cpu, 
    Boxes 
  } from '@lucide/svelte';

  // Svelte 5 Runes ($state)
  let activeTab = $state<'ps' | 'sh'>('ps');
  let copied = $state(false);

  const psCmd = "irm https://raw.githubusercontent.com/caya8205-2/ferrum-scan/main/install.ps1 | iex";
  const shCmd = "curl -fsSL https://raw.githubusercontent.com/caya8205-2/ferrum-scan/main/install.sh | bash";
  
  // Svelte 5 Derived Rune ($derived)
  let currentCmd = $derived(activeTab === 'ps' ? psCmd : shCmd);

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

<div class="min-h-screen bg-[#0a0c10] text-gray-100 selection:bg-orange-500 selection:text-black relative">
  <!-- Atmosphere Grid -->
  <div 
    class="fixed inset-0 pointer-events-none z-0 opacity-40"
    style="
      background-image: 
        radial-gradient(circle at 50% 0%, rgba(249, 115, 22, 0.15), transparent 50%),
        linear-gradient(to right, rgba(255, 255, 255, 0.03) 1px, transparent 1px),
        linear-gradient(to bottom, rgba(255, 255, 255, 0.03) 1px, transparent 1px);
      background-size: 100% 100%, 40px 40px, 40px 40px;
    "
  ></div>

  <!-- Header Nav -->
  <header class="relative z-10 max-w-6xl mx-auto px-6 py-6 flex justify-between items-center">
    <div class="flex items-center gap-3">
      <span class="bg-gradient-to-r from-orange-500 to-amber-500 text-black text-xs font-black px-2.5 py-1 rounded tracking-wider">
        RUST 2021
      </span>
      <span class="font-['Outfit'] text-xl font-extrabold tracking-tight text-white">
        ferrum-scan
      </span>
    </div>
    <nav class="flex items-center gap-6 text-sm font-medium text-gray-400">
      <a href="#features" class="hover:text-white transition-colors">Features</a>
      <a href="#benchmark" class="hover:text-white transition-colors">Benchmark</a>
      <a href="#terminal" class="hover:text-white transition-colors">Terminal</a>
      <a 
        href="https://github.com/caya8205-2/ferrum-scan" 
        target="_blank" 
        rel="noreferrer"
        class="flex items-center gap-2 bg-white/5 hover:bg-white/10 border border-white/10 px-4 py-2 rounded-lg text-white font-semibold transition-all"
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

    <p class="text-lg text-gray-400 max-w-2xl mx-auto mb-10 leading-relaxed">
      Analyze millions of lines of code, breakdown storage hogs, and detect duplicate files in milliseconds. Built with zero bloat and multi-core parallelism.
    </p>

    <!-- Installer Command Box -->
    <div class="bg-[#121620] border border-white/10 rounded-2xl p-4 max-w-2xl mx-auto shadow-2xl backdrop-blur-xl">
      <div class="flex gap-2 mb-3 border-b border-white/10 pb-3">
        <button 
          onclick={() => activeTab = 'ps'}
          class="px-3 py-1.5 rounded-lg text-xs font-semibold transition-all {activeTab === 'ps' ? 'bg-white/10 text-white' : 'text-gray-500 hover:text-gray-300'}"
        >
          Windows (PowerShell 1-Liner)
        </button>
        <button 
          onclick={() => activeTab = 'sh'}
          class="px-3 py-1.5 rounded-lg text-xs font-semibold transition-all {activeTab === 'sh' ? 'bg-white/10 text-white' : 'text-gray-500 hover:text-gray-300'}"
        >
          Linux / macOS (Bash 1-Liner)
        </button>
      </div>

      <div class="flex items-center justify-between bg-[#080a0e] border border-white/5 px-4 py-3 rounded-xl font-mono text-sm text-cyan-400">
        <span class="overflow-x-auto whitespace-nowrap text-left pr-4">
          {currentCmd}
        </span>
        <button 
          onclick={handleCopy}
          class="flex items-center gap-1.5 bg-orange-500 hover:bg-orange-600 text-white text-xs font-semibold px-3.5 py-2 rounded-lg transition-colors shrink-0"
        >
          {#if copied}
            <Check class="w-3.5 h-3.5" />
            Copied!
          {:else}
            <Copy class="w-3.5 h-3.5" />
            Copy
          {/if}
        </button>
      </div>
    </div>
  </main>

  <!-- Benchmark Stats -->
  <section id="benchmark" class="relative z-10 max-w-6xl mx-auto px-6 py-12">
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
      <div class="bg-[#121620] border border-white/10 p-6 rounded-2xl text-center hover:border-orange-500/40 transition-all hover:-translate-y-1">
        <div class="font-['Outfit'] text-4xl font-extrabold text-white mb-1">
          5.5<span class="text-amber-400">M+</span>
        </div>
        <div class="text-sm text-gray-400 font-medium">Lines of Code Processed</div>
      </div>

      <div class="bg-[#121620] border border-white/10 p-6 rounded-2xl text-center hover:border-orange-500/40 transition-all hover:-translate-y-1">
        <div class="font-['Outfit'] text-4xl font-extrabold text-white mb-1">
          34<span class="text-amber-400">k+</span>
        </div>
        <div class="text-sm text-gray-400 font-medium">Files Scanned Simultaneously</div>
      </div>

      <div class="bg-[#121620] border border-white/10 p-6 rounded-2xl text-center hover:border-orange-500/40 transition-all hover:-translate-y-1">
        <div class="font-['Outfit'] text-4xl font-extrabold text-white mb-1">
          ~5<span class="text-amber-400">s</span>
        </div>
        <div class="text-sm text-gray-400 font-medium">Full Scan Execution Time</div>
      </div>

      <div class="bg-[#121620] border border-white/10 p-6 rounded-2xl text-center hover:border-orange-500/40 transition-all hover:-translate-y-1">
        <div class="font-['Outfit'] text-4xl font-extrabold text-white mb-1">
          100<span class="text-amber-400">%</span>
        </div>
        <div class="text-sm text-gray-400 font-medium">Pure Rust Parallel Engine</div>
      </div>
    </div>
  </section>

  <!-- Terminal Mockup -->
  <section id="terminal" class="relative z-10 max-w-4xl mx-auto px-6 py-12">
    <h2 class="font-['Outfit'] text-3xl font-extrabold text-center text-white mb-8">
      Terminal Output Preview
    </h2>

    <div class="bg-[#080a0e] border border-white/10 rounded-2xl overflow-hidden shadow-2xl">
      <div class="bg-[#121620] px-4 py-3 flex items-center justify-between border-b border-white/10">
        <div class="flex items-center gap-2">
          <div class="w-3 h-3 rounded-full bg-red-500/80"></div>
          <div class="w-3 h-3 rounded-full bg-amber-500/80"></div>
          <div class="w-3 h-3 rounded-full bg-emerald-500/80"></div>
        </div>
        <div class="flex items-center gap-2 text-xs font-mono text-gray-500">
          <Terminal class="w-3.5 h-3.5" />
          ferrum-scan --full -s -d
        </div>
      </div>

      <div class="p-6 font-mono text-xs sm:text-sm text-gray-300 leading-relaxed overflow-x-auto">
        <p class="text-amber-400 font-bold mb-2">⚡ FERRUM-SCAN REPOSITORY REPORT ⚡</p>
        <p>📌 Path              : .</p>
        <p>📁 Total Files        : <span class="text-cyan-400">34,293</span></p>
        <p>💾 Total Size         : <span class="text-emerald-400">239.91 MB</span></p>
        <p>⏱️ Scan Time         : <span class="text-amber-400">5,076 ms</span></p>
        <p class="mb-4">📝 Total Lines        : <span class="text-cyan-400">5,561,940</span> (Code: 4.66M, Blank: 264k, Comments: 628k)</p>

        <p class="text-cyan-400 font-bold mb-1">--- LANGUAGE BREAKDOWN ---</p>
        <p class="text-gray-500">┌────────────┬───────┬──────────┬────────┬─────────┬───────────┬─────────┐</p>
        <p>│ Language   ┆ Files ┆ Code LOC ┆ Blank  ┆ Comment ┆ Total LOC ┆ Share % │</p>
        <p class="text-gray-500">├────────────┼───────┼──────────┼────────┼─────────┼───────────┼─────────┤</p>
        <p>│ JavaScript ┆ 12430 ┆ 1757605  ┆ 119502 ┆ 212924  ┆ 2090031   ┆ <span class="text-purple-400">37.6%</span>   │</p>
        <p>│ C          ┆ 22    ┆ 339409   ┆ 36073  ┆ 188454  ┆ 563936    ┆ <span class="text-purple-400">7.3%</span>    │</p>
        <p>│ TypeScript ┆ 4763  ┆ 268006   ┆ 36599  ┆ 212529  ┆ 517134    ┆ <span class="text-purple-400">5.7%</span>    │</p>
        <p>│ Rust       ┆ 25    ┆ 52878    ┆ 498    ┆ 46      ┆ 53422     ┆ <span class="text-purple-400">1.1%</span>    │</p>
        <p class="text-gray-500 mb-4">└────────────┴───────┴──────────┴────────┴─────────┴───────────┴─────────┘</p>

        <p class="text-cyan-400 font-bold mb-1">--- TOP DIRECTORIES BY STORAGE (--storage) ---</p>
        <p>• node_modules : <span class="text-emerald-400">207.07 MB</span> (26,134 files)</p>
        <p>• src-tauri    : <span class="text-emerald-400">15.55 MB</span> (7,741 files)</p>
        <p class="mb-4">• frontend     : <span class="text-emerald-400">8.50 MB</span> (101 files)</p>

        <p class="text-cyan-400 font-bold mb-1">--- DUPLICATE FILES DETECTOR (--duplicates) ---</p>
        <p class="text-red-400 mb-4">⚠️ Wasted Storage Space: 21.85 MB (1,930 duplicate groups)</p>

        <p class="text-cyan-400 font-bold mb-1">--- 💡 REPOSITORY INSIGHTS ---</p>
        <p>• Dominant Language: JavaScript (37.6% of code LOC).</p>
        <p>• Moderate documentation ratio (11.3% comments).</p>
        <p>• Overall Repository Health Rating: <span class="text-emerald-400 font-bold">A+ (Optimal & Clean)</span></p>
      </div>
    </div>
  </section>

  <!-- Features Grid -->
  <section id="features" class="relative z-10 max-w-6xl mx-auto px-6 py-16">
    <h2 class="font-['Outfit'] text-3xl font-extrabold text-center text-white mb-12">
      Engine Capabilities
    </h2>

    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      <div class="bg-[#121620] border border-white/10 p-6 rounded-2xl hover:bg-[#161c28] hover:border-orange-500/40 transition-all">
        <div class="w-10 h-10 bg-orange-500/10 text-orange-400 rounded-xl flex items-center justify-center font-mono font-bold mb-4">
          -s
        </div>
        <h3 class="font-['Outfit'] text-xl font-bold text-white mb-2">Storage Breakdown</h3>
        <p class="text-gray-400 text-sm leading-relaxed">
          Inspect top-level directories and pinpoint which folders consume disk space in bloated repositories.
        </p>
      </div>

      <div class="bg-[#121620] border border-white/10 p-6 rounded-2xl hover:bg-[#161c28] hover:border-orange-500/40 transition-all">
        <div class="w-10 h-10 bg-orange-500/10 text-orange-400 rounded-xl flex items-center justify-center font-mono font-bold mb-4">
          -d
        </div>
        <h3 class="font-['Outfit'] text-xl font-bold text-white mb-2">Duplicate Detector</h3>
        <p class="text-gray-400 text-sm leading-relaxed">
          Identify duplicate files across your workspace using parallel content hashing and calculate wasted space.
        </p>
      </div>

      <div class="bg-[#121620] border border-white/10 p-6 rounded-2xl hover:bg-[#161c28] hover:border-orange-500/40 transition-all">
        <div class="w-10 h-10 bg-orange-500/10 text-orange-400 rounded-xl flex items-center justify-center font-mono font-bold mb-4">
          <Boxes class="w-5 h-5" />
        </div>
        <h3 class="font-['Outfit'] text-xl font-bold text-white mb-2">Full Scan Override</h3>
        <p class="text-gray-400 text-sm leading-relaxed">
          Optionally bypass <code>.gitignore</code> and ignore rules to scan every single file in the directory tree.
        </p>
      </div>

      <div class="bg-[#121620] border border-white/10 p-6 rounded-2xl hover:bg-[#161c28] hover:border-orange-500/40 transition-all">
        <div class="w-10 h-10 bg-orange-500/10 text-orange-400 rounded-xl flex items-center justify-center font-mono font-bold mb-4">
          <GitBranch class="w-5 h-5" />
        </div>
        <h3 class="font-['Outfit'] text-xl font-bold text-white mb-2">Git Health Inspector</h3>
        <p class="text-gray-400 text-sm leading-relaxed">
          Inspect commit counts, total contributors, top committers, and recent activity dates automatically.
        </p>
      </div>

      <div class="bg-[#121620] border border-white/10 p-6 rounded-2xl hover:bg-[#161c28] hover:border-orange-500/40 transition-all">
        <div class="w-10 h-10 bg-orange-500/10 text-orange-400 rounded-xl flex items-center justify-center font-mono font-bold mb-4">
          <FileCode class="w-5 h-5" />
        </div>
        <h3 class="font-['Outfit'] text-xl font-bold text-white mb-2">Precise LOC Metrics</h3>
        <p class="text-gray-400 text-sm leading-relaxed">
          Distinguish actual source code, blank lines, and comment lines per programming language in milliseconds.
        </p>
      </div>

      <div class="bg-[#121620] border border-white/10 p-6 rounded-2xl hover:bg-[#161c28] hover:border-orange-500/40 transition-all">
        <div class="w-10 h-10 bg-orange-500/10 text-orange-400 rounded-xl flex items-center justify-center font-mono font-bold mb-4">
          <Cpu class="w-5 h-5" />
        </div>
        <h3 class="font-['Outfit'] text-xl font-bold text-white mb-2">Markdown & JSON Export</h3>
        <p class="text-gray-400 text-sm leading-relaxed">
          Export formatted reports to <code>SCAN_REPORT.md</code> or structured JSON for documentation & CI pipelines.
        </p>
      </div>
    </div>
  </section>

  <!-- Footer -->
  <footer class="relative z-10 border-t border-white/10 py-10 text-center text-sm text-gray-500">
    <p>Built with 🦀 Rust & Rayon by <a href="https://github.com/caya8205-2" target="_blank" rel="noreferrer" class="text-gray-300 hover:text-white underline">caya8205-2</a>. Released under MIT License.</p>
  </footer>
</div>
