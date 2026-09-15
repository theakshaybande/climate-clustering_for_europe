# Climate Risk Clustering for Europe

**From Indicators to Typologies: Unsupervised Machine Learning for Climate Risk Clustering in Europe**

Master's internship project by **Akshay Bande**, Department of Advanced Computing, **Maastricht University**, carried out at **Catella Investment Management**. Report dated December 2025.

This repository collects the internship report, defence presentation, and dashboard demonstrations. The project investigates how unsupervised machine learning can group European regions by climate risk and compare those groups with the RESIN European Climate Risk Typology. A related study applies clustering to housing affordability in German cities.

## Explore the work

| Material | Description |
| --- | --- |
| [Internship report](reports/catella-internship-report.pdf) | Full methodology, experiments, findings, discussion, references, and dashboard appendix (76 PDF pages). |
| [Climate risk defence presentation](presentations/climate-risk-clustering-defence.pdf) | Presentation of the climate clustering project (44 pages). |
| [CRIM climate dashboard demo](videos/crim-climate-dashboard-demo.mp4) | Video demonstration of the climate dashboard. |
| [German cities housing affordability presentation](presentations/german-cities-housing-affordability.pdf) | Companion study of city affordability patterns and transitions (45 pages). |
| [Housing affordability dashboard demo](videos/german-cities-housing-affordability-demo.mp4) | Video demonstration of the German cities study. |

Open the PDFs using the links above. Download the MP4 files to watch locally if GitHub does not offer an inline preview.

## Project summary

### Research objective

The study asks whether a data-driven classification can recover meaningful European climate-risk patterns using openly available indicators, without using expert typology labels during clustering. The spatial unit is **NUTS3**, a European statistical classification of small regions.

The analysis combines three dimensions:

- **Hazard:** physical climate pressures, including heat, drought, heavy precipitation, river and coastal flooding, and wildfire and landslide proxies.
- **Exposure:** people, settlements, buildings, land cover, and infrastructure that may be affected.
- **Vulnerability:** demographic and socioeconomic conditions associated with sensitivity and coping capacity.

These dimensions support both composite risk scores for regional comparisons and clusters that explain recurring combinations of risk drivers.

### Methodology

1. **Integrate regional indicators.** Harmonize climate, geographic, and socioeconomic sources on the Eurostat NUTS3 geography. The report describes EURO-CORDEX RCP 8.5 projections, flood products, CORINE land cover, and population and socioeconomic indicators.
2. **Prepare the feature space.** Check coverage and plausible values, handle missing data, reduce skew and outlier influence, filter highly correlated features, and apply robust scaling.
3. **Compare representations and clustering methods.** Explore principal component analysis (PCA), kernel PCA (KPCA), and exploratory alternatives; evaluate K-means, hierarchical clustering, Gaussian mixture models, and spectral clustering.
4. **Validate candidate typologies.** Combine silhouette, Calinski-Harabasz, and Davies-Bouldin scores with external agreement against RESIN. Inspect cluster sizes, geographic coherence, and sensitivity to modeling choices.
5. **Explain and communicate results.** Train surrogate classifiers to reproduce cluster assignments and use SHAP feature attributions to describe the drivers. The report selects logistic regression for stakeholder-facing explanations and documents interactive dashboards.

### Reported results

The Results chapter selects two complementary configurations using an RBF kernel PCA embedding with gamma = 0.001480:

| Configuration | Clusters | Silhouette | Adjusted Rand Index | Normalized Mutual Information |
| --- | ---: | ---: | ---: | ---: |
| KPCA + K-means: main reference typology | 8 | 0.2745 | 0.2112 | 0.3022 |
| KPCA + nearest-neighbor spectral clustering: finer segmentation | 10 | 0.1934 | 0.1881 | 0.3187 |

*Source: internship report, Section 6.1.4.6, Table 6.4 (printed page 30). These are reported results, not experiments rerun from this repository. The configuration names follow that results table; some later passages in the report describe the K-means embedding as PCA.*

The main findings are:

- Both reference typologies recover broad geographic patterns such as Mediterranean heat and drought, river and coastal flood zones, and highly exposed urban regions.
- Exposure and vulnerability help distinguish regions that have similar physical hazards but different social and infrastructure profiles.
- The eight-cluster solution provides a comparison at the same class count as RESIN; the ten-cluster solution adds finer subdivisions. K-means has the higher reported ARI, while spectral clustering has the higher NMI.
- Very high silhouette scores can hide unhelpful partitions dominated by one large cluster and a few outliers. The study therefore combines numerical scores with cluster balance, map inspection, and interpretability.
- Agreement with RESIN is partial. ARI and NMI measure similarity between partitions and should not be read as classification accuracy or percentages of correctly predicted regions.

### Related applications

**Climate dashboards and flood scenarios.** The report documents regional typology maps, flood-focused scenario views, asset and portfolio climate-risk summaries, and adaptation-related dashboard views.

**German housing affordability.** A companion study combines city-level housing, demographic, labor-market, construction, and economic indicators. It applies transformations, robust scaling, dimensionality reduction, and clustering to identify affordability regimes, then examines transitions over time. The report appendix includes city transition heatmaps for 2010-2024; the presentation and video provide further context.

### Interpretation and limitations

The typologies support regional screening and explanation. NUTS3 aggregation can conceal local extremes, and the analysis depends on indicator coverage, proxy choices, preprocessing, and model settings. The report's climate projections use a single model and scenario; broader scenario ensembles and validation against observed impacts are identified as future work. The clusters are not causal explanations or direct predictions of financial losses.

## Repository contents and reproducibility

```text
.
├── README.md
├── reports/
│   └── catella-internship-report.pdf
├── presentations/
│   ├── climate-risk-clustering-defence.pdf
│   └── german-cities-housing-affordability.pdf
└── videos/
    ├── crim-climate-dashboard-demo.mp4
    └── german-cities-housing-affordability-demo.mp4
```

This is a documentation and demonstration archive. The supplied folder contains PDFs and videos; it does not include the Python notebooks, Dataiku flows, input datasets, trained models, or dashboard source code described in the report. Reproducing the numerical results requires those additional materials and their environment specifications.

### File naming

The original folder's files use descriptive lowercase names here. Their binary contents are preserved.

| Original filename | Repository path |
| --- | --- |
| `Catella_Internship_Report (6).pdf` | `reports/catella-internship-report.pdf` |
| `Final presentation (1) (1).pdf` | `presentations/climate-risk-clustering-defence.pdf` |
| `German Cities Affordibility Study PPT (1).pdf` | `presentations/german-cities-housing-affordability.pdf` |
| `CRIM Climate Dashboard new (2).mp4` | `videos/crim-climate-dashboard-demo.mp4` |
| `Video German Cities Affordibility Study (2).mp4` | `videos/german-cities-housing-affordability-demo.mp4` |

## Reference

Bande, Akshay. *From Indicators to Typologies: Unsupervised Machine Learning for Climate Risk Clustering in Europe*. Master's Internship Report, Maastricht University / Catella Investment Management, December 2025. See the [full report](reports/catella-internship-report.pdf) for source references and detailed methods.
