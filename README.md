### Deterministic Top2Vec

This is a fork of [`Top2Vec`](https://github.com/ddangelov/Top2Vec) based on discussion of [issue 86](https://github.com/ddangelov/Top2Vec/issues/86). Edits in this fork allow for replicable results of `Top2Vec` using sentence encoders as the embedding model by leveraging [UMAP](https://umap-learn.readthedocs.io/en/latest/reproducibility.html) as suggested by github user `tploetz`.

### Installing the Fork

I currently running this fork on Fedora Linux. To do so, it should be sufficient to create a new python environment and run `pip install -r requirements.txt`. I am not installing `Top2Vec` directly with `pip` currently -- though this shouldn't be too much trouble.  

### Running the Fork

This fork of `Top2Vec` can be run with roughly the following assuming that the `top2vec` folder has been placed within the same directory as your script. The following is an example python script `test.py`.

```python
import pandas as pd
from top2vec import Top2Vec

seed = 34

df = pd.read_csv("documents.csv")
documents = df['documents'].tolist()

model_1 = Top2Vec(ngram_vocab = True, seed = seed, embedding_model = 'universal-sentence-encoder')
model_1.save("model_1")
model_2 = Top2Vec(ngram_vocab = True, seed = seed, embedding_model = 'universal-sentence-encoder')
model_2.save("model_2")
`
```

Then the following bash script can be used to ensure that consecutive runs produce the same model.

```bash
python test.py
diff model_1 model_2
```

The final line should not return any text, indicating that the model produced in the first script is identical to the model produced in the second script.

