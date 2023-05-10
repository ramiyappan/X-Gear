## Exploring X-GEAR for Zero-Shot Cross-Lingual Event Argument Extraction

Reproducing ACL-2022 paper [Multilingual Generative Language Models for Zero-Shot Cross-Lingual Event Argument Extraction](https://arxiv.org/abs/2203.08308).

Repo of the published paper: https://github.com/PlusLabNLP/X-Gear

### Setup 

  - Python=3.8.6-ff
  ```
  module load python/3.8.6-ff
  ```
  - Create environment
  ```
  python -m venv <env_name>
  source <env_name>/bin/activate
  ```
  env_name can be any name.
  
  - install all required dependencies using `requirements.txt`.
  ```
  pip install -r requirements.txt
  ```
  
### Connect to a GPU
  
  Run the following command to connect to a GPU and assign jobs in the Cluster.
  ```
  salloc -p gpuq -q gpu --nodes=1 --ntasks-per-node=1 --gres=gpu:A100.80gb:1 --mem=90G --cpus-per-task=24
  ```
  
  You can modify the arguments of this command based on specific needs and resources.
  
### Training

- Run `./scripts/generate_data_ace05.sh` to generate training examples of different languages for X-Gear. 
  The generated training data will be saved in `./finetuned_data/`.
- Run `./scripts/train_ace05.sh` to train X-Gear. Alternatively, you can run the following command.

  ```
  python ./xgear/train.py -c ./config/config_ace05_mT5copy-base_en.json
  ```
  
  This trains X-Gear with mT5-base + copy mechanisim for ACE-05 English. The model will be saved in `./output/`.
  You can modify the arguments in the config file.
  You can use `./config/config_ace05_mT5copy-base_ar.json` and `./config/config_ace05_mT5copy-base_zh.json` to train with copy mechanisim for ACE-05 Arabic and Chinese respectively.
  
### Evaluating

- Run the following script to evaluate the performance for ACE-05 English, Arabic, and Chinese.

  ```
  ./scripts/eval_ace05.sh [model_path] [prediction_dir]
  ```
  `model_path` would be `best_model.mdl` inside logs(having year, date and time format) folder of `output`.
  `prediction_dir` could be any directory name of where you want to store the predictions.

### Authors

```
  Ramaswamy Iyappan, Masters in Computer Science, riyappan@gmu.edu
  Abhijeet Banerjee, Masters in Computer Science, abanerj@gmu.edu
  Bhargava Canakapally, Masters in Computer Science, bcanakap@gmu.edu
  Title: Exploring X-GEAR for Zero-Shot Cross-Lingual Event Argument Extraction
  Organization: George Mason University
  Year: 2023
