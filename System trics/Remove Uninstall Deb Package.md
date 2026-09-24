# Remove Uninstall Deb Package

This command will extract the package name from the deb and remove that package name.

`dpkg -r $(dpkg -f your-file-here.deb Package)`

Unused packages in Linux can be removed using package managers. For Debian and Ubuntu, use 
`sudo apt-get autoremove && sudo apt-get autoclean`