# Hosting Your Resume on GitHub Pages Using Pelican

## Purpose
This README provides instructions on how to take your Markdown resume, add the necessary metadata, and host it on GitHub Pages using Pelican. This guide is aimed at Marvin McLaren, the Foomatic finance manager from Assignment 1, who is familiar with Markdown but needs help setting up a static website using Pelican and GitHub Pages.

## Prerequisites
Before you can host your resume, make sure you have the following resources ready:

1. **Git** – A version control system to track your changes and upload to GitHub.
2. **Python** – Pelican is a Python-based static site generator.
3. **Pelican** – A tool to generate static HTML files from your Markdown resume.
4. **GitHub Account** – A platform to host your resume on GitHub Pages.
5. **Basic Command Line Knowledge** – Ability to run commands like `git` and `python` from the terminal.

If you don’t already have these installed, follow these installation guides:
- [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Install Python](https://www.python.org/downloads/)
- [Install Pelican](https://docs.getpelican.com/en/latest/)

## Instructions

### 1. Set Up Your GitHub Repository
**Principle from Etter’s Modern Technical Writing**: **Clarity and Simplicity** – Keep the process straightforward and avoid overwhelming the user with unnecessary details.

- **Create a GitHub Repository**:
    - Go to [GitHub](https://github.com/).
    - Click on **New** to create a repository.
    - Name the repository **your-username.github.io** (replace `your-username` with your actual GitHub username).
    - Set it to **Public** and initialize it with a **README**.
    - Click **Create Repository**.

- **Clone the Repository Locally**:
    Open your terminal and clone the repository using the following command:

    ```bash
    git clone https://github.com/your-username/your-username.github.io.git
    ```

    Replace `your-username` with your actual GitHub username.

### 2. Use `pelican-quickstart` to Create Your Pelican Site
**Principle from Etter’s Modern Technical Writing**: **Efficiency** – Automate the process to minimize errors and simplify setup.

Instead of manually setting up the Pelican configuration and file structure, we can use `pelican-quickstart` to create the necessary files for you:

- In your terminal, navigate to the directory where you want to create the Pelican site and run the following command:

    ```bash
    pelican-quickstart
    ```

- This will ask you a few questions to set up the project. Here are the key options you should choose:
    - **Your name**: Enter your name.
    - **Your site’s title**: Enter the title of your site (e.g., “John Doe’s Resume”).
    - **Where do you want to create your content (path)?**: Just hit **Enter** to accept the default (`./content`).
    - **What will the URL of your site be?**: Set this to `https://your-username.github.io/`.
    - **Do you want to generate a Makefile/Makefile for you?**: Choose **Yes** for convenience.
    - **Do you want to enable Pelican plugins?**: Choose **No** (unless you need plugins).
    - **Do you want to use the default theme?**: Choose **Yes**.

This will create the necessary folder structure and configuration files for your Pelican site.

### 3. Add Metadata to Your Markdown Resume
**Principle from Etter’s Modern Technical Writing**: **Precision** – Provide exactly what needs to be done, including the exact metadata structure to be added.

Now that the site structure is set up, you’ll need to add metadata to your `.md` resume file for Pelican to process it correctly. In the `content` directory, create a Markdown file (e.g., `resume.md`) and add the following metadata at the top:

```markdown
Title: John Doe's Resume
Date: 2025-03-06
Slug: resume
Category: pages
Summary: A professional finance manager with 5+ years of experience.

# John Doe

## Summary
A detail-oriented finance manager with 5+ years of experience in budgeting, forecasting, and financial analysis.

## Skills
- Budgeting & Forecasting
- Financial Modeling
- Data Analysis

## Experience
### Finance Manager | Foomatic
*January 2020 – Present*
- Managed budgets for multiple departments.
- Led financial reporting and analysis for senior management.

## Education
- **Bachelor's Degree in Finance**, Example University
```

Here’s what each field means:
- **Title**: The title of your page.
- **Date**: The date your page was created or last modified.
- **Slug**: The URL path for your page (e.g., `/resume/`).
- **Category**: Assign this as `pages` to ensure it’s treated as a standalone page (not a blog post).
- **Summary**: A brief description of the page (optional, but useful for SEO).

### 4. Generate Your Static Website with Pelican
**Principle from Etter’s Modern Technical Writing**: **Actionable Steps** – Every instruction should lead to a clear and actionable next step.

To generate the static HTML files for your resume, run the following command in your terminal:

```bash
pelican content -o output -s pelicanconf.py
```

This command will process your `.md` file, convert it to HTML, and place the output in the `output/` directory.

### 5. Push Your Resume to GitHub Pages
**Principle from Etter’s Modern Technical Writing**: **Clarity** – Ensure the user knows exactly what to do next.

Since your repository is set up as `your-username.github.io`, you can push directly to the `main` branch of this repository:

- Use the following commands to push the generated files to GitHub Pages:

    ```bash
    ghp-import output -b main
    git push -f origin main
    ```

This will upload the contents of the `output` folder to the `main` branch of your GitHub repository.

### 6. View Your Hosted Resume
After you’ve pushed your changes, you can view your resume live on GitHub Pages. Go to the following URL in your browser:

```
https://your-username.github.io/
```

Your resume should now be visible to the world!

## Further Resources/Readings
1. [Pelican Documentation](https://docs.getpelican.com/en/latest/) – Official Pelican docs.
2. [GitHub Pages Guide](https://pages.github.com/) – A guide to using GitHub Pages for hosting static websites.
3. [Markdown Guide](https://www.markdownguide.org/) – A comprehensive Markdown tutorial.
4. [Technical Writing Fundamentals](https://www.amazon.com/Modern-Technical-Writing-Andrew-Etter/dp/194536701X) – A great resource for learning technical writing.

## FAQ

### Why is Markdown better than writing raw HTML?
Markdown is simpler and more readable compared to raw HTML. It allows for clear, concise formatting without the complexity of HTML tags, making it perfect for writing content like resumes or documentation.

### I changed the Markdown version of my resume, but why don’t I see the changes when I refresh the website in my browser?
This is likely because you haven't rebuilt the static site after updating the `.md` file. Run the `pelican content -o output -s pelicanconf.py` command again to regenerate the HTML files, then push them to GitHub Pages with `ghp-import`.

## Credits
- Written by [Your Name].
- Special thanks to [Group Members] for peer reviewing this guide.
- Pelican theme: [Theme Name or Source].
