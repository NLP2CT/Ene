# Ene

Analysis notebooks for **Encoded but Not Express: Probing Subtle Speech-Conditioned Emotion in Large Audio Language Models**.

## Files

All analysis notebooks are in [`notebooks/`](notebooks/).

| File | Purpose |
| --- | --- |
| [basline.ipynb](notebooks/basline.ipynb) | Qwen2-Audio baseline inference, prompt evaluation, and representation extraction. |
| [Copy of basline.ipynb](notebooks/Copy%20of%20basline.ipynb) | Audio-Flamingo-3 baseline inference, prompt evaluation, and representation extraction. |
| [gemini_audio_probe_pipeline.ipynb](notebooks/gemini_audio_probe_pipeline.ipynb) | Gemini audio evaluation, perturbation runs, and audio-only prompt experiments. |
| [Copy of gemini_audio_probe_pipeline.ipynb](notebooks/Copy%20of%20gemini_audio_probe_pipeline.ipynb) | Gemini text-only evaluation using fixed prompts. |
| [Another copy of gemini_audio_probe_pipeline.ipynb](notebooks/Another%20copy%20of%20gemini_audio_probe_pipeline.ipynb) | Gemini audio-and-text evaluation using fixed prompts. |
| [probe.ipynb](notebooks/probe.ipynb) | Layer-wise emotion probe training, evaluation, and audio representation extraction. |
| [sensitive.ipynb](notebooks/sensitive.ipynb) | Speech-perturbation sensitivity analysis, including probe shifts, intensity, delivery cues, and cosine distances. |
| [sensitivity_extend (3).ipynb](notebooks/sensitivity_extend%20%283%29.ipynb) | Sensitivity, intensity, probe-stability, demographic, cosine-distance, and directional-alignment figures. |
| [appendix.ipynb](notebooks/appendix.ipynb) | Layer-wise probe accuracy figures across three random seeds for both open models. |
| [probe_viz_qwen.ipynb](notebooks/probe_viz_qwen.ipynb) | Qwen2-Audio representation visualizations and prompt-result summaries. |
| [probe_viz_flamingo.ipynb](notebooks/probe_viz_flamingo.ipynb) | Audio-Flamingo-3 representation visualizations and prompt-result summaries. |
| [Copy of probe_viz.ipynb](notebooks/Copy%20of%20probe_viz.ipynb) | Combined representation visualizations, centroid analyses, and prompt-result summaries. |
| [geometry.ipynb](notebooks/geometry.ipynb) | Emotion-centroid geometry and CREMA-D intensity-transition analysis. |
| [geometry_with_statistics.ipynb](notebooks/geometry_with_statistics.ipynb) | Emotion-centroid geometry with speaker-level statistics for CREMA-D intensity transitions. |
| [Unified_representation_geometry.ipynb](notebooks/Unified_representation_geometry.ipynb) | Unified separability, centroid displacement, directional alignment, and statistical exports for both open models. |
| [fusion-probe.ipynb](notebooks/fusion-probe.ipynb) | Qwen2-Audio layer probes and audio-language fusion-weight experiments. |
| [Copy of fusion-probe.ipynb](notebooks/Copy%20of%20fusion-probe.ipynb) | Audio-Flamingo-3 layer probes and audio-language fusion-weight experiments. |
| [residual.ipynb](notebooks/residual.ipynb) | Audio-Flamingo-3 representation reinjection experiments with multiple seeds and bootstrap summaries. |
| [Copy of residual.ipynb](notebooks/Copy%20of%20residual.ipynb) | Qwen2-Audio representation reinjection experiments with multiple seeds and bootstrap summaries. |
| [abla-qwen.ipynb](notebooks/abla-qwen.ipynb) | Qwen2-Audio speech-only, text-only, and multimodal ablation experiments. |
| [abla-flamingo.ipynb](notebooks/abla-flamingo.ipynb) | Audio-Flamingo-3 speech-only, text-only, and multimodal ablation experiments. |
| [`requirements.txt`](requirements.txt) | Python libraries used by the notebooks. |
| [`.gitignore`](.gitignore) | Keeps local credentials, datasets, model files, and generated outputs in the local workspace. |

## Quick start

1. Open the notebook you need in Google Colab. For local use, open it in Jupyter and adapt the Google Drive mount cells to your local paths.
2. Install the libraries with `pip install -r requirements.txt`. In Colab, upload `requirements.txt` and run `%pip install -r requirements.txt` in a setup cell. Select a GPU runtime for model inference and representation extraction.
3. Mount your data drive and set the notebook's input and output paths. Match each metadata CSV to the corresponding model's representations. Common roots are `probing/`, `probe/`, and `subprobe/`.
4. Run the setup cells, followed by the experiment or plotting section you need. Read the saved CSV tables and figures from that section's output directory.

### Inputs and workflow

- **Inference and extraction:** use the baseline or Gemini notebooks with your audio files, metadata, and emotion annotations. The open-model notebooks save representations and prediction tables.
- **Probes and sensitivity:** use `probe.ipynb` with the saved representation index and tensors, then `sensitive.ipynb` with the probes and paired baseline/perturbation results.
- **Geometry, fusion, and ablations:** select the corresponding notebook and configure its model-specific metadata, representation roots, and output paths.
- **Figures:** use the visualization notebooks with saved results. `sensitivity_extend (3).ipynb` exports PDF, SVG, and PNG figures; `appendix.ipynb` reads the three probe-seed CSV files.

Typical inputs include `metadata.csv`, `subset_data.csv`, `merged_subtle_emotion.csv`, `task3_results.csv`, `probe_rep_index.csv`, and `.pt` representation files. The configuration cells show the paths and columns used by each section. For existing result tables, start with the corresponding analysis or plotting notebook.

### Gemini setup

Before running a Gemini notebook, configure an API key and an OpenAI-compatible endpoint supporting the notebook's Gemini audio request format. In a private setup cell, run:

```python
import getpass
import os

os.environ["GEMINI_API_KEY"] = getpass.getpass("API key: ")
os.environ["GEMINI_BASE_URL"] = input("Compatible API base URL: ").strip()
```

Then set `MODEL_NAME`, the data paths, and the output directory in the notebook.
