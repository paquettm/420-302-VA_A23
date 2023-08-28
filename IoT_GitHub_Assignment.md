# Assignment 1: Working with GitHub

## Learning objectives

By the end of this assignment, you will be able to:

- Create a GitHub account and set up your profile
- Create a new repository on GitHub and add some files
- Clone the repository to your local machine using Git
- Modify the code on your local machine and commit the changes
- Push the changes back to GitHub and view them online

## Instructions

### Step 1: Create a GitHub account and set up your profile

- Go to https://github.com/ and click on **Sign up**.
- Enter your email address, create your password, enter your username, answer their questions, and click on **Create account**.
- Verify your email address by entering the code sent to you by email.
- Answer more questions about your use of GitHub and click **Continue for Free**.
- Go to https://github.com/your-username (replace your-username with your actual username) and click **Edit profile** to enter your profile information, such as your name, bio, location, etc. You can also upload a profile picture if you want.

### Step 2: Create a new repository on GitHub and add some files

- Go to https://github.com/your-username (replace your-username with your actual username) and click the **Repositories** tab at the top. Click **New** at the right.

It is now time to enter the repository details: 
- Enter a name for your repository, such as "IoT_Assignment_1". Add a description of your repository, such as "420-302-VA IoT Assignment 1".
- Choose whether you want your repository to be public or private. Public repositories are visible to anyone on the internet, while private repositories are only accessible by you and people you invite. Make your assignments private to prevent plagiarism, but make your cool projects public to share your wizdom. This time, make your repository **private**.
- Check the box next to **Add a README file**. This will create a file named README.md in your repository, which you can use to describe your project and its features.
- Optionally, check the boxes next to **Add .gitignore** and **Choose a license**. These will create files named .gitignore and LICENSE in your repository, which you can use to specify which files should be ignored by Git and what terms apply to your project's usage and distribution.
- Click on **Create repository**.

You have now created your IoT Assignment 1 repository on GitHub. You can view it online by going to https://github.com/your-username/your-repository-name (replace your-username and your-repository-name with your actual values).


To add more files to your repository, you can use the web interface or the command line. For this assignment, we will use the web interface.

- Click on **Add file** and select **Create new file**.
- Enter a name for your file, such as "hello.py".
- In the editor, write some Python code for a simple program, such as:

```python
print("Hello, world!")
```

- Scroll down to the bottom of the page and enter a message describing your changes, such as "Create hello.py".
- Click on **Commit new file**.

You have now added a new file to your repository! You can view it online by going to https://github.com/your-username/your-repository-name/blob/main/hello.py (replace your-username and your-repository-name with your actual values).

You can repeat this process to add more files to your repository.

### Step 3: Clone the repository to your local machine using Git

To work on your code locally, you need to clone the repository from GitHub to your local machine using Git. Git is a version control system that lets you track changes to your files and collaborate with others.

To clone the repository using Git, you need to:

- Have Git installed on your machine. If not, install Git on your machine. You can download it from https://git-scm.com/downloads and follow the instructions for your operating system.
- Open a terminal such as Command Prompt on Windows. (Click Start, type "cmd", click on "Command Prompt") and navigate to the folder where you want to store your local copy of the repository with OS instructions. For example:

```bash
cd C:\Users\your-name\Documents
```

(replace your-name with your actual value)

- Type the following command:

```bash
git clone https://github.com/your-username/your-repository-name.git
```

(replace your-username and your-repository-name with your actual values)

You can also find the reference to your repository path (the part after "git clone") in the Web interface for your repository by clicking on the green "Code" button.

This will create a folder named after your repository name in the current folder, and download all the files from GitHub into it. You can view it by opening the folder in your file explorer or IDE (such as Visual Studio Code).

### Step 4: Modify the code using online-python.com and commit the changes

To modify the code using online-python.com, you can:

- Go to https://www.online-python.com/ and start editing the provided example file. 
- Save the file by clicking on the **Save File to Disk** icon that represents a disquette.
- You can also modify an existing file by clicking on the **Open File from Disk** icon represented by an open folder, making the code changes, and then saving as above.

**EDIT: For this assignment, to know the true potential of git and GitHub, modify the hello.py file that you have created in previous steps.**

You have now modified the code using online-python.com. You can run it by clicking on **Run** and see the output in the console below.

To commit the changes to Git, you must:

- Save the modified new or modified files from online-python.com into your local repository folder.
- Open a terminal as previously and navigate to the folder where you cloned the repository. For example:

```bash
cd C:\Users\your-name\Documents\your-repository-name
```
(replace your-name and your-repository-name with your actual values)

- Type the following command:

```bash
git status
```

This will show you which files have been modified, added or deleted.

- Type the following command:

```bash
git add .
```

This will stage all the changes for commit. Alternatively, you can specify individual files to stage, such as:

```bash
git add hello.py
```

- Type the following command:

```bash
git commit -m "Your message"
```

This will commit the changes with a message describing them. For example:

```bash
git commit -m "Modify hello.py"
```

You have now committed the changes to Git. You can view them by typing:

```bash
git log
```

This will show you a history of all the commits made to the repository. But be warned, your commited changes have not yet been published to your online GitHub repository...

### Step 5: Push the changes back to GitHub and view them online

To push the changes back to GitHub, you need to:

- Open a terminal and navigate to the folder where you cloned the repository. For example:

```bash
cd C:\Users\your-name\Documents\your-repository-name
```

(replace your-name and your-repository-name with your actual values)

- Type the following command:

```bash
git push origin main
```

or simply

```bash
git push
```

This will push the changes from your local branch (main) to your remote branch (origin) on GitHub.

You have now pushed the changes back to GitHub! You can view them online by going to https://github.com/your-username/your-repository-name (replace your-username and your-repository-name with your actual values).

## Submitting the Assignment

For this private repository to be visible to anyone, you must invite them as a collaborator. To accomplish this for your teacher, whose username is **paquettm**, in your GitHub repository, at https://github.com/your-username/your-repository-name/blob/main/hello.py (replace your-username and your-repository-name with your actual values),  
- Click **Settings**
- Click **Collaborators**
- Click **Add people**
- In the text input, enter **paquettm**
- Click on that user in the listing
- Click **Add paquettm to this repository**

The submission deadline is Monday, August 28.
