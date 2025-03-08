# Hosting Your Markdown File on GitHub Pages Using Pelican

## Purpose
This README provides instructions on how to take your Markdown file (e.g., your resume) and host it on GitHub Pages using Pelican. I've successfully hosted my resume on [my GitHub Page](https://dngminh.github.io/), and you can view the source code at [my GitHub repository](https://github.com/DNgMinh/DNgMinh.github.io).  

*Note: This instruction is for Windows*

## Prerequisites
Before you can host your resume, make sure you have the following resources ready. For Git and Python, follow the installation guides on the official websites.
1. **Git** - A version control system to track your changes and upload to GitHub. [Install Git](https://git-scm.com/downloads/win)
2. **Python** - Pelican is a Python-based static site generator. [Install Python](https://www.python.org/downloads/)
3. **Pelican** - A tool to generate static HTML files from your Markdown resume.  
   To install Pelican, run the following command in your terminal:
    ```bash
    pip install pelican
    ```
4. **ghp-import** - A tool that helps push your generated HTML files to GitHub Pages.  
   To install ghp-import, run the following command in your terminal:
    ```bash
    pip install ghp-import
    ```
5. **GitHub Account** - A platform to host your static website.

## Instructions

### 1. Set Up Your GitHub Repository 
*(Etter’s Principle: Help Others Write (Chapter 2.7). Etter emphasizes the importance of making it easy for others to contribute to documentation. By putting your source code on GitHub, you create a collaborative environment where other people like me can view and contribute to your project)*

- **Create a GitHub Repository**:
    - Go to [GitHub](https://github.com/).
    - Click on **New** to create a repository.
    - Name the repository **your-username.github.io** (replace `your-username` with your actual GitHub username).
    - Set it to **Public** and initialize it with a **README**.
    - Click **Create Repository**.

- **Clone the Repository Locally**:
    Open your terminal, navigate (`cd`) to your desired directory, and clone the repository using the following command:

    ```bash
    git clone https://github.com/your-username/your-username.github.io.git
    ```
    Replace `your-username` with your actual GitHub username.   

### 2. Use `pelican-quickstart` to Create Your Pelican Site
*(Etter’s Principle: Make Static Websites (Chapter 3.4). Etter advocates for static websites because they are fast, secure, and portable. Although you could manually create a simple static website, he recommends using a static site generator like Pelican)*

In your terminal, `cd` to the directory you just cloned from the GitHub repository (referred to as your **_project directory_**), then run the following command:

```bash
pelican-quickstart
```

This will ask you a few questions to set up the project. Here are some important questions:
- **Where do you want to create your new web site? [.]**: Press Enter to use this directory.
- **What will be the title of this web site?**: Enter the title of your site (e.g., “Marvin McLare’s Resume”).
- **Who will be the author of this web site?**: Enter your name.
- **Do you want to specify a URL prefix?**: Choose **No (n)**.
- **Do you want to generate a tasks.py/Makefile to automate generation and publishing?**: Choose **Yes (y)** for convenience.
- **Do you want to upload your website using GitHub Pages?**: Choose **Yes**.
- **Is this your personal page (username.github.io)?**: Choose **Yes**.
- **_For all other questions_**: Press Enter to accept the default answers.

This will create the necessary folder structure and configuration files for your Pelican site. Your project directory should now look like this:

```perl
my_project/
├── content/       # Your source files (Markdown)
├── output/        # Generated static files
├── pelicanconf.py # Pelican settings
└── README.md      # Your project information
# There may be other files, but don't worry about them.
```  

### 3. Your Markdown Resume  
*(Etter’s Principle: Use Lightweight Markup (Chapter 3.1). Etter highlights the superiority of lightweight markup languages like Markdown for documentation, which are easier to write and maintain than XML like HTML)*  

Now, move your `.md` resume file into the `content` folder that was just created by Pelican. For Pelican to process it correctly, add the following metadata at the top of your `.md` file:  

```markdown
Title: Marvin McLare's Resume  
Date: 2025-03-06  
Slug: resume  
Category: pages  
Summary: A professional finance manager.  

<!-- your resume goes here -->
```  

For an example of how to make a nice resume using Markdown, you can check out [my resume in Markdown](https://github.com/DNgMinh/DNgMinh.github.io/blob/main/content/Resum%C3%A9.md?plain=1).  

### 4. Generate Your Static Website with Pelican    

Run the following command in your terminal in your project directory:

```bash
pelican content -o output -s pelicanconf.py
```

This command will process your `.md` file inside the `content/` folder, convert it to HTML, and place the output in the `output/` folder.  

*Note: You should run this command after you make any change to the content folder, the markdown file, the Pelican configuration file, etc... to update your website static files in `output`. Refer to **step 8**.*  

### 5. Preview Locally

To check your site before publishing:

```bash
pelican --listen
```

Open http://localhost:8000 in your browser to view your webpage. Press `Ctrl C` in the terminal to stop hosting locally.

### 6. Deploy to GitHub Pages  

Now that the web page looks good on your local host, it’s time to push it to GitHub Pages.  

It is a good practice to have 2 branches: `main` and `gh-pages` in your website repository. We will push the content of the website (i.e., the `output` folder) to the `gh-pages` branch, while pushing the source code that generates the website (i.e., the Pelican files in your `project directory`) to the `main` branch.

- **Push to main:**  
    First, make a `.gitignore` file in your project directory and write the following lines:  
    ```
    output/
    __pycache__/
    ```  
    This will tell Git not to include the `output` folder (i.e., we only want the source code) and the Python cache files in the `main` branch.  
    In your project directory, run these commands:  
    ```bash
    git add .
    git commit -m "your commit message"
    git push -u origin main
    ```    

- **Push to gh-pages:**  
    ```bash
    ghp-import output -b gh-pages
    git push origin gh-pages --force
    ```
    This will push the `output` folder to the `gh-pages` branch.  

*Note: You should run these commands every time you make changes in the corresponding folder to keep your Github repository up-to-date. Refer to **step 8**.*

### 7. View Your Hosted Resume  
*(Etter’s Principle: Build a Website (Chapter 2.6).
Etter emphasizes that documentation should be hosted on websites rather than distributed as PDFs. Websites are easy to update while PDFs become outdated in users' hard drives. This guide follows that principle by showing you how to host your Markdown file as a static website using GitHub Pages)*  

After you’ve pushed the static files to the `gh-pages` branch, you can view your resume live on GitHub Pages. Go to the following URL in your browser:  

```
https://your-username.github.io/
```  

Before that, you may need to go to the Settings of your GitHub repository, go to "Pages", and under the "Deploy from a branch" option, change the branch from "main" to "gh-pages".  

Your resume should now be visible to the world!

### 8. Update Your Website 
*(Etter’s Principle: Publish Frequently (Chapter 2.8).
Etter emphasizes the importance of frequently updating your documentation to ensure it remains accurate and relevant. This applies to your resume as well - always rebuild and republish after making changes.)*  

Any time you make changes to your website source files, such as editing the Markdown file in the `content` folder or modifying the Pelican configuration, you need to run the following commands to reflect the changes on your hosted website:  

```bash
pelican content -o output -s pelicanconf.py
ghp-import output -b gh-pages
git push origin gh-pages --force
```

If you don't see the changes immediately, press `Ctrl + Shift + R` to perform a hard refresh on the page.  

One fun thing you can do is change the theme of your website. Visit the [Pelican themes repository](https://github.com/getpelican/pelican-themes), download a theme you like, unzip it, and place the theme folder into your project directory. For example, if the theme folder is named `bluegrass`, open `pelicanconf.py` and add this line:

```python
THEME = "bluegrass"
```

Then, run the above three commands to update your GitHub Page, and you'll see your website in a new theme!

Additionally, make sure you update your source code in the `main` branch, too:
```bash
git add .
git commit -m "your commit message"
git push -u origin main
```

## Further Resources/Readings  
1. [Pelican Documentation](https://docs.getpelican.com/en/latest/) – Official Pelican docs.  
2. [GitHub Pages Guide](https://pages.github.com/) – A guide to using GitHub Pages for hosting static websites.  
3. [Markdown Guide](https://www.markdownguide.org/) – A comprehensive Markdown tutorial. 
4. [Technical Writing Fundamentals](https://www.amazon.ca/Modern-Technical-Writing-Introduction-Documentation-ebook/dp/B01A2QL9SS) – Etter's book for learning technical writing.  

## FAQ  

### Why is Markdown better than writing raw HTML?  
Markdown is simpler, more readable, and faster to write compared to raw HTML. It allows for clear, concise formatting without the complexity of HTML tags, making it perfect for writing content like resumes or documentation.  

### I changed the Markdown version of my resume, but why don’t I see the changes when I refresh the website in my browser?  
This is likely because you haven't rebuilt the static site after updating the `.md` file. Run the `pelican content -o output -s pelicanconf.py` command again to regenerate the HTML files, then push them to GitHub Pages with `ghp-import`. For details, refer to **step 8**.  

## Credits  
- Written by Minh Do.  
- Special thanks to Patrick Chauhari for peer reviewing this guide.  
- Pelican theme: [Blue Grasshopper](https://github.com/gregseth/bluegrasshopper-theme/tree/3f40c24001d6e633c9e5fed28c54cda109acc495). 
