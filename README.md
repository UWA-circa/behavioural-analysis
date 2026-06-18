# SLEAP Automated HPC Pipeline

This pipeline automatically processes raw video files through [SLEAP](https://sleap.ai/), exports the tracking data to CSV, and generates a unified, interactive HTML Quality Control (QC) report. 

It is built using **Nextflow** to natively handle parallel job submission, Slurm queue management, and automatic fault-tolerance (retries and resource escalation).

## Features
- **Parallel Processing:** Dynamically queues up to 20 GPU jobs at a time.
- **Auto-Healing:** If a SLEAP job fails (e.g., Out of Memory), Nextflow deletes the corrupted files, doubles the RAM allocation, and automatically resubmits the job.
- **Unified QC Report:** Groups multiple video chunks by Camera ID and timestamps, rendering a continuous chronological tracking timeline and extracting the highest-confidence tracking frame for visual validation.
- **Auto-Dependencies:** Automatically checks for and installs missing Python dependencies for the QC report generator into the user's local directory.

---

## 🛠 Prerequisites

1. **Nextflow**: Must be installed or available as a module on your HPC.
2. **Conda Environment**: A Conda environment with `sleap` installed. 
3. **Data Naming Convention**: Video files must contain a Camera ID (e.g., `CH01`) and standard timestamps (e.g., `20240425000000`) for the chronological QC report to sort correctly. 
   *(Example: `record-0000-0000-CH01-20240425000000-20240425010000.avi`)*

---

## 📂 File Structure

To run the pipeline, ensure these three files are in your working directory:
1. `main.nf` - The Nextflow pipeline logic.
2. `nextflow.config` - The configuration file (paths, Slurm profiles, retries).
3. `start_pipeline.sh` - The Slurm submission script for the Nextflow orchestrator.

Python helper scripts live under `scripts/`:
- `scripts/trimmer.py` - Selects active segments from SLEAP CSVs.
- `scripts/copy_selected_media.py` - Copies selected CSV/video files into output folders.
- `scripts/generate_qc_report.py` - Builds the HTML QC report.

---

## ⚙️ Configuration

Before running, open **`nextflow.config`** and update the `User Configuration` block with your specific paths:

```groovy
// --- User Configuration ---
params.video_dir = "/path/to/your/videos"
params.outdir    = "/path/to/output_folder"
params.model     = "/path/to/sleap/model_folder"
params.conda_env = "/path/to/your/Conda/sleap_env"