# Next Word Prediction (LSTM + Streamlit)

Lightweight demo that trains an LSTM language model on Shakespeare's Hamlet (NLTK Gutenberg) and serves next-word predictions through a Streamlit UI.

** Live Demo:** [https://next-word-prediction-lstm-4d5jelusag4weborb5jdgv.streamlit.app/](https://next-word-prediction-lstm-4d5jelusag4weborb5jdgv.streamlit.app/)

## Repository layout
- [LSTM RNN/app.py](LSTM%20RNN/app.py) – Streamlit UI that loads the trained Keras model and tokenizer.
- [LSTM RNN/experiments.ipynb](LSTM%20RNN/experiments.ipynb) – notebook to download Hamlet, tokenize, build n-gram sequences, train the LSTM, and save artifacts.
- [LSTM RNN/hamlet.txt](LSTM%20RNN/hamlet.txt) – corpus pulled from NLTK Gutenberg.
- [LSTM RNN/next_word_prediction_model.h5](LSTM%20RNN/next_word_prediction_model.h5) – saved Keras model.
- [LSTM RNN/tokenizer.pickle](LSTM%20RNN/tokenizer.pickle) – fitted tokenizer.
- [requirements.txt](requirements.txt) – Python dependencies.

## Setup
```powershell
cd "C:\LSTM Project"
python -m venv venv
venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt
```

## Run the Streamlit app
```powershell
cd "C:\LSTM Project"
venv\Scripts\activate
streamlit run "LSTM RNN/app.py"
```
Then open the provided local URL. The default prompt is "to be or not to be"; enter any text and click Predict.

## Retrain or tweak the model
1) Open and run the notebook [LSTM RNN/experiments.ipynb](LSTM%20RNN/experiments.ipynb). It will download Hamlet via NLTK, build sequences, train the LSTM (with early stopping available), and save new `next_word_prediction_model.h5` and `tokenizer.pickle` files.
2) Copy the regenerated artifacts into `LSTM RNN/` (they already save there by default).
3) Restart the Streamlit app to load the new model/tokenizer.

## Notes
- The model expects lowercase input; the notebook lowercases the corpus during preprocessing.
- Sequences are padded to `max_sequence_len - 1`; the app infers `max_sequence_len` from the model input shape at runtime.
- If pushing to GitHub, ensure `venv/` stays ignored (already in `.gitignore`).

## Model Analysis & Limitations
- Observed that prediction quality degrades as the input context grows longer, highlighting the difficulty of recurrent networks in modeling long-range dependencies.
- The LSTM tends to emphasize recent tokens over distant context, which can limit coherence in longer sequences.
- Training on a relatively small corpus (Hamlet) restricts vocabulary diversity and generalization.
- These limitations motivate the use of attention-based or transformer architectures for improved long-context modeling in future work.

## Future Work
- Compare LSTM performance with transformer-based language models on the same corpus.
- Evaluate perplexity and top-k accuracy to quantify prediction quality.
- Extend the interface to display multiple candidate predictions with confidence scores.


