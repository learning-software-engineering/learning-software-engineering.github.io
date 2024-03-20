
## Managing Channels

Information about channels and how they are searched through when installing packages.

### Conda Channels

- **What They Are**: Channels are the locations (URLs) where Conda packages are stored.
- **Default Behavior**: By default, Conda searches a set of default channels and downloads/updates packages from there.
- **Channel Collisions**: These occur when multiple channels host the same package. Conda has ways to resolve these collisions.

### Channel Priority

- **Default Priority Resolution**: Conda prioritizes packages based on the channel priority (higher priority channels are preferred), then by version number, and finally by build number within each channel.
- **Strict Channel Priority**: This mode, available from Conda 4.6.0 onwards, ensures that packages in lower priority channels are not considered if the same package is available in a higher priority channel. It speeds up operations and reduces package incompatibility issues.
- **Flexible Channel Priority**: This is the default setting where Conda can reach into lower priority channels to fulfill dependencies if necessary.
- **Disabled Channel Priority**: Here, the package version takes precedence, and channel priority only breaks ties.

### Configuring Channel Priority

- **Setting Strict Priority**: Use conda config --set channel_priority strict.
- **Disabling Channel Priority**: Add channel_priority: disabled in the .condarc file or use conda config --set channel_priority disabled.
- **Adding Channels**: Use conda config --add channels new_channel to add a channel to the top (highest priority) or conda config --append channels new_channel to the bottom (lowest priority).

### Practical Implications

- **No Collisions with Defaults Only**: Using only the default channel prevents collisions.
- **Prioritizing Channels**: The order of channels in your configuration affects how packages are resolved, especially when multiple channels offer the same package.
- **Using Strict Priority**: This is recommended for faster operations and fewer incompatibility problems, but it might limit the availability of certain packages if they're only found in lower-priority channels.

For more comprehensive guidance, refer to the official documentation on [Managing Channels](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-channels.html).
