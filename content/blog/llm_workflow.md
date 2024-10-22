+++
title = "85% of Cursor AI in a Shell Script and Good Prompting" 
date = "2024-10-22" 
+++
This is an example workflow of how to integrate LLMs into your software dev.  

First script (`prompt.sh`) does one thing: dumps your entire codebase context into a text file. It first appends the file tree while ignoring what you tell it to ignore (node_modules, files not needed contextually, etc), and recursively finds and auto includes what you want to include (e.g. *.ts, *.tsx), and adds any extra files you need (API docs, project plans).

Second (optional) script (`create_file.sh`) takes the LLM output and creates files in the right path. This is based of the fact that you prompted the code generation LLM to prepend files with something like this:
```js
// src/app/project/components/ProjectCompletionScreen.tsx
``` 

Both scripts are available on my github and linked at the end. 

The workflow:
1. Write (use o1-preview to write) a `project_plan.md`[1]. Write any other docs you want it to reference, I wrote a UX design guide with the colors, fonts, and style I wanted to use. Write what you think a junior dev would need to complete the project on their own. 
2. Set up three prompt templates/files:
   - task_giver_prompt: Asks the LLM what to do next (but doesn't write any code, just makes a plan, like what component/file to next create/implement)
   - llm_task_proposal: Where you paste the output from the last guy
   - task_execution:_prompt The prompt for the LLM that does the actual implementation  
3. Run it:
```bash
prompt.sh -i"node_modules" -e"*.ts *.tsx" -f"plan.md,task_giver_prompt"
# This command will make an out.txt with your entire project and all the docs/prompts specified
# Copy out.txt to o1-mini (using xcopy for convience)
# Copy o1's response to llm_task_proposal_prompt

prompt.sh -i"node_modules" -e"*.ts *.tsx" -f"plan.md,task_execution_prompt,llm_task_proposal"
# Copy output to Claude 3.5 Sonnet (using xcopy for convience)
# This time we want to include a different prompt and the output from o1-mini
# Use create_file.sh to make the file for the response quickly. You run create_file.sh, paste the code, and press ctrl_d. It will make the file in the right directory, instead of manually having to create the file and then copy/paste-ing.
```
4. Review the code. Fix any errors. Start a new chat. Repeat/tweak 2-3 until project is done.

You get the improved recall and reasoning of o1 with the code gen ability of claude. If your project gets too big, decouple your code and write better docs to lower context, and lower the scope of your project plan.

You/others can work on it and leave stuff unfinished and the AI will pick it right back up. It is not on the level of doing stuff on its own yet, so you need to still write code and be in charge of it. 

The magic is in crafting the prompts, so look at some of these examples:

**Example Prompts**
-   **Task Giver Prompt**  
    [_View on Github_](https://gist.github.com/Ocean-Moist/87cb55ef5d7664802326f79a400c570d)
    
-   **Task Execution Prompt**  
    [_View on Github_](https://gist.github.com/Ocean-Moist/a0721110b72ad5aee99bab7a10757ff1)
    
-   **Project Plan (`plan.md`)**  
    [_View on Github_](https://gist.github.com/Ocean-Moist/57c8b3d1bc8d6003f7c81c16eda55284)

Scripts as promised:

**Scripts**
-   **prompt.sh**  
    [_View on Github_](https://gist.github.com/Ocean-Moist/dec0fc92723fe9bcfcefc041d233fab6)
    
-   **create_file.sh**  
    [_View on Github_](https://gist.github.com/Ocean-Moist/68ce4ea771314d7d96aba0ed12c68cea)

## notes
[1] Keep project plans clear and scoped. Take the guesswork away from the LLMs. Let them focus on one component at a time.

## P.S.
This is an example. Scripts need work. prompt.sh args are messy and should auto call xcopy. create_file.sh should handle multiple files. The magic is in the prompting--tweak until it flows. I am in the process of making something 10x better email me if interested **rganapav [at] purdue [dot] edu**. 

