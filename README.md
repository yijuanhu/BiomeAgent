# BiomeAgent
A Specialist AI Agent for End-to-End Microbiome Data Analysis

BiomeAgent is an open-source project designed to help researchers move from microbial abundance data to transparent and reproducible results. It brings data ingestion, quality control, statistical analysis, biological interpretation, and report generation into one structured workflow.


> [!IMPORTANT]
> **BiomeAgent is currently in early development.** This repository describes the intended direction of the project. Features, interfaces, dependencies, and workflows may change before the first stable release.

## Why BiomeAgent?

The project is motivated by a common challenge in biomedical research: a large amount of time is spent writing code, reading and aligning input data, selecting statistical methods, interpreting outputs, and building reports. BiomeAgent aims to automate these repetitive tasks while keeping analytical decisions visible and under the researcher's control.

BiomeAgent is being developed around five goals:

- apply domain-standard statistical workflows;
- reduce repetitive data-processing and analysis work;
- preserve a complete record of analytical decisions;
- produce results that researchers can inspect, reproduce, and extend.

BiomeAgent is not intended to replace statistical expertise or biological interpretation. Instead, it acts as a research assistant that prepares analyses, documents decisions, flags potential issues, and presents evidence for expert review.

## Planned Capabilities

### Data ingestion and harmonization

- Import user-provided microbiome and multi-omics datasets.
- Retrieve data and metadata from supported public repositories.
- Detect common tabular formats, delimiters, orientations, and identifier columns.
- Harmonize sample identifiers across abundance tables and metadata.
- Preserve original files while creating standardized downstream inputs.
- Generate machine-readable summaries of imported datasets.

### Quality control

- Assess library size, missingness, sparsity, and feature prevalence.
- Identify duplicated or inconsistent sample identifiers.
- Inspect potential outliers, batch effects, and technical artifacts.
- Document every filtering threshold and the number of affected samples or features.
- Warn users before potentially consequential filtering or transformation steps.
- Produce reusable QC tables and publication-ready visualizations.

### Statistical analysis

- Alpha- and beta-diversity analysis.
- Differential-abundance testing with methods appropriate for microbiome data.
- Presence/absence and abundance-based association analysis.
- Covariate-aware and matched-sample workflows where supported.
- Microbial association network analysis.
- Multi-omics analysis.
- Explicit reporting of assumptions, parameters, failures, and skipped analyses.

The analytical framework is expected to include established R-based methods such as LDM, LOCOM2, and TestNet when they are compatible with the study design and available data.

### Annotation and interpretation

- Organize taxonomic and functional annotations.
- Connect statistical outputs with relevant feature metadata.
- Summarize consistent and method-specific findings.
- Separate exploratory observations from statistical associations and causal claims.
- Prepare structured interpretation files for downstream reporting.

### Automated reporting

- Generate a human-readable HTML research report.
- Combine dataset summaries, QC results, statistical findings, figures, and tables.
- Include analysis parameters, software versions, random seeds, and output locations.
- Clearly identify unavailable analyses rather than fabricating results.
- Preserve links between report statements and their underlying result files.

## Workflow

```text
Local or public data
        │
        ▼
1. Data ingestion and validation
        │
        ▼
2. Quality control and filtering
        │
        ▼
3. Statistical analysis and annotation
        │
        ▼
4. Reproducible report generation
```

Each stage produces explicit files that can be reviewed before the next stage begins. Important analytical decisions remain visible, and potentially irreversible operations should require user confirmation.

## Supported Data Types

The planned workflow is intended to support:

| Data type | Examples |
| --- | --- |
| Taxonomic abundance | OTU, ASV, species, genus, or family abundance tables |
| Functional profiles | KEGG, MetaCyc, GO, or other pathway profiles |
| Sample metadata | Phenotypes, treatments, clinical variables, and other covariates |
| Longitudinal data | Repeated measurements or matched samples |
| Metabolomics | Metabolite abundance or intensity tables |
| Other omics | Paired transcriptomic or related feature matrices |

Common input formats are expected to include CSV, TSV, TXT, BIOM, XLSX, and Parquet. Actual format support will be documented and tested as the implementation matures.

## Dataset-level Isolation

BiomeAgent treats every dataset as an independent project. Generated code, processed data, results, reports, and logs remain inside the dataset directory.

```text
project/<dataset_name>/
├── raw/          # Original inputs; never overwritten
├── processed/    # Standardized and filtered data
├── metadata/     # Dataset and sample metadata
├── code/         # Reproducible, dataset-specific analysis code
├── results/      # Tables, statistics, and figures
├── reports/      # Final reports and supplementary material
└── logs/         # Decisions, warnings, errors, and execution records
```

This structure prevents outputs from different studies from being mixed and makes it easier to archive, share, or rerun an analysis.

## Design Principles

### Reproducibility first

Analyses should be rerunnable from the original inputs. BiomeAgent records parameters, random seeds, software versions, generated code, intermediate outputs, and execution logs wherever possible.

### Scientific transparency

The agent should never silently remove data, hide failed analyses, or present unsupported conclusions. Filtering rules, model choices, assumptions, and limitations must be documented.

### Human-in-the-loop decision making

Automation should reduce repetitive work without removing researcher oversight. Decisions with meaningful scientific consequences—such as aggressive filtering, batch correction, rarefaction, or changes to the study design—should be explained before they are applied.

### Modular and extensible workflows

Data ingestion, QC, analysis, annotation, and reporting are separate stages. Individual methods can be maintained or extended without replacing the complete workflow.

### Readable research code

Generated code should favor explicit parameters, clear structure, and maintainability over compact or opaque implementations. R is the preferred language for core microbiome statistics, with Python used where it offers a clear advantage.

## Intended Users

BiomeAgent is being developed for:

- microbiome and bioinformatics researchers;
- wet-lab scientists working with sequencing data;
- analysts performing public-dataset reanalysis;
- research teams that need consistent workflows across multiple studies;
- developers building reproducible scientific analysis systems.

Some statistical and command-line experience may be required during the early development phase. A more accessible user experience is part of the longer-term roadmap.

## Example Outputs

Depending on the dataset and study design, a completed workflow may produce:

- standardized abundance and metadata tables;
- data-validation and quality-control summaries;
- sample- and feature-level QC figures;
- diversity statistics and ordination plots;
- differential-abundance result tables;
- microbial network results;
- structured biological interpretation notes;
- analysis parameters and execution logs;
- a reproducible HTML report.

## Project Status and Roadmap

BiomeAgent is currently a work in progress. The near-term roadmap includes:

- [ ] Finalize the standard project and dataset structure.
- [ ] Implement robust data detection, import, and validation.
- [ ] Complete transparent sample- and feature-level QC workflows.
- [ ] Integrate and test the core statistical analysis modules.
- [ ] Add study-design-aware method selection.
- [ ] Improve biological annotation and result interpretation.
- [ ] Generate reproducible template-based HTML reports.
- [ ] Add example datasets and end-to-end tutorials.
- [ ] Add automated tests and continuous integration.
- [ ] Publish installation instructions and a versioned release.

## Repository Documentation

The current design documents describe the main workflow stages:

- [`01_data_ingestion.md`](01_data_ingestion.md) — data retrieval, import, and standardization;
- [`02_quality_control.md`](02_quality_control.md) — sample- and feature-level quality control;
- [`03_analysis_annotation.md`](03_analysis_annotation.md) — statistical analysis and annotation;
- [`04_report_generation.md`](04_report_generation.md) — reproducible report generation;
- [`user_workflow.md`](user_workflow.md) — the intended user workflow;
- [`coding_rules.md`](coding_rules.md) — engineering and reproducibility principles.

These documents currently represent the project specification and may evolve alongside the implementation.

## Responsible Use

BiomeAgent is a research-support tool. Its outputs should not be treated as clinical advice or accepted without expert review. Users remain responsible for validating input data, confirming that methods match the study design, checking model assumptions, interpreting results in context, and independently verifying important findings.

## Contributing

The project is at an early stage, and feedback is welcome. You can contribute by:

- opening an Issue to describe a use case or dataset format;
- reporting unclear assumptions or reproducibility gaps;
- proposing statistical methods or validation tests;
- improving documentation and examples;
- discussing potential research collaborations.

Contribution guidelines will be added as the project approaches its first public release.

## License

A license has not yet been selected. Licensing information will be added before the first formal release. Until then, no permission to use, modify, or redistribute the project should be assumed.

## Citation

Citation information will be provided with the first public release. If you use an early version of BiomeAgent in a research project, please record the exact commit or release version to support reproducibility.
