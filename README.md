# Lunar Regolith Compositional Analyser

An interactive tool for estimating lunar regolith composition, maturity, grain-size distribution, and particle type modal abundances at any near-side location. Click a point on the hemispheric map (or enter coordinates manually) and get a full sample report integrated over a user-selected depth column (0.5--30 cm).

Built on the complete Apollo 11, 12, 14, 15, 16, 17 and Luna 16, 20, 24 returned-sample database -- the most comprehensive aggregation of ground-truth lunar soil data available.

<img width="1193" height="616" alt="Screenshot 2026-04-06 at 8 24 54 PM" src="https://github.com/user-attachments/assets/2d4d9461-135b-4abf-8609-7a0e13aa8fbe" />

## Usage

Open `lunar_regolith_tool.html` in any modern browser. No build tools, no server, no dependencies.

```
open lunar_regolith_tool.html
```

Click anywhere on the lunar disc to generate a sample report. Adjust the depth slider to see how maturity, agglutinate content, grain-size distribution, and particle types evolve with depth.

## What it reports

- **Bulk composition** -- 11 major oxides (wt%) + thorium (ppm), with weighted standard deviation uncertainty ranges
- **Maturity** -- Is/FeO index and agglutinate fraction, surface and column-averaged, with depth evolution
- **Grain-size distribution** -- 6-bin Wentworth histogram (vol%), depth-adjusted
- **Particle types** -- Agglutinate, lithic, mineral, and glass modal abundances (vol%)
- **Terrane classification** -- PKT, FHT, or SPA per Jolliff et al. (2000)
- **TiO2 classification** -- High-Ti / Low-Ti / Very-Low-Ti for mare basalts per Neal & Taylor (1992)
- **Data provenance** -- Which sample sites contributed and their IDW weights

## Scientific model

| Component | Method | Source |
|-----------|--------|--------|
| Spatial interpolation | Inverse-distance-weighted (1/d², top 5 sites) with 3x cross-type penalty | Standard IDW; cross-boundary penalty is a design choice |
| Composition | Weighted average of bulk-soil major oxides | Heiken et al. (1991); Meyer (2012) |
| Maturity depth decay | Exponential, k = 0.04 cm⁻¹ | Calibrated to Apollo 15 deep drill core; Morris (1978) |
| Grain-size evolution | Agglutinate-linked redistribution from fine bins | McKay et al. (1974) Fig. 3 |
| Particle types | Depth-dependent agglutinate decay into lithic + mineral | Heiken et al. (1991) Table 7.9; Papike et al. (1982) |
| Uncertainty | Weighted standard deviation of contributing sites | See Methodology § V.b |

## Files

| File | Description |
|------|-------------|
| `lunar_regolith_tool.html` | The tool -- all CSS, HTML, and JS in a single file |
| `moon_nearside.jpg` | NASA Clementine nearside mosaic (PIA00302) |

## Key references

1. Heiken, Vaniman & French (1991) -- *Lunar Sourcebook*, Cambridge University Press
2. Meyer (2012) -- *Lunar Sample Compendium*, NASA JSC
3. Graf (1993) -- *Lunar Soils Grain Size Catalog*, NASA RP-1265
4. Morris (1978) -- Is/FeO maturity index, Proc. LPSC IX
5. Jolliff et al. (2000) -- Terrane definitions, JGR Planets
6. McKay et al. (1974, 1991) -- Grain size evolution; regolith depth properties
7. Papike, Simon & Laul (1982) -- Particle type modal abundances

## Known limitations

This tool represents the best available aggregation of returned lunar sample data. Most limitations are fundamental to the current state of lunar science and can only be resolved through future landed missions and sample-return campaigns. See the Methodology tab (§ V.g) in the tool for full discussion.

## License

Basemap image: NASA/JPL/USGS (public domain). All sample data derived from published literature.
