Website Deployment Overview

Welcome to the overview of our website's distribution and deployment process on our server, **coxeter**. This document aims to provide a high-level explanation of how our website is maintained and updated. While technical details are simplified, key concepts are introduced so you can explore them further if you're interested.

## Table of Contents

1. [Introduction](#introduction)
2. [Server Structure](#server-structure)
3. [Content Management with Git and GitHub](#content-management-with-git-and-github)
4. [Building the Website with Jekyll](#building-the-website-with-jekyll)
5. [Automated Deployment Script](#automated-deployment-script)
6. [Scheduled Updates with Cron](#scheduled-updates-with-cron)
7. [Backup and Deployment Process](#backup-and-deployment-process)
8. [Key Concepts to Explore](#key-concepts-to-explore)
9. [Conclusion](#conclusion)

---

## Introduction

Our website is a **static site**, meaning it consists of fixed content—HTML, CSS, JavaScript, and media files—that doesn't change unless updated by us. To efficiently manage, build, and deploy the website, we use a combination of tools and automation scripts on our server, **coxeter**. This ensures that any updates made to the website's content are reflected online promptly and reliably.

---

## Server Structure

On the server **coxeter**, the home directory contains several key folders related to the website:

- **www-backups**: Contains backups of previous versions of the website. Each backup is stored in a folder labeled with the date and time it was created.
- **www-data**: The live version of the website served to visitors.
- **www-log**: Contains logs of the deployment process, useful for monitoring and troubleshooting.
- **www-readme**: This document, providing an overview of the website's deployment process.
- **www-repository**: The local copy of the website's Git repository.
- **www-script**: The automation script that manages building and deploying the website.

Understanding the purpose of each folder helps in managing and maintaining the website effectively.

---

## Content Management with Git and GitHub

We use **Git**, a version control system, to manage changes to the website's content. Git allows multiple contributors to work on the website simultaneously without overwriting each other's changes. All the website's source files are stored in a **Git repository**, which is maintained locally on **coxeter** in the **www-repository** folder.

To host this repository and collaborate more effectively, we use **GitHub**, an online platform for Git repositories. GitHub provides a centralized location where all changes are pushed (uploaded) and where the latest version of the website's source code resides.

**Key Points:**

- **Git**: A system that tracks changes in files and coordinates work among multiple people.
- **GitHub**: A web-based platform for hosting Git repositories and facilitating collaboration.

---

## Building the Website with Jekyll

Our website is built using **Jekyll**, a static site generator. Jekyll takes the content written in simplified formats (like Markdown) and templates, and transforms them into a complete static website.

This allows us to write content without worrying about the underlying HTML structure, making the process more efficient and less error-prone. The building process occurs on **coxeter** using the **www-script**.

**Key Points:**

- **Jekyll**: A tool that converts plain text files into a static website.
- **Static Site Generator**: Software that creates a static website from templates and content files.

---

## Automated Deployment Script

To automate the process of updating the website, we use a custom **script** located in the **www-script** folder on **coxeter**. A script is a set of instructions that tells the computer how to perform a task automatically.

Our script performs the following actions:

1. **Checks for Updates**: It looks for any new changes in the GitHub repository.
2. **Builds the Website**: If changes are found, it uses Jekyll to build the updated website.
3. **Backs Up the Current Site**: Before deploying the new version, it saves a backup of the current website into the **www-backups** folder.
4. **Deploys the New Site**: Copies the newly built website to the **www-data** folder, making it live to visitors.

**Key Points:**

- **Script**: A program or sequence of instructions that automate tasks.
- **Automation**: Using technology to perform tasks without human intervention.

---

## Scheduled Updates with Cron

To ensure the website stays up-to-date without manual checks, we use **cron**, a time-based job scheduler in Unix-like operating systems.

The script runs **every five minutes** using cron on **coxeter**. This means:

- The script automatically checks for updates at regular intervals.
- Any new changes are deployed promptly.
- Human intervention is minimized, reducing the chance of oversight.

**Key Points:**

- **Cron**: A tool that schedules scripts or commands to run automatically at specified times.
- **Scheduled Tasks**: Automated actions that occur at predetermined times.

---

## Backup and Deployment Process

Before deploying the new version of the website, the script performs a **backup** of the current live site. This ensures that we can **restore** the previous version if needed. Backups are stored in the **www-backups** folder on **coxeter**.

The process includes:

1. **Creating a Backup Directory**: A new folder is created in **www-backups**, labeled with the current date and time.
2. **Moving Current Site to Backup**: The existing website files from **www-data** are moved into this backup directory.
3. **Deploying the New Site**: The freshly built website is copied into the **www-data** folder, replacing the old version.

**Key Points:**

- **Backup**: A copy of data saved to prevent loss or to restore previous versions.
- **Deployment**: The process of making the website live and accessible to users.

---

## Key Concepts to Explore

If you're interested in learning more about the tools and concepts mentioned, here are some terms you can search for:

- **Git**: Understand version control and how it manages changes in projects.
- **GitHub**: Explore collaborative development and repository hosting.
- **Jekyll**: Learn how static site generators work and how they simplify website creation.
- **Cron**: Discover how scheduled tasks are set up in Unix-like systems.
- **Automation Scripts**: Delve into how scripts automate repetitive tasks.
- **Static Websites vs. Dynamic Websites**: Understand the differences and use cases for each.
- **Website Deployment**: Learn about various methods to deploy websites to servers.
- **Backup Strategies**: Explore the importance of backups in data management.
- **Server Management**: Gain insight into how servers like **coxeter** are used to host websites.

---

## Conclusion

Our website's distribution relies on a combination of powerful tools and automation to ensure it remains current and reliable. By using Git and GitHub for version control, Jekyll for site generation, and automation scripts scheduled with cron on our server **coxeter**, we maintain an efficient workflow that minimizes manual effort while maximizing uptime and accuracy.

We hope this overview provides a clear understanding of our website deployment process. Feel free to explore the key concepts mentioned to gain a deeper insight into each component.

---

**Last Updated:** 2024-09-24

---

**Note:** This document is stored in the **www-readme** file on the server **coxeter** and is distributed elsewhere for informational purposes.--
