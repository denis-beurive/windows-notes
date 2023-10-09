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

## Get/set the keyboard layout

Get a textual description:

    Get-WinUserLanguageList

Or

Get a numerical ID:

    (Get-Culture).keyboardLayoutID

> This ID is listed [here](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/windows-language-pack-default-values?view=windows-11).

Set the layout:

    Set-WinUserLanguageList -LanguageList fr-FR

## Show environment variables

```Batchfile
set
```

> * System: `reg query "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment"`
> * User: `reg query HKEY_CURRENT_USER\Environment`

## UNIX "find" equivalent

```Batchfile
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

```Batchfile
rmdir <directory path> /s /q
```

## Delete all files excepts certain files

```Batchfile
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

```Batchfile
echo %errorlevel%
```

> Unix equivalent: `echo $?`

## Load a password from a file

```Batchfile
SET /p PASSWORD=<password.txt
echo %PASSWORD%
```

## Get the path to this script

```Batchfile
SET PWD=%~dp0
```

> `PWD` is the path to the executed `.BAT` script's directory.

## MSDOS colors

![](images/dos-colors.png)

Usage:

```Batchfile
IF not exist src\ (
  echo %WARN%WARNING: no sub direcory "src" found under GOPATH.%END_WARN%
)
```

> See: [https://gist.githubusercontent.com/mlocati/fdabcaeb8071d5c75a2d51712db24011/raw/b710612d6320df7e146508094e84b92b34c77d48/win10colors.cmd](https://gist.githubusercontent.com/mlocati/fdabcaeb8071d5c75a2d51712db24011/raw/b710612d6320df7e146508094e84b92b34c77d48/win10colors.cmd)

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



