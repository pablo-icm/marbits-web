---
type: landing

sections:

  # ─── COVER IMAGE (full width) ────────────────────────────────────────────
  - block: markdown
    id: cover-image
    content:
      title: ''
      text: |
        <img src="/media/cover.png" alt="MARBITS HPC Cluster" class="marbits-cover">
    design:
      background:
        color: '#ffffff'
      spacing:
        padding: ["0px", "0px", "0px", "0px"]

  # ─── HERO TEXT ────────────────────────────────────────────────────────────
  - block: hero
    id: hero
    content:
      title: |
        MARBITS HPC Cluster
      text: |
        The **Marine Bioinformatics** High-Performance Computing platform at the
        [Institut de Ciències del Mar (ICM-CSIC)](https://www.icm.csic.es/), Barcelona.  
        Powering cutting-edge research in marine and environmental genomics.

        ⚠ **Notice:** `/mnt/lustre` is temporarily unreliable. Use `/mnt/smart` for computation and remove files when done. [→ File system docs](/docs/filesystem/)
      cta:
        label: "Get Started"
        url: /docs/getting-started/
        icon: rocket
        icon_pack: fas
      cta_alt:
        label: "System Overview"
        url: /docs/system-overview/
    design:
      background:
        gradient_end: '#0d3b6e'
        gradient_start: '#1a6496'
        text_color_light: true

  # ─── STATS (as markdown) ─────────────────────────────────────────────────
  - block: markdown
    id: stats
    content:
      title: ''
      text: |
        <div class="container py-2">
          <div class="row text-center justify-content-center">
            <div class="col-6 col-md-3 py-4 px-3">
              <div class="stat-number">396</div>
              <div class="stat-label">CPU Cores<br><span class="stat-sub">(792 with HT)</span></div>
            </div>
            <div class="col-6 col-md-3 py-4 px-3">
              <div class="stat-number">4.6 TB</div>
              <div class="stat-label">Total RAM</div>
            </div>
            <div class="col-6 col-md-3 py-4 px-3">
              <div class="stat-number">1+ PB</div>
              <div class="stat-label">Total Storage</div>
            </div>
            <div class="col-6 col-md-3 py-4 px-3">
              <div class="stat-number">22</div>
              <div class="stat-label">Compute Nodes</div>
            </div>
          </div>
        </div>
    design:
      background:
        color: '#f0f8ff'

  # ─── FEATURES ────────────────────────────────────────────────────────────
  - block: features
    id: features
    content:
      title: What MARBITS Offers
      text: A powerful research computing infrastructure for the marine biology and bioinformatics community at CMIMA.
      items:
        - name: High-Performance Nodes
          icon: microchip
          icon_pack: fas
          description: >
            22 compute nodes — 8 Supermicro high-memory nodes (up to 2 TB RAM each)
            and 12 IBM nodes — for any workload size.
        - name: Parallel Storage
          icon: database
          icon_pack: fas
          description: >
            Lustre parallel filesystem delivering high-speed I/O shared across all nodes,
            plus NFS volumes for archival data.
        - name: SLURM Workload Manager
          icon: tasks
          icon_pack: fas
          description: >
            Fair-share job scheduling ensures all users get their share of
            resources. Supports arrays, parallelism and interactive sessions.
        - name: Environment Modules
          icon: puzzle-piece
          icon_pack: fas
          description: >
            Pre-installed bioinformatics software managed via `module load`.
            Multiple versions coexist so your pipelines stay reproducible.
        - name: Fast Interconnect
          icon: network-wired
          icon_pack: fas
          description: >
            10 Gbps dedicated storage network and 1 Gbps HPC interconnect ensure
            data flows freely between nodes and storage.
        - name: Community & Support
          icon: comments
          icon_pack: fas
          description: >
            GitHub-based discussions, issue tracker, and a growing user-contributed
            wiki. Your knowledge can help the next researcher.
    design:
      background:
        color: white

  # ─── ABOUT ───────────────────────────────────────────────────────────────
  - block: markdown
    id: about
    content:
      title: About MARBITS
      text: |
        MARBITS is the Marine Bioinformatics Service at the **Centre Mediterrani
        d'Investigacions Marines i Ambientals (CMIMA)**, operated by the
        Institut de Ciències del Mar (ICM-CSIC) in Barcelona.

        The cluster is physically located in the CPD room of CMIMA,
        a short walk from the Somorrostro beach. It serves as the primary computing
        infrastructure for marine genomics and environmental metagenomics research
        carried out at the centre — and is available to all affiliated researchers.

        To request an account, send an email to [psanchez@icm.csic.es](mailto:psanchez@icm.csic.es)
        with your name, supervisor, and the project/bank account to be billed. See the
        [System Overview](/docs/system-overview/) for full hardware specs.
    design:
      background:
        color: '#f0f4f8'

  # ─── DOCUMENTATION LINKS ─────────────────────────────────────────────────
  - block: markdown
    id: docs
    content:
      title: Documentation
      text: |
        <div class="row mt-3">
          <div class="col-12 col-sm-6 col-md-4 mb-4">
            <a href="/docs/getting-started/" class="card h-100 text-decoration-none shadow-sm p-3 d-block">
              <h5 class="card-title"><i class="fas fa-rocket text-primary mr-2"></i> Getting Started</h5>
              <p class="card-text text-muted">Account setup, login, and first steps on the cluster.</p>
            </a>
          </div>
          <div class="col-12 col-sm-6 col-md-4 mb-4">
            <a href="/docs/system-overview/" class="card h-100 text-decoration-none shadow-sm p-3 d-block">
              <h5 class="card-title"><i class="fas fa-server text-primary mr-2"></i> System Overview</h5>
              <p class="card-text text-muted">Hardware specs, compute nodes, and network topology.</p>
            </a>
          </div>
          <div class="col-12 col-sm-6 col-md-4 mb-4">
            <a href="/docs/filesystem/" class="card h-100 text-decoration-none shadow-sm p-3 d-block">
              <h5 class="card-title"><i class="fas fa-hdd text-primary mr-2"></i> File System</h5>
              <p class="card-text text-muted">Lustre, quotas, scratch space, and storage best practices.</p>
            </a>
          </div>
          <div class="col-12 col-sm-6 col-md-4 mb-4">
            <a href="/docs/running-jobs/" class="card h-100 text-decoration-none shadow-sm p-3 d-block">
              <h5 class="card-title"><i class="fas fa-play-circle text-primary mr-2"></i> Running Jobs</h5>
              <p class="card-text text-muted">SLURM scripts, arrays, interactive sessions, and benchmarking.</p>
            </a>
          </div>
          <div class="col-12 col-sm-6 col-md-4 mb-4">
            <a href="/docs/software/" class="card h-100 text-decoration-none shadow-sm p-3 d-block">
              <h5 class="card-title"><i class="fas fa-cube text-primary mr-2"></i> Software Environment</h5>
              <p class="card-text text-muted">Environment modules, loading apps, and requesting new software.</p>
            </a>
          </div>
          <div class="col-12 col-sm-6 col-md-4 mb-4">
            <a href="/docs/faq/" class="card h-100 text-decoration-none shadow-sm p-3 d-block">
              <h5 class="card-title"><i class="fas fa-question-circle text-primary mr-2"></i> FAQ</h5>
              <p class="card-text text-muted">Common questions and answers about using MARBITS.</p>
            </a>
          </div>
        </div>
    design:
      background:
        color: white

  # ─── CTA ─────────────────────────────────────────────────────────────────
  - block: markdown
    id: cta
    content:
      title: Ready to get started?
      text: |
        Request an account, learn the basics, and start running your first jobs on MARBITS.
        Join the community on GitHub and help us build better documentation!

        <div class="mt-3">
          <a href="/docs/getting-started/" class="btn btn-primary btn-lg mr-3">New Users Start Here</a>
          <a href="https://github.com/marbits-icm/marbits-public/discussions" class="btn btn-outline-primary btn-lg" target="_blank">GitHub Discussions</a>
        </div>
    design:
      background:
        gradient_end: '#0d3b6e'
        gradient_start: '#1a6496'
        text_color_light: true

  # ─── CITE MARBITS ────────────────────────────────────────────────────────
  - block: markdown
    id: cite
    content:
      title: How to cite MARBITS
      text: |
        If you use MARBITS in your research, please include the following in your publications, posters, and presentations:

        > *High-Performance computing analyses were run at the Marine Bioinformatics Service (MARBITS) of the Institut de Ciències del Mar (ICM-CSIC) in Barcelona.*

        If you received direct help from a team member, please also add:

        > *We thank Pablo S. / Vane B. / Ramiro L. for his/her assistance with bioinformatics analyses.*

        We also have a **logo** available — ask the admins to include in your slides.
    design:
      background:
        color: '#f0f4f8'
---
