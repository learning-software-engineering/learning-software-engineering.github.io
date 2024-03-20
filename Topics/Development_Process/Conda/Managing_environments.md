## Managing environments

Various operations involved with creating, updating, exporting, and removing environments, plus more

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
