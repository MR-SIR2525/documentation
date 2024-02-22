# Git and SSH - Getting Started

## Installing Git
- First, you'll need to install <a href="https://git-scm.com/downloads">Git</a> on your computer. 


## Setting Up SSH Keys
Now we will generate a new SSH key pair, add the public key to your GitHub account, and instruct your system to use the key when connecting to GitHub.


### Step 1: Generate a New SSH Key Pair

1. **Open Git Bash or Terminal**:
   - If you're on Windows, open Git Bash. 
   - On macOS or Linux, you can use the Terminal.

2. **Generate SSH Key**:
   - Run the following command, replacing `your_email@example.com` with your GitHub email address. This creates a new SSH key, using the provided email as a label.
     ```sh
     ssh-keygen -t ed25519 -C "your_email@example.com"
     ```
     - *If your system does not support the `ed25519` algorithm, you can use RSA:*
       ```sh
       ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
       ```
   - When prompted to "Enter a file in which to save the key," press Enter to accept the default file location, or enter a custom path/to/key/file.

3. **Set a Password on it** (optional):
   - You'll be asked to enter a passphrase. While optional, a passphrase adds an extra layer of security.


### Step 2: Add Your SSH Key to the SSH Agent

1. **Start the SSH Agent in the Background**:
   ```sh
   eval "$(ssh-agent -s)"
   ```

2. **Add Your SSH Private Key to the SSH Agent**:
    ```sh
    ssh-add ~/.ssh/id_ed25519
    ```
     - If you used a custom name or location for your SSH key, use that.


### Step 3: Add Your SSH Key to Your GitHub Account

1. **Copy the SSH Public Key to Your Clipboard**, or print it to the Terminal:
   - For Windows:
     ```sh
     clip < ~/.ssh/id_ed25519.pub
     ```
   - For macOS:
     ```sh
     pbcopy < ~/.ssh/id_ed25519.pub
     ```
   - For Linux:
     ```sh
     cat ~/.ssh/id_ed25519.pub
     ```

2. **Add the SSH Key to Your GitHub Account**:
   - Go to your GitHub account settings.
   - Click on "SSH and GPG keys" in the sidebar.
   - Click on "New SSH key" or "Add SSH key."
   - Paste your key into the "Key" field.
     - **The format should be something like:**
       ```
       ssh-ed25519 AAAAAB3NzaC1ylkjlhpouhuwqy7b6w your_email@example.com
       ```
   - Click "Add SSH key."

### Step 4: Verify Your SSH Connection Works

1. **Open Git Bash or Terminal**.
2. **Connect to GitHub**:
   ```sh
   ssh -T git@github.com
   ```
3. **Verify That You've Successfully Connected**:
   - You may see a warning about the authenticity of the host. Type `yes` to continue.
   - If everything is set up correctly, you'll see a message saying you've successfully authenticated.

### Troubleshooting

- If you encounter errors, double-check that you've correctly copied the entire public key and added it to GitHub.
- Ensure your SSH agent is running and that your key is added.
- Verify your email address in the key matches the one on your GitHub account.

This setup allows you to securely connect to GitHub without needing to use your username and password each time.


## Configuring Git
Now, we will set up your name and email address for Git to use in commits.

### Step 1: Open Git Bash or Terminal
- Open Git Bash (on Windows) or Terminal (on macOS or Linux).

### Step 2: Set Your User Name
- Use the following command to set your user name. This can be your real name or the name you wish to appear in your commits:
  ```sh
  git config --global user.name "Your Name"
  ```
- Replace `"Your Name"` with your actual name.

### Step 3: Set Your Email Address
  - Next, set your email address with Git. This should match the email address you use for your GitHub account:
    ```sh
    git config --global user.email "your_email@example.com"
    ```
  - Replace `"your_email@example.com"` with the email address associated with your GitHub account.
  - **Note about public email settings on Github:**
    - If your Github account settings are set to block your private email address from being published to the internet for commits, PR's, etc., you will need to use your account's public email address which can be found in your Github account settings.
      - Account > Settings > Emails. 
      - Once there, under "Emails" at the top, you'll see your private email address and this message:  "Not visible in emails:  This email will not be used as the 'from' address for web-based Git operations, e.g., edits and merges. We will instead use 123456789+your_usernane@users.noreply.github.com." Copy that public email address and use that the `git config --global user.email "public_email"` command.

  - Why It Matters
    - **Attribution**: Your name and email address are attached to your commits and tags. They are visible in the commit history and are used to identify the author of the changes.
    - **Collaboration**: If you're contributing to a project with multiple contributors, having your correct name and email configured helps others recognize your contributions.
    - **GitHub Integration**: For GitHub to link your commits to your GitHub account, the email address used in your commits must match one of the email addresses associated with your GitHub account.

### Step 4: Verifying Your Configuration
- To verify your configuration, you can use these commands:
  ```sh
  git config --global user.name
  git config --global user.email
  ```
- These commands will display the name and email address Git will use for your commits.

### You're Done!

### Additional Configuration
- If you work on multiple projects and need to use different email addresses for different contexts, you can omit the `--global` flag and run the `git config user.name` and `git config user.email` commands within the specific project directory. This sets the configuration locally for that project.

By setting your name and email in Git, you ensure that your work is properly attributed to you and that your commits are linked to your GitHub account.