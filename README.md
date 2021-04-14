<p align="center">
  <a href="https://www.gitpod.io">
    <img src="https://raw.githubusercontent.com/gitpod-io/gitpod/master/components/dashboard/src/icons/gitpod.svg" height="200">
    <h1 align="center">Gitpod</h1>
  </a>
  <p align="center">Always ready-to-code.</p>
</p>

[![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-blue?logo=gitpod)](https://gitpod.io/from-referrer/)

---
https://www.gitpod.io/docs/languages-and-frameworks
Table of contents
=================

- [Introduction to Gitpod](#Introduction-to-Gitpod)
- [Getting Started](#Getting-Started)
  - [Example Projects](#Example-Projects)
- [Workspaces](#Workspaces)
  - [Context URLs](#Context-URLs)
  - [Life of a Workspace](#Life-of-a-Workspace)
  - [Collaboration & Sharing](#Collaboration-&-Sharing)
  - [Command Line Interface](#Command-Line-Interface)
 - [Configure Your Project](#Configure-Your-Project)
  - [.gitpod.yml](#.gitpod.yml)
  - [Docker Configuration](#Docker-Configuration)
  - [Start Tasks](#Start-Tasks)
  - [VS Code Extensions](#VS-Code-Extensions)
  - [Exposing Ports](#Exposing-Ports)
  - [Prebuilt Workspaces](#Prebuilt-Workspaces)
  - [Environment Variables](#Environment-Variables)
  - [Workspace Location](#Workspace-Location)
  - [Editor Configuration ](#Editor-Configuration)
- [Integrations](#Integrations)
  - [GitLab Integration](#GitLab-Integration)
  - [GitHub Integration](#GitHub-Integration)
  - [Bitbucket Integration](#Bitbucket-Integration)
  - [Browser Extension](#Browser-Extension)
- [Languages & Frameworks](#Languages-&-Frameworks)
  - [JavaScript](#JavaScript)
  - [Python](#Python)
  - [HTML/CSS](#HTML/CSS)
  - [Java](#Java)
  - [C++](#C++)
  - [Go](#Go)
  - [Bash](#Bash)
  - [Ruby](#Ruby)
  - [PHP](#PHP)
  - [Vue](#Vue)
  - [Svelte](#Svelte)
  - [Scala](#Scala)
  - [Rust](#Rust)
  - [.NET](#.NET)
  - [Dart](#Dart)
  - [Julia](#Julia)
  - [LaTeX](#LaTeX)
  - [R](#R)
  - [Kotlin](#Kotlin)
  - [Pandas](#Pandas)
  - [Deno](#Deno)
- [Gitpod Self-Hosted](#Gitpod-Self-Hosted)
  - [Install on Google Cloud Platform](#Install-on-Google-Cloud-Platform)
  - [Install on Amazon Web Services](#Install-on-Amazon-Web-Services)
  - [Install on self-managed Kubernetes](#Install-on-self-managed-Kubernetes)
  - [Configure Ingress](#Configure-Ingress)
  - [Configure OAuth](#Configure-OAuth)
  - [Configure a Database](#Configure-a-Database)
  - [Configure a Docker Registry](#Configure-a-Docker-Registry)
  - [Configure Storage](#Configure-Storage)
  - [Configure Nodes](#Configure-Nodes)
  - [Configure Workspaces](#Configure-Workspaces)
- [Subscriptions](#Subscriptions)
  - [Professional Open Source](#Professional-Open-Source)
  - [Create a Team](#Create-a-Team)

---

# Introduction to Gitpod

[Gitpod](https://www.gitpod.io/) is an open source platform for automated and ready-to-code development environments that blends into your existing workflow. It enables developers to describe their dev environment as code and start instant and fresh development environments for each new task directly from your browser.

Gitpod does to Dev Environments what Docker did to Servers 🐳
-------------------------------------------------------------

Today we are emotionally attached (for better or worse) to our dev environments, give them names & massage them over time. They are pets - similar to servers before docker took advantage of `namespaces` and `cgroups` in Linux and turned these nice puppies into cattle.

With Gitpod it is the same - we treat dev environments as automated resources you can spin up when you need them and close down (and forget about) when you are done with your task. Dev environments become fully automated and ephemeral. Only then you are always ready-to-code - immediately creative, immediately productive with the click of a button and without any friction.

This is what is at the heart of Gitpod: an open platform that removes all friction of manually setting up and maintaining dev environments allowing yourself and your team to build applications quicker and more collaboratively.

Gitpod Concepts
---------------

Gitpod seamlessly integrates in your workflow and works with all major git hosting platforms including GitHub, GitLab and Bitbucket. It understands the context you are in and adjusts your dev environment accordingly. For example, if you create a Gitpod workspace from a Pull or Merge Request, Gitpod will open a fully-initialized dev environment in code-review mode.

![gitpod-architecture](https://www.gitpod.io/images/docs/gitpod-architecture.png)

At its core Gitpod relies on a client-server architecture where the client can either be:

-   Any device with a browser and internet connection (Gitpod works with Chrome, Firefox, Safari, Edge and other Chromium-based browsers)
-   Your local machine via local VS Code, IntelliJ or simply your shell/terminal where you SSH into your Gitpod workspace (*expected to be released in early Q1/2021*)

Server-side Gitpod is a Kubernetes application that understands the context from GitLab, GitHub and Bitbucket and spins up containerized dev environments. Under the hood is a customizable Linux container, which we call your *workspace*.

### 🗳 Workspace

A workspace comprises your whole development environment and gives you similar capabilities to a Linux machine. Compared to the latter it is however pre-configured and optimized for your individual development workflow. Each workspace includes:

-   Your source code
-   A shell with [root / sudo capabilities](https://www.gitpod.io/blog/root-docker-and-vscode/#root-access)
-   Your IDE of choice* - currently this is [VS Code](https://www.gitpod.io/blog/root-docker-and-vscode/#vs-code) or [Theia](https://theia-ide.org/)
-   Your personal IDE extensions, themes, editor prefs
-   Full [Docker support](https://www.gitpod.io/blog/root-docker-and-vscode/#docker)

**Jetbrain's IDEs, Jupyter Notebook, Jupyter Labs are already available in [private beta](https://www.gitpod.io/contact).*

### 🏗 Dev-environments-as-code

Spinning up dev environments is easily repeatable and reproducible, because Gitpod applies lessons learned from infrastructure-as-code allowing you to automate, version-control and share dev environments across your team. We call this [dev-environments-as-code](https://www.gitpod.io/blog/dev-env-as-code/).

To reap the resulting automation benefits you provide a then versioned configuration file `.gitpod.yml` in the root of your git repository. The `.gitpod.yml` contains everything that describes your dev environment:

-   A Docker image or file as the base to run your workspace in.
-   Commands executed before workspace startup (see [Prebuilds](https://www.gitpod.io/docs#prebuilds)).
-   Commands executed on workspace startup.
-   Ports to expose on dev workspace startup.
-   and [more](https://www.gitpod.io/blog/gitpodify/).

Learn more about how to configure your repository [here](https://www.gitpod.io/docs/configuration/).

### ⚡️ Prebuilds

Gitpod continuously builds *all* your git branches like a CI server. Whenever your code changes (e.g. when new commits are pushed to your repository), Gitpod can prebuild workspaces, i.e. run the `init` commands in your `.gitpod.yml` before you even start a workspace.

Then, when you do create a new workspace on a branch, or Pull/Merge Request, for which a prebuild exists, this workspace will load much faster, because all dependencies will have been already downloaded ahead of time and your code will be already compiled.

Only with [prebuilds enabled](https://www.gitpod.io/docs/prebuilds/#enable-prebuilt-workspaces) your dev environment can turn fully ephemeral.

More on [prebuilds](https://www.gitpod.io/docs/prebuilds/).

----------

With Gitpod you start treating your dev environments as something ephemeral: you start them, you code, you push your code, and you forget about them. For your next task, you'll use a fresh dev environment.

---

# Getting Started

[Gitpod](https://www.gitpod.io/) is an open source platform for automated and ready-to-code development environments that blends into your existing workflow.

> For an overview of Gitpod you should first read [Introduction to Gitpod](https://www.gitpod.io/docs/).

You can start using Gitpod with one or more of the following ways:

-   Use a [Prefixed URL](https://www.gitpod.io/docs/getting-started#prefixed-url)
-   Install [Browser Extension](https://www.gitpod.io/docs/getting-started#browser-extension)
-   Enable [GitLab Integration](https://www.gitpod.io/docs/getting-started#gitlab-integration)
-   Quick start using an [Example Project](https://www.gitpod.io/docs/getting-started#example-project) or [OSS Project](https://www.gitpod.io/docs/getting-started#gitpodified-open-source-project)

[](https://www.gitpod.io/docs/getting-started#prefixed-url)Prefixed URL
-----------------------------------------------------------------------

You can quickly open a new workspace for your project using a context URL like repository, branch, pull request, issue, or file. Just prefix the URL in the address bar of your browser with `gitpod.io/#`.

For example, try opening <https://gitpod.io/#https://gitlab.com/gitpod/spring-petclinic> or <https://gitlab.com/gitpod/spring-petclinic/-/merge_requests/2>.

[Learn more →](https://www.gitpod.io/docs/context-urls/)

[](https://www.gitpod.io/docs/getting-started#browser-extension)Browser Extension
---------------------------------------------------------------------------------

For convenience, we've made a browser extension that works with Google Chrome, Mozilla Firefox, and Safari. The extension adds a Gitpod button on every project and branch across GitLab, GitHub, and Bitbucket so you can easily open a new workspace for any existing project.

[Learn more →](https://www.gitpod.io/docs/browser-extension/)

[](https://www.gitpod.io/docs/getting-started#gitlab-integration)GitLab Integration
-----------------------------------------------------------------------------------

GitLab comes with a native Gitpod which is enabled by default for GitLab.com. To use the GitLab integration, you need to enable it from your [user preferences](https://gitlab.com/-/profile/preferences) at GitLab. Then you can choose to open a Gitpod workspace as an alternative to the GitLab Web IDE directly from GitLab for any existing project.

[Learn more →](https://www.gitpod.io/docs/gitlab-integration/)

[](https://www.gitpod.io/docs/getting-started#example-project)Example Project
-----------------------------------------------------------------------------

Many example projects already have a working Gitpod configuration. We've listed a few of them in [Example Projects](https://www.gitpod.io/docs/examples/) so that you can inspect their configurations and try them out in Gitpod.

For instance, you could try opening [Vuepress](https://gitpod.io/#https://github.com/vuejs/vuepress) or a [Java with Spring Boot](https://gitpod.io/#https://github.com/gitpod-io/spring-petclinic) example.

[](https://www.gitpod.io/docs/getting-started#gitpodified-open-source-projects)Gitpodified Open Source Projects
---------------------------------------------------------------------------------------------------------------

Setting up a local dev environment for a contribution to your favourite OSS project can be daunting. Luckily there are already numerous projects out there that gitpodified their repositories allowing everyone to contribute with a single click. With [contribute.dev](https://contribute.dev/) we even made a website to list them.

See for yourself and try opening some of our favorite OSS projects out there:

-   [freeCodeCamp](https://gitpod.io/#https://github.com/freeCodeCamp/freeCodeCamp)
-   [Prometheus](https://gitpod.io/#https://github.com/prometheus/prometheus)
-   [GitLab](https://gitpod.io/#https://gitlab.com/gitlab-org/gitlab)
-   [Forem](https://gitpod.io/#https://github.com/forem/forem) powering [dev.to](https://dev.to/)
-   [Nushell](https://gitpod.io/#https://github.com/nushell/nushell)

---

# Example Projects

Here are a few example projects that have already been configured for Gitpod.

Take a look at their `.gitpod.yml` file and try them in Gitpod with a single click.

| Language | Project | Try it |
| --- | :-- | --- |
| JavaScript | [SvelteJS template](https://github.com/gitpod-io/sveltejs-template), a project template for [Svelte](https://svelte.dev/) apps | [![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/gitpod-io/sveltejs-template) |
| TypeScript | [Theia](https://github.com/eclipse-theia/theia), a cloud & desktop IDE framework implemented in TypeScript | [![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/eclipse-theia/theia) |
| Python | [Todo List API in Python Flask](https://github.com/breatheco-de/python-flask-api-tutorial), an interactive tutorial about using Python Flask | [![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/breatheco-de/python-flask-api-tutorial) |
| Go | [Prometheus](https://github.com/prometheus/prometheus), a monitoring system and time series database | [![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/prometheus/prometheus) |
| Rust | [Nushell](https://github.com/nushell/nushell), a terminal emulator written in Rust | [![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/nushell/nushell) |
| Java | [Spring PetClinic](https://github.com/gitpod-io/spring-petclinic), a sample web application in Spring in Java | [![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/gitpod-io/spring-petclinic) |
| Ruby | [Ruby on Rails template](https://github.com/gitpod-io/ruby-on-rails) with a PostgreSQL database | [![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/gitpod-io/ruby-on-rails) |
| C# | [C# .NET Core template](https://github.com/gitpod-io/dotnetcore), a simple pipeline example for a .NET Core application | [![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/gitpod-io/dotnetcore) |
| PHP | [Symfony Demo Application](https://github.com/symfony/demo), a reference application for PHP developers | [![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/gitpod-io/symfony-demo) |

You can find more example projects in the [Languages & Frameworks](https://www.gitpod.io/docs/languages-and-frameworks/) pages.

---

# Workspaces

A workspace is what you code in. It consists of the files, configuration and the underlying docker file. Workspaces are created on the fly, driven by convention and configuration.

A Gitpod workspace can be created from any GitLab, GitHub, or Bitbucket project, branch, issue, or pull request.

In Gitpod workspaces usually have a very short life. Gitpod creates one when you need it and forgets about it when you are done. There is no reason to go back and do any maintenance. Because everything is driven by configuration, you can always create a fresh one when you need it.

-   [Context URLs](https://www.gitpod.io/docs/context-urls/)
-   [Life of a Workspace](https://www.gitpod.io/docs/life-of-workspace/)
-   [Shared Workspaces](https://www.gitpod.io/docs/sharing-and-collaboration/)
-   [Command Line Interface](https://www.gitpod.io/docs/command-line-interface/)

---

