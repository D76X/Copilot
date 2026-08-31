# Description 

On this Windows PC I have istalled Genna4 the LLM from Google and I have managed to 
use it locally through Ollama and OpenWeb UI. However, I would like to be able to 
have a way to tell my local Gemma4 that it can go aout to the web and search.
I have found this hard to do, probabily because I do not fully understand the 
steps and the required configurations.

I need some step-by-step instructions on how to get this to work and references
to articles or YouTube videos that illustrate the issue and how to achieve a 
working setup.

You can use all the info already in the @Copilot foilder and all that is relevant 
from the web and also produce a doicument where you summarize the steps that must
be taken to get this to work on this Windows PC.

I do not always use OpenWeb UI, often I prefer to use gemma4 from the Copilot CLI 
that I have learned to start with the commands below.

```
$env:COPILOT_PROVIDER_BASE_URL = "http://localhost:11434/v1"
$env:COPILOT_MODEL = "gemma4:latest"
$env:COPILOT_OFFLINE = "true"
```