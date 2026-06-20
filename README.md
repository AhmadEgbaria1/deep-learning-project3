# deep-learning-project3
Deep Learning: Assignment #3 - Chatbot and Neural Machine Translation
Submission Details
Submitted by:
Morad kutt 
Ahmad Egbaria 
Topics Covered
Recurrent Neural Networks (RNNs)
Gated Recurrent Units (GRUs)
Long Short-Term Memory networks (LSTMs)
Transformers (conceptual discussion in Q1)
Project Overview
This assignment explores two fundamental applications of deep learning in Natural Language Processing: building a neural chatbot and implementing a Neural Machine Translation (NMT) system. The project is divided into two main questions, each focusing on a distinct task and model architecture.

Question 1: Chatbot Tutorial (35 Points)
Goal: To implement a generative chatbot using recurrent sequence-to-sequence (seq2seq) models.

Dataset: The chatbot is trained on conversational data extracted from the Cornell Movie-Dialogs Corpus. Each training example consists of an input sentence and a corresponding response sentence.

Key Concepts Implemented/Explored:

Data Preprocessing: Loading and reformatting movie dialog data, Unicode to ASCII conversion, normalization, filtering by MAX_LENGTH.
Vocabulary (Voc class): Custom implementation for managing word-to-index mappings, handling special tokens (PAD, SOS, EOS, UNK), and trimming rare words below MIN_COUNT.
Data Preparation for Model: Converting sentence pairs to padded numerical tensors, using inputVar and outputVar functions, and batch2TrainData for mini-batch creation.
Model Architecture (Seq2Seq):
Encoder (GRU-based): A multi-layer, bidirectional GRU that processes input sequences, uses pack_padded_sequence and pad_packed_sequence for efficiency.
Decoder with Attention (GRU-based): A unidirectional GRU that generates responses token-by-token, incorporating Luong-style Global Attention (dot, general, concat methods).
Training Procedure:
Masked NLL Loss: Computes loss only over non-padding positions.
Single Training Iteration: Implements teacher forcing (with teacher_forcing_ratio) and gradient clipping.
Training Loop (trainIters): Manages iterations, prints statistics, and saves checkpoints.
Model Evaluation:
Greedy Decoding: Generates responses by selecting the most probable token at each step.
Interactive Chat: Provides a simple interface to interact with the trained chatbot.
Beam Search Decoding: Implements a more advanced decoding strategy to find globally better sequences by keeping multiple hypotheses.
Question 2: Neural Machine Translation (NMT) with Sequence-to-Sequence Models (35 Points)
Goal: To build a Neural Machine Translation system for Portuguese to English translation using an encoder-decoder model with attention.

Dataset: A Portuguese-English parallel translation dataset derived from TED Talks, loaded using tensorflow-datasets.

Key Concepts Implemented/Explored:

Data Loading & Preprocessing: Converting TensorFlow datasets to Python lists.
Tokenization (Vocabulary class): Custom implementation for handling language-specific vocabularies, special tokens (<pad>, <unk>, <bos>, <eos>), and encoding/decoding sentences.
Length-Aware Batching (Bucketing): Using TranslationDataset, collate_fn, and BucketBatchSampler to efficiently group sentences of similar lengths for mini-batch training, reducing padding.
Model Architecture (Seq2Seq with Attention):
Encoder (Bi-LSTM): A 1-layer bidirectional LSTM that processes Portuguese source sentences, producing contextual hidden representations.
Attention Mechanism (DotProductAttention): Computes relevance scores between decoder hidden states and encoder outputs, creating a context vector while masking padding positions.
Decoder Initialization (DecoderInit): Bridges the mismatch between bidirectional encoder states and a unidirectional decoder, projecting concatenated states to initialize the decoder's hidden and cell states.
Decoder (Uni-LSTM): A unidirectional LSTM that generates English target sentences autoregressively, integrating the attention mechanism to focus on relevant source parts.
Output Projection: A linear layer mapping decoder attentional vectors to target vocabulary logits.
Full Model (Seq2SeqNMT): Connects all components for end-to-end training.
Training:
Training Loop: Trains the model for a specified number of epochs using Adam optimizer and token-level cross-entropy loss with teacher forcing.
Validation: Evaluates the model on a validation set after each epoch to monitor loss and prevent overfitting.
Loss Plotting: Visualizes training and validation loss curves.
BLEU Evaluation:
Beam Search Decoding: Uses the implemented beam search from Q1 to decode translations for the test set.
compute_bleu function: Calculates the corpus-level BLEU score to quantitatively assess translation quality.
How to Run the Notebook
Clone/Download the Notebook: Ensure you have access to this .ipynb file.
Install Dependencies: The notebook will guide you through pip install commands for tensorflow-datasets. Ensure PyTorch is also installed.
Run Cells Sequentially: Execute all cells in the notebook from top to bottom.
For Question 1 (Chatbot):
The cell _Mqe24ejcUJq will download and unzip the movie dialog corpus.
The trainIters function call in cell UllNVty_XyH7 will train the chatbot model. This may take a considerable amount of time depending on hardware.
The evaluateInput call in cell kAWQIcv2X4MO will start an interactive chat session with the greedy decoder. You can type sentences and the bot will respond. Type 'q' or 'quit' to exit.
The cell q3IWk_5ZvS8d compares greedy and beam search decoding with sample prompts.
For Question 2 (NMT):
The cell Ohht5l8pBhfX will install tensorflow-datasets.
The training loop in cell anHH0EC7xs0K will train the NMT model for 25 epochs. This will also take significant time.
The final block in cell Bd8Fg-MhmGAB will perform BLEU evaluation on the test set and display example translations.
Review Outputs: All figures, printed results, and outputs should remain visible. Do not clear outputs before submission.
Instructions for Submission
Submissions are in pairs only. Both names and IDs should be at the top of the notebook.
Keep your code clean, concise, and readable.
Write textual answers in red using <font color='red'>your answer here</font>.
Use relative paths only.
Your submission must be entirely your own work; plagiarism will result in a grade of 0.
