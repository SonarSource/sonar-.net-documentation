[VISUAL STUDIO ALM RANGERS](http://aka.ms/vsaraboutus)
 ---

# SonarQube Installation Guide for existing Team Foundation Server 2013 Single Server Environment

| [**Introduction**](./_README.md) | [Prerequisites](./Prerequisites.md) | [Installation and Configuration](./Installation%20and%20Configuration.md) | [Additional Configurations](Additional%20Configurations.md) | [Appendix](Appendix.md) |

## Table of Contents

- Introduction
- [Prerequisites](./Prerequisites.md)
	- Java
	- Database
	- Web Browser
	- Hardware
	- File Encoding
- [Installation and Configuration](./Installation%20and%20Configuration.md)
	- Installation Topologies
	- Setup SonarQube Server
	- Setup the Build Agent Machine
	- Integrate with Team Build
- [Additional Configurations](Additional%20Configurations.md)
	- Running SonarQube as a Service on Windows
	- Configuring SonarQube to use Microsoft SQL Database
	- Secure the SonarQube Portal
- [Appendix](Appendix.md)
	- Analysis Parameters

## Introduction

“*SonarSource products generate process-level benefits, such as decreasing software development risk, raising software quality and improving team productivity*” .

This guide aims to provide insightful and practical guidance around installing and configuring the **SonarQube™** (previously known as “**Sonar**”) platform on an existing Team Foundation Server 2013 setup.

[Technical Debt](http://en.wikipedia.org/wiki/Technical_debt) has many causes: business pressures to release early with uncompleted features, software architecture does not allow for adaptation to changing business needs, inadequate testing and documentation, isolation of changes requiring future merging of the changes, and lack of scheduling for refactoring. Paying down on the debt is the only debt reduction strategy.

As we continue ongoing development, the cost of paying down on the technical debt will increase, as does the cost of fixing a bug later in the development cycle. In theory, paying down technical debt is easy if you simply complete the uncompleted work. However, knowing what technical debt exists or what to track can be challenging. Enter **SonarQube** and **Team Foundation Server**.

SonarQube is an open source platform providing continuous inspection of your code quality. Through integration with Team Foundation Server and SonarQube you will be empowered to continuously inspect the technical debt, manage the debt, and pay down on the debt.

The following are the details of getting the integration in place with an existing deployment of Team Foundation Server.

**>> NOTE >>** For more information on SonarQube, please refer to [Technical Debt](http://docs.sonarqube.org/display/SONAR/Technical+Debt) and [Evaluate your technical debt with Sonar](http://www.sonarqube.org/evaluate-your-technical-debt-with-sonar/).

The Visual Studio ALM Rangers includes members from the Visual Studio Product group, Microsoft Services, Microsoft Most Valuable Professionals (MVP) and Visual Studio Community Leads. Their mission is to provide out-of-band solutions to missing features and guidance. A growing Rangers Index is available online. 
- [Home](http://aka.ms/vsarunderstand)
- [Solutions](http://aka.ms/vsarsolutions)
- [Membership](http://aka.ms/vsarindex)
- Contributors: Anil Chandra Lingam, Baruch Frei, Brian Blackman, Cesar Solis Brito, Clementino de Mendonca, Darren Rich, Duncan Pocklington, Hosam Kamel, Jean-Marc Prieur, Jeff Bramwell, Marcelo Silva, Mathew Aniyan, Michael Wiley
- Special thanks to: Colin Dembovsky