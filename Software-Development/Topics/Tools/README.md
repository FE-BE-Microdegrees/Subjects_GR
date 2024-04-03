# Tools

- [Tools](#tools)
  - [Learning Outcomes](#learning-outcomes)
  - [Excercises and Assignments](#excercises-and-assignments)

## Learning Outcomes

After completing this topic, you'll be able to:

- identify the different types of tools used in software development;
- describe various tools used in software development;
- use different tools in software development.

In the context of software development, tools encompass a wide range of software applications, libraries, frameworks, and utilities that developers use to aid in various stages of the software development life cycle (*SDLC*). These tools are designed to streamline processes, enhance productivity, ensure code quality, and facilitate collaboration. Here's an overview of the different types of tools that are commonly used in software development:

- **Integrated Development Environments (IDEs):**
    - **Purpose:** Lightweight tools for writing and editing code, often used for scripting or web development. Likely the first tool developers use.
    - **Examples:** 
      - [Eclipse](https://www.eclipse.org/) 
      - [Visual Studio](https://visualstudio.microsoft.com/)
      - [IntelliJ IDEA](https://www.jetbrains.com/idea/)
      - [PyCharm](https://www.jetbrains.com/pycharm/)
      - [Xcode](https://developer.apple.com/xcode/)

- **Version Control Systems:**
    - **Purpose:** Track and manage changes to code over time.  Code is a critical asset in software development that must be carefully maintained and protected. Version control systems allow developers to collaborate easily, track changes, and restore previous versions of an application if necessary.
    - **Examples:** 
      - [Git](https://git-scm.com/)
      - [Mercurial](https://www.mercurial-scm.org/)
      - [Subversion (SVN)](https://subversion.apache.org/)
      - [CVS](https://www.gnu.org/software/trans-coord/manual/cvs/cvs.html)

- **Build Tools:**
    - **Purpose:** Automate the process of compiling and building applications.
    - **Examples:** Maven, Gradle, Ant, Make.

- **Continuous Integration/Continuous Deployment (CI/CD) Tools:**
    - **Purpose:** Automate the processes of compiling, testing, and deploying applications. Nowadays, development processes are moving towards being carried out in small and rapid steps. If we had to manually perform all these steps each time an update is made, it would take a lot of time, and errors would be prone to occur. CI/CD tools help automate this process, speed it up, and reduce the likelihood of errors.
    - **Examples:** 
      - [Jenkins](https://www.jenkins.io/)
      - [Travis CI](https://www.travis-ci.com/)
      - [CircleCI](https://circleci.com/)
      - [GitLab CI/CD](https://docs.gitlab.com/ee/ci/)

- **Dependency Management Tools:**
    - **Purpose:** Manage software dependencies and libraries.
    - **Examples:** npm (Node.js), pip (Python), Maven (Java), NuGet (.NET).

- **Testing Tools:**
- **Purpose:** Automatically test software quality, performance, and security. As applications grow during development, the risk of not noticing all the bugs the application contains increases. It's always possible to manually check the application's functionality after making changes to ensure everything works as it should, but this is a time-consuming and expensive process. Various tools help automate this process.
    - **Unit Testing:** 
      - [JUnit (Java)](https://junit.org/junit5/)
      - [NUnit (.NET)](https://nunit.org/)
      - [Pytest (Python)](https://docs.pytest.org/en/8.0.x/)
    - **Functional/End-to-End Testing:** 
      - [Selenium](https://www.selenium.dev/)
      - [Cypress](https://www.cypress.io/)
      - [Protractor](https://www.protractortest.org/#/)
    - **Performance Testing:**
      - [JMeter](https://jmeter.apache.org/)
      - [LoadRunner](https://www.microfocus.com/en-us/products/loadrunner-professional/overview)

- **Code Quality and Review Tools:**
    - **Purpose:** Analyze code quality, style, and potential issues. Most activities in software development are aimed at ensuring the application works as it should. However, that's not the only thing developers need to consider. It's important to remember that software development is teamwork, and if the code is written in a way that makes it difficult for other developers to understand, it can cause problems. It's also important for the code to be written securely and without bugs. All these aspects are important, and there are various tools to help check these aspects.
    - **Examples:** 
      - [SonarQube](https://www.sonarsource.com/products/sonarqube/)
      - [ESLint](https://eslint.org/)
      - [Pylint](https://pypi.org/project/pylint/)
      - [CodeClimate](https://codeclimate.com/quality)
- **Package Managers:**
    - **Purpose:** Manage and organize libraries and modules for specific programming languages.
    - **Examples:** npm, pip, Composer, RubyGems.

- **Bug Tracking/Issue Tracking Systems:**
    - **Purpose:** Track, manage, and prioritize software bugs and tasks. Developers inevitably make mistakes. The error might not even be in the code written by the developer but in poorly described requirements that the developer followed. Various tools exist to help manage and track these errors.
    - **Examples:**
      - [JIRA](https://www.atlassian.com/software/jira)
      - [Bugzilla](https://www.bugzilla.org/)
      - [GitHub Issues](https://github.com/features/issues)
      - [Trello](https://trello.com/)
- **Documentation Tools:**
    - **Purpose:** Create and manage software documentation. Documentation is crucial in software development as it helps new developers quickly understand existing code and how the application works. Besides various text-based documentation (user manuals, etc.), there are also different tools specifically for creating and managing documentation about software code.
  - **Examples:**
    - [Doxygen](https://www.doxygen.nl/)
    - [Sphinx](https://www.sphinx-doc.org/en/master/)
    - [JSDoc](https://jsdoc.app/about-getting-started)

- **Database Management Tools:**
    - **Purpose:** Design, manage, and communicate with databases. Applications often require some type of database to store data. Designing, creating, and managing databases is quite a complex process that can be done manually, but there are also various tools that simplify this process.
    - **Examples:**
      - [MySQL Workbench](https://www.mysql.com/products/workbench/)
      - [pgAdmin](https://www.pgadmin.org/)
      - [Microsoft SQL Server Management Studio](https://learn.microsoft.com/en-us/sql/ssms/sql-server-management-studio-ssms?view=sql-server-ver16)
- **Containerization and Virtualization Tools:**
    - **Purpose:** Create, deploy, and manage containers or virtualized environments. Containers and virtualized environments have become very popular in recent years because they allow developers to create environments similar to where the application will later run, which are easy to create and delete. There are various tools that help simplify this process and avoid situations where the application works on the developer's computer/server but not on the client's computer/server.
    - **Examples:**
      - [Docker](https://www.docker.com/)
      - [Kubernetes](https://kubernetes.io/)
      - [VMware](https://www.vmware.com/)
      - [VirtualBox](https://www.virtualbox.org/)


- **Cloud Platforms and Tools:**
    - **Purpose:** Develop, deploy, and scale applications in cloud environments. Increasingly, applications are not kept on client's own servers but are hosted in various cloud environments, which are flexible and often more cost-effective in the long run.
    - **Examples:** 
      - [AWS](https://aws.amazon.com/)
      - [Google Cloud Platform](https://cloud.google.com/)
      - [Microsoft Azure](https://azure.microsoft.com/en-us)
      - [Heroku](https://www.heroku.com/)

- **Collaboration and Communication Tools:**
    - **Purpose:** Facilitate team communication and collaboration. Software development is mostly teamwork, and it's important for team members to communicate and collaborate with each other. Simple communication tools like email or a common messaging app can often be used, but there are also special tools designed to facilitate teamwork in software development. For example, it may be necessary in a messaging app to share code snippets that other team members can quickly review, and ordinary communication tools may not facilitate this very well.
    - **Examples:** 
      - [Slack](https://slack.com/) 
      - [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/group-chat-software) 
      - [Zoom](https://zoom.us/)
      - [Confluence](https://www.atlassian.com/software/confluence)

- **Development Frameworks and Libraries:**
    - **Purpose:** Provide a structured foundation for more efficient application development. In addition to the dependencies mentioned above, there are also various frameworks and libraries that help developers create applications faster. For example, there may be a framework that helps quickly create web applications or libraries that simplify interacting with databases.applications more efficiently.
    - **Examples:** 
      - [Angular](https://angular.io/)
      - [React](https://react.dev/)
      - [Vue.js](https://vuejs.org/)
      - [Spring Boot (Java)](https://spring.io/guides/gs/spring-boot)
      - ... and many others
- **Code Editors:**
  - **Purpose:** Lightweight tools for writing and editing code, often used for scripting or web development. Likely the first tool developers use.
  - **Examples:**
    - [Visual Studio Code](https://code.visualstudio.com/)
    - [Sublime Text](https://www.sublimetext.com/)
    - [Atom](https://atom-editor.cc/)

- **API Development and Testing Tools:**
    - **Purpose:** esign, simulate, test, and document APIs. Application interfaces (*APIs*) are very important in modern software development as they offer a great way to exchange data between different applications. Sometimes we can test a simpler API just by typing something in the browser's address bar, but for more complex APIs, there are special tools that help simplify the creation, testing, and documentation of APIs.
    - **Examples:**
      - [Postman](https://www.postman.com/)
      - [Swagger/OpenAPI](https://swagger.io/specification/)
      - [Insomnia](https://insomnia.rest/)

- **Task & Project Tracking:**
  - **Purpose:**  Plan, track, and manage software projects from start to finish. As mentioned several times before, software development is teamwork, and for teamwork to be smooth, all team members need to know what they are supposed to do and when. Various project and task management/tracking tools help simplify this process and ensure project success.
  - **Examples:**
    - [JIRA (Atlassian)](https://www.atlassian.com/software/jira)
    - [Trello](https://trello.com/)
    - [GitHub Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects)

## Excercises and Assignments

