---
id: r4lr6w6ow7m7sk02sak2iue
title: '160416'
desc: ''
updated: 1738730878119
created: 1722204259784
---
> ...my journey learning PowerShell (aka how I learned to stop worrying and just love Windows)

![alt text](<../assets/PowerShell editing with Visual Studio Code/image.png>)

[Ubunto explains the command | YouTube video tutorial](https://www.youtube.com/shorts/cGPkb7KX2H4?feature=share )

[PowerShell](https://learn.microsoft.com/powershell/) is a task-based command-line shell and scripting language built on [.NET](https://learn.microsoft.com/dotnet) that provides a powerful toolset for administrators on any platform. ^8xy95qfmn3ws

The Microsoft [PowerShell](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell) extension for Visual Studio Code (VS Code) provides rich language support and capabilities such as syntax completions, definition tracking, and linting for PowerShell. The extension should work anywhere VS Code itself and PowerShell Core 7.2 or higher is [supported](https://docs.microsoft.com/en-us/powershell/scripting/powershell-support-lifecycle). For Windows PowerShell, only version 5.1 is supported and only on a best-effort basis. PowerShell Core 6, 7.0, and 7.1 have reached end-of-support. We test the following configurations:

-   **Windows Server 2022** with Windows PowerShell 5.1 and PowerShell 7.2
-   **Windows Server 2019** with Windows PowerShell 5.1 and PowerShell 7.2
-   **macOS 11** with PowerShell Core 7.2
-   **Ubuntu 20.04** with PowerShell Core 7.2

## [Installing the PowerShell extension](https://code.visualstudio.com/docs/languages/powershell#_installing-the-powershell-extension)

The PowerShell extension can be installed from the Visual Studio Code Marketplace by clicking the [Install Button](vscode:extension/ms-vscode.PowerShell). You can also install the PowerShell extension from within VS Code by opening the **Extensions** view with keyboard shortcut Ctrl+Shift+X, typing _PowerShell_, and selecting the PowerShell extension:

![PowerShell extension](../../../../notes/PowerShell editing with Visual Studio Code/PowerShellExtension.png)

## [Major features](https://code.visualstudio.com/docs/languages/powershell#_major-features)

-   [Syntax highlighting](https://github.com/PowerShell/EditorSyntax)
-   Advanced built-in [code snippets](https://code.visualstudio.com/docs/editor/userdefinedsnippets)
-   [IntelliSense](https://code.visualstudio.com/docs/editor/intellisense) for cmdlets and more
-   [Problems](https://code.visualstudio.com/docs/getstarted/tips-and-tricks#_errors-and-warnings) reported by [PowerShell Script Analyzer](http://github.com/PowerShell/PSScriptAnalyzer)
-   [Go to Definition](https://code.visualstudio.com/docs/editor/editingevolved#_go-to-definition) of cmdlets, variables, classes and more
-   [Find References](https://code.visualstudio.com/docs/editor/editingevolved#_reference-information) of cmdlets, variables, classes and more
-   Document and Workspace [Symbol Navigation](https://code.visualstudio.com/docs/editor/editingevolved#_open-symbol-by-name)
-   Symbol-based [Outline View](https://code.visualstudio.com/docs/getstarted/userinterface#_outline-view)
-   Run selected PowerShell code in current terminal using F8
-   Launch online help for the symbol under the cursor using Ctrl + F1
-   PowerShell [Debugger](https://learn.microsoft.com/powershell/scripting/dev-cross-plat/vscode/using-vscode#debugging-with-visual-studio-code) integration
-   An Extension Terminal that can interact with the debugger (try `Set-PSBreakpoint`!)
-   PowerShell ISE theme findable in the [theme picker](https://code.visualstudio.com/docs/getstarted/themes)
-   Also try ISE mode using Ctrl+Shift+P then search for "Enable ISE Mode"

### [Debugging](https://code.visualstudio.com/docs/languages/powershell#_debugging)

The PowerShell extension uses the built-in [debugging interface](https://code.visualstudio.com/docs/editor/debugging) of VS Code to allow for debugging of PowerShell scripts and modules. For more information about debugging PowerShell, see [Using VS Code](https://learn.microsoft.com/powershell/scripting/dev-cross-plat/vscode/using-vscode#debugging-with-visual-studio-code).

### [Multi-version support](https://code.visualstudio.com/docs/languages/powershell#_multiversion-support)

You can configure the PowerShell extension to use any supported version of PowerShell installed on your machine by following [these instructions](https://learn.microsoft.com/powershell/scripting/dev-cross-plat/vscode/using-vscode#choosing-a-version-of-powershell-to-use-with-the-extension).

Or run the **PowerShell: Show Session Menu** command from the Command Palette (Ctrl+Shift+P).

### [CodeLens support](https://code.visualstudio.com/docs/languages/powershell#_codelens-support)

CodeLenses are a VS Code feature to provide actionable, contextual information that's displayed within the source code.

CodeLens features include:

-   Pester **Run tests** and **Debug tests**.

    ![Pester CodeLens Integration](../../../../notes/PowerShell editing with Visual Studio Code/pesterCodeLens.png)

-   Pester symbol support

    ![CodeLens Pester Symbol Support](../../../../notes/PowerShell editing with Visual Studio Code/codeLensPesterSymbol.gif)

-   Function, variable, class, and other symbol references

    CodeLens reference support shows the number of times a symbol is referenced within your code and allows you to jump to specific references.

    ![CodeLens Function Reference Support](../../../../notes/PowerShell editing with Visual Studio Code/codeLensFuncRef.gif)


### [PSScriptAnalyzer integration](https://code.visualstudio.com/docs/languages/powershell#_psscriptanalyzer-integration)

[PSScriptAnalyzer](https://learn.microsoft.com/powershell/utility-modules/psscriptanalyzer/overview) is a PowerShell module that provides a static source code checker for modules and scripts. **PSScriptAnalyzer** has rules that verify the quality of PowerShell code. These rules are based on PowerShell best practices identified by the PowerShell Team and the community. **PSScriptAnalyzer** generates diagnostic records (errors and warnings) to inform users about potential code defects and suggests possible solutions for improvements.

The PowerShell extension includes **PSScriptAnalyzer** by default, and automatically performs analysis on PowerShell script files you edit in VS Code.

**PSScriptAnalyzer** comes with a collection of built-in rules that check various aspects of PowerShell source code such as presence of uninitialized variables, usage of **PSCredential** type, usage of `Invoke-Expression`, and others. The module also allows you to include or exclude specific rules.

To disable **PSScriptAnalyzer**, open your settings (Ctrl+,), browse **Extensions**, select the **PowerShell** extension, and deselect the checkbox for **Script Analysis: Enable** (`powershell.scriptAnalysis.enable`).

![PSScriptAnalyzer Settings](../../../../notes/PowerShell editing with Visual Studio Code/pssaExtensionSetting.png)

**PSScriptAnalyzer** also provides code formatting. You can invoke automatic document formatting with the **Format Document** command or the (Shift+Alt+F) keyboard shortcut.

### [Pester integration](https://code.visualstudio.com/docs/languages/powershell#_pester-integration)

[Pester](https://pester.dev/) is a framework for running unit tests to execute and Windows PowerShell 5.1 comes with **Pester** 3.40 preinstalled. To update **Pester** or to install the latest version on other platforms, follow the [Pester installation instructions](https://pester.dev/docs/introduction/installation).

### [Plaster integration](https://code.visualstudio.com/docs/languages/powershell#_plaster-integration)

[Plaster](https://github.com/PowerShell/Plaster) is a template-based file and project generator written in PowerShell. Its purpose is to streamline the creation of PowerShell module projects, Pester tests, DSC Configurations and more.

The PowerShell extension allows the creation of new Plaster projects using the **PowerShell: Create New Project from Plaster Template** command from the Command Palette (Ctrl+Shift+P).

![Plaster Project](../../../../notes/PowerShell editing with Visual Studio Code/cpPlasterCommand.png)

## [PowerShell extension settings](https://code.visualstudio.com/docs/languages/powershell#_powershell-extension-settings)

You can customize VS Code [settings](https://code.visualstudio.com/docs/getstarted/settings) from the **File** > **Preferences** > **Settings** menu item.

You can also select the gear icon located in the lower left corner of the Activity Bar.

![codeGear](../../../../notes/PowerShell editing with Visual Studio Code/codeGear.png)

You can also use the keyboard shortcut Ctrl+, to open your settings. You can still open the `settings.json` file using **Preferences: Open User Settings (JSON)** command from the Command Palette (Ctrl+Shift+P) or by changing the default settings editor with the `"workbench.settings.editor"` setting.

Go to [User and Workspace settings](https://code.visualstudio.com/docs/getstarted/settings) for more information on configuring VS Code settings.

### [Types.ps1xml and Format.ps1xml files](https://code.visualstudio.com/docs/languages/powershell#_typesps1xml-and-formatps1xml-files)

PowerShell `.ps1xml` files are used to extend the type system and define output formatting. For more information on these files, see the official PowerShell documentation on [Types.ps1xml](https://learn.microsoft.com/powershell/module/microsoft.powershell.core/about/about_types.ps1xml) and [Format.ps1xml](https://learn.microsoft.com/powershell/module/microsoft.powershell.core/about/about_format.ps1xml). You can get IntelliSense features when authoring `.ps1xml` files by installing the [XML extension by Red Hat](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-xml). After installing, add this configuration to your user settings:

```
<span><span>"xml.fileAssociations"</span><span>: [</span></span>
<span><span>  {</span></span>
<span><span>    </span><span>"systemId"</span><span>: </span><span>"https://raw.githubusercontent.com/PowerShell/PowerShell/master/src/Schemas/Format.xsd"</span><span>,</span></span>
<span><span>    </span><span>"pattern"</span><span>: </span><span>"**/*.Format.ps1xml"</span></span>
<span><span>  },</span></span>
<span><span>  {</span></span>
<span><span>    </span><span>"systemId"</span><span>: </span><span>"https://raw.githubusercontent.com/PowerShell/PowerShell/master/src/Schemas/Types.xsd"</span><span>,</span></span>
<span><span>    </span><span>"pattern"</span><span>: </span><span>"**/*.Types.ps1xml"</span></span>
<span><span>  }</span></span>
<span><span>]</span></span>
<span></span>
```

This configuration tells the XML extension to use the official XML schemas from the PowerShell repository for all `.ps1xml` files. Configuring these schemas enables the following features in `ps1xml` files:

-   Syntax error reporting
-   Schema validation
-   Tag and attribute completion
-   Autoclose tags
-   Symbol highlighting
-   Document folding
-   Document symbols and outline
-   Renaming support
-   Document formatting

## [Example scripts](https://code.visualstudio.com/docs/languages/powershell#_example-scripts)

Example scripts are included with the extension and can be found at the following path.

`~/.vscode/extensions/ms-vscode.PowerShell-<version>/examples`

To open or view the examples in VS Code, run the following from your PowerShell command prompt:

```
<span><span>code (</span><span>Get-ChildItem</span><span> ~\.vscode\extensions\ms</span><span>-</span><span>vscode.PowerShell</span><span>-*</span><span>\examples)[</span><span>-1</span><span>]</span></span>
<span></span>
```

You can also open the examples from the Command Palette (Ctrl+Shift+P) with the **PowerShell: Open Examples Folder** command.

![Open PowerShell Examples](../../../../notes/PowerShell editing with Visual Studio Code/pwshExamples.png)

## [Additional resources](https://code.visualstudio.com/docs/languages/powershell#_additional-resources)

There are more detailed articles in the PowerShell documentation. Start with [Using VS Code](https://learn.microsoft.com/powershell/scripting/dev-cross-plat/vscode/using-vscode).

Check out the [troubleshooting guide](https://github.com/PowerShell/vscode-powershell/blob/main/docs/troubleshooting.md#troubleshooting-powershell-extension-issues) for answers to common questions.

For more information on debugging, check out the _Hey, Scripting Guy!_ two-part blog post series written by [@keithHill](https://twitter.com/r_keith_hill) on debugging with the PowerShell extension:

-   [Debugging PowerShell script in Visual Studio Code - Part 1](https://devblogs.microsoft.com/scripting/debugging-powershell-script-in-visual-studio-code-part-1/)
-   [Debugging PowerShell script in Visual Studio Code - Part 2](https://devblogs.microsoft.com/scripting/debugging-powershell-script-in-visual-studio-code-part-2/)

## [Testing new features and providing feedback](https://code.visualstudio.com/docs/languages/powershell#_testing-new-features-and-providing-feedback)

We would encourage you to try the _pre-release_ version whenever possible. When a _Pre-Release_ is available, it can be installed from the marketplace using the **Switch to Pre-Release Version** button. You can switch back to the stable version of the extension by using the **Switch to Release Version** button that will appear. You can also downgrade to other versions of the extension using the arrow next to the **Uninstall** button and choosing **Install Another Version...**.

![Screenshot showing the button to switch to a pre-release version.](../../../../notes/PowerShell editing with Visual Studio Code/prerelease-switch.png)

If you find a bug, [open an issue](https://github.com/PowerShell/vscode-powershell/issues/new/choose) and revert to the stable version while we fix it.

07/11/2023


