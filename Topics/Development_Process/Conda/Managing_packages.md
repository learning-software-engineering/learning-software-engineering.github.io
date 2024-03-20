
## Managing Packages

Details related to how to find, install, remove, and update packages in a given environment.

### Searching for Packages

- **Basic Search**: `conda search packageName` to check if a package is available.
- **Search in Specific Channel**: `conda search --override-channels --channel channelURL packageName` for searching in a particular channel.

### Installing Packages

- **Basic Installation**: `conda install packageName` to install a package in the current environment.
- **Specific Environment Installation**: `conda install --name envName packageName` to install in a specified environment.
- **Version-Specific Installation**: `conda install packageName=versionNumber` for installing a specific version.
- **Multiple Packages**: `conda install packageName1 packageName2` to install multiple packages simultaneously.
- **Packages from Anaconda.org**: Use `conda install -c channelName` packageName for packages available on Anaconda.org but not in the default channels.
- **Non-Conda Packages**: If a package isn't available through conda, it can be installed via `conda-forge` or `pip`.

### Updating Packages

- **Update Specific Package**: `conda update packageName`.
- **Update Python**: `conda update python` updates to the latest in the current series (e.g., Python 3.7 to Python 3.8).
- **Update Conda**: `conda update conda`.
- **Update Anaconda Metapackage**: `conda update anaconda`.

### Preventing Package Updates (Pinning)

- **Pinning Packages**: Prevent specific packages from updating by adding them to a `pinned` file in the `conda-meta` directory of the environment.

### Setting Default Packages for New Environments

- **Default Packages**: `conda config --add create_default_packages packageName` to automatically install certain packages in every new environment.

### Removing Packages

- **Remove Specific Package**: `conda remove -n envName packageName` from a specific environment, or `conda remove packageName` from the current environment.
- **Multiple Packages**: `conda remove packageName1 packageName2` to remove multiple packages at once.

### Listing Installed Packages

- **List Packages**: `conda list` to view packages installed in the current environment, or `conda list -n envName` for a different environment.

### Finding Package Dependencies

- To find what packages depend on a specific package, use a combination of `conda search` and file searching in the Conda package cache.

For more comprehensive guidance, refer to the official documentation on [Managing Packages](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-pkgs.html).
