# Custom n8n Workflows

<img src="https://img.shields.io/github/repo-size/sapthesh/n8n?style=for-the-badge&logo=github&color=ff69b4&logoColor=white" alt="Repo Size"> <img src="https://img.shields.io/github/last-commit/sapthesh/n8n?style=for-the-badge&logo=github&color=f4d03f&logoColor=white" alt="Last Commit"> 
<a href="https://hits.sh/github.com/sapthesh/n8n/"><img alt="Hits" src="https://hits.sh/github.com/sapthesh/n8n.svg?style=for-the-badge"/></a>
<a href="https://hits.sh/github.com/sapthesh/n8n/"><img alt="Hits" src="https://hits.sh/github.com/sapthesh/n8n.svg?view=today-total&style=for-the-badge&color=fe7d37"/></a>
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](LICENSE)
[![Version](https://img.shields.io/badge/Version-1.0-blue.svg?style=for-the-badge)]()

Welcome to my personal repository of custom n8n workflows. This collection contains automations I've built to streamline various tasks.

## 🚀 About n8n

n8n is an extendable, self-hostable workflow automation tool. It allows you to connect different services (APIs, SaaS products, etc.) and create complex automations using a visual, node-based editor.

## 📂 Available Workflows

This repository is organized by workflow. Each workflow's JSON file can be found in the `workflows/` directory.

*(**Note:** You can update this section as you add more workflows. Here are a few examples of how you could list them.)*

* **Dropbox Workflows (`/workflows/Dropbox`)**
    * **Description:** A collection of workflows related to Dropbox automation.
    * `dropbox-file-upload.json`: A sample workflow that watches a folder and uploads new files to Dropbox.

* **[Workflow Name 2]**
    * **Description:** What does this workflow do?
    * `workflow-file-name.json`: What is this specific file?

* **[Workflow Name 3]**
    * **Description:** What does this workflow do?

## 💡 How to Use These Workflows

You can import any workflow JSON file directly into your n8n instance.

1.  **Download the Workflow:**
    * Navigate to the workflow file you want (e.g., `workflows/Dropbox/workflow-name.json`).
    * Click the "Raw" button (or download the file).
    * Save the file to your local machine as a `.json` file.

2.  **Import to n8n:**
    * Open your n8n canvas.
    * Go to **File** > **Import from File...**
    * Select the `.json` file you just downloaded.

3.  **Configure Credentials:**
    * The workflow will appear on your canvas.
    * You will need to reconnect any nodes (like Dropbox, Google Sheets, etc.) with your own credentials. Click on a node that has a "credential" warning and add your own.

4.  **Activate!**
    * Once your credentials are set, **Save** and **Activate** the workflow.

## 🤝 Contributing

This is a personal collection, but if you find a bug or have a suggestion for improving a workflow, feel free to:
* Open an [Issue](https.github.com/sapthesh/n8n/issues)
* Submit a [Pull Request](https.github.com/sapthesh/n8n/pulls)
