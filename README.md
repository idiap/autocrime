**The source code of `autocrime` will be released soon. This is a draft of the README file.**


![](pictures/logo.png)

Welcome to `autocrime`, a tool for researchers and Law Enforcement Agencies (LEAs) to process intercepted conversations in ongoing investigations.  The tool expects audio files and an input, and will produce a JSON file as an output (compatible with most our your visualization tools). A graphical user interface is also included, hereon referred to as the **frontend**. The technologies themseleves are pacakged together independent of the frontend, henceforth referred to as the **backend**.

> Current release: **1.4.0**

# 1. Supported Technologies
- A summary of the integrated technologies to-date is presented in this table:


### 1.1 Speech/Audio Processing

| Technology                                       | Partner(s) | Method                              | Performance (Other datasets) | Performance ( ROXSD ) |
|:-------------------------------------------------|:-----------|:------------------------------------|:-----------------------------|:-----------------------|
| Closed set Speaker ID                                       | BUT & Phonexia      | ResNet architecture |99.95% speaker accuracy (subset of ROXSD) | 96.49% accuracy (plda), 96.92% accuracy (cosine)|
| Open set Speaker ID                              | BUT               | Same as SID         |90% accuracy (subset of ROXSD)                    |  93.43% (with ROXSD threshold 30) |
| Gender ID                                        | Idiap      | x-vector based                           | 90% accuracy (subset of ROXSD)| 75.08% accuracy |
| ASR (English)       | Idiap      | XLSR-LFMMI + 4gram LM               | 23% WER on SLURP              | 28.4% WER |
| ASR (German)       | Idiap      | XLSR-LFMMI + 4gram LM               | 11.1% on TUDA-v4              | 35.9% WER |
| ASR (Greek)       | Idiap      | XLSR-LFMMI + 4gram LM               | 12.72% WER TED talk Greek             | - |
| ASR (Spanish)       | Idiap      | XLSR-LFMMI + 4gram LM               | 7.8% on Voxpopuli              |-|
| ASR (Arabic)       | Idiap      | XLSR-LFMMI + 4gram LM               | 14.9% WER on GALE arabic              |-|
| ASR (Dutch)       | Idiap      | XLSR-LFMMI + 4gram LM               | 5.9% WER CGN              |-|
| ASR (Lithuanian)      | Idiap      | XLSR-LFMMI + 4gram LM               | 20.0% WER on MATERIAL (CS,NTB)              |-|
| Word boosting (English) | Idiap | Lattice Rescoring | - | 28.46% WER [impact of boosted ASR is seen on NER and Mention network] |
| Word boosting (German) | Idiap | Lattice Rescoring | - |  35.95% WER [impact of boosted ASR is seen on NER and Mention network] |
| Speaker Diarization                              | BUT & Phonexia | Energy-based VAD + VBx              | DER 5.91%  on CALLHOME | 14.8%  DER |

### 1.2 Natural Language Processing

| Technology                                       | Partner(s) | Method                              | Performance (Other datasets) | Performance ( ROXSD) |
|:-------------------------------------------------|:-----------|:------------------------------------|:-----------------------------|:-----------------------|
| Topic Detection (English)     | Idiap      | Cross-Encoder (distilroberta)            | 76.72% accuracy(ground-truth), 75% accuracy (subset of ROXSD) (ASR) | 28.66% (ground-truth), 21.34% (ASR) accuracy  |
| NER (English)| USAAR | RoBERTa-large | 79% F1-Score (subset of ROXSD) | 82.8% F1 (ground-truth), 39.7% F1 (ASR), 43.24% F1 (Boosted ASR)|
| NER (German) | USAAR | RoBERTa-large | - | 70.1% F1 (ground-truth), 27.9% F1 (ASR), 30.57% F1 (Boosted ASR) |
| Mention network    | USAAR      | Custom co-reference analysis module | 82% accuracy | 74.81% accuracy (ground-truth), 71.62% accuracy (ASR), 75.29% accuracy (Boosted ASR) |

### 1.3 Network Analysis

| Technology                                       | Partner(s) | Method                              | Performance (Other datasets) | Performance ( ROXSD) |
|:-------------------------------------------------|:-----------|:------------------------------------|:-----------------------------|:-----------------------|
| Community Detection | LUH (methods) & UCSC (assessments) |   Greedy Modularity | F1-score 75% (subset of ROXSD) for communities based on speaker languages | F1-score 32.8 |
| Social Influence Analysis | LUH (methods) & UCSC (assessments) |  Pagerank | Speaker Accuracy (using Degree Centrality): 93.5% in ROXANNE Speaker Network and 80.2% in Telephone Network (subset of ROXSD) | 95% in ROXANNE network, 79.5% in Telephone Network  |
| Link Prediction | LUH (methods) & UCSC (assessments) |  Jaccard Coefficient | 67.2% accuracy (Top-5) (Burglary dataset) | 58.82% accuracy (Top-5) |
| Outlier Detection | LUH (methods) & UCSC (assessments) |  Pagerank & Threshold=0.3 | - | 100% accuracy with Threshold less than or equal 0.3 |
| Cross-Network Node Matching | LUH (methods) & UCSC (assessments) | Node2Vec and DeepLink    | - | Node Matching: <br/> top-1 accuracy: 75% <br/> on ROXSD with 60% nodes as training data |

### 1.4 Visual Analytics

| Technology                                       | Partner(s) | Method                              | Performance (Other datasets) | Performance ( ROXSD) |
|:-------------------------------------------------|:-----------|:------------------------------------|:-----------------------------|:-----------------------|
| Face detection and similarity match | AIRBUS | RetinaFace + ArcFace | 98.06% on MegaFace, 99.8% on LFW | 98% recall and 100% precision on ROXSD-videos |
| Scene characterization and similarity match | AIRBUS | ResNet + ArcFace | N/A | 70% recall and  86% precision on ROXSD-videos |


# 2. Supported Languages

The list of current supported languages is presented below:

| Language | ASR | NER | Topic |
| --- | --- | --- | --- |
| English | ðŸŸ¢ | ðŸŸ¢ | ðŸŸ¢ |
| German | ðŸŸ¢ | ðŸŸ¢ | ðŸ”´ |
| Arabic | ðŸŸ¢ | ðŸ”´ | ðŸ”´ |
| Spanish | ðŸŸ¢ | ðŸ”´ | ðŸ”´ |
| Greek | ðŸŸ¢ | ðŸ”´ | ðŸ”´ |
| Dutch | ðŸŸ¢ | ðŸ”´ | ðŸ”´ |
| Lithuanian | ðŸŸ¢ | ðŸ”´ | ðŸ”´ |


# 3. Get the code

Clone the project directly in command line, type this in your terminal:

```
GIT_LFS_SKIP_SMUDGE=1 git clone https://github.com/idiap/autocrime.git
cd autocrime && git lfs pull
```

``GIT_LFS_SKIP_SMUDGE=1`` will make sure that you clone only the repository and not the ASR models. This will reduce the size of the repository being pulled, otherwise you may face network-related issues.
The next step (``git lfs pull``) will now download all ASR models.

You usually want to run this command in your root or home folder. This will ask you for your credentials for this specific Gitlab folder. This has the big advantage of being connected to the source code, meaning that you can easily install updates via a simple `git pull`. 


# 4. Installing the platform

The autocrime platform can be installed using two environments: (1) conda and (2) docker.

(1) Conda based installation is recommended for Linux and MacOS users. Please refer to the [section 4.1](#installation-using-conda-environment).

(2) Docker based installation is recommended for Windows users. To use a pre-built docker image refer to [README_docker](./README_docker.md)

The summary highlights the diverse installation environments across various operating systems:

| Installation Environment | Linux | MacOS | Windows |
|--------------------------|-------|-------|---------|
| Conda                    | Y     | Y     | N       |
| Docker                   | N     | N     | Y       |

Conda is optimal for Linux and MacOS, while Docker emerges as the preferred choice for Windows.

## [4.1 Installation of Autocrime using Conda Environment](#installation-using-conda-environment)

## 4.1.0 Pre-Requisites

- (1) Operating System: (a) Linux Ubuntu (tested on Ubuntu 18.04 LTS) and (b) macOS
- (2) Environment: conda needs to be installed. Refer to it's installation for [Linux](https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html) and [MacOS](https://docs.conda.io/projects/conda/en/latest/user-guide/install/macos.html). For M1 machines install miniforge3 using ```brew install miniforge``` and then run ```conda init zsh```
- (3) Memory Requirements: 16Gb of RAM and 60Gb of disk space
- (4) Python Version > 3.7
- (5) sox (SOund eXchange package): refer to it's installation for [Linux](https://ziangzhou.com/blog/Install-Sox-Locally/) and MacOS (```brew install sox```)

## 4.1.1 Installation Stages

There are two stages of installing the autocrime platform: (1) backend (section [4.1.2]((#install_of_backend))) and (2) front-end (section [4.1.3]((#install_of_frontend))).

The installation environments used for both backend and frontend setups is shown below:


| Installation Environment | Backend | Frontend |
|--------------------------|---------|----------|
| Conda                    | Y       | N        |
| Docker                   | Y       | Y        |

(1) Conda: This option indicates whether the Conda environment is utilized for installation. It is marked with "Y" for backend installations, indicating its usage, while it's marked "N" for frontend installations, denoting its absence.

(2) Docker: Indicates the usage of Docker for both backend and frontend installations, marked with "Y" for presence and "N" for absence.


## [4.1.2  Installation of Backend](#install_of_backend)


There are two ways to install the backend from the code

1. Build a docker image and follow the instructions described in [section A](#install_backend_docker)
2. Create your conda environment and follow for Linux users ([section B](#install_backend_conda_linux)) and MacOS users ([section C](#install_backend_conda_MacOS))

## [A. Installation of backend using Docker](#install_backend_docker)

To create the docker image simply run

```
docker build --platform=linux/amd64 -t autocrime:latest .
```

The ``--platform=linux/amd64`` is required because the requirements.txt file is tested to work on x86_64 Ubuntu and Debian machines.



## [B. Installation of backend using Conda (for Linux users)](#install_backend_conda_linux)


It is advised to create a virtual environment on your machine before installing the requirements. If you don't wish to follow this step, you need at least to make sure to use Python 3.7 on your machine (check that with the command `python --version`).

You can use `conda`, the package manager installed at the previous step (or `virtualenv` if you prefer). Type the following commands in your terminal to use `conda`. For Linux and Mac Intel architecture run:

```bash
# This is a command for Linux and Mac Intel users ONLY
(# Possible necessary step to avoid issue with disk space during next step:
export TMPDIR=/home/user/temp/
[ ! -d $TMPDIR ] && mkdir -p $TMPDIR
export TEMP=$TMPDIR
export TMP=$TMPDIR
)
conda env create -f environment.yml

conda activate autocrime
# some instructions to install ASR and Video
AUTOCRIME_DIR=$PWD bash utils/install_w2v.sh && \
    pip install --upgrade numpy==1.20.0 pandas==1.2.1 \
    pip install scikit-image==0.19.3 opencv-python==4.7.0.72 torchvision==0.8.2
git lfs install
git lfs pull
``` 

## [C. Installation of backend using Conda (for MacOS users)](#install_backend_conda_MacOS)

For Mac M1 users, run

```bash
CONDA_SUBDIR=osx-64 conda create -n autocrime python=3.7
conda activate autocrime
conda env config vars set CONDA_SUBDIR=osx-64
conda deactivate
# IMPORTANT!!! Create new tab
conda activate autocrime
pip install -r requirements_mac_m1.txt
conda install -c conda-forge mkl kaldi
pip install --upgrade hydra-core==1.2.0
export PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION=python
pip install --upgrade protobuf==4.21.6
pip install --upgrade numpy=1.20.0
pip install --upgrade pandas==1.2.1
pip install --upgrade hydra-core==1.2.0
pip install --upgrade transformers==4.17.0
pip install xlsxwriter # required for export to i2 tool
# for whatever reason! see https://github.com/aws/aws-cli/issues/7325
pip3 uninstall pyOpenSSL
```



## [4.1.3 Installation or Visualization of Front-end](#install_of_frontend)

The docker image used for front-end is ```andreasalexop/roxanne_new:fvt2022v17```

The front-end provides a graphical user interface to the user. To start it, follow these steps

1. Make sure the paths in ``docker-compose.yml`` are valid. On Ubuntu machines, these can be automatically fixed with the following script

```
python utils/fix_fvt_paths.py
```

2. Start the front-end:

```
docker compose up
```
The expected front end outcome is shown below:
 
![](pictures/frontend_initial_page.png)


# 5. Visualizing precomputed ROXSD results

The processing of ROXSD dataset on autocrime platform backend takes approximately 3 hours. In order to visualize ROXSD outcomes without running a case, you can do the following:

1. Download the ROXSD package:

    cd autocrime/ & bash utils/data/download_roxsdv3_dataset.sh

    Here is the folder structure downloaded from ROXSD package:
    ```
        data/
        â”œâ”€â”€ roxsdv3
        â”‚Â Â  â”œâ”€â”€ calls
        â”‚Â Â  â”œâ”€â”€ CSV
        â”‚Â Â  â”œâ”€â”€ diarization
        â”‚Â Â  â”‚Â Â  â””â”€â”€ refs
        â”‚Â Â  â”œâ”€â”€ kaldi_english
        â”‚Â Â  â”œâ”€â”€ kaldi_german
        â”‚Â Â  â”œâ”€â”€ manual_transcripts
        â”‚Â Â  â”œâ”€â”€ nlp_annotations
        â”‚Â Â  â”œâ”€â”€ nlp_annotations_german
        â”‚Â Â  â””â”€â”€ output
        â””â”€â”€ roxsdv3-videos-eval
            â”œâ”€â”€ enrolled_images
            â”œâ”€â”€ images
            â””â”€â”€ output
      ```
    
2. Ensure that the result.json file already exists inside autocrime/data/roxsdv3/output directory.
3. RUN the following commands to visualize the autocrime platform:

    To run the front-end and display the platform follow the following steps:
    ```
    (1) Open the terminal
    (2) cd Desktop/autocrime
    (3) RUN 
        ```docker compose up -d``` 
        Optionally the user can visualize the logs using
        ```docker compose logs -f``` 
    (4) To stop running the front-end run the following command in the same terminal:
        ```docker compose down```
    ```

Expected outcomes from the platform is shown below:
 
![](pictures/frontend_network.png)


# 6. Running a case

## 6.1 RUN the ROXSD setup

The ROXSD case folder is in ``data/roxsdv3``. To download the data run **from the root of the autocrime folder** (NOTE: this will download the data from Switchdrive)

```bash
cd autocrime/
bash utils/data/download_roxsdv3_dataset.sh
```

To run the ROXSD case with only the backend:

```bash
python script.py --config-path data/roxsdv3
```

Note: Processing all ROXSD takes up to 7 hours (4 hours for ASR English and German, 3 hours for other technologies) on a machine with Intel i9 processor and 32G RAM.

The platform will generate an output JSON file in ``data/roxsdv3/output/result.json``, that follows a simple format (nodes and links).

The sample output of the ``data/roxsdv3/output/result.json`` is shown below:

```
{
    "communities": [],
    "link_predictions": [],
    "links": [
        {
            "call_id": "RE8ff8ec4c4e445c13a3d3a6258a7f4a61.wav",
            "call_type": "stereo",
            "date": "2019-12-04 00:00:00",
            "id_from": "cs01M_T",
            "id_to": "ru06F_T",
            "language": [
                "Unknown"
            ],
            "name_from": "unknown",
            "name_to": "unknown",
            "ner": [
                "nan"
            ],
            "phone_from": "+420 680 71230",
            "phone_to": "+420 726 14522",
            "topic": {
                "family discussion": 0.6002352237701416
                ...
                ...
            }
        }
    ]
    "social_influence_scores": []
}
```

## 6.2 Running a custom case

1. Create a folder with your case name (e.g. 'mycase') inside the ``data/``.
2. Create the following directories inside the case folder
    - `calls` contains all the wav files. If you input files that are not sampled at 8kHz, they will be re-sampled automatically.
    - (Optional) Similarly, put the images and videos you want to process in the `images` directory (see below for more details on how to process images and videos). You will also need to change the CSV file with a suitable format.
    - `CSV` contains a description of the metadata in a csv format. Refer to ``data/roxsdv3/CSV/data.csv`` for a sample.
3. Create config.yaml inside ``data/your_casename``. The contents in the `config.yaml` and the necessary changes to be done to run a custom case is described below:

    Now, you will choose which technologies to run on your data. All of that is handled directly in the `config.yaml` file. Here, you can choose which technologies to run, with which parameters, and on which data.

    By default, the first few rows should look like this:

    ```yaml
    run:
      dir: "."
      method: "batch"
    data:
      case: "mycase"
      file: "data.csv"
      sep: ','
      start: 0
      num_files_run: 5
    tech:
      speech:
        diarization:
          run: True
          min_speaker: 2
          max_speaker: 5
        verification:
          run: True
          mode: "real-time"
          backend: "cosine"
          threshold: 0.85
    ```

    The first five calls of `mycase` will be processed. If you want to run one technology, simply set it to `True`, and to `False` to disable it. The following technologies are available:

    - speech:
      - vad (Voice Activity Detection)
      - diarization (Speech Diarization)
      - verification (Speaker Verification)
      - lid (Language Identification)
      - asr (Automatic Speech Recognition)
      - gender (Gender Detection)
    - nlp (Natural Language Processing):    
      - topic (Topic Detection)
      - ner (Named Entity Recognition)
      - mention_network (Mention Network)
    - na (Network Analysis):    
      - community
      - centrality
      - link prediction
      - outlier detection


4. Once you decided which mode to run in the `config.yaml` file, then just run `python main.py` in your terminal. 

# 7. Evaluation of Technologies

## 7.1 Speech
<details>
  <summary><b style="font-size:2em;">Closed set Speaker ID</b></summary>

1. We take one embedding for each of the 95 speakers
2. We have 925 embeddings, so we consider 925-95 = 830 embeddings for the evaluation
3. We compare each embedding from the 830 with all the enrolled speakers using the cosine similiraty/PLDA.
4. We assign test recording to the speaker with biggest similarity to our embedding
### Command to RUN:
    python speech/sid/embedding_13speakers.py

### Closed-set speaker ID results:

| Num. enrolled | Distance measure | Accuracy (%) |
| ------------- | ----------------- | ------- |
| 13 | Cosine | 96.9 |
| 13 | PLDA | 96.5 |

By default, the evaluation script uses PLDA. To use cosine scoring change ``distance_metric`` variable to ``cosine``.

</details>

<details>
  <summary><b style="font-size:2em;">Open set Speaker ID</b></summary>

### Command

Run the following command:

```
bash ./speech/scripts/eval_clusters.sh > eval_clusters.sh.log 2>&1
```
### Results

The evaluation result is available in ``eval_clusters.log``. Here is the sample result for 
threshold value of 45

```
Evaluation ROXSD threshold 45
Number of overlapping conversations in the reference and the automatic clustering are 472
Number of reference labels is 50
Number of automatic labels is 60
Hungarian
Hungarian correct: 443
Greedy
Greedy correct: 443
Cluster acc Hung. 443
```

The evaluation metric is how many recordings are assigned to the correct cluster.
In order to do this we need to map the cluster names from the system to the names used in the references.
For example suppose we have the following:

```
          Reference  Automatic
 Call 1 [R1 ,R3]    [A6, A2]
 Call 2 [R1 ,R3]    [A7, A6]
 Call 3 [R2 ,R3]    [A1, A7]
 ```
If we map R1= A6, R3=A7 we get

```
Call 1 [R1 ,R3]    [A6, A2]  1 error
Call 2 [R1 ,R3]    [A7, A6]  2 error
Call 3 [R2 ,R3]    [A1, A7]  1 error
```

 We use the Hungarian algorithm to find the mapping that gives the fewest errors. 


</details>

<details>
  <summary><b style="font-size:2em;">Gender ID</b></summary>

### Command to run

The GID system uses Gaussian Mixture Models (GMM) to classify a given audio as either Male or Female speaker. On ROXSDV3, it has an accuracy of 75.1%. This result can be obtained with the following
command

```bash
 python speech/gender/eval.py data/roxsdv3/CSV/data.csv 
 ```

### Results

75.08% accuracy

</details>

<details>
  <summary><b style="font-size:2em;">ASR</b></summary>

The xlsr ASR can be evaluated on Roxsdv3 as a standalone module by passing the `-scoring` argument.
Make sure that the roxsdv3 dataset has been extracted (see step 1. "Download the datasets" under the Tutorials section). This makes sure
that ``data/roxsdv3/kaldi_english`` and ``data/roxsdv3/kaldi_german`` folders are available. These folders contain 'text' file
required for evaluation.

### Command to run

```
export AUTOCRIME_DIR=/path/to/autocrime
cd speech/asr/xlsr_lfmmi
source path.sh
python scripts/run_xlsr_asr.py -c "roxsdv3" --csv-path data/roxsdv3/CSV/data_ft_scenario.csv -scoring --wav "calls"
```

### Results

```
------------------------------------------------------
The ASR Word Error Rate on roxsdv3 for English is 28.4%
------------------------------------------------------
------------------------------------------------------
The ASR Word Error Rate on roxsdv3 for German is 35.9%
------------------------------------------------------
```

</details>

<details>
  <summary><b style="font-size:2em;">Word boosting</b></summary>

XLSSR-LFMMI engine works in the same was as the Idiap one. Its working directory is ``autocrime/speech/asr/xlsr_lfmmi`` and the main function is ``produce_asr_transcriptions(case_name, data_dir, wav_dir, seg_dir, clean_results, scoring, words_to_boost)`` from ``autocrime/speech/asr/xlsr_lfmmi/scripts/run_xlsr_english_asr.py``.

The XLSR ASR accepts argument `words_to_boost`. It selects monograms existing in lexicon from given list. These monograms are used to boost the ASR outputs, the probability of recognition of these monograms will increase - given monograms, appearing in lexicon will be boosted.

From ROXSDv3, the following monograms are identified as the words to boost (count: 58)
```
['kristyna','marko','gerhard','munich','dorothea','zahra','johan','kuba','petr','adam','michal','oskar','jakub','prague','brno','dave','andi','yesterday','marek','paul','yan','tomorrow','dima','spiros','costas','damir','mael','czechia','zijian','idiap','christiana','graham','saeed','sam','evzen','slava','marionplatz','andreas','michael','tonight','kristi','today','samuel','france','jimmy','ukraine','czech','david','hlavak','max','iran','brauhaus','marienplatz','pat','maniny','skalka','hauptbahnhof','tom']
```

They are automatically split into the words appearing in lexicon (count: 55)
```
['adam','andi','andreas','brauhaus','brno','christiana','costas','czech','czechia','damir','dave','david','dima','dorothea','evzen','france','gerhard','graham','hauptbahnhof','idiap','iran','jakub','jimmy','johan','kristi','kristyna','kuba','mael','marek','marienplatz','marko','max','michael','michal','munich','oskar','pat','paul','petr','prague','saeed','sam','samuel','skalka','slava','spiros','today','tom','tomorrow','tonight','ukraine','yan','yesterday','zahra','zijian']
```

and Out-Of-Vocabulary words (count: 3)
```
['marionplatz','maniny','hlavak']
```

### Command to run word boosting

```
export AUTOCRIME_DIR=/path/to/autocrime
cd speech/asr/xlsr_lfmmi
source path.sh
python scripts/run_xlsr_asr.py -c "roxsdv3" --csv-path data/roxsdv3/CSV/data_ft_scenario.csv --words-to-boost=['kristyna','marko','gerhard','munich','dorothea','zahra','johan','kuba','petr','adam','michal','oskar','jakub','prague','brno','dave','andi','yesterday','marek','paul','yan','tomorrow','dima','spiros','costas','damir','mael','czechia','zijian','idiap','christiana','graham','saeed','sam','evzen','slava','marionplatz','andreas','michael','tonight','kristi','today','samuel','france','jimmy','ukraine','czech','david','hlavak','max','iran','brauhaus','marienplatz','pat','maniny','skalka','hauptbahnhof','tom'] -- scoring --wav "calls"
```

### Results

```
------------------------------------------------------
The ASR Word Error Rate on roxsdv3 for English is 28.4%
------------------------------------------------------
------------------------------------------------------
The ASR Word Error Rate on roxsdv3 for German is 35.9%
------------------------------------------------------
```

Eventhough, the WER on boosted ASR isn't changed significantly, it's impact can be observed when tested on NER and Mention network evaluation.

</details>

<details>
  <summary><b style="font-size:2em;">Speaker Diarization</b></summary>

***NOTE*** *Autocrime* currently supports either **stereo** audio files (with only one speaker in one channel) or **mono** channel audio files *with only two speakers* in the recording.

You do not have to activate speaker diarization manually. Speaker diarization is chosen automatically when using mono files as input data (located in folder "*calls*".
After data processing by Autocrime, the speaker diarization results are in folder **data/YOUR_CASE/calls_mono**, where *YOUR_CASE* represents the name of the folder with your data (e.g. *roxsdv1*).

You can test the speaker diarization by converting stereo to mono. 

### Convert Stereo to Mono

```
bash speech/scripts/stereo2Mono.sh

```

###	Run_diarization

```
python run_SpkDia.py
```
Note: The above function takes up to 3 hours on a machine with Intel i9 processor and 32G RAM.

### Evaluate Diarization Performance

```
pip install -r speech/scripts/dscore/requirements.txt
python speech/scripts/dscore/score.py -r data/roxsdv3/diarization/refs/*.rttm -s data/roxsdv3/intermediate/vad_diar/*.rttm --collar 0.25  --ignore_overlaps
```
	
### Results

14.89 DER

</details>

## 7.2 NLP

<details>
  <summary><b style="font-size:2em;">NER</b></summary>

The NER evaluation scripts and the corresponding readme files can be found at `autocrime/nlp/ner/evaluation`.  The example data for the evaluation can be found at `autocrime/nlp/ner/evaluation/data`.

**NER-English**

### Command to RUN:
    
    python nlp/ner/evaluation/evaluation_lab_yaml_ac.py # for groundtruth
    python -O nlp/ner/evaluation/evaluation_asr_yaml_ac.py # for ASR
In order to run NER on boosted ASR, please make sure to rename asr output directory from 
```autocrime/data/roxsdv3/output/asr/audacity_results_idiap_lattice_rescoring```
to
```autocrime/data/roxsdv3/output/asr/audacity_results_idiap```
and run the following:

    python -O nlp/ner/evaluation/evaluation_asr_yaml_ac.py # for boosted ASR

### Results

On ground truth:

    PERSON precision: 0.926530612244898, recall: 0.9322381930184805, f1: 0.9293756397134084
    tp:454
    fp:36
    fn:33
    LOCATION precision: 0.8252427184466019, recall: 0.85, f1: 0.8374384236453202
    tp:255
    fp:54
    fn:45
    TIME precision: 0.6877323420074349, recall: 0.7535641547861507, f1: 0.7191448007774537
    tp:370
    fp:168
    fn:121
    total_number_of_entities:1278

    Average 
    F1:0.8286529547120608

On ASR:

    PERSON precision: 0.1553133514986376, recall: 0.11704312114989733, f1: 0.13348946135831383
    tp:57
    fp:310
    fn:430
    LOCATION precision: 0.504, recall: 0.42, f1: 0.45818181818181825
    tp:126
    fp:124
    fn:174
    TIME precision: 0.5909090909090909, recall: 0.6089613034623218, f1: 0.5997993981945838
    tp:299
    fp:207
    fn:192
    total_number_of_entities:1278
    Average F1:0.39715689257823866

On Boosted ASR:

    PERSON precision: 0.22392638036809817, recall: 0.18024691358024691, f1: 0.19972640218878246
    tp:73
    fp:253
    fn:332
    LOCATION precision: 0.5235849056603774, recall: 0.4493927125506073, f1: 0.48366013071895425
    tp:111
    fp:101
    fn:136
    TIME precision: 0.6004415011037527, recall: 0.628175519630485, f1: 0.6139954853273137
    tp:272
    fp:181
    fn:161
    total_number_of_entities:1085
    Average F1:0.4324606727450168



**NER-German**

### Command to RUN:
    
    python nlp/ner/evaluation/evaluation_lab_yaml_ac.py --data_dir 'nlp_annotations_german/german_annotations/' --model_id 'de_mbert_asr' # for groundtruth
    python -O nlp/ner/evaluation/evaluation_asr_yaml_ac.py --yaml_input_dir=./data/roxsdv3/nlp_annotations_german/german_annotations --model_id 'de_mbert_asr' # for ASR

### Results

On ground truth:

    PERSON precision: 0.7244094488188977, recall: 0.9787234042553191, f1: 0.832579185520362
    tp:92
    fp:35
    fn:2
    LOCATION precision: 0.6615853658536586, recall: 0.9079497907949791, f1: 0.7654320987654321
    tp:217
    fp:111
    fn:22
    TIME precision: 0.3778337531486146, recall: 0.7731958762886598, f1: 0.5076142131979695
    tp:150
    fp:247
    fn:44
    total_number_of_entities:527
    Average F1:0.7018751658279211


On ASR:

    PERSON precision: 0.1827956989247312, recall: 0.40476190476190477, f1: 0.2518518518518519
    tp:34
    fp:152
    fn:50
    LOCATION precision: 0.30275229357798167, recall: 0.44594594594594594, f1: 0.36065573770491804
    tp:99
    fp:228
    fn:123
    TIME precision: 0.16997167138810199, recall: 0.3333333333333333, f1: 0.225140712945591
    tp:60
    fp:293
    fn:120
    total_number_of_entities:486
    Average F1:0.27921610083412035

On Boosted ASR:

    PERSON precision: 0.22167487684729065, recall: 0.4787234042553192, f1: 0.30303030303030304
    tp:45
    fp:158
    fn:49
    LOCATION precision: 0.2976190476190476, recall: 0.41841004184100417, f1: 0.3478260869565217
    tp:100
    fp:236
    fn:139
    TIME precision: 0.2032520325203252, recall: 0.3865979381443299, f1: 0.2664298401420959
    tp:75
    fp:294
    fn:119
    total_number_of_entities:527
    Average F1:0.30576207670964023




</details>

<details>
  <summary><b style="font-size:2em;">Topic Detection</b></summary>

### Command to RUN

```
python nlp/topic/topic_detection_eval_groundtruth.py ## on ground truth
python nlp/topic/topic_detection_eval_asr.py ## on ASR
```

The script for evaluating the topic detection on manual transcripts can be called from the main autocrime directory with `python nlp/topic/topic_detection_eval_groundtruth.py`. It evalulates the topic detection module on manula transcripts from `roxsdv3` dataset. It can only run if the manual transcipts and the ground truth annotations are present in `roxsdv3` directory (make sure you run `./utils/data/download_roxsdv3_dataset.sh` before). If you wish to run the evaluation on another dataset, call the evaluation script with `--case-name` parameter, i.e., `python nlp/topic/topic_detection_eval_groundtruth.py --case-name <some-case-name>`. Running the script on `roxsdv3` should produce:

```
                     precision    recall  f1-score   support

              Drugs       0.00      0.00      0.00         3
            Meeting       0.38      0.68      0.49        22
              Money       0.00      0.00      0.00         1
  Work Conversation       0.39      0.35      0.37        20
Family Conversation       0.00      0.00      0.00         0
              Other       0.27      0.71      0.39        35

          micro avg       0.29      0.58      0.38        81
          macro avg       0.17      0.29      0.21        81
       weighted avg       0.32      0.58      0.39        81

Topic detection accuracy: 28.66%
```

The script for evaluating the topic detection on ASR outputs can be called from the main autocrime directory with `python nlp/topic/topic_detection_eval_asr.py`. It automatically evaluates the topic detection module on `roxsdv3` data set and the XLSR ASR outputs. It can only run if the ASR outputs and the ground truth annotations are present in the `roxsdv3` directory (make sure you downloaded the dataset as above and that you ran the ASR). If you wish to run the evaluation on another ASR or another case, call the evaluation script with `--asr` and/or `--case-name` parameters, i.e., `python nlp/topic/topic_detection_eval_asr.py --case-name <some-case-name> --asr <some-asr-engine>`. Running the script on `roxsdv3` and the XLSR ASR outputs should produce:

```
                     precision    recall  f1-score   support

              Drugs       0.00      0.00      0.00         3
            Meeting       0.27      0.50      0.35        22
              Money       0.00      0.00      0.00         1
  Work Conversation       0.25      0.20      0.22        20
Family Conversation       0.00      0.00      0.00         0
              Other       0.24      0.57      0.34        35

          micro avg       0.21      0.43      0.29        81
          macro avg       0.13      0.21      0.15        81
       weighted avg       0.24      0.43      0.30        81

Topic detection accuracy: 21.34%
```

</details>

<details>
  <summary><b style="font-size:2em;">Mention network</b></summary>

### Command to RUN mention network on ground truth:

    export CUDA_VISIBLE_DEVICES=-1 #if you want to run specifically on CPU
    python nlp/ner/evaluation/generate_predictions_for_mentionnetwork.py --input_type manual
    python nlp/coref/eval/mention_eval.py --input_type manual

### Results: Mention network on groundtruth


    Mentions in Ground Truth : 289 

    Mentions Predicted by NER model : 290 

    Correct Entity Detections : 270 

    Correctly labelled by mention network : 202 
                
    Acccuracy of Mention Labelling : 0.7481481481481481 

    Total accuracy (NER+Mention Labelling) : 0.698961937716263 


### Command to RUN mention network on ASR:

    python nlp/ner/evaluation/generate_predictions_for_mentionnetwork.py
    python nlp/coref/eval/mention_eval.py --input_type asr

### Results: Mention network on ASR


    Mentions in Ground Truth : 289 

    Mentions Predicted by NER model : 301 

    Correct Entity Detections : 74 

    Correctly labelled by mention network : 53 
                
    Acccuracy of Mention Labelling : 0.7162162162162162 

    Total accuracy (NER+Mention Labelling) : 0.18339100346020762

### Command to RUN mention network on Boosted ASR:

In order to run mention network on boosted ASR, please make sure to rename asr output directory from 
```autocrime/data/roxsdv3/output/asr/audacity_results_idiap_lattice_rescoring```
to
```autocrime/data/roxsdv3/output/asr/audacity_results_idiap```
and run the following:

    python nlp/ner/evaluation/generate_predictions_for_mentionnetwork.py
    python nlp/coref/eval/mention_eval.py --input_type asr

### Results: Mention network on Boosted ASR


    Mentions in Ground Truth : 289 

    Mentions Predicted by NER model : 275 

    Correct Entity Detections : 85 

    Correctly labelled by mention network : 64 
                
    Acccuracy of Mention Labelling : 0.7529411764705882 

    Total accuracy (NER+Mention Labelling) : 0.22145328719723184 



</details>

## 7.3 Network

<details>
  <summary><b style="font-size:2em;">Outlier detection</b></summary>

### Command to RUN:

    python network/scripts/eval_outlier_detection.py

### Results

Recall with different thresholds
0.2
0.3
0.4
0.5
1.0
1.0
1.0
0.935

100% accuracy with Threshold less than or equal 0.3

</details>

<details>
  <summary><b style="font-size:2em;">Social influence analysis</b></summary>

### Command to RUN:

    python network/evaluation/evaluate_social_influence.py

### Results

    Total ratio:  0.9416

95% in ROXANNE network, 79.5% in Telephone Network

</details>

<details>
  <summary><b style="font-size:2em;">Cross network analysis</b></summary>

### Command to RUN:

    python network/scripts/analyzer_cross_network_analysis.py

### Results

    {
      True 10
      [[1.10849529 0.58510244 0.38101688 1.10468963]
      [0.51336956 1.18051359 0.26372698 0.44309771]
      [0.31324339 0.2544679  1.11830861 0.30014914]
      [1.18603316 0.45828819 0.32462722 1.17285882]]
      {'AUC': 0.9166666666666667, 'MRR': 0.875, 'Success_at_k': 1.0}
    }

Node Matching top-1 accuracy: 75% on ROXSDv3 with 60% nodes as training data

</details>

<details>
  <summary><b style="font-size:2em;">Community Detection</b></summary>

The expected README will contain the following information:

### Evaluate Community detection

1. Make sure the CSV in data/roxsdv3/config.yaml is data.csv
2. Create community detection input

  ```
  python network/scripts/data_csv_to_json.py  --config-path=$PWD/data/roxsdv3 +task=community_detection
  ```

3. Run community detection

  ```
  python network/scripts/analyzer_community_detection.py
  ```

4. Evaluate

  ```
  python network/evaluation/evaluate_community_detection.py data/roxsdv3/network_analysis_output/community_detection_results.json
  ```

Expected results

  ```
  Community:  3 Lang:  cs Population:  22 Recall:  0.2727272727272727 Precision:  0.5454545454545454
  Community:  4 Lang:  fa Population:  7 Recall:  0.8571428571428571 Precision:  0.6
  Community:  5 Lang:  de Population:  27 Recall:  0.1111111111111111 Precision:  0.3
  Community:  6 Lang:  el Population:  10 Recall:  0.5 Precision:  0.625
  Community:  7 Lang:  ru Population:  10 Recall:  0.7 Precision:  1.0
  Community:  8 Lang:  fr Population:  5 Recall:  0.6 Precision:  0.5
  Community:  11 Lang:  en Population:  11 Recall:  0.2727272727272727 Precision:  1.0
  Community:  12 Lang:  ar Population:  2 Recall:  1.0 Precision:  1.0
  Macro F1:  0.32748513000613844
  ```

</details>

<details>
  <summary><b style="font-size:2em;">Link Prediction</b></summary>

### Command to RUN:

    bash network/evaluation/evaluation_link_prediction.sh 10


### Results

    Graph named 'ROXSD V3 UCSC - Ground Truth Network' with 114 nodes and 167 edges
    Number of removed links: 17
    Graph named 'ROXSD V3 UCSC - Ground Truth Network' with 114 nodes and 150 edges
    length of candidate_links: 748
    {('vi02M_T', 'vi03F_T'): {'top_5': False, 'top_3': False, 'top_1': False}, ('cs01M_T', 'cs02F_T'): {'top_5': False, 'top_3': False, 'top_1': False}, ('ro04F', 'ro05M'): {'top_5': False, 'top_3': False, 'top_1': False}, ('ru03M_T', 'de02F_T'): {'top_5': False, 'top_3': False, 'top_1': False}, ('de01M_T', 'silent_8'): {'top_5': False, 'top_3': False, 'top_1': False}, ('de03M_T', 'de05F_T'): {'top_5': True, 'top_3': True, 'top_1': True}, ('en03M_NT', 'de10M_NT'): {'top_5': False, 'top_3': False, 'top_1': False}, ('fr01M_NT', 'de11M'): {'top_5': False, 'top_3': False, 'top_1': False}, ('ru06F_T', 'ru08M_NT'): {'top_5': False, 'top_3': False, 'top_1': False}, ('cs07F_T', 'cs13M_NT'): {'top_5': False, 'top_3': False, 'top_1': False}, ('de02F_T', 'en04M_NT'): {'top_5': False, 'top_3': False, 'top_1': False}, ('cs06M_T', 'en13F_NT'): {'top_5': True, 'top_3': True, 'top_1': True}, ('fa03F_NT', 'de19F_NT'): {'top_5': True, 'top_3': True, 'top_1': False}, ('ru01M_T', 'ru10F_NT'): {'top_5': False, 'top_3': False, 'top_1': False}, ('de03M_T', 'fr04M_T'): {'top_5': True, 'top_3': True, 'top_1': True}, ('fr02M_NT', 'en07M_NT'): {'top_5': False, 'top_3': False, 'top_1': False}, ('cs05M_NT', 'de11M'): {'top_5': False, 'top_3': False, 'top_1': False}}
    top_1: 17.6471
    top_3: 23.5294
    top_5: 23.5294
    0.0073 s
    ###################  Iteration 20 complete.###################################  
    ###################  Best Accuracy on top-5 Nodes = ##################################
    52.9412


</details>

## 7.4 Visual Analytics

<details>
  <summary><b style="font-size:2em;">Face detection and Scene characterization</b></summary>

The autocrime platform integrates image processing algorithms to characterize faces and scenes observed in images and videos. 

The face detection and characterization (embedding extraction) algorithms come from the Pytorch implementation of the paper "Additive Angular Margin Loss for Deep Face Recognition" paper (code in https://github.com/foamliu/InsightFace-Pytorch).

Autocrime enables to enroll a limited set of faces of suspects or victims. To enroll a face to a given node:
  - update the global CSV file with one line per image to be enrolled:
    - the AUDIO column shall contain the face picture file name
    - the Enroll_FACE column shall contain the node name in which the picture should be enrolled. If this node does not exist, a new 'speaker' node will be created in the graph 
  - copy the images to be enrolled in the data/enrolled_images folder.
    (note that current Autocrime GUI only supports jpg images. png images are not supported)

Similarly, "scenes" consisting of observations of a location of interest, or object of interest, can also be enrolled to be searched in ingested images or videos. To enroll scenes:
  - update the global CSV file with one line per image to be enrolled: 
    - the AUDIO column shall contain the scene piture file name
    - the Enroll_SCENE column shall contain the node name in which the picture should be enrolled. If this node does not exist, a new 'media' node will be created in the graph. 
  - copy the corresponding images in the data/enrolled_images folder 

  Once some faces and/or scenes are enrolled, they will be searched in all other images or videos ingested in the platform. Images and videos to be ingested in the platform are listed in the global CSV file, with their file name in the AUDIO column. As each enrolled face or scene is linked to a node in the speaker network, each time an enrolled face or scene is detected in a given image or video, this image or video is added to the set of `media` attached to this node. If a same image or video is attached to two or more different nodes, `image` links are created between the corresponding nodes, indicating that these two nodes are related to each other thanks through a given image or video.

  Note that the audio part of each video is also processed with the audio technologies that have been selected in the config.yaml file.

  To reproduce the evaluation assessment on roxsdv3 + selfie videos dataset:
1 - copy the video/data/roxsdv3-videos-eval folder in the data folder to create a new case:
```
cp -r video/data/roxsdv3-videos-eval data
```
2 - download the image and video data. This is already taken care when you run ``utils/data/download_roxsdv3_dataset.sh``. If it has not already been done, please run it once.
This will update the `images` and `enrolled_images` folders with the images and videos to be ingested and the enrolled faces and scenes respectively.

3 - download and copy the roxsdv3 tapped calls in the data/calls directory

```
ln -r -s  data/roxsdv3/calls data/roxsdv3-videos-eval/calls
```

4 - run: 

```
python script.py --config-path=data/roxsdv3-videos-eval
```  
(This should take around 12 hours on cpu)\
  5 - in the video folder: run: 
```
python evalVisual.py --case=roxsdv3-videos-eval --gt=data/gt/roxsdv3_videos_eval_full_gt.csv
``` 
This script parses the result.json and checks for documents automatically associated to nodes based on voice, face or scene matches. Based on the corresponding ground truth, it provides a global recall and precision rate for document associations based on voice, face and scene matches:

```
------------------------------------------
FACES
RECALL          PRECISION
------------------------------------------
98.0% (96/98)   100.0% (96/96)
------------------------------------------
SCENES
RECALL          PRECISION
------------------------------------------
70.0% (105/150) 86.8% (105/121)
------------------------------------------
VOICES (computed on following enrolled voices: ['cs06M_T', 'cs07F_T', 'fr04M_T', 'cs17M_T', 'ro03M', 'el11M', 'de03M_T', 'de02F_T', 'fa03F_NT', 'cs05M_NT', 'cs21M', 'sk01M_NT', 'el10F_T', 'ro04F', 'ro05M'] )
RECALL          PRECISION
------------------------------------------
79.6% (125/157) 100.0% (125/125)
------------------------------------------
```

NOTE THAT FACE SIMILARITY MATCH IS USED TO FOCUS THE ATTENTION OF THE ANALYST ON PICTURES THAT MAY CONTAIN ENROLLED SUSPECT's FACES BUT DOES NOT GUARANTEE THAT THE FACE MATCH IS CORRECT. THIS IS WHY THE LINKS CREATED BY VISUAL ANALYSIS ARE IN 'pending' MODE TO BE CHECKED AND CONFIRMED BY THE ANALYST.
</details>


Questions regarding the installation? Contact me at: srikanth.madikeri@idiap.ch or create an issue on Gitlab.
