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



