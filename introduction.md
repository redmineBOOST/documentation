---
layout: documentation
title: Introduction
id: introduction
---
# Introduction

**redmineBOOST** is a productivity increasing command line tool in daily work with Redmine.

Describe repetitive tasks in a domain-specific language within a **redmineBOOST** Process Description. Tasks such as creating or updating a Redmine issue are mapped as work items. Items can be instantiated, which results in executing the specific task e. g. `UpdateIssue{...}`, or read from Redmine by Queries e. g. `GetIssue(id=12)`. Items can be nested to express hierarchies, dependencies and relationships.

By creating the right Process Descriptions you can map business processes to complex Redmine issue structures in corporate specification, support standardized issue creation, provision new projects with default data, automate file uploads, manage user accounts and much more. Process Description files have the file extension `rbo` e. g. `create-issue.rbo`.

**redmineBOOST** uses the Redmine [REST API](https://www.redmine.org/projects/redmine/wiki/rest_api) to execute the Process Description and is limited to the available features of the REST API.

> Access to the [REST API](https://www.redmine.org/projects/redmine/wiki/rest_api) must be *activated* in the settings by a Redmine administrator.

> Redmine version *3.0.0* or higher is supported.

The tool is [.NET](https://dotnet.microsoft.com/en-us/) based and is available for Linux®, macOS® and Windows®.

The macOS release is currently distributed as an unsigned executable. To launch **redmineBOOST** you may have to follow the steps provided by Apple on how to [Open a Mac app from an unidentified developer](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616).

This is an example of a simple Process Description to create a Redmine issue in a project:
```
// create-issue.rbo
// Item to create a Redmine issue
Issue {
    // Set required project Property by quering the right project
    project: GetProject(identifier="AwesomeNewProject")
    
    // Set required tracker Property
    tracker: GetTracker(name="Feature")
    
    // Set a subject
    subject: "Awesome New Feature"
}
```

## <a name="commandLineInterface"></a> Command Line Interface

The command line interface is structured as follows:
```
$ rboost <command>|<process-file> [command-parameters]
```

`process-file`

**redmineBOOST** Process Description file to execute.

To simply execute a Process Description just provide the filename:
```
$ rboost create-issue.rbo
```

### Commands

`help`

Display help.

`config`

Enter interactive configuration mode.

`run <process-file>`

Executes specified **redmineBOOST** Process Description file. It's a longer version than just providing the Process Description file.

### Options

`-whatif`

Execute Process Description without mutating Redmine.

## <a name="configuration"></a> Configuration

Before **redmineBOOST** can be used it must be configured. Mainly, a text editor and the Redmine [REST API](https://www.redmine.org/projects/redmine/wiki/rest_api) Indentities need to be configured. The configuration will be stored in the current users home path in a `.rboostconfig` file.

To start the configuration execute the following command:
```
$ rboost config
```

The main config page will show up:
```
redmineBOOST - Configuration

[F1] Set external text editor
[F2] Manage Redmine Identities
```

### External Text Editor

Press `F1` key to configure an external text editor. The text editor is used for Items which require multiline user input.

```
redmineBOOST - Configuration

Set external text editor
[ENTER] Accept  [ESC] Cancel

Arguments can use placeholders to control the editor: ${Filepath}, ${Line}

File Path: _
Arguments:
```

In this page the full file path to the text editor must be provided. At first the `File Path` input is focused; enter file path to text editor. Press `ENTER` key to jump to `Arguments` input. With arguments you can provide the text editor with non default file opening arguments. Default behavior is that **redmineBOOST** will put the file to open behind the text editors file path when a file will be opened. By specifying `Arguments` this behavior can be refined for example to jump to a required line.

A text editor configuration for Visual Studio Code under Windows looks like this:

```
...
File Path: C:\Users\developer\AppData\Local\Programs\Microsoft VS Code\Code.exe
Arguments: --new-window --wait --goto ${Filepath}:${Line}
...
```

On macOS you have to point directly to the executable inside the application bundle. For Visual Studio Code the bundle is called Visual Studio Code.app but you have to set the file path to `/Applications/Visual Studio Code.app/Contents/MacOS/Electron`.


> It is important that the text editor is closed completely after the user has entered and saved its input, because **redmineBOOST** waits until the text editor process is finished to continue execution.

Press `ENTER` key to accept the text editor configuration.

### Manage Redmine Identities

Press `F2` key to configure Redmine Identities. The Identities are required so that **redmineBOOST** can connect to the Redmine [REST API](https://www.redmine.org/projects/redmine/wiki/rest_api).

> The Redmine [REST API](https://www.redmine.org/projects/redmine/wiki/rest_api) setting has to be enabled by an administrator.

```
redmineBOOST - Configuration

Manage Redmine Identities

Add, change or remove Redmine Identity
[↑/↓] Select identity  [A] Add identity  [ENTER] Change identity  [R] Remove identity
```

The Manage Redmine Identities page consists of a list which can be edited by adding (`A` key), changing (`ENTER` key with a selected identity) or removing (`R` key with a selected identity) identities. It is possible to have multiple Redmine Identities. Press `A` key to create the first Redmine Identity:

```
redmineBOOST - Configuration

Manage Redmine Identities

Add Redmine Identity
[ENTER] Accept  [ESC] Cancel

Label: _
URL:
Api key:
Allow Issue Assignment To Groups: [ ]
Maximum Attachment Size KB (default = 5120): 
```

A Redmine identity consists of a user defined Label, a Redmine provided API key, a Redmine URL, a flag indicating whether tickets can be assigned to groups or not, and the maximum attachment size. The Redmine API key can be found at: `https://<host>/redmine/my/account` where `host` must be replaced with the host of your Redmine. Input the Label, URL, API key data and the optional Redmine specific settings. Press `ENTER` key to move to the next editor or press `ENTER` key on the last editor to accept the Identity.

**redmineBOOST** is limited to the features provided by the [REST API](https://www.redmine.org/projects/redmine/wiki/rest_api). There is data which can't be accessed through the [REST API](https://www.redmine.org/projects/redmine/wiki/rest_api) but is required to validate specifics regarding Redmine Items like for instance how large the maximum attachment size of a file is or can an issue be assigned to a group.

> Ask your Redmine administrator to provide you with the correct configuration data so that **redmineBOOST** can *validate* your Process Descriptions to all details.

A possible Redmine Identity could look like this:

```
redmineBOOST - Configuration

Manage Redmine Identities

Add Redmine Identity
[ENTER] Accept  [ESC] Cancel

Label: CustomerRedmine
URL: https://mycompany/redmine
Api key: 65e5e5333e9390d27e304cc40c568683c7aaa5aa 
Allow Issue Assignment To Groups: [X]
Maximum Attachment Size KB (default = 5120): 
```

Back in the Manage Redmine Identities Page you will see one Identity entry in the list:

```
redmineBOOST - Configuration

Manage Redmine Identities

Add, change or remove Redmine Identity
[↑/↓] Select identity  [A] Add identity  [ENTER] Change identity  [R] Remove identity
CustomerRedmine: https://mycompany/redmine [65e5e5333e9390d27e304cc40c568683c7aaa5aa]
```

## <a name="runAProcess"></a> Run a Process

To execute a Process Description just provide the filename:
```
$ rboost <filename>
```

The main run page will show up:
```
Select Redmine Identity to run process on
[ESC] Quit  [ENTER] Use identity  [UP/DOWN] Select identity
CustomerRedmine: https://mycompany/redmine
```

Press the `UP` or `DOWN` arrows to select your Redmine identity.

To start the execution of the process description with the selected identity press `ENTER`.

## <a name="using-a-license"></a> Using a License

If you have a valid license in form of a license file `rboost.lic` you have to provide it for **redmineBOOST**. You can place the license file either in your home folder or directly in the directory where the executable file of **redmineBOOST** is located. **redmineBOOST** will always search first in the directory of the executable for a valid license. If this is unsuccessful **redmineBOOST** will search in the home folder for a valid license.