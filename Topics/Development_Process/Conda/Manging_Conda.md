## Managing Conda

Everything necessary to know about managing your installation of conda

### Verifying Conda Installation

- **Command**: `conda --version`
- This command should return the version of Conda installed. If it doesn't, ensure you are logged into the correct user account, are in a directory Conda can find, and have reopened the terminal after installation.

### Determining Conda Version

- **Commands**: `conda info` or `conda -V`
- Both commands provide details about the installed version of Conda.

### Updating Conda

- **Command**: `conda update conda`
- This command will check for the latest version of Conda and prompt you to update ('y' to proceed with the update). It also informs about other packages that will be updated or changed as a result of the Conda update.

### Suppressing Warning Messages About Conda Updates

- **Command to Suppress Warnings**: `conda config --set notify_outdated_conda false`
- This command stops Conda from displaying warnings about newer versions being available.
- Alternatively, you can manually add `notify_outdated_conda: false` to your `.condarc` file.

For more comprehensive guidance, refer to the official documentation on [Managing Conda](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-conda.html).

