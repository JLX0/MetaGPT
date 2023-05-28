# Introduction

MetaLLM-GPT is an application that automatically generates Python codes based on GPT (as used
in ChatGPT).

While the naive GPT model (as used in ChatGPT) can generate Python codes, the code 
it generates often contains errors. Compared to ChatGPT, MetaLLM-GPT tests the 
generated/managed codes locally and automatically ensures that the code can run 
smoothly and meet certain expectations.

Compared to [AutoGPT](https://github.com/Significant-Gravitas/Auto-GPT), MetaLLM-GPT is more
specialized in generating Python codes. By leveraging metaprogramming, MetaLLM-GPT is more
stable and easier to use.

MetaLLM-GPT combines metaprogramming (in Python) and large language models (LLMs) (GPT). 
* [Metaprogramming](https://en.wikipedia.org/wiki/Metaprogramming) refers to the 
programming method which involves one program (the meta program) writing another program
(the target program).
* [LLMs](https://en.wikipedia.org/wiki/Large_language_model) are recently developed neural 
networks that can generate text based on the context.

Here is a simple illustration of our algorithm:

![alt text](https://github.com/JLX0/MetaLLM-GPT/blob/main/illustration.png?raw=true)

<hr/>

# Installation and requirements

* Linux-based system (tested with Ubuntu 20.04 and 22.02)
* Python 3.7.1 or higher. We recommend using a new virtual environment 
(e.g., [conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html))
```
conda create -n mg python=3.10
```
```
conda activate mg
```
* This repository
```
git clone https://github.com/JLX0/MetaLLM-GPT.git
```
```
cd MetaLLM-GPT
```
* The OpenAI Python library (tested with 0.27.6)
```
pip install openai
```

* OpenAI API key with GPT-3.5 and/or GPT 4 access. You can get one from
[here](https://platform.openai.com/account/api-keys).

<hr/>

# Usage

## In general

Before using MetaLLM-GPT, please make sure that you have met the general requirements
as specified in *Installation and requirements*.

You can run the following command to check how to configure MetaLLM-GPT:
```
python3 mg.py -h
```

The file *mg.py* requires at least three arguments: *-o*, *-f*, and *-k*. 
* The argument *-o* describes the objective of this code
* The argument *-f* describes the path to the Python file that is supposed to be read 
and written by MetaLLM-GPT
* The argument *-k* describes the openAPI key you want to use

Please be careful about using a notebook format file (such as *.ipynb*) in *-f*, 
as GPT might try to execute Linux commands in the notebook.

If you want to use the *-e* argument (in order to create code beyond the built-in modules
in Python), it would be safer to download the required packages in the environment
beforehand.

By default, MetaLLM-GPT assumes you want to use GPT 3.5. If you want to use GPT 4, please
set the argument *-g* to "4".

## Example 1: Generate Python code of a deep neural network

This command assumes that in your current environment, Pytorch is installed. If you prefer other deep
learning packages, please modify the *-e* arguments. The expected input of the neural network is the
batch size, learning rate, and training epochs. The expected output of the neural network is the 
validation accuracy of the model.

```
python3 mg.py -o "create a deep neural network that uses GPU" -f "dnn.py" -k "aa-aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa" -in "1. bs: batch size 2. l:learning rate 3. e: training epochs " -out "the validation accuracy of the neural network" -e "1.pytorch" -l 300
```
Please replace the key *"aa-aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"* with your
own OpenAPI key. The generated code is saved in your current working directory as a file named 
*dnn.py*. Sample codes generated by this command can be found in the folder *samples* (*dnn_1.py* and 
*dnn_2.py*)

The above commands assume that in your current environment, a GPU device is available to the python packages. 
If not, please use the following command instead:

```
python3 mg.py -o "create a deep neural network that uses CPU" -f "dnn.py" -k "aa-aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa" -in "1. bs: batch size 2. l:learning rate 3. e: training epochs " -out "the validation accuracy of the neural network" -e "1.pytorch" -l 300
```

## Example 2: Generate Python code of a genetic algorithm

The expected input of the algorithm (arguments of the function) 
includes the size of the population and the maximum number of generations. The expected output of the algorithm is
the fitness of the best individual
```
python3 mg.py -o "create a genetic algorithm" -f "ga.py" -k "aa-aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa" -in "1.population_size: the size of the population, 2.max_generation: the number of generations the algorithm creates" -out "the fitness of the best individual" -e "1.numpy"
```
Please replace the key *"aa-aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"* with your
own OpenAPI key. The generated code is saved in your current working directory as a file named 
*ga.py*. Sample codes generated by this command can be found in the folder *samples* (*ga_1.py* and 
*ga_2.py*)

The above commands assume that in your current environment, NumPy is installed. 
If not, please use the following command instead:
```
python3 mg.py -o "create a genetic algorithm" -f "ga.py" -k "aa-aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa" -in "1.population_size: the size of the population, 2.max_generation: the number of generations the algorithm creates" -out "the fitness of the best individual"
```

## Example 3: Draw a picture of a cat

<hr/>

# Contributors

Jinglue Xu, Nagar Anthel Venkatesh Suryanarayanan, Ding Xia

If you have any inquiries or want to collaborate with us, please contact us by 
emailing: jingluexu@gmail.com

If you like our project, please star our repository and share it with your friends!