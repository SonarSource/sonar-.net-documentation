# SonarQube Setup Guide for .NET users

The goal of this documentation is to explain to any member of the .Net community how to install, configure and use the SonarQube ecosystem to analyze .Net projects.

## GitBook

The structure of this documentation has been designed to ease the generation of a global PDF file with help of http://www.gitbook.com each time this documentation is released.

### Installation Instructions

0. Install NPM (See npmjs.com)
0. Install GitBook with help of the following command line `npm install gitbook-cli -g`
0. Install Calibre (See http://calibre-ebook.com/download). The `ebook-converter` command line must be available in the $PATH. For Mac OS X users, this might be done with help of the following command line `sudo ln -s ~/Applications/calibre.app/Contents/MacOS/ebook-convert /usr/bin`

### Generation of PDF File

The following command line must be executed from the root directory of this GitHub Repository to generate the global PDF file:

`gitbook pdf ./doc ./SonarQube-Setup-Guide-For-Net-Users.pdf`