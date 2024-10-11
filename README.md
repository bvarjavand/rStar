### Fork of rStar: Mutual Reasoning Makes Smaller LLMs Stronger Problem-Solvers

This forked repository contains modified scripts to run **rStar**'s generator and discriminator on the `dair-ai/emotion` dataset.

#### WIP: Generator runs, need to update evaluation module to correctly extract predicted label.

## Prerequisites

- Python 3.10
- CUDA 12
- newest PyTorch
- newest `transformers`
- newest `vllm`

## Usage

The only change to the default usage options below is to change the `--dataset_name` flag to `Emotion`

### rStar Generator

Here is an example to run rStar generator:

```bash
bash scripts/run_gsm8k_generator.sh
```

The script `run_gsm8k_generator.sh` includes several configurable parameters:
- `--dataset_name`: Name of the dataset (choose from [MATH, GSM8K, GSM8KHARD, STG, SVAMP, MULTIARITH]).
- `--test_json_filename`: Filename for the test JSON (default: test_all).
- `--model_ckpt`: Path to the model checkpoint.
- `--note`: Additional note to mark the output folder. Without further arguments, the generator output folder will be `./run_outputs/<dataset_name>/<model_ckpt>/<execute_time>---[<note>]`
- `--num_rollouts`: Number of rollouts (default: 16).

Make sure to adjust these parameters according to your requirements.

#### Evaluate rStar Generator

Here is an example to evalute the results of **rStar** generator
```bash
python eval_src/do_eval.py --dataset_name GSM8K --exp_dir_path <generator_output_folder>
```

### rStar Discriminator

Here is an example to run rStar discriminator:

```bash
bash scripts/run_gsm8k_discriminator.sh
```

The script `run_gsm8k_discriminator.sh` includes several configurable parameters:

- `--model_ckpt`: checkpoint Path to the discriminator model.
- `--root_dir`: Path of evalution result folder.
- `--dataset_name`: Name of the dataset (choose from [MATH, GSM8K, GSM8KHARD, STG, SVAMP, MULTIARITH]).
- `--note`: Additional note to mark the output folder. Without further arguments, the discriminator output folder will be `<root_dir>/dis_<execute_time>---<note>`

## Results

Extensive experiments across five SLMs demonstrate rStar can effectively solve diverse reasoning problems. rStar boosts GSM8K accuracy from 12.51% to 63.91% for LLaMA2-7B, from 36.46% to 81.88% for Mistral-7B, from 74.53% to 91.13% for LLaMA3-8B-Instruct.

<p align="center">
  <img src="assets/result.png" width="600px">
</p>


## Citation

If you find our work helpful, please consider citing it:
```
@misc{qi2024mutual,
    title={Mutual Reasoning Makes Smaller LLMs Stronger Problem-Solvers},
    author={Zhenting Qi and Mingyuan Ma and Jiahang Xu and Li Lyna Zhang and Fan Yang and Mao Yang},
    year={2024},
    eprint={2408.06195},
    archivePrefix={arXiv},
    primaryClass={cs.CL}
}
```

## Read More

rStar has been recommended as a key technique in [Awesome LLM Strawberry (OpenAI o1)](https://github.com/hijkzzz/Awesome-LLM-Strawberry). Click and read more relevant papers.
