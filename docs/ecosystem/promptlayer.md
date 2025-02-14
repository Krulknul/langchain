# PromptLayer

This page covers how to use [PromptLayer](https://www.promptlayer.com) within LangChain.
It is broken into two parts: installation and setup, and then references to specific PromptLayer wrappers.

## Installation and Setup

If you want to work with PromptLayer:
- Install the promptlayer python library `pip install promptlayer`
- Create a PromptLayer account
- Create an api token and set it as an environment variable (`PROMPTLAYER_API_KEY`)

## Wrappers

### LLM

There exists an PromptLayer OpenAI LLM wrapper, which you can access with
```python
from langchain.llms import PromptLayerOpenAI
```

To tag your requests, use the argument `pl_tags` when instanializing the LLM
```python
from langchain.llms import PromptLayerOpenAI
llm = PromptLayerOpenAI(pl_tags=["langchain-requests", "chatbot"])
```

To get the PromptLayer request id, use the argument `return_pl_id` when instanializing the LLM
```python
from langchain.llms import PromptLayerOpenAI
llm = PromptLayerOpenAI(return_pl_id=True)
```
This will add the PromptLayer request ID in the `generation_info` field of the `Generation` returned when using `.generate` or `.agenerate`

For example:
```python
llm_results = llm.generate(["hello world"])
for res in llm_results.generations:
    print("pl request id: ", res[0].generation_info["pl_request_id"])
```
You can use the PromptLayer request ID to add a prompt, score, or other metadata to your request. [Read more about it here](https://magniv.notion.site/Track-4deee1b1f7a34c1680d085f82567dab9).

This LLM is identical to the [OpenAI LLM](./openai), except that
- all your requests will be logged to your PromptLayer account
- you can add `pl_tags` when instantializing to tag your requests on PromptLayer
- you can add `return_pl_id` when instantializing to return a PromptLayer request id to use [while tracking requests](https://magniv.notion.site/Track-4deee1b1f7a34c1680d085f82567dab9).


PromptLayer also provides native wrappers for [`PromptLayerChatOpenAI`](../modules/models/chat/examples/promptlayer_chat_openai.ipynb) and `PromptLayerOpenAIChat`
