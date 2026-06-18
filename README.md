# SLEAP Automated HPC Pipeline

This pipeline automatically processes raw video files through [SLEAP](https://sleap.ai/), exports the tracking data to CSV, and generates a unified, interactive HTML Quality Control (QC) report. 

It is built using **Nextflow** to natively handle parallel job submission, Slurm queue management, and automatic fault-tolerance (retries and resource escalation).

## Example Pipeline Structure
<img width="960" height="1704" alt="Example Processing Pipeline" src="https://github.com/user-attachments/assets/49c39c32-7cbc-4f84-a175-7c457dd068d0" />

## Example Annotated Video
https://github.com/user-attachments/assets/654c28a5-69b6-4507-94a9-ffb0c72b199e

## Example Annotated Video
<iframe 
  width="960" 
  height="350" 
  src="https://github.com/user-attachments/assets/654c28a5-69b6-4507-94a9-ffb0c72b199e" 
</iframe>
