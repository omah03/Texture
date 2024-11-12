
markdown
Copy code
# MVS-Texturing Docker Setup

This setup provides a Docker environment for 3D texturing from Multi-View Stereo (MVS) data using the MVS-Texturing tool. 
1. `run_calibrating.sh` - For camera calibration parsing into MVE format.
2. `run_texturing.sh` - For running the texturing pipeline.

---

## Prerequisites

- **Docker**: Make sure Docker is installed. See instructions at [Docker's official site](https://docs.docker.com/get-docker/).

---

## Setup Instructions

1. **Load the Docker Image** (if provided as `mvs-texturing.tar`):
   ```bash
   sudo docker load -i mvs-texturing.tar
Verify Docker Image: After loading, confirm the image by running:
bash
Copy code
sudo docker images
Usage
1. Calibration Preprocessing
The run_calibrating.sh script prepares camera calibration data by parsing XML into the MVE scene format. This script takes three arguments: the calibration XML file, source images, and the output MVE scene directory.

Command:

bash
Copy code
./run_calibrating.sh <CALIBRATION_XML_PATH> <IMAGE_SOURCE_DIR> <MVE_SCENE_DIR>
CALIBRATION_XML_PATH: Path to the calibration XML file (e.g., Calibration.xml).
IMAGE_SOURCE_DIR: Directory containing source images.
MVE_SCENE_DIR: Directory where the MVE scene data will be saved.
Example:

bash
Copy code
./run_calibrating.sh /path/to/Calibration.xml /path/to/images /path/to/output_mve_scene
2. Running the Texturing Process
The run_texturing.sh script performs the texturing based on the MVE scene. It takes paths for the MVE scene, the mesh file, and an output directory, with optional arguments for GAUSS_REJECTION_THRESHOLD and MINIMAL_COVARIANCE.

Command:

bash
Copy code
./run_texturing.sh <MVE_SCENE_DIR> <MESH_DIR> <OUTPUT_DIR> [GAUSS_REJECTION_THRESHOLD] [MINIMAL_COVARIANCE]
MVE_SCENE_DIR: Path to the MVE scene directory.
MESH_DIR: Path to the .ply mesh file.
OUTPUT_DIR: Directory where textured output will be saved.
GAUSS_REJECTION_THRESHOLD (optional): Default is 0.01.
MINIMAL_COVARIANCE (optional): Default is 0.0005.
Example:

bash
Copy code
./run_texturing.sh /path/to/mve_scene /path/to/mesh.ply /path/to/output_directory 0.01 0.0005
Example Workflow
Run Calibration:

bash
Copy code
./run_calibrating.sh /media/dc-04-vol03/omar/task_texture_mapping/input3/Calibration.xml /media/dc-04-vol03/omar/task_texture_mapping/input3/image /media/dc-04-vol03/omar/task_texture_mapping/mve_scene
Run Texturing:

bash
Copy code
./run_texturing.sh /media/dc-04-vol03/omar/task_texture_mapping/mve_scene /media/dc-04-vol03/omar/task_texture_mapping/input/mesh.ply /media/dc-04-vol03/omar/task_texture_mapping/output
Notes
Ensure the specified directories have read and write permissions.
Adjust GAUSS_REJECTION_THRESHOLD and MINIMAL_COVARIANCE parameters for different texturing quality requirements.
To enter the Docker container for debugging or manual checks, use:
bash
Copy code
sudo docker run -it --rm -v "/path/to/local/dir:/mnt" mvs-texturing /bin/bash
With this setup, you can seamlessly run both calibration and texturing workflows, enabling efficient 3D reconstruction.

Copy code





