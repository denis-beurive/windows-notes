# Windows note

## Find the OS encoding

Execute the code below under PowerShell:

```
C:\Users\dbeurive> Get-WinSystemLocale | Select-Object Name, DisplayName, 
>>                 @{ n='OEMCP'; e={ $_.TextInfo.OemCodePage } }, 
>>                 @{ n='ACP';   e={ $_.TextInfo.AnsiCodePage } } 
```
 
Result:

```
Name  DisplayName       OEMCP  ACP 
----  -----------       -----  --- 
fr-FR français (France)   850 1252 
```
 
List of code pages: [https://docs.microsoft.com/fr-fr/windows/win32/intl/code-page-identifiers](https://docs.microsoft.com/fr-fr/windows/win32/intl/code-page-identifiers)

* **OEMCP** (OemCodePage) represents the code page used for console applications (DOS).
* **ACP** (AnsiCodePage) represents the code page used for graphical applications.

GUI applications use the following code page:

`1252` => `windows-1252` aka `ANSI Latin 1; Europe occidentale (Windows)`

## Show environment variables

```
set
```

> * System: `reg query "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment"`
> * User: `reg query HKEY_CURRENT_USER\Environment`

## UNIX "find" equivalent

```
dir /s /b
dir /s /b "%HOMEPATH%"
dir /s /b "%HOMEPATH%" | findstr .html
dir /s /b "%HOMEPATH%" | findstr /i .html
```

## UNIX "cat" equivalent

```
type <file name>
```

## UNIX "rm -rf" equivalent

```
rmdir <directory path> /s /q
```

## Delete all files excepts certain files

```
REM Delete all files except ".gitignore" and "clean.bat".

echo off
REM Prevent unexpected behaviour that may lead to the removal of all files
REM including the ones that we want to keep.
set PWD=%~dp0
cd %PWD%

for %%i in (*) do (
    if not "%%i" == ".gitignore" (
         if not "%%i" == "clean.bat" (
            echo "Remove %%i"
            del "%%i"
         )
    )
)
```

## Get the return value of a command

```
echo %errorlevel%
```

> Unix equivalent: `echo $?`

## Load a password from a file

```
SET /p PASSWORD=<password.txt
echo %PASSWORD%
```

## Get the path to this script

```
SET PWD=%~dp0
```

> `PWD` is the path to a directory.

## OpenSSH for Windows

* OpenSSH for Windows: see [this link](http://sshwindows.sourceforge.net/)
* Default installation directory: `"%PROGRAMFILES(X86)%\OpenSSH"`
* Path to the SSH configuration files: `"%HOMEPATH%\.ssh"`

> Useful [link](https://www.thewindowsclub.com/system-user-environment-variables-windows) for Windows environment variables.

> Windows comes with OpenSSH preinstalled:
> 
> ```
> C:>where ssh
> C:\Windows\System32\OpenSSH\ssh.exe
> ```

## List open ports with the names of the associated process

```
netstat -aonb
```



