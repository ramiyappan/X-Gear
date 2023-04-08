## Exploring X-GEAR for Zero-Shot Cross-Lingual Event Argument Extraction

Reproducing ACL-2022 paper [Multilingual Generative Language Models for Zero-Shot Cross-Lingual Event Argument Extraction](https://arxiv.org/abs/2203.08308).


### Setup 

  - Python=3.8.6-ff
  ```
  $ module load python/3.8.6-ff
  ```
  - Create environment
  ```
  $ python -m venv <env_name>
    source <env_name>/bin/activate
  ```
  <env> name can be any name.
  
### Connect to a GPU
  
  Run the following command to connect to a GPU and assign jobs in the Cluster.
  ```
  $ salloc -p gpuq -q gpu --nodes=1 --ntasks-per-node=1 --gres=gpu:A100.80gb:1 --mem=90G --cpus-per-task=24
  ```

### Training

- Run `./scripts/generate_data_ace05.sh` to generate training examples of different languages for X-Gear. 
  The generated training data will be saved in `./finetuned_data/`.
- Run `./scripts/train_ace05.sh` to train X-Gear. Alternatively, you can run the following command.

  ```
  python ./xgear/train.py -c ./config/config_ace05_mT5copy-base_en.json
  ```
  
  This trains X-Gear with mT5-base + copy mechanisim for ACE-05 English. The model will be saved in `./output/`.
  You can modify the arguments in the config file or replace the config file with other files in `./config/`.
  
### Evaluating

- Run the following script to evaluate the performance for ACE-05 English, Arabic, and Chinese.

  ```
  ./scripts/eval_ace05.sh [model_path] [prediction_dir]
  ```
  
