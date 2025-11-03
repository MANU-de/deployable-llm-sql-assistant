# Fine-Tuning a Deployable Text-to-SQL Language Model

![GitHub License](https://img.shields.io/github/license/MANU-de/deployable-llm-sql-assistant)
![Python Version](https://img.shields.io/badge/Python-3.10%2B-blue)
[![Hugging Face Model](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Trained%20Adapter-yellow)](https://huggingface.co/manuelaschrittwieser/phi-3-mini-sql-assistant)


## Table of Contents
1. [Project Summary](#1-project-summary)
2. [Repository Structure](#2-repository-structure)
3. [Environment Setup and Execution](#3-environment-setup-and-execution)
4. [Model Architecture and Training](#4-model-architecture-and-training)
5. [Evaluation and Results](#5-evaluation-and-results)
6. [License](#6-license)

---

## 1. Project Summary

This repository provides a complete and reproducible pipeline for fine-tuning a Large Language Model (LLM) to function as a specialized technical assistant. The project demonstrates the use of Parameter-Efficient Fine-Tuning (PEFT) to adapt the `microsoft/Phi-3-mini-4k-instruct` model for a Text-to-SQL generation task.

The model is trained for two epochs using the QLoRA method, resulting in an enhanced adapter that reliably translates natural language questions into accurate SQL queries based on a given database schema. This project was developed to meet the standards of a graduate-level engineering and deployment course, emphasizing reproducibility, clear documentation, and robust implementation.

### Key Features:
- **Reproducible Environment:** Uses a pinned `requirements.txt` to guarantee a stable environment.
- **Structured Code:** The entire process is encapsulated within a well-documented Google Colab notebook.
- **Professional Documentation:** Includes a detailed evaluation report and a clean project structure.
- **Enhanced Model:** Training for two epochs significantly improves reliability over single-epoch versions.

---

## 2. Repository Structure

The project is organized into logical directories for code, documentation, and configuration.

.
├── notebooks/ # Contains the primary Colab notebook for the project.
│ └── Technical_Assistant_LLM.ipynb
├── docs/ # Contains detailed supplementary documentation.
│ └── EVALUATION_AND_QUANTIZATION.md
├── .gitignore # Specifies files for Git to ignore.
├── LICENSE # The open-source license for this project.
├── README.md # This overview and guide.
└── requirements.txt # A list of pinned Python dependencies.

---

## 3. Environment Setup and Execution

To replicate the fine-tuning process or run inference, follow these steps.

### Prerequisites
- A Google Account for accessing Google Colab.
- A Hugging Face account with an access token (with "write" permissions).
- Git installed on your local machine.

### Setup and Installation
1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/YourUsername/deployable-llm-sql-assistant.git
    cd deployable-llm-sql-assistant
    ```

2.  **Upload to Google Colab:**
    - Navigate to [Google Colab](https://colab.research.google.com/).
    - Select `File > Upload notebook`.
    - Upload the `notebooks/Technical_Assistant_LLM.ipynb` file from your cloned repository.

3.  **Configure the Colab Runtime:**
    - In the notebook, navigate to `Runtime > Change runtime type`.
    - Select **T4 GPU** from the "Hardware accelerator" dropdown menu and click `Save`.

### Execution
- Execute the cells in the notebook sequentially. The notebook handles the installation of all required dependencies from the `requirements.txt` file, data preparation, the fine-tuning process, and the final evaluation.

---

## 4. Model Architecture and Training

| Parameter                 | Specification                                                                            |
| ------------------------- | ---------------------------------------------------------------------------------------- |
| **Base Model**            | `microsoft/Phi-3-mini-4k-instruct`                                                       |
| **Fine-Tuning Method**    | QLoRA (Quantized Low-Rank Adaptation)                                                    |
| **Quantization**          | 4-bit NormalFloat (NF4) via `bitsandbytes`                                               |
| **Dataset**               | `b-mc2/sql-create-context` (10,000-sample subset)                                        |
| **Training Epochs**       | **2**                                                                                    |
| **Learning Rate**         | `2e-4` with a Cosine Learning Rate Scheduler                                             |
| **LoRA Rank (r)**         | 8                                                                                        |
| **Target Modules**        | All linear layers in the Phi-3 architecture.                                             |

## 5. Evaluation and Results

The model's performance was evaluated qualitatively on a held-out test set. The extended two-epoch training successfully resolved the primary limitation of the previous version by ensuring consistent adherence to the chat template format. The model demonstrates high accuracy in generating correct SQL syntax.

For a comprehensive analysis, please see the full report:
[**docs/EVALUATION_AND_QUANTIZATION.md**](./docs/EVALUATION_AND_QUANTIZATION.md)

---

## 6. License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.