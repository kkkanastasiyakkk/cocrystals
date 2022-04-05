## Molecular Set Transformer
A deep learning model, namely Molecular Set Transformer, was designed for enabling high-throughput co-crystal screening for any type of molecular pairs. The model is able to provide score and uncertainty for any given molecular pair based on its probability to form a multicomponent cystal.
<img src="https://github.com/katerinavr/cocrystals/blob/master/figures/TOC.png" width="800" height="400">

## Extract co-crystals from the Cambridge Structural Database (CSD)
You need the CSD licence (https://www.ccdc.cam.ac.uk/) to use this script. You can extract multicomponent crystals after screening the whole > 1 million CSD database. If you do not want to include the solvents , you can use the option  `--no_solvents`

    python extract_cocrystals/extract_cocrystals.py --no_solvents

Our extracted csd co-crystals dataset using CSD 2020 can be found in `csd_data/csd_cocrystals2020.csv`
The training co-crystals dataset was created after removing the duplicate pairs, i.e., pairs found both in the csd_cocrystals2020 and in the benchmark data and is referred as `csd_data/csd_training_set.csv`

    python extract_cocrystals/drop_duplicates.py

## Benchmarks (Publically available co-crystal screening data)
All the is-silico co-crystal screening datasets gathered from literature can be found on the validation_data folder and are described below in chronological order:

|               |     Dataset reference                                                         |     Number or data                           |     Other methods tested on these   datasets    |
|---------------|-------------------------------------------------------------------------------|----------------------------------------------|-------------------------------------------------|
|     1         |     Wicker et al, CrystEngComm,   2017, 19, 5336–5340                         |     680 (408   negatives + 272 positives)    |                                                 |
|     2         |     Grecu   et al, Cryst.   Growth Des., 2014, 14, 165–171                    |     432 (300   negatives + 132 positives)    |     MEPS, COSMO-RS                              |
|     3         |     Wood et al, CrystEngComm,   2014, 16, 5839–5848                           |     38 (36   negatives + 2 positives)        |                                                 |
|     4         |     Vriza et al, Chem. Sci., 2021, 12, 1702–1719                              |     6 (4 negatives + 2 positives)            |                                                 |
|     5         |     Mapp et al, Cryst.   Growth Des., 2017, 17, 163–174     Khalaji et al     |     108 (90 negatives + 18 positives)        |     MC                                          |
|     6         |     Przybyłek   et al, Cryst.   Growth Des., 2019, 19, 3876–3887              |     712 (104 negatives + 608 positives)      |                                                 |
|     7         |     Przybyłek   and P. Cysewski, Cryst.   Growth Des., 2018, 18, 3524–3534    |     226 (58 negatives + 168 positives)       |                                                 |
|     8         |     Aakeröy   et al, Cryst.   Growth Des., 2009, 9, 432–441                   |     82 (17 negatives + 65 positives)         |                                                 |
|     9         |     Devogelaer   et al, Cryst.   Growth Des., 2021, 21, 3428–3437             |     30 (18 negatives + 12 positives)         |                                                 |
|     10        |     Wu et al, Cryst.   Growth Des., 2021, 21, 4531–4546                       |     63 (22 negatives + 41 positives)         |     COSMO-RS, MC                                |


## Using pretrained models to rank any test data

    python -representation<> -dataset_name<> -save_dir<> -get_plots<> -threshold<>

- `representation` The molecular embeddings to use. Choose among:
    - gnn
    - morgan
    - chemberta
    - mordred

- `dataset_name` The location of the .csv file including the molecular pairs 

- `save_dir` The folder to save the generated files
    
- `threshold` Only needed if plotting the results and have some known labels


## Or train your own models based on the prefered molecular representation

    python -representation<> -training_data<> -save_dir<> -n_epochs -lr

- `representation` The molecular embeddings to use. Choose among:
    - gnn
    - morgan
    - chemberta
    - mordred

- `training_data` The location of the .csv file containing the molecular pairs for training

- `n_epochs` The number of epochs to use for training
    
- `lr` Learning rate


## You can use Streamlit to get quick predictions for any given SMILES pair 

just click on the link: [https://share.streamlit.io/katerinavr/streamlit/app.py](https://share.streamlit.io/katerinavr/streamlit/app.py)