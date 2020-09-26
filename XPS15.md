# Dell XPS-15 9570

Productsupport:  
<https://www.dell.com/support/home/de-de/product-support/product/xps-15-9570-laptop/overview>

This repository contains all important configuration files of the windows system. To get them in the repostitory folder structure, we are using windows hardlinks. The local repository is located at: `%USERPROFILE%\Git\xps-15\`.

## Table of contents

- [Hardlinks](#hardlinks)
  - [Creating](#creating-hardlinks)
  - [Listing](#listing-hardlinks)
- [Configuration and script files](#configuration-and-script-files)
  - [Visual Studio Code](#visual-studio-code)
  - [Windows Terminal](#windows-terminal-configuration)
  - [SQLBase Server](#sqlbase-server)
  - [Diestein](#diestein)
  - [Signum](#signum)

## Hardlinks

Here you find a short documentation how to create and list hardlinks. You can find more information about hardlinks on [wikipedia](https://en.wikipedia.org/wiki/Hard_link).

[Back to table of contents](#table-of-contents)

### Creating hardlinks

Navigate to the repository root or subdirectory and create an hardlink.

#### Windows Command

    mklink /H {filename in git} {path to original filename}

#### Windows Powershell

    New-Item -ItemType HardLink -Name {filename in git} -Target {path to original filename}

#### Documentation

| mklink syntax           | PowerShell equivalent                                       |
| ----------------------- | ----------------------------------------------------------- |
| `mklink Link Target`    | `New-Item -ItemType SymbolicLink -Name Link -Target Target` |
| `mklink /D Link Target` | `New-Item -ItemType SymbolicLink -Name Link -Target Target` |
| `mklink /H Link Target` | `New-Item -ItemType HardLink -Name Link -Target Target`     |
| `mklink /J Link Target` | `New-Item -ItemType Junction -Name Link -Target Target`     |

[Back to table of contents](#table-of-contents)

### Listing hardlinks

List all symlinks, hardlinks and junctions recusive from current directory. Use this command in the root folder of the repository to check all hardlinks.

#### Windows Powershell

    dir '.' -recurse -force | ?{$_.LinkType} | select FullName,LinkType,Target

#### Example output

    FullName                                       LinkType Target
    --------                                       -------- ------
    %USERPROFILE%\Git\xps-15\Roga-Diverses.sql     HardLink {C:\SQLBase\Roga-Diverses.sql}
    %USERPROFILE%\Git\xps-15\Roga-MWST-16-2020.sql HardLink {C:\SQLBase\Roga-MWST-16-2020.sql}
    %USERPROFILE%\Git\xps-15\Roga-Repair-DB.sql    HardLink {C:\SQLBase\Roga-Repair-DB.sql}

[Back to table of contents](#table-of-contents)

## Configuration and script files

Here you find a short documentation of all config and script files added to the repository. Used file formats:

- [SQL](https://en.wikipedia.org/wiki/SQL), [SQL syntax](https://en.wikipedia.org/wiki/SQL_syntax)
- [INI](https://en.wikipedia.org/wiki/INI_file)
- [JSON](https://en.wikipedia.org/wiki/JSON)

[Back to table of contents](#table-of-contents)

### Visual Studio Code

Documentation: <https://code.visualstudio.com/docs>

| state       | file location                                       |
| ----------- | --------------------------------------------------- |
| original    | `%LOCALAPPDATA%\Roaming\Code\User\settings.json`    |
| hardlink    | `%USERPROFILE%\Git\xps-15\vs-code-settings.json`    |
|             |                                                     |
| original    | `%LOCALAPPDATA%\Roaming\Code\User\keybindings.json` |
| hardlink    | `%USERPROFILE%\Git\xps-15\vs-code-keybindings.json` |
| description | Visual Studio Code user settings                    |

[Back to table of contents](#table-of-contents)

### Windows Terminal configuration

Documentation: <https://docs.microsoft.com/de-de/windows/terminal/>

| state       | file location                                                                                    |
| ----------- | ------------------------------------------------------------------------------------------------ |
| original    | `%LOCALAPPDATA%\Local\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState\settings.json` |
| hardlink    | `%USERPROFILE%\Git\xps-15\windows-terminal-settings.jsonc`                                       |
| description | Windows Terminal user settings                                                                   |

[Back to table of contents](#table-of-contents)

### SQLBase Server

<https://www.opentext.com/products-and-solutions/products/specialty-technologies/opentext-gupta-development-tools-databases/opentext-gupta-sqlbase>

| original                        | hardlink                                      | #   |
| ------------------------------- | --------------------------------------------- | --- |
| `C:\SQLBase\sql.ini`            | `%USERPROFILE%\Git\xps-15\sql.ini`            | 1   |
| `C:\SQLBase\Roga-Repair-DB.sql` | `%USERPROFILE%\Git\xps-15\Roga-Repair-DB.sql` | 2   |

Description:

1. SQLBase settings
2. Repair corrupted database. If the OS crashes, the database und logfiles can be out of syn and the application will not start. This SQL script repaires the database.

[Back to table of contents](#table-of-contents)

### Diestein

<http://www.dietrich-software.de/>  
This application uses the [SQLBase server](#sqlbase-server)

| original                              | hardlink                                         | #   |
| ------------------------------------- | ------------------------------------------------ | --- |
| `%LOCALAPPDATA%\Windows\DIESTEIN.ini` | `%USERPROFILE%\Git\xps-15\diestein.ini`          | 1   |
| `C:\Dscs\Reports\REPIND.SQL`          | `%USERPROFILE%\Git\xps-15\Roga-Reports.sql`      | 2   |
| `C:\SQLBase\Roga-MWST-16-2020.sql`    | `%USERPROFILE%\Git\xps-15\Roga-MWST-16-2020.sql` | 3   |
| `C:\SQLBase\Roga-Diverses.sql`        | `%USERPROFILE%\Git\xps-15\Roga-Diverses.sql`     | 4   |

Description:

1. Diestein settings
2. Customizing reports. This SQL script copies existing reports with new names. So each report can have a different predefined printer. Some existing reports will be renamed too.
3. Changing tax between 2020-07-01 and 2020-12-31. All customers have a predefined tax value. This value must be set to 16 between 2020-07-01 and 2020-12-31. Starting 2021-01-01 the value must be 19 again. This SQL Script will do the job.
4. Some random test SQL statements.

[Back to table of contents](#table-of-contents)

### Signum

<http://www.zss.de/>

| original                                   | hardlink                                        | #   |
| ------------------------------------------ | ----------------------------------------------- | --- |
| `C:\Stein\Signum32.INI`                    | `%USERPROFILE%\Git\xps-15\Signum32.INI`         | 1   |
| `C:\Stein\SignumNext.INI`                  | `%USERPROFILE%\Git\xps-15\SignumNext.INI`       | 2   |
| `C:\Stein\SignumNext3D.INI`                | `%USERPROFILE%\Git\xps-15\SignumNext3D.INI`     | 3   |
| `C:\Stein\SignumNext\Export\ExportDef.INI` | `%USERPROFILE%\Git\xps-15\Signum-ExportDef.INI` | 4   |

Description:

1. Global settings
2. SignumNext settings
3. SignumNext3d settings
4. SignumNext export settings

[Back to table of contents](#table-of-contents)
