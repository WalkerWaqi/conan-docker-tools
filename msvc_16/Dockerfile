FROM mcr.microsoft.com/windows/servercore:20H2

LABEL maintainer="Walker Waqi <walkerwaqi@qq.com>"

SHELL ["powershell.exe", "-ExecutionPolicy", "Bypass", "-Command"]

ENV chocolateyUseWindowsCompression=false \
    PYTHONIOENCODING=UTF-8

RUN iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1')); \
    choco install --no-progress --yes git; \
    choco install --no-progress --yes git-lfs; \
    choco install --no-progress --yes svn; \
    choco install --no-progress --yes cmake --installargs 'ADD_CMAKE_TO_PATH=System'; \
    choco install --no-progress --yes python3

RUN choco install --no-progress --yes visualstudio2019buildtools --version=16.10.4.0
RUN choco install --no-progress --yes visualstudio2019-workload-vctools --version=1.0.1
RUN choco install --no-progress --yes visualstudio2019-workload-manageddesktop --version=1.0.2

RUN python -m pip install win-unicode-console conan conan_package_tools --upgrade --force-reinstall --no-cache

RUN conan profile new default --detect; \
    conan remote clean; \
    conan remote add myconan http://172.27.128.202:38081/artifactory/api/conan/conan; \
    conan remote add bincrafters https://bincrafters.jfrog.io/artifactory/api/conan/conan-legacy-bincrafters; \
    conan remote add conancenter https://center.conan.io; \
    conan remote add conan-center https://conan.bintray.com

WORKDIR "C:/Users/ContainerAdministrator"

ENTRYPOINT ["C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\BuildTools\\Common7\\Tools\\VsDevCmd.bat", "&&", "powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
