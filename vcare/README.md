# About

VCare is a participation entry into the Morgan Stanley ML-For-Good-Hackathon, aiming to mine knowledge from CRISIS survey dataset(s)

# Setup

## Git

Git - https://git-scm.com/download/win
Github Desktop - https://desktop.github.com/

## Python (core)

Python 3.9.7 - https://www.python.org/downloads/release/python-397/

## Environment

Anaconda version - https://repo.anaconda.com/archive/Anaconda3-2021.11-Windows-x86_64.exe (Windows)

Once installed, the environment could be activated by opening the Anaconda Shell using Windows Menu Item - "Anaconda Powershell Prompt"

## IDE

VS Code - version 1.62.3

Extensions
- Jupyter
- Python

## Libraries

Pre-packaged ones already as part of Anaconda 3 

Installing new libraries
- Identified an issue when using the 2021.11 version of Anaconda 3. On using Anaconda Shell to install / update library like 'conda install spacy', it fails at solving environment
- Workaround
    - Using pip for the purpose of installing packages
    - Open the Anaconda Powershell Prompt
    - python -m pip install --upgrade pip
    - python -m pip install --upgrade spacy
    - python -m pip install --upgrade gensim
Installed libraries
- Spacy (https://pypi.org/project/spacy/)
- Fasttext (https://pypi.org/project/fasttext/)

# Project Structure

## Notebooks (notebooks)

Jupyter notebooks for the purpose of data analytics, PoC and interactive development

## Library (lib)

Implementation of the solution as a library / package


