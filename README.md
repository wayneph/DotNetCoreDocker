# To understand docker containers on Linux with C# and DOT NET CORE -- Follow this readme #


# Project is an intro for: #
0. Installing DotNetCore on LINUX (UBUNTU 2004)
1. Creating a DotNet Core c# app - Running and Publishing such an app
2. Create & name the Docker Image - with THE ## DockerFile ## definitions
3. Create the Container off the image
4. Manage Container Basics

## 0. Installing  ##
### 0.0 IDE ###
    - I assume you have an IDE installed.
    - VScode for Linux
    https://linuxhint.com/install_use_vs_code_ubuntu/#:~:text=To%20install%20Visual%20Studio%20Code%20through%20GUI%2C%20Firstly%2C%20open%20Software,it%20to%20start%20the%20process.
### 0.1 DOCKER ###
    - Install Docker .. here .. (UBUNTU 20.04)
    https://docs.docker.com/engine/install/ubuntu/
## 1. Create App  ##
### 1.1 DOT NET CORE ###
    - Install the linux DOT NET CORE SDK (v6.0.300 here) (I suggest the MANUAL installation)
    https://docs.microsoft.com/en-gb/dotnet/core/install/linux-scripted-manual#manual-install
### 1.2 Create DOT NET CORE app ###
    - I strongly suggest creating this manually since it creates the C# coding environment for you.
    - I.e. -- Do not just download this code repo
### 1.3 MANUAL CREATION OF PROJECT ###
    - create as directory for all C# dev (mine was in ~/dev/sharp)
    - enter the directory and..
        - build DOT NET CORE APP scaffold with Bash..
            -   $> dotnet new console -o App -n DotNet.Docker
                    --- a console app called "App" with name "DotNet.Docker"
        - access & study the created code using command
            -   $> code .
        - re-access the bash in the App directory & run the app with
            -   $> dotnet run
                    -- see "hello World" or similar
        - Change the code to reflect what is in this repo's Program.cs.
            - re-run & it should output a counted app.  (This is important for seeing running containers)
        - For a Docker image, it must FIRST be published. To publish the app, run the following command:
            - dotnet publish -c Release
## 2. Create & name Docker Image and Create & name the Container  ##
### 2.1 Create Dockerfile ###
    -  When building the image it does od of a manifest.  Docker looks for & must find a file :: Dockerfile in the root of the App.
    -  Crate the file as per this repo Dockerfile
### 2.2 Build Image ###
    - @ the command line enter
        -$> docker build -t counter-image -f Dockerfile .
        (Note:  The "." is important as it is the bash entry point for the image)
        (Note:  The "-t" is the image name required)
        (Note:  The "-f" is the Dockerfile Definition directive)
### 2.3 Validate the  Image build ###
    - @ the command line enter
        -$> docker images
        (You will see the image definition with the name defined ion 2.2 above = "counter-image")
## 3 Create the Container off the image ##
### 3.1 Create the container ###
    - @ the command line enter
        -$> docker create --name core-counter counter-image
        (Will create a container called "core-counter" off the image "counter-image")
        -$> docker ps -a
        (Will list all the possible process containers -  the "-a" means all - not only those running )
        -$> docker create --name core-counter counter-image
### 3.2 Run the Container ###
    - @ the command line enter
        -$> docker start core-counter
        -$> docker attach --sig-proxy=false core-counter
        (Attach to the container - the --sig-proxy-false just means that Keystrokes at the OS level such  Ctrl+c will be ignored while running)
## 4 Container Basics ##
    - @ the command line enter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
        -$> docker start core-counter
        (starts a container called "core-counter")
        -$> docker stop core-counter
        (Will stop up the container called "core-counter")
        -$> docker ps
        (Will list the RUNNING containers but not "core-counter" - a blank list means no running containers)
        -$> docker start core-counter
        -$> docker attach --sig-proxy=false core-counter
        (Attach to the container - the --sig-proxy-false just means that Keystrokes at the OS level such  Ctrl+c will be ignored while running)
        (If you hit Ctrl+c the output stops but the container is still running)
        -$> docker attach --sig-proxy=false core-counter
        (You should see that the "Counter" did not restart but continued)
# https://raw.githubusercontent.com/sangam14/dockercheatsheets/master/dockercheatsheet8.png #

Thank you. Comments welcome to be sent to :: you may contact me [at] wayne.h.philip@gmail.com

