# How to Clone a Repository with a Git Submodule

When working with repositories that contain Git submodules, you need to perform additional steps beyond a simple `git clone` to properly initialize and fetch the submodule contents.

## Required Commands

There are two essential commands you need to remember when cloning repositories with submodules:

### `git submodule init`
This command initializes the submodules defined in the repository. When you clone a repository that contains submodules, Git doesn't automatically fetch the submodule contents. You need to run `git submodule init` to initialize them first.

Git reads the `.gitmodules` file in the repository to configure the submodules and prepares to fetch the submodule contents when you run `git submodule update`.

### `git submodule update`
This command fetches the latest commits from the submodule repositories.

If there are new commits in the submodule repositories, you may need to run `git submodule update` to update the submodules to the latest state.

## Step-by-Step Process

To clone repositories having submodules in them, follow these steps:

1. **Clone the main repository**
   ```bash
   git clone <repository_URL>
