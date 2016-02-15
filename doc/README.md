# Introduction

“*SonarSource products generate process-level benefits, such as decreasing software development risk, raising software quality and improving team productivity*” .

This guide aims to provide insightful and practical guidance around installing and configuring the **SonarQube™** (previously known as “**Sonar**”) platform for the analysis of C# and VB.NET projects.

[Technical Debt](http://en.wikipedia.org/wiki/Technical_debt) has many causes: business pressures to release early with uncompleted features, software architecture does not allow for adaptation to changing business needs, inadequate testing and documentation, isolation of changes requiring future merging of the changes, and lack of scheduling for refactoring. Paying down on the debt is the only debt reduction strategy.

As we continue ongoing development, the cost of paying down on the technical debt will increase, as does the cost of fixing a bug later in the development cycle. In theory, paying down technical debt is easy if you simply complete the uncompleted work. However, knowing what technical debt exists or what to track can be challenging. Enter **SonarQube** and **Team Foundation Server**.

SonarQube is an open source platform providing continuous inspection of your code quality. Through integration with Team Foundation Server and SonarQube you will be empowered to continuously inspect the technical debt, manage the debt, and pay down on the debt.

The following are the details of getting the analysis of a .NET project in place either integrated in an existing deployment of Team Foundation Server or in a standalone command line way using the *SonarQube Scanner for MSBuild*.

**>> NOTE >>** For more information on SonarQube, please refer to [Technical Debt](http://docs.sonarqube.org/display/SONAR/Technical+Debt) and [Evaluate your technical debt with Sonar](http://www.sonarqube.org/evaluate-your-technical-debt-with-sonar/).
