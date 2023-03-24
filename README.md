
<h1 align="center">
  <br>
  <a href="https://github.com/context-labs/autodoc"><img src="https://raw.githubusercontent.com/context-labs/autodoc/master/assets/autodoc.png" alt="Markdownify" width="200" style="border-radius:8px;"></a>
  <br>
Autodoc
  <br>
</h1>

<h4 align="center">⚡ Toolkit for auto-generating codebase documentation using LLMs ⚡</h4>

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) [![Twitter](https://img.shields.io/twitter/url/https/twitter.com/langchainai.svg?style=social&label=Follow%20%40LangChainAI)](https://twitter.com/autodoc_) [![](https://dcbadge.vercel.app/api/server/6adMQxSpJS?compact=true&style=flat)](https://discord.gg/6adMQxSpJS)

<p align="center">
  <a href="https://badge.fury.io/js/electron-markdownify">
	  <img alt="Twitter URL" src="https://img.shields.io/twitter/url?label=Follow%20%40autodoc_&style=social&url=https%3A%2F%2Ftwitter.com%2Fautodoc_">
  </a>
  <a href="https://gitter.im/amitmerchant1990/electron-markdownify"><img src="https://badges.gitter.im/amitmerchant1990/electron-markdownify.svg"></a>
  <a href="https://saythanks.io/to/bullredeyes@gmail.com">
      <img src="https://img.shields.io/badge/SayThanks.io-%E2%98%BC-1EAEDB.svg">
  </a>
  <a href="https://www.paypal.me/AmitMerchant">
    <img src="https://img.shields.io/badge/$-donate-ff69b4.svg?maxAge=2592000&amp;style=flat">
  </a>
</p>

<p align="center">
  <a href="#key-features">What is this?</a> •
  <a href="#how-to-use">Get Started</a> •
  <a href="#download">Community</a> •
  <a href="#download">Contribute</a> •
  <a href="#credits">Credits</a> •
  <a href="#license">License</a>
</p>


## What is this?
Autodoc is a toolkit for for auto-generating codebase documention for git repositories using Large Language Models, like [GPT-4](https://openai.com/research/gpt-4) or [Alpaca](https://github.com/ggerganov/llama.cpp). Autodoc can be [installed](#get-started) in your repo in about 5 minutes. It indexes your codebase through a depth-first traversal of all repository contents to create documentation that describes the different components of your system and how they work together. 

This generated documentation lives in your codebase, and travels where your code travels. Developers who download your code can use the `doc` command to ask questions about your codebase and get highly specific answers with references back to code files. Documentation is re-indexed on `git push`, so it is always up-to-date.


### Examples
Below are a few examples of how Autodoc can be used. 
1. [Autodoc](https://github.com/context-labs/autodoc) - This repository contains documentation for itself, generated by Autodoc. It lives in the `.autodoc` folder. Follow instructions here to learn how to query it.
2. [TolyGPT.com](https://tolygpt.com) - TolyGPT is an Autodoc chatbot trained on the [Solana validator](https://github.com/solana-labs/solana) codebase and deployed to the web for easy access.

## Get Started

Install the Autodoc CLI tool as a global NPM module:

```bash
$ npm install -g @context-labs/autodoc
```
This command installs the Autodoc CLI tool that will allow you to create and query Autodoc indexes. Run `$ doc` to see the available commands.

### Querying
We'll use the Autodoc repository as an example to demonstrate how querying in Autodoc works.

Clone Autodoc and change directory to get started:

```bash 
$ git clone https://github.com/context-labs/autodoc.git
$ cd autodoc
```

Right now Autodoc only supports OpenAI. Make sure you have have your OpenAI API key exported in your current session:

```bash
$ export OPENAI_API_KEY=<YOUR_KEY_HERE>
```

To start the Autodoc query CLI, run:

```bash
$ doc q
```

If this is your first time running `doc q`, you'll get a screen that prompts you to select which GPT models you have access to. Select whichever is appriopriate for your level of access. If you aren't sure, select the first option:

<img src="https://raw.githubusercontent.com/context-labs/autodoc/master/assets/select-models.png" alt="Markdownify" width="60%" style="border-radius:24px;">

You're now ready to query documentation for the Autodoc repository:

<img src="https://raw.githubusercontent.com/context-labs/autodoc/master/assets/output.gif" alt="Markdownify" width="60%" style="border-radius:24px;">

This is the core querying experience. It's very basic right now, with plenty of room of improvement. If you're interested in improving the Autodoc CLI querying experience, checkout this issue :)

### Indexing
Follow the steps below to generate documentation for your own repository using Autodoc.

Change directory into the root of your project:
```bash
cd $PROJECT_ROOT
```
Make sure your OpenAI API key is available in the current session:

```bash
$ export OPENAI_API_KEY=<YOUR_KEY_HERE>
```

Run the `index` command:
```bash
doc index
```
If this is the your first time running `doc index` on this repository, you will be prompted to enter the name of the project and the GitHub url. Enter the both correctly or the next step may not work. 

These values are stored in the root of your repository in a `autodoc.config.json` file. This file should be checked in to git.

You should see a screen like this:

<img src="https://raw.githubusercontent.com/context-labs/autodoc/master/assets/index-estimate.png" alt="Markdownify" width="60%" style="border-radius:24px;">

This screen estimates the cost of indexing your repository. You can also access this screen via the `doc estimate` command.

For every file in your project, Autodoc calculates the number of tokens in the file based on the file content. The more lines of code, the larger the number of tokens. Using this number, it determine which model it will use on per file basis, always choosing the cheapest model whose context length supports the number of tokens in the file. 

**Note:** This naive model selection strategy means that files under ~4000 tokens will be documented using GPT-3.5, which will result in less accurate documenation. Checkout this issue if you're interested in helping make model selection configurable in Autodoc.

For large projects, the cost can be several hundred dollars. View OpenAI pricing [here](https://openai.com/pricing). 

In the near future, we will support self-hosted models, such as [Llama](https://github.com/facebookresearch/llama) and [Alpaca](https://github.com/tatsu-lab/stanford_alpaca). Read this issue if you're interesting in contributing to this work.



## Credits

This software uses the following open source packages:

- [Electron](http://electron.atom.io/)
- [Node.js](https://nodejs.org/)
- [Marked - a markdown parser](https://github.com/chjj/marked)
- [showdown](http://showdownjs.github.io/showdown/)
- [CodeMirror](http://codemirror.net/)
- Emojis are taken from [here](https://github.com/arvida/emoji-cheat-sheet.com)
- [highlight.js](https://highlightjs.org/)

## Related

[markdownify-web](https://github.com/amitmerchant1990/markdownify-web) - Web version of Markdownify

## Support

<a href="https://www.buymeacoffee.com/5Zn8Xh3l9" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/purple_img.png" alt="Buy Me A Coffee" style="height: 41px !important;width: 174px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;" ></a>

<p>Or</p> 

<a href="https://www.patreon.com/amitmerchant">
	<img src="https://c5.patreon.com/external/logo/become_a_patron_button@2x.png" width="160">
</a>

## You may also like...

- [Pomolectron](https://github.com/amitmerchant1990/pomolectron) - A pomodoro app
- [Correo](https://github.com/amitmerchant1990/correo) - A menubar/taskbar Gmail App for Windows and macOS

## License

MIT

---

> [amitmerchant.com](https://www.amitmerchant.com) &nbsp;&middot;&nbsp;
> GitHub [@amitmerchant1990](https://github.com/amitmerchant1990) &nbsp;&middot;&nbsp;
> Twitter [@amit_merchant](https://twitter.com/amit_merchant)






# 🤖📄 Autodoc 



## What is this?
Autodoc is a 

## Quick install 
`npm install -g @context-labs/autodoc`

# 🦜️🔗 LangChain

⚡ Building applications with LLMs through composability ⚡

[![lint](https://github.com/hwchase17/langchain/actions/workflows/lint.yml/badge.svg)](https://github.com/hwchase17/langchain/actions/workflows/lint.yml) [![test](https://github.com/hwchase17/langchain/actions/workflows/test.yml/badge.svg)](https://github.com/hwchase17/langchain/actions/workflows/test.yml) [![linkcheck](https://github.com/hwchase17/langchain/actions/workflows/linkcheck.yml/badge.svg)](https://github.com/hwchase17/langchain/actions/workflows/linkcheck.yml) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) [![Twitter](https://img.shields.io/twitter/url/https/twitter.com/langchainai.svg?style=social&label=Follow%20%40LangChainAI)](https://twitter.com/langchainai) [![](https://dcbadge.vercel.app/api/server/6adMQxSpJS?compact=true&style=flat)](https://discord.gg/6adMQxSpJS)

**Production Support:** As you move your LangChains into production, we'd love to offer more comprehensive support.
Please fill out [this form](https://forms.gle/57d8AmXBYp8PP8tZA) and we'll set up a dedicated support Slack channel.

## Quick Install

`pip install langchain`

## 🤔 What is this?

Large language models (LLMs) are emerging as a transformative technology, enabling
developers to build applications that they previously could not.
But using these LLMs in isolation is often not enough to
create a truly powerful app - the real power comes when you can combine them with other sources of computation or knowledge.

This library is aimed at assisting in the development of those types of applications. Common examples of these types of applications include:

**❓ Question Answering over specific documents**

- [Documentation](https://langchain.readthedocs.io/en/latest/use_cases/question_answering.html)
- End-to-end Example: [Question Answering over Notion Database](https://github.com/hwchase17/notion-qa)

**💬 Chatbots**

- [Documentation](https://langchain.readthedocs.io/en/latest/use_cases/chatbots.html)
- End-to-end Example: [Chat-LangChain](https://github.com/hwchase17/chat-langchain)

**🤖 Agents**

- [Documentation](https://langchain.readthedocs.io/en/latest/use_cases/agents.html)
- End-to-end Example: [GPT+WolframAlpha](https://huggingface.co/spaces/JavaFXpert/Chat-GPT-LangChain)

## 📖 Documentation

Please see [here](https://langchain.readthedocs.io/en/latest/?) for full documentation on:

- Getting started (installation, setting up the environment, simple examples)
- How-To examples (demos, integrations, helper functions)
- Reference (full API docs)
- Resources (high-level explanation of core concepts)

## 🚀 What can this help with?

There are six main areas that LangChain is designed to help with.
These are, in increasing order of complexity:

**📃 LLMs and Prompts:**

This includes prompt management, prompt optimization, generic interface for all LLMs, and common utilities for working with LLMs.

**🔗 Chains:**

Chains go beyond just a single LLM call, and are sequences of calls (whether to an LLM or a different utility). LangChain provides a standard interface for chains, lots of integrations with other tools, and end-to-end chains for common applications.

**📚 Data Augmented Generation:**

Data Augmented Generation involves specific types of chains that first interact with an external datasource to fetch data to use in the generation step. Examples of this include summarization of long pieces of text and question/answering over specific data sources.

**🤖 Agents:**

Agents involve an LLM making decisions about which Actions to take, taking that Action, seeing an Observation, and repeating that until done. LangChain provides a standard interface for agents, a selection of agents to choose from, and examples of end to end agents.

**🧠 Memory:**

Memory is the concept of persisting state between calls of a chain/agent. LangChain provides a standard interface for memory, a collection of memory implementations, and examples of chains/agents that use memory.

**🧐 Evaluation:**

[BETA] Generative models are notoriously hard to evaluate with traditional metrics. One new way of evaluating them is using language models themselves to do the evaluation. LangChain provides some prompts/chains for assisting in this.

For more information on these concepts, please see our [full documentation](https://langchain.readthedocs.io/en/latest/?).

## 💁 Contributing

As an open source project in a rapidly developing field, we are extremely open to contributions, whether it be in the form of a new feature, improved infra, or better documentation.

For detailed information on how to contribute, see [here](.github/CONTRIBUTING.md).
