# Setting up a dev container for Rust

Primary author: [Jaxon Chavis](https://github.com/jkchavis)

## Prerequisites
* A GitHub account
* Git
* Visual Studio Code (VSCode)
* Docker
* Basic knowledge of CLI
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
```git init```

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
```git remote add origin https://github.com/<your-username>/rush-setup-tutorials.git```
> [!NOTE] 
> Replace <your-username> with your GitHub username.

2. Use the ```git branch``` subcommand to check your default branch. It should be main but older versions of git use the name master when refering to the default branch. You can rename your default branch by using the command: ```git branch -M main```.

3. Push local commits to your GitHub repository
```git push --set-upstream origin main```

4. Back in the browser, refresh your GitHub repository and you should be able to see your new commit.

### Part 2: Setting up the Development Environment

1. In VS Code, open the ```rust-setup-tutorial``` directory. You can do this via: File > Open Folder.

2. Install the Dev Containers extension for VS Code.

3. Create a ```.devcontainer``` directory in the root of you project with the following file inside of this "hidden" configuration directory:```.devcontainer/devcontainer.json```. To do this use the following two commands:
* ```mkdir .devcontainer```
* ```code .devcontainer/devcontainer.json```

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
  "postCreateCommand": "rustc --version"
}
```
### Part 3: Creating your Rust Project
1. Reopen the project in a dev container: To do so press Ctrl+Shift+P and type "Dev Containers:Reopen in Container" in the search bar.
> [!Note]
> This may take some time, as it will have to download the necessary version of Rust.
2. Next, we want to ensure that our version of rust is the newest version. To do this, open a new terminal and enter ```rustc --version```.
* You see something along these lines: ```rustc 1.83.0```.
3. Now that we've confirmed that we are running on the correct version of Rust. We must now create a new binary project:```cargo new hello_423 --vcs none```. Let's break this command down. ```cargo new``` is our command to make a new binary project. This command will create a project directory and three items inside that directory: a ```Cargo.toml``` file, an ```src``` directory, and a ```main.rs``` file inside of that ```src``` file. ```hello_423``` is the name that we give the directory. Adding ```--vcs none``` ensures that a new git repository won't automatically be created by the ```cargo new``` command.

4. With our project set up, we can begin writing our code.
* Open ```main.rs```
* Write the following code:
```
fn main(){
  println!("Hello COMP423")
}
```
> [!Important]
> Make sure you save your work before moving on.
5. Back in the terminal, enter ```cd hello_423```. Then, run ```cargo build```.
* ```cargo build``` compiles the source code into an executable binary. Similar to how we used ```gcc main.c -o main``` in COMP211.
6. Finally, run ```cargo run```.
* This is the same using ```./target/debug/hello_423```.

### Run vs Build
#### Cargo Run
Unlike ```cargo build```, which we used in the previous section. ```cargo run``` compiles and executes the local package by combinign the ```cargo build``` command and the ```./target/debug/hello_423``` command. 
#### Cargo Build
```cargo build``` compiles the local package and all of their dependencies. ```cargo build``` is a way to divide the ```cargo run``` command into two steps. This is often used in advanced debugging and working on multiple binaries. 

If you want learn more about these commands use ```cargo build --verbose``` and ```cargo run --verbose``` to get a closer look at what each command does behind the hill.

### Finalizing Project
#### Potential Errors and Warning (Optional)
If you are like me, you may have gotten a warning that looks something like this:
![Alt text](/workspaces/comp423-course-notes/Screenshot 2025-01-26 115928.png)
```os error 13``` is an error in which permission is denied to the user, likely due to the system believing you are not owner of these files. This causes ```.lock``` files that had been added to the working directory and .git files. As you can see you can complete the tutorial without fixing this error but it will prevent you from using some ```git``` and ```cargo``` commands. 
#### My solution
* First, follow this [guide](https://www.geeksforgeeks.org/git-a-lock-file-already-exists-in-the-repository-which-blocks-this-operation-from-completing/#) that will teach you more about the issue and how to delete the ```.lock``` files.
* Once all ```.lock``` files have been deleted use the following commands in your terminal.
1. ```sudo chmod -R u+w hello_423```. This will reset file permission.
2. ```sudo chown -R $(whoami):$(whoami) hello_423``` This will change the targeted file to owned by the current user.
3. ```cargo clean``` Run this to ensure that no files have been corrupted.
4. ```cargo run``` This will run the file again.
This should result in your terminal returning something like this:
![Alt text](/workspaces/comp423-course-notes/Screenshot 2025-01-26 123043.png)

Now that you have completed this tutorial remember to save all work using Ctrl+S.
Then, in your terminal run:
* ```git add .```
* ```git commit -m "<message>"```, replacing message with an appropriate and accurate message.
* ```git push --set-upstream origin main```

### Results
Below I have linked my own repository after completing the my tutorial. I have also linked my partner, Ana's Go tutorial, as well as my results from that.
#### Rust
[My Rust Repository](https://github.com/jkchavis/rust-setup-tutorial)
#### Go
[Ana's Tutorial](https://github.com/analrest/comp423-course-notes/blob/main/docs/tutorials/go-setup.md)
[My Go Repository](https://github.com/jkchavis/comp423-go)

> *Jordan, Kris "Starting a Static Website Project with MkDocs - COMP423 - Spring 2025" [https://comp423-25s.github.io/resources/MkDocs/tutorial/#step-2-add-requirementstxt-python-dependency-configuration](https://comp423-25s.github.io/resources/MkDocs/tutorial/#step-2-add-requirementstxt-python-dependency-configuration) 2025, January 17*