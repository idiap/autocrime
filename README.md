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



Questions regarding the installation? Contact me at: srikanth.madikeri@idiap.ch or create an issue on Gitlab.
