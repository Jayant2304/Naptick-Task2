# Naptick AI Challenge - Task 2: Voice-to-Voice Sleep Coaching Agent

This repository contains the submission for Task 2 of the Naptick AI Challenge by [Your Name] for the [Position Applied For, e.g., AI Engineer] position.

The project implements a voice-to-voice intelligent sleep coaching agent using open-source models, fine-tuned on custom sleep-related data to provide specialized advice. It also includes a Gradio-based user interface for interaction.

## Project Overview

The agent is designed to:
1.  Accept user queries via text input or live voice recording/audio upload.
2.  Transcribe voice input to text using an optimized Whisper model.
3.  Process the query using a fine-tuned Mistral-7B-Instruct-v0.2 Large Language Model. The LLM is adapted to understand and respond to questions about sleep health, routines, improvements, and interpret simulated wearable data/sleep diaries.
4.  Generate a text response.
5.  Synthesize the text response into audible speech using a Piper TTS model.
6.  Provide both text and audio (with autoplay) responses to the user via a Gradio interface.
7.  (Bonus) Handle multi-turn conversations with evolving sleep advice based on dialogue history.

## Key Features & Technologies

*   **Speech-to-Text (STT):** `faster-whisper` (base.en model) for efficient and accurate transcription.
*   **Large Language Model (LLM):** `mistralai/Mistral-7B-Instruct-v0.2` loaded with 4-bit quantization (`bitsandbytes`) for memory efficiency.
*   **Fine-Tuning:** Parameter-Efficient Fine-Tuning (PEFT) with LoRA (Low-Rank Adaptation) using the Hugging Face `transformers`, `peft`, and `datasets` libraries to adapt the LLM for specialized sleep coaching.
*   **Text-to-Speech (TTS):** `piper-tts` (en_US-lessac-medium voice) for fast, local speech synthesis.
*   **User Interface:** `Gradio` for an interactive web interface supporting text and voice input/output.
*   **Development Environment:** Google Colab with T4 GPU.
*   **Custom Fine-tuning Dataset:** A curated dataset of ~[State the approximate number of examples, e.g., 50-70+] instruction/response pairs covering:
    *   Simulated wearable data interpretation (Fitbit, Whoop, Apple Watch, Garmin, Oura).
    *   Sleep diary analysis.
    *   Research-backed sleep science Q&A and advice.
    *   Multi-turn conversational follow-ups.

## Repository Structure

*   `Naptick_Task2_Sleep_Coach.ipynb`: The main Google Colab notebook containing all the code for data preparation, fine-tuning, model loading, core agent logic, and the Gradio UI.
*   `sleep_coach_finetuning_data.jsonl`: The custom dataset used for fine-tuning the LLM.
*   `input_test_queries/` : Contains sample input for demonstration  of conversations with the fine-tuned agent.
*   `output/` : Contains sample output for demonstration  of conversations with the fine-tuned agent.
*   `README.md`: This file.
*   `submission_writeup.pdf`: A detailed PDF write-up (if you choose to create one in addition to in-notebook documentation).

## How to Run

1.  **Open the Notebook:**
   
    *   Download `Naptick_Task2_Sleep_Coach.ipynb` and upload it to your Google Colab environment.

2.  **Colab Setup:**
    *   Ensure a **T4 GPU** is selected: In Colab, go to `Runtime` -> `Change runtime type` -> `Hardware accelerator` -> `T4 GPU`.
    *   **Hugging Face Authentication:**
        *   The notebook requires access to the `mistralai/Mistral-7B-Instruct-v0.2` model, which is gated.
        *   You **must** first visit [https://huggingface.co/mistralai/Mistral-7B-Instruct-v0.2](https://huggingface.co/mistralai/Mistral-7B-Instruct-v0.2) and accept the terms to gain access with your Hugging Face account.
        *   The notebook uses Colab Secrets to store the Hugging Face token. If you are running your own copy of the notebook, you will need to:
            1.  Create a Hugging Face access token with `read` permissions at [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens).
            2.  In your copy of the Colab notebook, click the "Key" icon (🔑) in the left sidebar, click "Add a new secret", name it `HF_TOKEN`, and paste your token value. Ensure "Notebook access" is toggled ON.

3.  **Run Cells Sequentially:**
    *   Execute all cells in the notebook from top to bottom.
    *   The initial cells install dependencies and load base models.
    *   The "Step 8: Prepare and Load Fine-Tuning Dataset" cell loads the custom data.
    *   The "Step 9: Configure and Run Fine-Tuning" cell will perform the LoRA fine-tuning. **This step will take a significant amount of time (potentially 1-2+ hours depending on Colab resources and dataset size).**
    *   The "Step 10: Load Fine-Tuned Model" cell loads the adapted LoRA weights onto the base LLM.
    *   The **final cell**, "@title Gradio Application Cell", will launch the interactive Gradio interface.

4.  **Interact with the Gradio UI:**
    *   Once the Gradio cell is run, it will output a public link (e.g., `Running on public URL: https://xxxxxxx.gradio.live`).
    *   Click this link to open the NapCoach AI interface in a new browser tab.
    *   You can then interact by typing your query or using the microphone/upload option.
