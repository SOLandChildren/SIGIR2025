# Inside Out 2: Make Room for New Emotions & LLM

This repository contains the code files and results of a reproducibility study revisiting the Inside Out framework introduced by [Landoni et al.](https://dl.acm.org/doi/abs/10.1145/3340631.3394847), to be published as a full paper title "Inside Out 2: Make Room for New Emotions & LLM" at [SIGIR 2025](https://sigir2025.dei.unipd.it/). All personal data including queries procured from the user study conducted in the original study as well as IAS responses have been due to ethical considerations.

# Abstract

In an existing study, the InsideOut Framework is used to produce and explore the emotional profiles of search engines (SE) in response to queries formulated by children aged 9 to 11 in the classroom context revealing the emotional diversity of SE responses. Since then, there have been significant technological advances in emotion detection and information access. In this work, we conduct a comprehensive reproducibility study where we probe today’s emotional profile of SE using both a lexicon-based and a language-model based approach tailored to the Italian language, thus addressing an acknowledged limitation of the original study. Additionally, considering the prevalence of agents based on Large Language Models (LLM) as information access systems among children, we extend the analysis to capture the emotional undertones of LLM responses and juxtapose them to those of SE. Our findings emphasize the importance of leveraging the appropriate emotion detection technique to produce and explore emotional profiles and lead us to reflect on the
interplay of emotions on children’s search-as-learning experience.

# Citation
Hrishita Chakrabarti, Diletta Micol Tobia, Monica Landoni, and Maria Soledad Pera. 2025. Inside Out 2: Make Room for New Emotions & LLM: A Re-
producibility Study of the Emotional Side of Search in the Classroom . In *Proceedings of the 48th International ACM SIGIR Conference on Research and Development in Information Retrieval (SIGIR ’25)*. https://doi.org/10.1145/3726302.3730315

# Reproducibility Code

## User Queries
Refer to `Data/queries_example.csv` for an example file for user queries. The csv file contains the following coloumns:

1. QID: The unique query ID
2. Query: The query formulated by the child
3. Prompt Type: The type of prompt (General or Emotionally Charged in this study) given to the child to formulate a query
4. Task Sentiment: The sentiment category assigned to an search task (Positive or Negative, in this study)

## Synthetic Log Generation

### Step 1: Accessing API endpoints
We rely on official API endpoints to elicit responses from Bing, ChatGPT, and Gemma. Each API endpoint requires an access token which is stored in `Code/API_keys.json` at the time of execution. In the JSON file, `bing_api` refers to the access token for Bing Web Search API, `openAI_api` for OpenAI API to generate ChatGPT responses, `huggingface_api` for HuggingFace API to generate Gemma responses. 

Personal access tokens can be generated using the documentations linked below.

1. [Bing Web Search API](https://learn.microsoft.com/en-us/bing/search-apis/bing-web-search/create-bing-search-service-resource)
2. [OpenAI API](https://platform.openai.com/api-keys)
3. [HuggingFace API](https://huggingface.co/docs/hub/en/security-tokens)

**Note: Access tokens are meant to be private and it is strongly advised to remove the access token strings from the JSON file prior to sharing the code base publically to avoid any data leakage issues.**

### Step 2: Generating IAS responses

Assign the name of the file containing the user queries to `query_file_name` in the first code block in `Code/API_calls.ipynb`, and then run all all the code blocks in `Code/API_calls.ipynb` one after the other. It is advised to use a GPU to run the code block for Gemma response generation for time efficiency.

After all code blocks have run successfully, the `Data/` folder should be populated with three CSV files corresponding to the responses elicited from Bing, ChatGPT, and Gemma, respectively.

## Query-wise Emotional Detection

### Step 1: Loading Italian Lexicons and Models
For LexIT approach, the two Italian lexicons are downloaded using the embedded links below and stored in `Data/` folder.

1. [Distributional Polarity Lexicon](http://sag.art.uniroma2.it/demo-software/distributional-polarity-lexicon/): In our study, we use the DPLp-IT lexicon specifically.
2. [Italian EMotive lexicon (ItEM)](https://github.com/Unipisa/ItEM): In our study, we specifically use the pre-compiled lexicon `pre-compiled-lexica/ItEM.FBNEWS15.cos`.

In case of the FEEL-IT approach, the required models are loaded at the time of execution from [Hugging Face](https://huggingface.co/MilaNLProc/feel-it-italian-emotion).

### Step 2: Computing Sentiment and Emotion vectors
Assign the name of the file containing the user queries to `query_file_name` variable in `Code/sentiment_emotion_vectors.ipynb`, and then run all all the code blocks in `Code/sentiment_emotion_vectors.ipynb` from the beginning in order. 

Once all code blocks have run successfully, the query-wise sentiment and emotion vectors for each synthetic log will be stored under the `Results/` folder.

## Emotional Profile Generation
Run all code blocks in `Code/analysis.ipynb` notebook in order to obtain an emotional profile per synthetic log in `Data/` folder, as well as the statistical significance test values for each experiment conducted in the study.

Note that the files in `Data/InsideOutData/` folder are empty dummy files as we are not permitted to share the data from the original study. 


