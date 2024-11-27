
# echo.bat

```
@echo off
setlocal

rem Configuration variables
set PYTHON_VERSION=3.10.0
set PYTHON_INSTALL_PATH=C:\Python\Python%PYTHON_VERSION%

rem Step 1: Download Python installer
echo Downloading Python %PYTHON_VERSION% installer...
curl -o python-installer.exe https://www.python.org/ftp/python/%PYTHON_VERSION%/python-%PYTHON_VERSION%-amd64.exe

rem Step 2: Install Python
echo Installing Python %PYTHON_VERSION%...
python-installer.exe /quiet InstallAllUsers=1 PrependPath=1 TargetDir="%PYTHON_INSTALL_PATH%"

rem Step 3: Add Python to PATH
echo Adding Python to PATH...
setx /M PATH "%PYTHON_INSTALL_PATH%;%PYTHON_INSTALL_PATH%\Scripts;%PATH%"

rem Step 4: Install keyboard module
echo Installing keyboard module...
pip install keyboard

rem Step 5: Clean up
echo Cleaning up...
del python-installer.exe

echo Installation complete.
pause

```

   This file is to be saved as .bat and executed with admin privs for creating the favorable env for strokes to run.
