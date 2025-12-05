Hi, welcome to our manuscript repository
<h1 align = "center" >
Quantitative Reasoning Evaluation of Large Language Model Performances in Indoor Air Quality Engineering
</h1>
<div align="center" style="font-size: 14px;">
Nhan Dinh Ngo<sup>1,2,*</sup>, Aijia Zhou<sup>2</sup>, Khang Nguyen Duy Lam<sup>1</sup>, Andrew W. Taylor-Robinson<sup>3,4</sup>, Kok-Seng Wong<sup>1,5</sup>, Thanh H. Nguyen<sup>2</sup>
</div>
<br>

<sup>1</sup>VinUni-Illinois Smart Health Center, VinUniversity, Hanoi 100000, Vietnam
<br>
<sup>2</sup>Department of Civil & Environmental Engineering, University of Illinois at Urbana−Champaign, Urbana, IL 61801, United States
<br>
<sup>3</sup>College of Health Sciences, VinUniversity, Hanoi 100000, Vietnam
<br>
<sup>4</sup>Center for Global Health, Perelman School of Medicine, University of Pennsylvania, Philadelphia, PA 19104, USA
<br>
<sup>5</sup>College of Engineering and Computer Science, VinUniversity, Hanoi 100000, Vietnam
<br>
# 1. Introduction
This repository contains source codes and detailed instructions for successfully reproducing our manuscript.
# 2. Requirements for successfully re-implementing our mansucript
- Create an OpenRouter API to access LLMs
  1) Login to OpenRouter: https://openrouter.ai/
  2) Create an API by following these steps: **Settings / API Key / Create API Key**
  3) Note: Some LLMs are **free-of-charge, but some are not**. Therefore, to prevent the sudden interuption during LLM runnig, we encourage to pay for API service.
- Several LLMs take hours to complete generate solution for the entire 480 problems. Therefore, we encourage you to use Pro+ version of Google Colab platform.
- Create a Google Drive folder to store LLMs outputs
- Alternative, other platforms can be used to run LLMs on local machine but this will be memory-consuming.
- Format your quantitative dataset to **.CSV (Please use our dataset template)**.
# 3. Step-by-Step Re-implementation
## 3.1 Obtain OpenRouter LLM addresses from the OpenRouter portal
- Login to OpenRouter: https://openrouter.ai/
- Search for model name. For example, *GPT-4.1, Claude 3.7 Sonnet, Gemini 2.5 Pro, ERNIE-4.5-300B-A47B, Mistral Large 2, Llama 4 Scout, DeepSeek-R1-0528*, and *Grok 3*
- Copy model address. It should be right below the model name. For example, *openai/gpt-4.1*
## 3.2 User Initialization

```python
# USER INPUT
user_output_folder= "[Paste your Google Drive folder for storing LLMs output here" // For example: "/content/drive/MyDrive/LLM_Nhan/GPT-41_Outputs"
user_base_url="https://openrouter.ai/api/v1"
user_api_key="[Paste your OpenRouter API here]"

user_model = "[Paste LLMs OpenRouter address here]". For example, "openai/gpt-4.1"
user_filename_id = "[Name the model here]". For example, "gpt-4.1"
user_max_token = 16384

print("Done")

```
**Notes**:
- user_base_url="https://openrouter.ai/api/v1" might be changed by Openrouter overtime. To get the latest URL. Please refer to "base_url" field from this OpenRouter link: 
  https://openrouter.ai/docs/quickstart#using-the-openrouter-api-directly 
## 3.3 Upload dataset

```python
# Initialize the solver
solver = initialize_solver()

# Load CSV data
df, total_problems = load_data(solver)
```
## 3.4 Run the model
```python
# Run the model
run_model(
    solver,
    df,
    batchsize=5,                  // This is the number of replications, in this study, we set it to 5.
    answermode = "NSD",           // Type "NSD" for NSD prompt; and "IAQ" for IAQ-prompt
    maxproblems = total_problems,
    displays = False,             // "True" if you want model to show solutions within Colab interface; "False" otherwise
    saves = True                  // "True" if you want to save LLMs outputs, "No" otherwise.
)
```
- When the running is done. You will see a message **"Done processing all problems"**
  ```python
  ....
  ....
  Markdown file saved successfully: /content/drive/MyDrive/LLM_Nhan/IAQ_DeepSeek_R1_0528_Outputs/Name: Example 1452-IAQ-deepseek-r1-5.md
  Successfully saved file Name: Example 1452-IAQ-deepseek-r1-5 to folder /content/drive/MyDrive/LLM_Nhan/IAQ_DeepSeek_R1_0528_Outputs
  Done processing all problems
  ```
## 3.5 LLM response visualization
- Download all LLM reponse stored on your Google Drive to local computer.
- Since the reponse format is Markdown. So, you can use any Markdown compiler to read the solution.
- In this study, we used Visual Studio Code and we installed a Markdown extension to view the LLMs responses.
# 5. Troubleshootings
- If a LLM successfully generate a solution for a problem. It will show the below message, for example:
  ```python
  Generating response for Name: Example 1312-NSD-gpt-4.1-5...
  Markdown file saved successfully: /content/drive/MyDrive/LLM_Nhan/GPT-41_Outputs/Name: Example 1312-NSD-gpt-4.1-5.md
  Successfully saved file Name: Example 1312-NSD-gpt-4.1-5 to folder /content/drive/MyDrive/LLM_Nhan/GPT-41_Outputs
  ```
- However, a LLM will sometimes fails to generate solutions. In that bad situation, you will see the message, for example: 
  ```python
  Generating response for Name: Example 1152-IAQ-deepseek-r1-2...
  Failed to generate response for Name: Example 1152-IAQ-deepseek-r1-2
  Generating response for Name: Example 1211-IAQ-deepseek-r1-2...
  ```
- In this case, one thing you should do is that you should note the index of the problem, for example "Example 1152", and re-run it then.
# 6. Conlusions 
- We designed the code using Object Oriented Programming (OPP) methodology. This helps to well organize the code and minimizing the human effort to reproduce our work.
- Therefore, user can look into the coding blocks in source file for reference, but should not change any thing inside those blocks, except for aforementioned blocks here.
