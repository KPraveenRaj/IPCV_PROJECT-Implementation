# PFT-SR: Google Colab Implementation
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/KPraveenRaj/IPCV_PROJECT-Implementation/blob/main/IPCV_Project_PFT_SR_Implementation.ipynb)

This repository contains a Google Colab notebook to implement: **Progressive Focused Transformer for Single Image Super-Resolution (PFT-SR)**. This implementation was created as part of an MTech (IPCV) course project.

The primary goal of this repository is to provide a convenient, ready-to-run Google Colab environment that handles the specific dependencies (CUDA 12.1, PyTorch 2.5.0, custom CUDA ops) required by the original project.

### 📄 Original Project
* **Paper:** Progressive Focused Transformer for Single Image Super-Resolution
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

#### Step 1: Mount Drive & Create Cache (Cell 1)
Run the first code cell to mount your Google Drive. This will create a cache folder in your Drive at `/MyDrive/Colab_Notebooks/MTech_IPCV/IPCV_Project/PFT_SR_CACHE`.

> **Why?** This cache is used to store the downloaded repository and, more importantly, the compiled CUDA extensions. This means you only have to compile the custom code **once**. On future runs, it will load from your Drive, saving you ~10-15 minutes of setup time.

#### Step 2: Check GPU (Cell 2)
Run this cell (`!nvidia-smi`) to confirm that Colab has assigned you a GPU. You should see an output table showing a GPU like a Tesla T4 and a CUDA Version (e.g., 12.4).

#### Step 3: Clone Repository (Cell 3)
This cell clones the PFT-SR repository.
* **First Run:** It clones from GitHub and saves a copy to your Drive cache.
* **Future Runs:** It loads the repo directly *from* your cache, which is much faster.

#### Step 4: ‼️ IMPORTANT: Load Pretrained Models (Manual Step)
This is the most important **manual step**. The notebook (Cell 4) will link you to a Google Drive folder.
1.  **[Click this link to download the models](https://drive.google.com/drive/folders/1ChkxVDghFWUtJydJKLp5yssrUfm0VWfg)**.
2.  In your Google Colab file explorer (left-hand sidebar), navigate to `/content/PFT-SR/`.
3.  Create a new folder named `experiments`.
4.  Inside `experiments`, create another folder named `pretrained_models`.
5.  Upload the `.pth` files you downloaded into this `pretrained_models` folder.

The final path should look like this:
`/content/PFT-SR/experiments/pretrained_models/PFT_lightweight_SRx4.pth`

#### Step 5: Install Environment (Cells 5-8)
Run these cells in order. They will:
1.  Install the specific **CUDA Toolkit (12.1)** required by the project.
2.  Install the matching **PyTorch version (`2.5.0+cu121`)**.
3.  Install all other Python dependencies (like `opencv`, `lmdb`, etc.).

#### Step 6: Compile Custom CUDA Ops (Cell 9)
This cell compiles the custom `ops_smm` operator required by PFT-SR. This step may take several minutes.

On its first run, it will compile the code and then **save the compiled files to your Drive cache**. On all future runs, this cell should load the cached version (this logic is in the notebook).

#### Step 7: Run Inference (Cells 10-11)
Now you're ready to test!
1.  **Cell 10:** Run this cell to open an "Upload" widget. Upload any low-resolution (LR) test image from your computer.
2.  **Cell 11:** This cell runs the main `inference.py` script on the image you just uploaded. You can modify the arguments:
    * `--scale 4`: Sets the upscaling factor (e.g., 4x).
    * `--task lightweight`: Selects the model to use.

#### Step 8: Download Result (Cell 12)
Run the final cell. This will automatically find the super-resolved (SR) image in the `results/colab_output/` folder and download it to your computer.

---

## 🖼️ Example Result
Here is an example using the `sign.jpg` image (from the notebook) with the `lightweight` model at 4x scale.

**(To add your images, take screenshots of your input/output and upload them to your GitHub repo. Then, replace the file paths below.)**

### Input (sign.jpg)
*(You should place your input image here)*

![Input Image](path/to/your/input_image.jpg)

### Output (sign_PFT_lightweight_SRx4.jpg)
*(You should place the resulting output image here)*

![Output Image](path/to/your/output_image.jpg)
