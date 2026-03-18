# DSAG's ABAP guide

![GitHub contributors](https://img.shields.io/github/contributors/1DSAG/ABAP-Leitfaden)
![GitHub](https://img.shields.io/github/license/1DSAG/ABAP-Leitfaden)
![GitHub stars](https://img.shields.io/github/stars/1DSAG/ABAP-Leitfaden?style=social)
![GitHub forks](https://img.shields.io/github/forks/1DSAG/ABAP-Leitfaden?style=social)

This is not the guide itself (this can be accessed via <https://1dsag.github.io/ABAP-Leitfaden>), but the associated repository with instructions on how to contribute to the guide.

The DSAG ABAP guide is a living document 👨‍💻 - it lives from and with its community 🥳.

The guide is written in `markdown` (variant `kramdown`) and is provided in `GitHub Pages` (<https://1dsag.github.io/ABAP-Leitfaden>) using `jekyll`.

## Inhalte

- [DSAG's ABAP guide](#dsags-abap-leitfaden)
  - [Inhalte](#inhalte)
  - [Erste Schritte](#erste-schritte)
    - [Quick start with GitHub web editor](#schnellstart-mit-github-web-editor)
    - [Development with Docker container](#entwicklung-mit-docker-container)
      - [Installation steps for Docker container](#installationsschritte-für-docker-container)
    - [Local installation](#lokale-installation)
      - [Prerequisites for Windows](#vorbedingungen-für-windows)
      - [Installation steps for local installation](#installationsschritte-für-lokale-installation)
  - [Mitwirken](#mitwirken)
  - [Lizenzierung](#lizenzierung)

## Erste Schritte

### Quick start with GitHub web editor

:point_right: No local installation  
:point_right: Everything in the browser  
:point_right: Preview after each commit

----

The [web-based editor](https://docs.github.com/de/codespaces/the-githubdev-web-based-editor) is an IDE that runs entirely in your browser. The web-based editor allows you to navigate through GitHub files and source code repositories and make and commit code changes. You can open any repository, fork, and pull request using the editor.
You can also preview Markdown files while editing.
This makes it very easy to get started as no local installation is required.
You may not see the end result immediately, but GitHub can generate that for you too.

1. Fork erstellen  
   ![Fork erstellen](img/00-fork.png)
2. Navigate to the created fork  
   ![Jump to Fork](img/01-jump-to-fork.png)
3. Press `.` on your keyboard to switch to the IDE
4. Erstellen Sie einen neuen Branch  
   ![Branch erzeugen](img/02-create-new-branch.png)
5. Give the branch a name  
   ![Branch Namen vergeben](img/03-branch-name.png)
6. Start writing  
   The contents of the guide are stored in the `/docs` folder. Simply change the content of an existing Markdown page (`.md` file) or create a new subchapter.
7. Preview the page  
   You can also view the final page on GitHub.

   Simply go to your repository's settings and then `Pages`.
   The link to it is as follows `https://github.com/YOURUSERNAME/ABAP-Leitfaden/settings/pages`.
   Select your branch you are currently working on and select the `docs` folder.
   After you have saved, it will take a few minutes until the page is accessible at the specified URL.
   From then on, the page will be recreated after every commit.  

   ![fork a github project](img/04-publish-branch.png)

### Development with Docker container

:point_right: Only Visual Studio Code and Docker are required  
:point_right: Instant preview of your changes

----

This is the easiest way to deploy your development environment in the shortest amount of time.
You receive a ready-to-use Debian container that is transparently used by Visual Studio Code.

#### Installation steps for Docker container

Install the following programs

- [Visual Studio Code](https://code.visualstudio.com/)
- [Dev Containers Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) (early Remote Containers Extension)
- [Docker](https://code.visualstudio.com/docs/remote/containers)

<details>
<summary>Install Docker on Windows in Linux (WSL)</summary>

##### Use Docker in WSL instead of Docker Desktop

Under Windows, Docker can also be installed in the Windows Subsystem for Linux (WSL) to, among other things: to circumvent the licensing issue of Docker Desktop.

To do this, the [WSL Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) must be installed in VS Code. One
Instructions for installing the WSL can be found at [Microsoft: Installing Linux on Windows with WSL](https://learn.microsoft.com/de-de/windows/wsl/install).
Docker [using these instructions](https://docs.docker.com/engine/install/ubuntu/) can then be installed.

Please also note the step for assigning the Docker user group in the [Post-Installations-Anleitung](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user).

Then look in the VS Code settings for the *Dev Containers > Execute in WSL* setting for the Dev Containers plugin and activate it:
![Setting: Dev Containers > Execute in WSL](img/01-dev-containers-wsl-setting.png)

You can then continue cloning the repository according to the normal instructions.
</details>

Clone the repository using the command *[Dev Containers: Clone Repository in Container Volume...](https://code.visualstudio.com/docs/remote/containers-advanced#_use-clone-repository-in-container-volume)*

This performs the following tasks:

- Cloning the repository in a container volume
- Creation of the Docker image
- Starting the Docker container and assigning the required ports
- Mounting the created container drive
- Installation of the required `npm` packages
- Installation of the required `ruby` according to

Now all you have to do is open the console in Visual Studio Code (it is connected to the running development container), navigate to the `docs` folder and start the development server:

```shell
cd docs
bundle exec jekyll serve --livereload
```

### Local installation

:point_right: Genau wie Docker Container  
:point_right: Complete control over development environment

----

#### Prerequisites for Windows

- <https://chocolatey.org/> installieren
- Install MSYS2 with Chocaletey  
  `choco install msys2` <https://chocolatey.org/packages/msys2>
- Ruby installieren  
  `choco install ruby` <https://chocolatey.org/packages/ruby>
- Build Toolchain aktualisieren:  
  `ridk install 3`
- See also [Test GitHub Pages website locally with Jekyll](https://docs.github.com/de/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)

#### Installation steps for Local Installation

- Make sure `ruby` 2.7 is installed on your system
- Clone the repository
- Go to the root folder of the site  
  `$ cd docs`
- Run the `bundle install` command in the terminal to install all necessary packages for Jekyll and GitHub Pages
- Start the local `gh-pages` instance, including web browser live reload

  ```shell
    bundle exec jekyll serve --livereload
    Configuration file: /Users/you/ABAP-Leitfaden/docs/_config.yml
                Source: /Users/you/ABAP-Leitfaden/docs
           Destination: /Users/you/ABAP-Leitfaden/docs/_site
     Incremental build: disabled. Enable with --incremental
          Generating...
           Jekyll Feed: Generating feed for posts
                        done in 0.233 seconds.
     Auto-regeneration: enabled for '/Users/you/ABAP-Leitfaden/docs'
     LiveReload address: http://127.0.0.1:35729
        Server address: http://127.0.0.1:4000/
      Server running... press ctrl-c to stop.
  ```

- Open the URL <http://localhost:4000> in your favorite web browser

## Mitwirken

All information about the development process and best practices for content creation can be found at [Mitwirken](contributing.md)

## Lizenzierung

This project uses CC BY 4.0 [Lizenz](LICENSE).
