# CpG DNA 3D Molecular Viewer

> Interactive 3D structural comparison of CpG-A, CpG-B, and Adenoviral dsDNA, built to visualize liquid-liquid phase separation (LLPS) mechanisms in innate immunity.

**[▶ Live Demo](https://AnishSubedi-create.github.io/cpg-dna-3d-viewer/)** Main File
**[▶ Live Demo](https://anishsubedi-create.github.io/cpg-dna-3d-viewer/v1/general.html)** Prototype 

## What this is

This is a zero-dependency, browser-based molecular visualization tool built entirely with HTML5 Canvas and vanilla JavaScript. It was developed as a research communication tool to compare three structurally and functionally distinct DNA ligands involved in innate immune sensing:

| Structure | Identity | Key feature |
|---|---|---|
| **CpG-A** | ODN2216, 20-mer | G-quadruplex tetramer, mixed PS/PO backbone |
| **CpG-B** | ODN2006, 24-mer | Linear ssDNA, full phosphorothioate backbone |
| **Adenoviral dsDNA** | B-form dsDNA | ~36 kbp linear genome, protein VII-HMGB1 axis |

The Compare tab visualizes all three side-by-side and contextualizes their distinct **liquid-liquid phase separation (LLPS)** mechanisms relevant to HMGB1, cGAS-STING, and RAGE signaling.

## The biology it encodes

### CpG-A G-quadruplex tetramer
- Four parallel strands assemble via poly-G G-quadruplex caps (parallel topology)
- K⁺ ions coordinate between G-tetrad layers at ~2.8 Å from O6 atoms
- Palindromic phosphodiester center forms duplex stems bridging the caps
- **Biological relevance:** Binds HMGB1 → LLPS condensates → RAGE-SLP76 axis → inflammasome + IFN-α/β *(PNAS 2025)*

### CpG-B linear ssDNA
- Full phosphorothioate (PS) backbone replaces bridging oxygens with sulfur at every phosphate
- No poly-G ends → no G-quadruplex formation possible
- Three GTCGTT CpG motifs engage TLR9 directly (1:1 stoichiometry)
- **Biological relevance:** Strong NF-κB/B-cell activator, weak IFN-α, does NOT trigger HMGB1-LLPS

### Adenoviral dsDNA
- B-form double helix: right-handed, 10.5 bp/turn, major groove ~22 Å, minor groove ~12 Å
- Adenovirus protein VII sequesters HMGB1 via A-box interaction → suppresses IFN-β release
- Cytosolic dsDNA (post-lysis) → cGAS·DNA LLPS → cGAMP → STING → TBK1 → IRF3 → IFN-I
- **Biological relevance:** Two competing axes — viral immune evasion (protein VII/HMGB1) vs host sensing (cGAS-STING)

## Usage

### Option 1 — Just open it
```bash
git clone https://github.com/your-username/cpg-dna-3d-viewer.git
cd cpg-dna-3d-viewer
open index.html          # macOS
# or just drag index.html into any browser
```
No build step. No npm install. No server required.

### Option 2 — GitHub Pages (recommended)
1. Fork or push this repo to your GitHub account
2. Go to **Settings → Pages → Source → Deploy from branch → main → / (root)**
3. Your viewer will be live at `https://your-username.github.io/cpg-dna-3d-viewer`

### Option 3 — Embed in any webpage
```html
<iframe 
  src="https://your-username.github.io/cpg-dna-3d-viewer"
  width="100%" 
  height="700px" 
  frameborder="0">
</iframe>
```

## Interaction

| Input | Action |
|---|---|
| **Click + drag** | Rotate molecule in 3D |
| **Scroll wheel** | Zoom in/out |
| **⟳ Auto-rotate button** | Toggle continuous rotation |
| **⊡ Reset button** | Return to default orientation |
| **Sidebar tabs** | Switch between structures |

## Technical details

### Architecture
- **Zero dependencies** — pure HTML5 Canvas 2D API with a custom painter's-algorithm depth sort
- **3D engine** — rotation matrix applied per-frame; orthographic-ish projection with perspective fov=700
- **Geometry** — all molecular coordinates are programmatically generated from known structural parameters (G-tetrad geometry, B-form helix rise/twist, Hoogsteen bond angles)
- **Rendering** — painter's algorithm (sort by Z depth per frame), per-object type draw calls

### Molecular geometry parameters used
```
CpG-A G-quadruplex:
  Strand radius:        55 Å
  Helical twist:        π × 2.5 per strand over tail region
  G-tetrad rise:        ~23 Å between layers (TY array)
  K⁺ coordination:     ~2.8 Å from O6 (modeled at axis center)
  Hoogsteen angle:      0.38 rad between G-tetrad bases

B-form dsDNA (adenoviral):
  Rise per base pair:   7.0 Å
  Twist per base pair:  2π / 10.5 = 34.3°
  Helix radius:         ~15 Å (backbone centroid)
  Major groove:         ~22 Å (represented by outer sphere markers)
  Minor groove:         ~12 Å (represented by inner sphere markers)
```

### File structure
```
cpg-dna-3d-viewer/
└── index.html      # entire application — self-contained, ~700 lines
```
## Scientific context

This viewer was built to support a journal club presentation on LLPS mechanisms in innate immunity, specifically comparing how structurally distinct DNA ligands activate different immune pathways:

- **CpG-A → HMGB1-LLPS → RAGE axis** (PNAS 2025, doi:10.1073/pnas.2505826122)
- **Adenoviral dsDNA → cGAS-LLPS → STING axis** (Science 2018, Du & Chen)
- **Adenovirus protein VII → HMGB1 A-box sequestration → IFN-β suppression** (PLOS Pathogens 2023)

The G-quadruplex topology of CpG-A is the structural basis for its HMGB1 binding and phase separation capacity — a property absent in CpG-B (linear ssDNA) and mechanistically distinct from the long B-form dsDNA that drives cGAS condensation.

## Key references

1. *CpG-A induces liquid–liquid phase separation of HMGB1 to activate the RAGE-mediated inflammatory pathway.* PNAS 2025. https://doi.org/10.1073/pnas.2505826122

2. *DNA-induced liquid phase condensation of cGAS activates innate immune signaling.* Du M, Chen ZJ. Science 2018;361(6403):704–709.

3. *Adenovirus protein VII binds the A-box of HMGB1 to repress interferon responses.* PLOS Pathogens 2023. https://doi.org/10.1371/journal.ppat.1011633

4. *Crystal structure of a tetrameric RNA G-quadruplex formed by hexanucleotide repeat expansions of C9orf72 in ALS/FTD.* Nucleic Acids Res 2024. https://pmc.ncbi.nlm.nih.gov/articles/PMC11260476/

5. *Structural basis of CpG and inhibitory DNA recognition by Toll-like receptor 9.* Nature 2015. https://doi.org/10.1038/nature14138

## Contributing

Pull requests welcome. If you want to add:
- A CpG-C structure (Class C ODN hybrid)
- Animated LLPS droplet formation
- TLR9 receptor docking visualization
- HMGB1 protein structure overlay

Open an issue or fork away.

## License

MIT — use freely for research, education, or presentations. Attribution appreciated.

*Built with original biological reasoning and Claude AI (Anthropic) — demonstrating how AI-assisted scientific visualization can be developed iteratively with domain expertise guiding every structural decision.*
