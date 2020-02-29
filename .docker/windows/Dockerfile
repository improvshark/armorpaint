# escape=`
# Use the latest Windows Server Core image with .NET Framework 4.8.
FROM mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019

# Restore the default Windows shell for correct batch processing.
# SHELL ["cmd", "/S", "/C"]

RUN Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1')) 
RUN choco install -y git nodejs 7zip
RUN choco install -y vcredist140
# missing visual studio poop here
RUN & 'C:\Program Files\Git\bin\git.exe' clone --recursive https://github.com/armory3d/armorpaint
WORKDIR C:\armorpaint
RUN & 'C:\Program Files\nodejs\node.exe' .\Kromx\make -g direct3d11
RUN cd Kromx; & 'C:\Program Files\7-Zip\7z.exe' e .\v8\libraries\win32\release\v8_monolith.7z -o'.\v8\libraries\win32\release\'
RUN cd Kromx; & 'C:\Program Files\nodejs\node.exe' .\Kinc\make -g direct3d11 --compile

# Default to PowerShell if no other command specified.
CMD ["powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
