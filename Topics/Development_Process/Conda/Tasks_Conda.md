## Managing Conda

Managing Conda effectively is crucial for maintaining the integrity and functionality of your Conda environment. Regular updates ensure you have the latest features and security updates, while understanding how to check and manage its version can help troubleshoot any issues that may arise. These commands are an essential part of using Conda for managing Python environments, especially in environments where consistent and reproducible setups are important.

### Verifying Conda Installation

- Command: `conda --version`
- This command should return the version of Conda installed. If it doesn't, ensure you are logged into the correct user account, are in a directory Conda can find, and have reopened the terminal after installation.

### Determining Conda Version

- Commands: `conda info` or `conda -V`
- Both commands provide details about the installed version of Conda.

### Updating Conda

- Command: `conda update conda`
- This command will check for the latest version of Conda and prompt you to update ('y' to proceed with the update). It also informs about other packages that will be updated or changed as a result of the Conda update.

### Suppressing Warning Messages About Conda Updates

- Command to Suppress Warnings: `conda config --set notify_outdated_conda false`
- This command stops Conda from displaying warnings about newer versions being available.
- Alternatively, you can manually add `notify_outdated_conda: false` to your `.condarc` file.

For more comprehensive guidance, refer to the official documentation on [Managing Conda](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-conda.html).

## Managing environments

### Creating Environments:

- Basic creation: `conda create --name <my-env>`
- With a specific Python version: `conda create -n myenv python=3.9`
- Including specific packages: `conda create -n myenv scipy` or `conda install -n myenv scipy`
- With specific package versions: `conda create -n myenv scipy=0.17.3`
- Combining Python version and multiple packages: `conda create -n myenv python=3.9 scipy=0.17.3 astroid babel`

### Environment File:

- Create an environment from environment.yml: `conda env create -f environment.yml`
- Activate the new environment: `conda activate myenv`
- Verify the environment: `conda env list` or `conda info --envs`

### Specifying Environment Location:

- Create an environment in a specific directory: `conda create --prefix ./envs jupyterlab=3.2`
- Activate with: `conda activate ./envs`
- Modify .condarc for a custom prompt

### Updating an Environment:

- Update based on changes in environment.yml: `conda env update --file environment.yml --prune`

### Cloning an Environment:

- Clone an existing environment: `conda create --name myclone --clone myenv`

### Building Identical Environments:

- Generate a spec file: `conda list --explicit > spec-file.txt`
- Create an environment from a spec file: `conda create --name myenv --file spec-file.txt`

### Activating an Environment

- Purpose: Adds environment entries to PATH and runs activation scripts, setting necessary environment variables.
- Command: `conda activate myenv` (replace myenv with your environment name).
- Windows Specifics: Due to its reliance on a dynamic-link library search order, proper activation on Windows is crucial to avoid errors like HTTP or SSL issues.

### Conda Init

- Background: Introduced in Conda 4.4, improved in Conda 4.6 to support a variety of shells (bash, zsh, csh, fish, xonsh).
- Key Feature: Allows the use of conda activate without modifying the PATH, reducing disruptions to other software.
- Auto-activation of Base Environment: Can be controlled via the auto_activate_base setting.

### Nested Activation

- Usage: `conda activate --stack myenv` to retain current environment in the PATH.
- Auto-Stacking: Configurable for automatic stacking when moving from outermost (base) environment.

### Environment Variables for DLL Loading

- Warning: Without activation, environment variable setting and script activations don't occur. Full support is only for activated environments.

### Deactivating an Environment

- Command: `conda deactivate` to remove the path of the current active environment.
- Note: From the base environment, use `conda activate` to return to the base instead of `conda deactivate`.

### Determining Your Current Environment

- Indication: Active environment shown in parentheses or brackets at the beginning of the command prompt.
- Checking Environment: `conda info --envs` shows a list with the current environment marked.
- Prompt Display Setting: Can be toggled with `conda config --set changeps1 false/true`.

### Viewing a List of Your Environments

- Command: `conda info --envs` or `conda env list` to see all environments.
- Administrator View: Shows all environments for all users if run by an administrator.

### Viewing a List of Packages in an Environment

- For a Non-Activated Environment: `conda list -n myenv`
- For an Activated Environment: `conda list`
- To Check for a Specific Package: `conda list -n myenv scipy`

### Using Pip in an Environment

- It's recommended to use Conda before Pip within environments for package installation.
- Using Pip after Conda helps avoid potential dependency conflicts.
- Creating isolated Conda environments for Pip usage is advised.
- If you need to make significant changes after using Pip, recreate the Conda environment.

### Setting Environment Variables
- `conda env config vars set` and `unset` commands are used to manage environment variables.
- Set environment variables are specific to each Conda environment and are removed upon deactivation.

### Saving Environment Variables

- Scripts can be written to automatically set and unset environment variables upon activation and deactivation of an environment.
- Different scripts are used for Windows (`env_vars.bat`) and UNIX-like systems (macOS and Linux, `env_vars.sh`).

### Sharing an Environment

- Environments can be shared via an `environment.yml` file, which lists all packages and versions.
- The `conda env export > environment.yml` command is used to create this file.
- For cross-platform compatibility, `conda env export --from-history` includes only explicitly requested packages.

### Restoring an Environment

- `conda list --revisions` shows the history of changes made to the environment.
- Environments can be restored to previous states using `conda install --revision=REVNUM`.

### Removing an Environment

- Environments are removed with `conda remove --name myenv --all` or `conda env remove --name myenv`.
- The removal can be verified using `conda info --envs`.

For more comprehensive guidance, refer to the official documentation on [Managing Environments](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html).

## Managing Channels

### Conda Channels

- What They Are: Channels are the locations (URLs) where Conda packages are stored.
- Default Behavior: By default, Conda searches a set of default channels and downloads/updates packages from there.
- Channel Collisions: These occur when multiple channels host the same package. Conda has ways to resolve these collisions.

### Channel Priority

- Default Priority Resolution: Conda prioritizes packages based on the channel priority (higher priority channels are preferred), then by version number, and finally by build number within each channel.
- Strict Channel Priority: This mode, available from Conda 4.6.0 onwards, ensures that packages in lower priority channels are not considered if the same package is available in a higher priority channel. It speeds up operations and reduces package incompatibility issues.
- Flexible Channel Priority: This is the default setting where Conda can reach into lower priority channels to fulfill dependencies if necessary.
- Disabled Channel Priority: Here, the package version takes precedence, and channel priority only breaks ties.

### Configuring Channel Priority

- Setting Strict Priority: Use conda config --set channel_priority strict.
- Disabling Channel Priority: Add channel_priority: disabled in the .condarc file or use conda config --set channel_priority disabled.
- Adding Channels: Use conda config --add channels new_channel to add a channel to the top (highest priority) or conda config --append channels new_channel for the bottom (lowest priority).

### Practical Implications

- No Collisions with Defaults Only: Using only the defaults channel prevents collisions.
- Prioritizing Channels: The order of channels in your configuration affects how packages are resolved, especially when multiple channels offer the same package.
- Using Strict Priority: This is recommended for faster operations and fewer incompatibility problems, but it might limit the availability of certain packages if they're only found in lower-priority channels.

For more comprehensive guidance, refer to the official documentation on [Managing Channels](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-channels.html).

## Managing Packages

### Searching for Packages

- Basic Search: `conda search packageName` to check if a package is available.
- Search in Specific Channel: `conda search --override-channels --channel channelURL packageName` for searching in a particular channel.

### Installing Packages

- Basic Installation: `conda install packageName` to install a package in the current environment.
- Specific Environment Installation: `conda install --name envName packageName` to install in a specified environment.
- Version-Specific Installation: `conda install packageName=versionNumber` for installing a specific version.
- Multiple Packages: `conda install packageName1 packageName2` to install multiple packages simultaneously.
- Packages from Anaconda.org: Use `conda install -c channelName` packageName for packages available on Anaconda.org but not in the default channels.
- Non-Conda Packages: If a package isn't available through conda, it can be installed via `conda-forge` or `pip`.

### Updating Packages

- Update Specific Package: `conda update packageName`.
- Update Python: `conda update python` updates to the latest in the current series (e.g., Python 3.7 to Python 3.8).
- Update Conda: `conda update conda`.
- Update Anaconda Metapackage: `conda update anaconda`.

### Preventing Package Updates (Pinning)

- Pinning Packages: Prevent specific packages from updating by adding them to a `pinned` file in the `conda-meta` directory of the environment.

### Setting Default Packages for New Environments

- Default Packages: `conda config --add create_default_packages packageName` to automatically install certain packages in every new environment.

### Removing Packages

- Remove Specific Package: `conda remove -n envName packageName` from a specific environment, or `conda remove packageName` from the current environment.
- Multiple Packages: `conda remove packageName1 packageName2` to remove multiple packages at once.

### Listing Installed Packages

- List Packages: `conda list` to view packages installed in the current environment, or `conda list -n envName` for a different environment.

### Finding Package Dependencies

- To find what packages depend on a specific package, use a combination of `conda search` and file searching in the Conda package cache.

For more comprehensive guidance, refer to the official documentation on [Managing Packages](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-pkgs.html).
