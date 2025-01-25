# Setting up a dev container for Rust

Primary author: [Jaxon Chavis](https://github.com/jkchavis)

## Prerequisites
A GitHub account
Git
Visual Studio Code (VSCode)
Docker
Basic knowledge of CLI
## Instructions
### Part 1: Setting up your project

#### Step 1: Create a Local Directory and Git Repository
 
A. Open your terminal or command prompt

B. Create a new directory(Note: Decide where you want to store this directory. You should choose this before making your directory. Additionally, name your directory what you want as long as it is appropriate and siginificant to what we are trying to accomplish.)
```
mkdir rust-setup-tutorial
cd rust-setup-tutorial
```

C. Initialize a new Git Repository.
```
git init
```

D. Create a README.md file
```
echo "# Our first Rust project" > README.md
git add README.md
git commit -m "Initial commit with README"
```

#### Step 2: Create a Remote Repository on GitHub

A. Log in to your GitHub account and navigate to the "Create a New Repository" page.

B. Fill in the details as follows:
    - Repository Name: rust-setup-tutorials
    - Description: "Tutorial to Rust"
    - Visibility: Public

C. Do not initialize the repository with a README, .gitignore, or license.

D. Click Create Repository.

#### Step 3: Link your Local Repository to GitHub

1. Add the Github repository as a remote:
    git remote add origin https://github.com/<your-username>/comp423-course-notes.git
> [!NOTE] 
> Replace <your-username> with your GitHub username.

2. Use the ```git branch``` subcommand to check your default branch. It should be main but older versions of git use the name master when refering to the default branch. You can rename your default branch by using the command: ```git branch -M main```.

3. Push local commits to your GitHub repository
```git push --set-upstream origin main```

4. Back in the browser, refresh your GitHub repository and you should be able to see your new commit.

### Part 2: Setting up the Development Environment

#### Step 1: 

1. In VS Code, open the ```rust-setup-tutorial``` directory. You can do this via: File > Open Folder.

2. Install the Dev Containers extension for VS Code.

3. Create a ```.devcontainer``` directory in the root of you project with the following file inside of this "hidden" configuration directory:
```.devcontainer/devcontainer.json```

The ```devcontainer.json``` file defines the configuration for your development environment. Here we're specifying the following:

* ```name```: A descriptive name for your dev container.
* ```image```: The Docker image to use, in this case the latest version of a Rust environment.
* ```customizations```: Adds useful configurations to VS Code, like installing extensions. This ensures everyone using this dev container will automatically install the necessary extensions.
* ```postCreateCommand``` A command to run after the container is created.
```
{
  "name": "Rust Tutorial Setup",
  "image": "mcr.microsoft.com/devcontainers/rust:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": ["rust-lang.rust-analyzer"]
    }
  },
  "postCreateCommand":
}
```
### Step 3: Creating your Rust Project
* Reopen the project in a dev container: To do so press Ctrl+Shift+P and type "Dev Containers:Reopen in Container" in the search bar.
> [!Note]
> This may take some time, as it will have to download the necessary version of Rust.
* Next, open a new terminal and enter ```rustc --version```.
* You see something along these lines: ``````.