# Crawless IDE

- [Introduction](#introduction)
- [Installation](#installation)
  - [For Mac](#for-mac)
  - [For Windows](#for-windows)
  - [For Linux](#for-linux)
- [Get Started](#get-started)
  - [User Interface](#user-interface)
  - [Views](#views)
    - [Home](#home)
    - [Projects](#projects)
    - [Store](#store)
    - [Documentation](#documentation)
- [Using the IDE](#using-the-ide)
  - [Tasks](#tasks)
  - [Queue](#queue)
  - [State](#state)
  - [Storage](#storage)
  - [Logs](#logs)
  - [Metrics](#metrics)
- [Best Practices](#best-practices)

## Introduction

At its core, Crawless is an integrated development environment (IDE) and a cloud infrastructure for web automation.

It is a desktop application that allows you to build web automation projects and run them locally or distribute them across multiple machines.

Thus, like any other integrated development environment (IDE), Crawless essentially is a text editor with extra features, that serves as an environment to achieve your goals without compromising productivity, by having all necessary tools at hand.

Here are some use cases that Crawless can help you with, but not limited to any:
- **Web Scraping** - Crawless can help you to extract data from websites and save it in a structured format.
- **Web Testing** - Crawless can help you to automate your web testing process.
- **Web Monitoring** - Crawless can help you to monitor websites and notify you when something changes.
- **Web Automation** - Crawless can help you to automate your web tasks.

The following is a comprehensive guide on getting started and becoming proficient with the Crawless IDE.

Let's dive in and see how it works.

## Installation

### For Mac

- Download the latest version of Crawless for Mac from [here]().
- Double-click on the downloaded file and drag `Crawless.app` to the Applications directory.

### For Windows

- Download the Crawless installer for Windows from [here]().
- Double-click on the downloaded file and follow the instructions.

### For Linux

- Download the Crawless installer for Linux from [here]().
- Double-click on the downloaded file and follow the instructions.

## Get Started

Let's get started by opening the Crawless IDE and exploring its user interface.

### User Interface

> The user interface consists of three main areas, the activity bar, the sidebar, and the view container.

![user-interface](assets/user-interface.png)

#### Activity Bar

In the far left side you find the `Activity Bar` which lets you switch between views, set preferences, and `Connect to Edge`.

> Switching to a view in the `Activity Bar` will open the corresponding navigation in the `Side Bar`.

> `Connect to Edge` is a feature that allows you to connect to a Crawless Edge instance, and use it as a remote execution environment for your projects.

#### Side Bar

Next is `Side Bar` which contains a more detailed navigation and actions for the current view.

#### View Container

The `View Container` is where the content of the current view is shown.

Move on to the following chapters to learn more about the content for each view.

### Views

#### Home

> The `Home` view serves as a starting point for your work in Crawless, get quickly to your projects, and find useful links and information.

It contains the following sections:

- **Welcome** - the fastest way to access your recent projects, community, and get help.
- **Edge Statistics** - the summary of your Edge instances computational resources usage.
- **Dashboards** - a compact collection of metrics to monitor all your workflows in a single place.

#### Projects

> The `Projects` view is where you may create, manage, share, run, and monitor your automation.

To learn more about each aspect of a project, please, refer to the [Using the IDE](#using-the-ide) section.

#### Store

> The `Store` is where you may find and install third-party Crawless tools and extensions, but also get ready workflows and tasks to bootstrap your ideas.

#### Documentation

> The `Documentation` view is where one quickly accesses the necessary information on how to operate the Crawless IDE and use the automation API provided by it in your code.

## Using the IDE

> The process of automation within the Crawless begins with the creation of a project and a workflow within it, followed by creation of tasks out of which a workflow consists, and an optional storage instance to store collected or intermediate data.

> Note that you can also import an existing workflow or work on a project that had been shared with you.

### Tasks

> A task, in the context of Crawless, is a piece of code, written in `JavaScript`, following the [Crawless API](https://docs.stage.crawless.com) convention and a set of configurations that instructs the Crawless and its underlying framework on how it should execute a specific set of actions in the same manner as a real user would do.

> A task may be executed in a specific order, and may depend on other tasks or run in a [queue](#queue).

> Tasks may share data between each other using the built-in [state](#state) feature, and store final data in a [storage](#storage).

Begin with creation of a new project, and a workflow within it.

![tasks-1](assets/tasks-1.gif)

Once created, you may add tasks to your workflow, fill in with code, and configure them to your needs.

> You will notice that every workflow comes with a default task called `main` - this is the entry point of your workflow, and the first task to be executed. You may create as many tasks as you wish, organize, and use them in any order you like.

> Also, note that you may configure and run your tasks directly from their own editor view, by clicking on the task, or from the workflow dashboard view, by clicking on the workflow in the sidebar and selecting the task you wish to run.

As a demonstration, we will create a task that collects the current weather in the New York City.

First we will create our `collect` task, which we will include in our `main` task.

![tasks-2](assets/tasks-2.gif)

On the right side of our opened code editor view, you will find the `Browser` and the `Selectors` panes. The `Browser` pane allows us to navigate to the desired destination and visualize the performance of our tasks, and the `Selectors` pane allows us to interactively find and save the necessary elements into variables, so we can reuse them later.

Assuming we want to extract the current weather in New York City from Google, step by step, we will navigate to our desired destination, set up the necessary selectors, and write our code.

We will need to select the search input field, and the search button, so we can type in our query and submit it.

![tasks-3](assets/tasks-3.gif)

Next, we will add the code which will enter our query into the search field and submit it.

![tasks-4](assets/tasks-4.gif)

Once done, let's select the first result from the search results page, in our case the text with the current temperature in New York City, and log it to the console.

![tasks-5](assets/tasks-5.gif)

This is a brief demonstration on how to get started with automation in Crawless, but we are just scratching the surface, follow to the next chapters to learn how to scale to a different level.

### Queue

> The [queue](https://docs.stage.crawless.com/#/app/queue) feature is a way to execute multiple tasks in background and make sure they run repeatedly if the execution failed, thus not blocking the main execution of the program, and can be also used to schedule tasks to run at a specific time or interval.

Following our previous example, we will create a queue to execute multiple `collect` tasks in the background thus fetch weather data for multiple cities.

Let's include the necessary code in our `main` task.

![queue-1](assets/queue-1.gif)

And run the workflow from the workflow dashboard view.

![queue-2](assets/queue-2.gif)

As you can see, the `collect` task is executed multiple times, and the data is logged to the console.

Feel free to tinker on your own, and try to create a queue that will run at a specific time or interval using the [schedule](https://docs.stage.crawless.com/#/app/queue?id=schedule) feature.

### State

> [State](https://docs.stage.crawless.com/#/app/state) instance provides methods to work with key-value data. The data is saved across your workflow, and you may use it to share stuff between tasks.

> Note that the state can be made global therefore shared across any project.

Let's use the state feature to store weather data, collected by our `collect` task, and instead of directly logging it to the console, we will log it from the `main` task.

First send the data to the state from the `collect` task.

![state-1](assets/state-1.png)

Then, retrieve the data from the state in the `main` task, and log it to the console.

![state-2](assets/state-2.png)

### Storage

> A storage is where we optionally store any data collected during the process of our workflow, usually the fruit of our automation, and may be a `SQL` or `NoSQL` database, a file, or a cloud storage.

Following the previous example, we will create a storage, and instead of logging the weather data to the console, we will store it in the storage.

Let's create a simple file storage on our local machine with the `JSON` format.

![storage-1](assets/storage-1.gif)

Next, add the necessary code to our `main` task to save collected weather data into the storage and visualize it.

![storage-2](assets/storage-2.png)

In the `Storage` view, you will find the `Files` pane, which allows you to navigate and manage your storage files and instances.

Crawless supports a variety of storage types, and you may find more information about them in the [documentation](https://docs.stage.crawless.com/#/app/storage).

### Logs

> The [logs](https://docs.stage.crawless.com/#/app/log) feature allows you to debug your code by logging messages to the console, and monitor the activity of your workflows.

There are two ways to monitor your logs, one is by opening the task view and monitoring the logs in the `Logs` pane.

![logs-1](assets/logs-1.png)

And another is by opening the workflow dashboard view and monitoring the logs in the `Logs` pane.

![logs-2](assets/logs-2.png)

### Metrics

> As soon as you created a project, you may wish to monitor the activity of its workflows and the usage of the computational resources for each process, as well as being informed with notifications about the state of your automation.

In Crawless, we offer two ways to monitor your workflows, one is by opening the workflow dashboard view and monitoring the metrics in the `Summary` pane, and another is by creating a dashboard entry on the `Dashboards` view, which allows you to visualize multiple metrics for multiple workflows simultaneously in a single location.

![metrics](assets/metrics.gif)

## Best Practices

- **Organization** - keep your workflows organized by splitting them into smaller tasks, and grouping them into modules.
- **Modularity** - make your tasks reusable by making them independent of each other, and using them in multiple workflows.
- **Optimization** - optimize your tasks by making them run in [queues](https://docs.stage.crawless.com/#/app/queue), use the [state](https://docs.stage.crawless.com/#/app/state) to cache and share data between tasks, and make use of the [storage](https://docs.stage.crawless.com/#/app/storage) to store final data.
- **Documentation** - document your code, so that others may understand it, and you may remember it.
- **Consistency** - be consistent with your code style, and naming conventions, so that you may easily navigate your codebase.
- **Testing** - test your code, so that you may be confident in its correctness, and others may trust it.
- **Debugging** - use the [logs](https://docs.stage.crawless.com/#/app/log) to debug your code, so that you may quickly find and fix issues.
- **Versioning** - version your code, so that you may track its changes, and others may contribute to it.
- **Community** - use store based third party tools and extensions provided by the community and Crawless team, so that you may save time, and others may benefit from your work.
- **Monitor** - take full advantage of the metrics features within the Crawless to monitor your workflows, so that you may be aware of their state, and be notified of any issues.
- **Learn** - always consult the latest [documentation](https://docs.stage.crawless.com) and changelogs, so that you may be aware of the latest features, thus improving your productivity.