## **Licensing**

This project uses a split-licensing model. By using this repository, you agree to the terms of both licenses as they apply to their respective components:

#### **1. Project Code & Scripts**
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

* **Applies to:** All `.txt`, `.yaml`, `.yml`, `.md`  files, `docker-compose` examples, Python scripts, and documentation. Essentially everything NOT in the voice folder.
* **License:** **[MIT License](./LICENSE)**. You are free to use, modify, and distribute this code as long as the original copyright notice is included.

#### **2. Voice Models (The "Bonder" Voices)**
[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)

The custom Piper voice models provided in this repo are licensed under **[Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/)** with the following **Additional Terms & Permissions**:

* **Attribution & Rehosting:** You must give credit if you share or adapt these models. **Restriction:** You are not authorized to rehost or reupload these models to any third-party sites (e.g., Hugging Face, CivitAI, Discord). GitHub forks are the sole exception as they automatically include the files.
* **Non-Commercial:** You **MAY NOT** use these voice models for any commercial purposes, paid services, or revenue-generating projects. 
* **Purpose:** These are transformative works created for personal, hobbyist use as a tribute to the character "Bender" and are not intended to replace or infringe upon the professional work of John DiMaggio.
* **The "John DiMaggio" Clause:** If you are John DiMaggio, feel free to do what you want with these files, including selling or relicensing them. 
* **The "Don't Be That Guy" Rule:** If you want to make money off this voice, **pay John**. Commercial use without his direct involvement is strictly prohibited.

---

# Bonder  

A smart ass AI assistant for Home Assistant.  

Futurama is my favourite show. So I made my own Bender, with black jack and hookers.  
Only I forgot the black jack and hookers.  

I started working on this ages ago but gave up on it as the AI available was kind of shit at portraying Bender. Well all that has changed.  

This repo serves as a home for the prompt, voice, scripts, automation, docker compose examples, and WakeWords.  

 **Full disclosure**  
- I did use Gemini 3 Pro to help work out the kinks and get the personality right.  
  - Surly nothing bad can come from using AI to make AI
- Even with it's help this still took me many sleepless nights and the better part of a week to get right.   
  - If there was a vibe when doing this I would say it was anger. The AI would keep forgetting we are making Bender and think it was bender.  
    - It would also tell me to use non existent thing or things that have been depreciated.  
- After I got all the kinks worked out, I had g3p format the prompt in a "efficient for AI" way. That way it uses minimal tokens and has less chance of messing up.  
    - Same for the memory file.  
- I'm currently using the [Google AI Studios Gemini API](https://aistudio.google.com/) for bender.  
  - It is private as it's a business product.  
- I had G3P estimate the cost and it will be way cheaper to run it this way vs fully local. 
  - I have 60 entities exposed and that gets factored into the cost to run.  
- I also used it to help with some parts of the readme.  

------

### Features

- Private by default.  
  - The Gemini API Is private and cheap.  
    - I'm using the "2.5 flash" model for bender
- More secure than your avg compose file as it uses the `no-new-privileges:true` option.
    - Prevents an attacker from being able to get out of a container if they get into it.
- It can insult you and your family.  
- Help control your "smart home".  
- Search the web.   
  - Uses [SearXNG](https://github.com/searxng/searxng) to do the searching.
- Built in fail-safe, "Flexo" to ensure you always have control of your Home.  
  - There's an automation that runs and if the internet goes down, it'll auto swap the default assistant to "flexo" and when it comes back it swaps back to "bender"  
- "flexo" is completely local. he can answer questions, but only what the model was trained on.  
  - Set Home Assistant to handle commands first and if it can't then it'll sends it to flexo.  
    - "Flexo" is using the LLama3.2:1b model.
- Can Be setup fully local which wouldn't require "Flexo"
  - use Gemma4 or 3 as it should handle the prompt in a similar fashion as Gemini.  
- "Memory" he can remember facts about you and your family. This is saved locally.  
  - The "Memory" File goes next to your HA Config.yaml
- You can also hardcode things into the prompt if you want.  
  - I hardcoded our ages/birthdays, some health facts, and some preferences as an example.  
- If done in Docker, you'll have a setup with static IPs Out of the box.  
  - If you use my networking example. Do `docker network ls` to get your networks actual name if you changed it from my example.
- The scripts and the automation are ready to be copied into the UI YAML editor.  
- Uses the H.A. Notify function.
  - The config yaml contains the parts that need to be added to your HA config.   
    - Using this instead of just writing to a text file. HA has a really low limit of 250 characters for that.
- Sound like bender.
  - I have personally created voice files that are licensed differently than the rest of the repo. I paid money to rent a server to do it.  
- Uses [Whisper](https://github.com/tannisroot/wyoming-whisper-cpp-intel-gpu-docker). Docker is a little weird to setup as it must be built. But that's easy. 
  - I included a .env example. The prompt section is for you to put words that are common or the STT mishears. 
- The compose files are more of an example than ready to use files.  
  - You'll have to change the directories for the volumes to your stuff at a minimum.  
  - Networking stuff I left in for those that'd like to have static IP addresses for their containers, it's an example on how that's setup. 
  - Same goes for all the group IDs.  
- Shows how to do networking inside a compose file and how to connect to an "external" network in compose.  


------

### **Voice Previews**

Listen to the different quality levels of the Bonder voice:

| Quality | Preview Player |
| :--- | :--- |
| **High** | <audio controls src="./Voice/Samples/test_bonder_high.wav"></audio> |
| **Medium** | <audio controls src="./Voice/Samples/test_bonder_medium.wav"></audio> |
| **Low** | <audio controls src="./Voice/Samples/test_bonder_low.wav"></audio> |

> If the players do not appear, you can listen to the files directly: 
> [High](./Voice/sample/test_bonder_high.wav) | [Medium](./Voice/sample/test_bonder_medium.wav) | [Low](./Voice/sample/test_bonder_low.wav)

------


### Internet check  

I've included the automation for the internet check. You'll want to use the HA Ping Integration.  
You can use as many as you want, I figured 3 was a good amount to avoid any accidental swaps.  

Example:  

<p align="center"><img width="1120" height="713"  alt="Ping" src="https://github.com/pbanj/bonder/blob/main/Files/ping.png" /></p>  

-------

### Web search  

By default you can't have an assistant control the home and search the web.
  - It's a HA issue. There's a simple workaround that's what's used here.  
The majority of the search engines are disabled.  
  - There was a lot enabled that don't fit the setup.   
I suggest you get a free brave search API key.  
  - should prevent brave from blocking anything.
  
AI handled the settings file.
  - my ass was lazy and didn’t want to change everything manually.  

------

### WakeWords 

I made 2 different ones for OpenWakeWord.  
- I paid for Hey Bendurr and it seems to work the best at detection. 
- I made the Hey bender OpenWW with the colab. but haven't tested it yet.  
  - Train your own for free(needs chromium based browser) [here](https://www.google.com/search?q=https://colab.research.google.com/drive/1q1oe2zOyZp7UsB3jJiQ1IFn8z5YfjwEb). Or [here](https://openwakeword.com/), not free, costs like $4.

#### OpenWakeWord  

 - Hey Benduur  
   - You want to make it so the test voices say the word how it should sound, not how it's spelled.   
 - Hey Bender  


#### MicroWakeWord  

Home assistant refuses to see this so not sure if it works. [Hey Bender](https://github.com/TaterTotterson/microWakeWords/raw/refs/heads/main/microWakeWordsV2/hey_bender.tflite)
The json is next to it if you need it.  

#### Train your own MicroWakeWord


**1. Run the Training Container:**  

**Majority of this section is from the AI with some cleanup by me.**   
**For AMD GPU Users you'll need the [ROCm](https://github.com/ROCm/rocm) drivers installed on your host machine.**

Replace `Bender` with your desired wake word.  

This'll generate:  
- Synthetic training data.   
- Train the model.   
- Output the files to your current directory.


| Category | Samples | Examples |
| :--- | :--- | :--- |
| **Positive** | Target Name | "Bender" |
| **Confusable Negatives** | Phonetic Matches | "Gender", "Render", "Vendor", "Panda", "Defender" |
| **Hard Negatives** | Environmental Noise | Dinner party chatter, TV background, white noise |

For training you'll want to avoid a "lazy" model. Biggest issue is False Positives.   
  - Confusable negatives should prevent that.  


##### **Why this matters:**

- To ensure the wakeword is responsive but doesn't trigger accidentally, we'll use a specific training list. 
    - This differentiates the wakeword from similar-sounding "confusable" words.

- **Confusable Negatives:** prevents the  model becoming "lazy."  
  - It learns that any two-syllable word ending in an "er" sound is a match.   

By adding negatives, you force it to pay attention to the specific sounds. For example, the "B" and "D" sounds in "Bender."


### Training Commands

| Hardware | Acceleration | Docker Flag |
| :--- | :--- | :--- |
| **NVIDIA** | CUDA | `--gpus all` |
| **AMD** | ROCm | `--device=/dev/kfd --device=/dev/dri` |
| **Intel** | XPU | `--device /dev/dri` |
| **Generic** | CPU | *No extra flags required* |

| Hardware | Acceleration | Docker Command |
| :--- | :--- | :--- |
| **NVIDIA** | **CUDA** | `docker run --rm -it --gpus all -v $(pwd)/export:/data ghcr.io/tatertotterson/microwakeword-trainer:latest train_wake_word --samples 20000 Bender` |
| **AMD** | **[ROCm](https://github.com/ROCm/rocm)** | `docker run --rm -it --device=/dev/kfd --device=/dev/dri --group-add video -v $(pwd)/export:/data rocm/tensorflow:latest /bin/bash -c "pip install microwakeword && train_wake_word Bender"` |
| **Intel** | **XPU** | `docker run --rm -it --device /dev/dri -v $(pwd)/export:/data intel/intel-extension-for-tensorflow:xpu /bin/bash -c "pip install microwakeword && train_wake_word Bender"` |
| **Generic** | **CPU** | `docker run --rm -it -v $(pwd)/export:/data ghcr.io/hadlock/microwakeword-trainer:latest -c "Bender"` |

> **Performance Note:** If you have DDR5 RAM (5000MHz+), CPU mode is surprisingly viable if you don't want to mess with GPU drivers, typically a 20k sample training finishes in under 30 minutes.


**2. Open the UI:**  

Navigate to http://localhost:8888.

   - **Record:** Enter "Hey Bender" and record yourself saying it ~10-20 times.

   - **Train:** Click "Train." The container will automatically generate thousands of synthetic variations and mix them with your recordings.

   - **Output:** When finished, it generates both "Bender.tflite" and "Bender.json" (for the ESPHome manifest).

**3. Integration:**
Place the files in your ESPHome folder and reference them in your YAML:  

```
micro_wake_word:
  models:
    - model: "local:Bender.json"
```

------

### Setup Tips

I recommend taking all but the WakeWord out of Home Assistant and move them to docker if using Home Assistant in a VM.  
   - I'm not using The Whisper Add-on but it should work plenty fine if you use that. 
If using Home Assistant OS, you might want to use a separate server as HA-OS lacks drivers for GPUs and whatnot.  
   
Per Geminis own recommendation, Don't use the STT or TTS from the Gemini API as the cost is way higher than running them locally.

In the "Bender" prompt you will need to make some changes for him to work right. It should be pretty obvious what needs to be replaced. I left our sons nickname in as an example of a word that STT has trouble with.   
I also included one of the earlier prompts as it is a much meaner bender. If you prefer that. just note you'll prob have to work out the memory function for it.   

------


### Model Cost Comparison (April 2026)

I had some cost examples made by g3p.

| Provider | Model | Input (per 1M) | Output (per 1M) | Monthly Est.* | Best For |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **[Google](https://aistudio.google.com/)** | **Gemini 2.5 Flash** | $0.30 | $2.50 | **~$0.18** | **Recommended:** Best logic/personality. |
| **[OpenAI](https://openai.com/api/)** | **GPT-5 Mini** | $0.25 | $2.00 | **~$0.15** | **Alternative:** Strong reasoning & reliability. |
| **[Google](https://aistudio.google.com/)** | **Gemini 3.1 Flash-Lite** | $0.25 | $1.50 | **~$0.12** | **Efficiency:** Fast response, lower output cost. |
| **[OpenAI](https://openai.com/api/)** | **GPT-4o Mini** | $0.15 | $0.60 | **~$0.06** | **Budget:** Reliable and extremely cheap. |
| **[Google](https://aistudio.google.com/)** | **Gemini 2.5 Flash-Lite** | $0.10 | $0.40 | **~$0.04** | **Ultra-Budget:** Lowest possible cost. |


### Price Notes  

 **Estimated monthly cost** is based on a setup with **100 Entities** and **20 voice interactions/searches per day**.   
(~150,000 total tokens per month).   

#### Free Tiers:  
   - **Google:** Most users will pro stay within the Google AI Studio free limits (up to 1,500 requests/day), resulting in an actual cost of **$0.00**.  
   ***>>> THIS IS NOT PRIVATE LIKE PAID IS. <<<***
   - **OpenAI:** Doesn't typically offer a permanent free API tier; usage is "pay-as-you-go" from your credit balance, **your balance expires**. I'd personally avoid OpenAI.


### Privacy & Data Safety


**The Gemini "Privacy Gap"**
 By default, if you use the **Free Tier** of Google AI Studio, your prompts and home data are **NOT PRIVATE**—Google uses them to train and improve their models. 
 
 **To ensure 100% Privacy:**  
 1. Link a billing account to your [Google AI Studio](https://aistudio.google.com/) project. 
 2. Even if you stay under the free usage limits, being on a **Paid/Pay-as-you-go** tier legally changes your data status. 
 3. Under the Paid terms, Google is **prohibited** from using your inputs or outputs to train their models. For a smart home assistant with access to your entities, this is a mandatory step.

---
