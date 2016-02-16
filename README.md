# Introduction

The goal of this documentation is to explain to any member of the .Net community how to install, configure and use the SonarQube ecosystem to analyze .Net projects.

# PDF version of the documentation
The pdf for the latest release is available [here](https://github.com/SonarSource-VisualStudio/sonar-.net-documentation/releases/download/1.3/SonarQube-Setup-Guide-For-Net-Users-v-1-3.pdf).


# GitBook

The structure of this documentation has been designed to ease the generation of a global PDF file with help of http://www.gitbook.com each time this documentation is released.

## Installation Instructions

0. Install NPM (See npmjs.com)
0. Install GitBook with help of the following command line `npm install gitbook-cli -g`
0. Install Calibre (See http://calibre-ebook.com/download). The `ebook-convert` command line must be available in the `%PATH%` (or `$PATH`). For Mac OS X users, this might be done with help of the following command line `sudo ln -s ~/Applications/calibre.app/Contents/MacOS/ebook-convert /usr/bin`

## Manual actions required when doing a release

0. Edit the 'cover.pptx' file to update the release date and the version
0. Generate a 'cover.jpg' image from  'cover.pptx' and update 'doc/cover.jpg'
0. Execute the following command line from the root directory of the GitHub Repository: `gitbook pdf ./doc ./SonarQube-Setup-Guide-For-Net-Users-V-X-Y-Z.pdf`
