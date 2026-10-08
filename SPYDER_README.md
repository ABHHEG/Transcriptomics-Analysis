# Running the updated pipeline in Spyder

1. Keep `spyder_app.py`, `spyder_compat.py`, `spyder_analysis.py`, and `komagataella_dummy_TPM_5timepoints.csv` in the same folder.
2. Install the packages from `requirements-spyder.txt` in the Python environment used by Spyder.
3. Open `spyder_app.py` in Spyder and click **Run** (or press F5). Select a reference time point (18 hr by default) and a fold-change threshold.
4. The pipeline compares that reference against every other time point, classifies per-contrast fold changes, and summarizes each gene's overall time-course direction. It then prompts for NCBI, UniProt, InterPro, and KEGG annotations.
5. Matplotlib figures appear in Spyder's Plots pane when the Inline graphics backend is enabled. Full tables and PNG figures are saved in `spyder_outputs` beside the scripts.

The expression heatmap uses per-gene z-scores of log₂(TPM + 0.01) for genes that pass the threshold in at least one comparison. The heatmap shows relative expression shape. The overall Upregulated/Downregulated labels require a threshold-sized first-to-last change and at least 75% of successive steps in the same direction. Transient and mixed trends remain separately labeled. KEGG red/blue coloring is applied only to the overall Upregulated/Downregulated genes.

A statistical volcano plot cannot be calculated from the supplied CSV because it has a single TPM value per gene at each time point and no biological replicates. The code saves an explanatory `volcano_plot_unavailable.png`; valid p-values/FDR require replicate-aware differential-expression analysis, normally from replicate-level raw counts. Current fold-change classifications are descriptive screens, not statistical significance tests.

The colored KEGG map is also rendered as an image in Spyder's Matplotlib Plots pane and saved as a PNG. When QtWebEngine is available, the interactive KEGG page opens in a Qt window from the same Spyder session. If the viewer reports that QtWebEngine is unavailable, the colored map image still appears in the Plots pane; install the WebEngine package that matches Spyder's Qt binding (`PyQtWebEngine` or the corresponding PySide WebEngine package) to enable the interactive page.

Optional: define `NCBI_API_KEY` and `NCBI_EMAIL` as environment variables before starting Spyder if you have an NCBI API key and want to provide contact information. External annotation stages need internet access and can take time because they query NCBI, UniProt, InterPro, and KEGG.

