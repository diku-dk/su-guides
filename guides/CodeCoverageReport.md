# How to Generate a Code Coverage Report
## Installation
First you must install the report generator, this command can be executed at any path.

    dotnet tool install -g dotnet-reportgenerator-globaltool

To install the package used to generate code coverage data execute the following command in the `test project` folder.

    dotnet add package coverlet.collector

## Generation of Code Coverage Data
Now everytime you want to run the tests and generate code coverage data use the command below.

    dotnet test --collect:"XPlat Code Coverage"

## Report Generation
To generate a website with code coverage reported, firstly generate the code coverage data and then execute the command below in the `test project` folder. Afterwards navigate inside the Report folder and open the `index.html` file in a browser.

### Mac and Linux

    reportgenerator -reports:`find TestResults -name coverage.cobertura.xml` -targetdir:Report -reporttypes:Html

### Windows

    reportgenerator -reports:$(gci TestResults -r -fi coverage.cobertura.xml | % { $_.FullName }) -targetdir:Report -reporttypes:Html

If this does not work in cmd.exe then do it in PowerShell.

### LaTeX Report

If you wish to generate a LaTeX report use `-reporttypes:Latex` instead. A `Summary.tex` file will be inside the Report folder.