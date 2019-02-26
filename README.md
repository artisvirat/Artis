# Artis

A simple encoder-decoder model based on recurrent neural networks (RNNs) for machine translation. Supports model training and translation with trained models.

`Artis` is derived from [`romanesco`](https://github.com/laeubli/romanesco) written by Samuel Läubli.

## Training the model

`Artis` doesn't preprocess training data. If you want to train a model on lowercased input, for example, you'll need to lowercase the training data yourself.

To train a model from `source.txt` and `target.txt` using GPU 0, run

```bash
CUDA_VISIBLE_DEVICES=0 Artis train --source source.txt --target target.txt
```

By default, the trained model and vocabulary will be stored in a directory called `model`, and logs (for monitoring with Tensorboard) in `logs`. You can use custom destinations through the `-m` and `-l` command line arguments, respectively. Folders will be created if they don't exist.

Some hyperparameters can be adjusted from the command line; run `Artis train -h` for details. Other hyperparameters are currently hardcoded in `Artis/constants.py`.


## Translation

A trained model can be used to translate new text. To translate a string on GPU 0 run

```bash
CUDA_VISIBLE_DEVICES=0 echo "Here is a sample input text" | Artis translate
```

This assumes there is a folder called `model` in your current working directory, containing a model trained with `Artis` (see above). If your model is stored somewhere else, use the `-m` command line argument.

For further options, run `Artis translate -h`.


## Scoring

Finally, `Artis` can score existing translations (pairs of source and target sentences):

```bash
CUDA_VISIBLE_DEVICES=0 Artis score --source source.txt --target target.txt 
```

Assuming, again, that there is a folder called `model` in your current working directory that contains a trained model.

For further options, run `Artis score -h`.
