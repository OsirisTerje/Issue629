# xunit-nunit-clash
Demonstrates [nunit/nunit3-vs-adapter#629](https://github.com/nunit/nunit3-vs-adapter/issues/629)

### Repro

```PowerShell
git clone https://github.com/damonbarry/xunit-nunit-clash.git
cd xunit-nunit-clash
dotnet build xunit-test  -f netcoreapp2.2 -o ../bin
dotnet build nunit-test  -f netcoreapp2.2 -o ../bin
dotnet vstest bin/xunit-test.dll
```

### Output

```
PS C:\Users\damonbarry\projects\xunit-nunit-clash> dotnet build xunit-test  -f netcoreapp2.2 -o ../bin
Microsoft (R) Build Engine version 16.0.450+ga8dc7f1d34 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 1.31 sec for C:\Users\damonbarry\projects\xunit-nunit-clash\xunit-test\xunit-test.csproj.
  xunit-test -> C:\Users\damonbarry\projects\xunit-nunit-clash\bin\xunit-test.dll

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:02.69
PS C:\Users\damonbarry\projects\xunit-nunit-clash> dotnet build nunit-test  -f netcoreapp2.2 -o ../bin
Microsoft (R) Build Engine version 16.0.450+ga8dc7f1d34 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 1.22 sec for C:\Users\damonbarry\projects\xunit-nunit-clash\nunit-test\nunit-test.csproj.
  nunit-test -> C:\Users\damonbarry\projects\xunit-nunit-clash\bin\nunit-test.dll

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.46
PS C:\Users\damonbarry\projects\xunit-nunit-clash> dotnet vstest bin/xunit-test.dll
Microsoft (R) Test Execution Command Line Tool Version 16.0.1
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
Error initializing RunSettings. Default settings will be used
System.IO.FileNotFoundException: Could not load file or assembly 'System.Xml.XPath.XmlDocument, Version=4.0.2.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'. The system cannot find the file specified.
File name: 'System.Xml.XPath.XmlDocument, Version=4.0.2.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'
   at NUnit.VisualStudio.TestAdapter.AdapterSettings.Load(String settingsXml)
   at NUnit.VisualStudio.TestAdapter.NUnitTestAdapter.Initialize(IDiscoveryContext context, IMessageLogger messageLogger) in D:\repos\nunit\nunit3-vs-adapter\src\NUnitTestAdapter\NUnitTestAdapter.cs:line 126


Exception System.IO.FileNotFoundException, Exception thrown executing tests
Could not load file or assembly 'System.Xml.XPath.XmlDocument, Version=4.0.2.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'. The system cannot find the file specified.
   at NUnit.VisualStudio.TestAdapter.NUnit3TestExecutor.RunAssembly(String assemblyPath, TestFilter filter)
   at NUnit.VisualStudio.TestAdapter.NUnit3TestExecutor.RunTests(IEnumerable`1 sources, IRunContext runContext, IFrameworkHandle frameworkHandle) in D:\repos\nunit\nunit3-vs-adapter\src\NUnitTestAdapter\NUnit3TestExecutor.cs:line 99

Total tests: 1. Passed: 1. Failed: 0. Skipped: 0.
Test Run Successful.
Test execution time: 1.8620 Seconds
PS C:\Users\damonbarry\projects\xunit-nunit-clash>
```
