---
title: "Setting up the Command Prompt"
teaching: 5
exercises: 0
questions:
- "How can I visualize Git information at a glance in the command prompt?"
objectives:
- "Improve your command prompt for working with Git"
keypoints:
- "Use available prompt definitions to show repository summary at a glance."
---

When working with the command prompt in Git, it may prove helpful to keep
some information about the repository available at a glance. As Unix shells
allow to modify the prompt, a natural approach is to integrate such information
into the prompt itself.

> ## What would be useful information to integrate into the prompt?
>
> Take a minute to think about which information might be helpful to be shown as part of the prompt.
>
>> ## Some ideas.
>>
>> - **The active branch.** As you can swith between different branches of the same repository, it
>>   can sometimes be confusing to know which branch your working copy currently reflects. Presenting
>>   the branch name as part of the directory name you are currently in may help as a reminder.
>> - **The state of the branch.** An indicator on whether there are modified or uncommitted files in
>>   the repository may help in noticing uncommited changes in the repository.
> {: .solution}
{: .challenge}

## Setting up the query infrastructure

Individual shells have specific ways to define the prompt and the information shown. Select the
appropriate code snippet according to the shell you are running. If you are unsure which shell
you are using, try the following code to identify the shell you are running.

~~~
you@computer:~$ basename $SHELL
bash
~~~
{: .language-bash}

As the idea to augment the command prompt with Git information is not new, the Git repository on
Github (i.e., the repository hosting the source code for Git itself) also provides the shell code
to query different information. You can download it to your home directory with the following commands.

~~~
you@computer:~$ curl https://raw.githubusercontent.com/git/git/refs/heads/master/contrib/completion/git-prompt.sh -o $HOME/.git-prompt.sh
~~~
{: .language-bash}

> ## bash
>
> To use the `git-prompt.sh` in `bash` add the following line to `$HOME/.bashrc`.
> ~~~
> source ~/.git-prompt.sh
> ~~~
> {: .language-bash}
{: .solution}
> ## zsh
> To use the `git-prompt.sh` in `zsh` add the following line to `$HOME/.zshrc`.
> ~~~
> source ~/.git-prompt.sh
> ~~~
> {: .language-bash}
{: .solution}

Some shells, such as fish, xonsh, and others already have support for displaying Git repository information built-in.

Now you have the infrastructure set up to augment the command prompt with desired information about your Git repository.

## Modifying the prompts

With the code to query the information is already available in the shell session,  we still need to use the information in the definition of our prompt.

> ## bash
> Add the following to your `$HOME/.bashrc`.
> ~~~
> PROMPT_COMMAND='__git_ps1 "\u@\h:\w" "\\\$ "'
> ~~~
> will show username, at-sign, host, colon, cwd, then
> various status string, followed by dollar and SP, as
>   your prompt.
> {: .language-bash}
{: .solution}

> ## zsh
> Add the following to your `$HOME/.bashrc`.
> ~~~
> setopt PROMPT_SUBST
> PS1='[%n@%m %c$(__git_ps1 " (%s)")]\$ '
> ~~~
> This will show username, pipe, then various status string, followed by colon, cwd, dollar and SP, as your prompt.
> {: .language-bash}
{: .solution}


{% include links.md %}
