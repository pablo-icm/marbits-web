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
        MARBITS is the Marine Bioinformatics Service at the Institut de Ciències del Mar (ICM-CSIC) in Barcelona. Located within a short walk from the Somorrostro beach, it serves as the primary computing infrastructure for marine genomics and environmental metagenomics research carried out at the Institute — and is available to all affiliated researchers.
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
              <div class="stat-number">{{< spec "cores" >}}</div>
              <div class="stat-label">CPU Cores<br><span class="stat-sub">({{< spec "cores_ht" >}} with HT)</span></div>
            </div>
            <div class="col-6 col-md-3 py-4 px-3">
              <div class="stat-number">{{< spec "ram" >}}</div>
              <div class="stat-label">Total RAM</div>
            </div>
            <div class="col-6 col-md-3 py-4 px-3">
              <div class="stat-number">{{< spec "storage_total" >}}</div>
              <div class="stat-label">Total Storage</div>
            </div>
            <div class="col-6 col-md-3 py-4 px-3">
              <div class="stat-number">{{< spec "nodes" >}}</div>
              <div class="stat-label">Compute Nodes</div>
            </div>
          </div>
        </div>
    design:
      background:
        color: '#f0f8ff'

  

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

  

  # ─── CITE MARBITS ────────────────────────────────────────────────────────
  - block: markdown
    id: cite
    content:
      title: How to cite MARBITS
      text: |
        If you use MARBITS in your research, please include the following in your publications, posters, and presentations:

        > *High-Performance computing analyses were run at the Marine Bioinformatics Service (MARBITS) of the Institut de Ciències del Mar (ICM-CSIC) in Barcelona.*

        We also have a **logo** available — ask the admins to include in your slides.
    design:
      background:
        color: '#f0f4f8'
---
