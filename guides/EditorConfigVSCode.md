## C# IntelliSense & DIKU Style
IntelliSense for C# in VSCode is provided through OmniSharp. Currently you have to have a .sln file for it to analyze your code.

`.editorconfig` in this repository contains the config that enforces the specified [SU Style Guide](CSharpStyle.md).

### How to set-up EditorConfig with VS Code
1. First ensure that you **have the C# and EditorConfig extensions**. These can be installed via the Marketplace or Extensions tab (on the left) in VS Code. Remember to restart after installing.

2. Copy and place the [.editorconfig](../files/.editorconfig) file as is in the root of your project. 

3. Then proceed to open your preferences(`CTRL+SHIFT+P` => `>Preferences: Open Settings (UI)`), search OmniSharp and tick `Omnisharp: Enable Editor Config Support`. 

4. If the C# extension is installed a tiny flame should appear in the bottom left. Click this flame or `CTRL+SHIFT+P` and select `OmniSharp: Select Project` and choose the `.sln` to analyze. This `.sln` must have the `.csproj` you are working in added. You can examine this by looking through the `.sln` file. 

5. Restart VS Code.

6. Now the `format` option in VS Code should use the options specified in the editorconfig file. This will happen as long as you are working in a project part of the solution which you have selected your intellisense (Omnisharp) to analyze (see step 4). You can try it out: `CTRL+SHIFT+P` -> `Format Document`.

7. You now have the option to format on save or with a special keybind. To format on save simply open Preferences as in step 3 and search and tick Format on Save. See [here](https://code.visualstudio.com/docs/getstarted/keybindings) for setting up a specific keybind or changing the keybind for save and format.

`.editorconfig` is a powerful tool to streamline style and formatting when working on different projects with different people. If you're curious about `.editorconfig` and its uses you can find more information about it on [the official site](https://editorconfig.org/)!
