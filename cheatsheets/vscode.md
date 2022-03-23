### My VS Code `settings.json`
```json
{
    "workbench.colorTheme": "Monokai",
    "workbench.iconTheme": "material-icon-theme",
    "editor.fontSize": 16,
    "editor.renderWhitespace": "boundary",
    "editor.wordWrapColumn": 111,
    "path-intellisense.showHiddenFiles": true,
    "code-runner.fileDirectoryAsCwd": true,
    "code-runner.ignoreSelection": true,
    "gitlens.currentLine.scrollable": false,
    "gitlens.hovers.avatars": false,
    "gitlens.hovers.annotations.enabled": false,
    "gitlens.hovers.annotations.details": false,
    "gitlens.hovers.enabled": false,
    "gitlens.liveshare.allowGuestAccess": false,
    "gitlens.mode.statusBar.enabled": false,
    "gitlens.showWhatsNewAfterUpgrades": false,
    "git.allowForcePush": true,
    "git.autofetch": true,
    "git.autofetchPeriod": 1800,
    "git.postCommitCommand": "push",
    "python.pythonPath": "/usr/bin/python",
    "code-runner.saveFileBeforeRun": true,
    "window.title": "${activeEditorLong}${separator}${rootName}",
    "editor.renderLineHighlight": "gutter",
    "editor.minimap.enabled": false,
    "explorer.confirmDelete": false,
    "breadcrumbs.enabled": true,
    "breadcrumbs.filePath": "last",
    "git.enableSmartCommit": true,
    "code-runner.executorMapByGlob": {
        "*.f90": "cd $dir && gfortran $fileName -o $fileNameWithoutExt.out && $dir$fileNameWithoutExt.out",
        "*.f": "cd $dir && gfortran $fileName -o $fileNameWithoutExt.out && $dir$fileNameWithoutExt.out",
        "*.F90": "cd $dir && gfortran $fileName -o $fileNameWithoutExt.out && $dir$fileNameWithoutExt.out",
        "*.plt": "cd $dir && gnuplot $fileName ",
        "*.eps": "cd $dir && epspdf $fileName "
    },
    "code-runner.executorMap": {
        "fortran": "cd $dir && gfortran $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt"
    },
    "editor.renderControlCharacters": false,
    "explorer.confirmDragAndDrop": false,
    "files.exclude": {
        "**/*.pyc":true,
        "**/*.mod":true,
        "**/*.out":true,
        "**/__pycache__": true,
        "**/*.so": true,
        ".vscode":true,
        ".ipynb_checkpoints":true
    },
    "editor.fontLigatures": true,
    "fortran-ls.enableCodeActions": true,
    "fortran-ls.hoverSignature": true,
    "fortran-ls.lowercaseIntrinsics": true,
    "fortran-ls.variableHover": true,
    "fortran-ls.autocompletePrefix": true,
    "scm.defaultViewMode": "tree",
    "git.showPushSuccessNotification": true,
    "python.autoComplete.addBrackets": true,
    "code-runner.clearPreviousOutput": true,
    "gitlens.views.repositories.files.layout": "tree",
    "python.analysis.memory.keepLibraryAst": true,
    "fortran-ls.notifyInit": true,
    "files.associations": {
        "*.config": "ini"
    },
    "gitlens.gitCommands.closeOnFocusOut": true,
    "python.linting.pylintUseMinimalCheckers": false,
    "python.linting.pylintEnabled": false,
    "python.linting.flake8Enabled": true,
    "python.linting.maxNumberOfProblems": 20,
    "python.linting.flake8Args": [
        "--ignore=E12,E2,E7,W3,W2,E3,E4,F401",
        "--max-line-length=132",
        "--max-complexity=20"
    ],
    "javascript.format.insertSpaceAfterOpeningAndBeforeClosingJsxExpressionBraces": true,
    "editor.find.seedSearchStringFromSelection": false,
    "search.exclude": {
        "**/*.min.*": true
    },
    "window.enableExperimentalProxyLoginDialog": true,
    "jupyter.askForKernelRestart": false,
    "jupyter.disableJupyterAutoStart": true,
    "gitlens.currentLine.pullRequests.enabled": false,
    "gitlens.hovers.currentLine.enabled": false,
    "gitlens.views.lineHistory.avatars": false,
    "gitlens.blame.highlight.locations": [
        "overview"
    ],
    "gitlens.hovers.annotations.changes": false,
    "gitlens.hovers.changesDiff": "hunk",
    "gitlens.hovers.currentLine.changes": false,
    "gitlens.hovers.currentLine.details": false,
    "gitlens.codeLens.recentChange.enabled": false,
    "gitlens.codeLens.authors.enabled": false,
    "gitlens.hovers.currentLine.over": "line",
    "gitlens.currentLine.enabled": false,
    "gitlens.statusBar.enabled": false,
    "liveServer.settings.donotShowInfoMsg": true,
    "workbench.editorAssociations": [
        {
            "viewType": "jupyter.notebook.ipynb",
            "filenamePattern": "*.ipynb"
        }
    ],
    "terminal.integrated.commandsToSkipShell": [
        "language-julia.interrupt"
    ],
    "julia.enableTelemetry": true,
    "julia.execution.codeInREPL": true,
    "C_Cpp.updateChannel": "Insiders",
    "julia.enableCrashReporter": true,
    "python.showStartPage": false,
    "explorer.sortOrder": "modified",
    "cmake.configureOnOpen": false,
    "fortran.linterExtraArgs": [
        "-I usr/lib/grub/i386-pc/mpi.mod"
    ],
    "files.autoSave": "afterDelay",
    "[dart]": {
        "editor.formatOnSave": true,
        "editor.formatOnType": true,
        "editor.selectionHighlight": false,
        "editor.suggest.snippetsPreventQuickSuggestions": false,
        "editor.suggestSelection": "first",
        "editor.tabCompletion": "onlySnippets",
        "editor.wordBasedSuggestions": false
    },
    "diffEditor.ignoreTrimWhitespace": false,
    "dart.previewFlutterUiGuides": true,
    "dart.previewFlutterUiGuidesCustomTracking": true,
    "errorLens.addNumberOfDiagnostics": true,
    "errorLens.gutterIconsEnabled": true,
    "errorLens.excludePatterns": [
        "**/*.dart"
    ],
    "dart.lineLength": 120,
    "dart.checkForSdkUpdates": false,
}
```

### My VS Code installed extensions
```
aaron-bond.better-comments
austin.code-gnu-global
brunnerh.insert-unicode
christian-kohler.path-intellisense
CoenraadS.bracket-pair-colorizer
cssho.vscode-svgviewer
Dart-Code.dart-code
Dart-Code.flutter
eamodio.gitlens
formulahendry.code-runner
hansec.fortran-ls
julialang.language-julia
krvajalm.linter-gfortran
mammothb.gnuplot
marcelovelasquez.flutter-tree
ms-python.python
ms-python.vscode-pylance
ms-toolsai.jupyter
ms-vscode.cpptools
Nash.awesome-flutter-snippets
PKief.material-icon-theme
ritwickdey.LiveServer
tomoki1207.pdf
tomoki1207.selectline-statusbar
usernamehw.errorlens
WakaTime.vscode-wakatime
wwm.better-align
```