## Creating Custom Channels

Before proceeding, ensure that you have conda-build installed. If not, the user can install it with the following command:

![conda_build](conda_build.png)

Next, organize all the packages the user wish to include in subdirectories based on the platforms intend to serve. Here's an example structure:

![conda_channel](conda_channel.png)

Run conda index command on the root directory : 

![conda_channel_index](conda_channel_index.png)

The conda index command generates a repodata.json file in each repository directory, which contains metadata for the packages in the channel.

To test custom channel, the user can serve it using a web server or via a file:// URL to the channel directory. The user can then test by sending a search command to the custom channel. For example, if the user  want to search for files in the custom channel location /opt/channel/linux-64/, the user can use the following command:

![conda_channel_search](conda_channel_search.png)
