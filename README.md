# PFT-SR: Implementation (Google Colab)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/KPraveenRaj/IPCV_PROJECT-Implementation/blob/main/IPCV_Project_PFT_SR_Implementation.ipynb)

This repository contains a Google Colab notebook to implement: **Progressive Focused Transformer for Single Image Super-Resolution (PFT-SR)**. This implementation was created as part of an MTech (IPCV) course work.

The primary goal of this repository is to provide a convenient, ready-to-run Google Colab environment that handles the specific dependencies (CUDA 12.1, PyTorch 2.5.0, custom CUDA ops) required by the original project.

### 📄 Original Project
* **Paper:** [Progressive Focused Transformer for Single Image Super-Resolution](https://arxiv.org/pdf/2503.20337)
* **Original Repo:** [https://github.com/LabShuHangGU/PFT-SR](https://github.com/LabShuHangGU/PFT-SR)

All credit for the model architecture and original source code goes to the original authors.

---

## 🚀 How to Use this Notebook

This guide will walk you through running the `IPCV_Project_PFT_SR_Implementation.ipynb` notebook in Google Colab.

### Prerequisites
1.  A **Google Account** (for Google Colab and Google Drive).
2.  A **GPU-enabled runtime** in Colab.
    * In the notebook, go to **Runtime > Change runtime type**.
    * Select **T4 GPU** (or any available GPU) from the "Hardware accelerator" dropdown.

---

### 📝 Step-by-Step Guide

Follow these steps by running the cells in the notebook in order.

#### Step 1: Mount Drive & Create Cache
Run the first code cell to mount your Google Drive. This will create a cache folder in your Drive at `/MyDrive/Colab_Notebooks/MTech_IPCV/IPCV_Project/PFT_SR_CACHE` by default or change it to your prefered location in drive.

> **Why?** This cache is used to store the downloaded repository and, more importantly, the compiled CUDA extensions. This means you only have to compile the custom code **once**. On future runs, it will load from your Drive, saving you ~10-15 minutes of setup time.

#### Step 2: Clone Repository (Download original work with git)
This cell clones the PFT-SR repository.
* **First Run:** It clones from GitHub and saves a copy to your Drive cache.
* **Future Runs:** It loads the repo directly *from* your cache, which is much faster.

#### Step 3: ‼️ IMPORTANT: Load Pretrained Models (Manual Step)
This is the most important **manual step**. The notebook will link you to a Google Drive folder.
1.  **[Click this link to download the models](https://drive.google.com/drive/folders/1ChkxVDghFWUtJydJKLp5yssrUfm0VWfg)**.
2.  In your Google Colab file explorer (left-hand sidebar), navigate to `/content/PFT-SR/`.
3.  go into the folder named `experiments`.
4.  Inside `experiments`, you'll find another folder named `pretrained_models`.
5.  Upload the `.pth` files you downloaded into this `pretrained_models` folder.

The final path should look like this in your local memory allocated for the colab:
`/content/PFT-SR/experiments/pretrained_models/PFT_lightweight_SRx4.pth`

#### Step 4: Install Environment (‼️ IMPORTANT: Despite the warning to restart the runtime, wait till this whole section to install before restarting the runtime)
Run these cells in order. They will:
1.  Install the specific **CUDA Toolkit (12.1)** required by the project.
2.  Install the matching **PyTorch version (`2.5.0+cu121`)**.
3.  Install all other Python dependencies (like `opencv`, `lmdb`, etc.).

#### Step 5: Compile Custom CUDA Ops (Restart the runtime if not yet at this point)
This cell compiles the custom `ops_smm` operator required by PFT-SR. This step may take several minutes.

On its first run, it will compile the code and then **save the compiled files to your Drive cache**. On all future runs, this cell should load the cached version (this logic is in the notebook).

#### Step 6: Run Inference (experiment)
Now you're ready to test!
1.  Run this cell to open an "Upload" widget. Upload any low-resolution (LR) test image from your computer.
2.  This cell runs the main `inference.py` script on the image you just uploaded. You can modify the arguments:
    * `--scale 4`: Sets the upscaling factor (e.g., 4x).
    * `--task lightweight`: Selects the model to use.
3. This will automatically find the super-resolved (SR) image in the `results/colab_output/` folder and download it to your computer.

#### Step 8: Batch processing (optional)
 This step runs the main `inference.py` script on the image you just uploaded. You can modify the arguments:
    * `-i inference_images/`: Sets the input batch set path.
    * `-o results/test/`: Sets the output path.

---

## 🖼️ Example Result
Here is an example using the `lenna.png` image (from the notebook) with the `lightweight` model at 4x scale.

### Comparing (lenna)

![comparing Image](test_lenna.png)


### Input (lenna)

![Input Image](test/lenna.png)

### Output (x4 lenna)


![Output Image](test/results/lenna_PFT_lightweight_SRx4.png)
