<p align="center">
  <img src="logo.svg" alt="Ace Reports logo" width="96">
</p>

<h1 align="center">Ace Reports</h1>

<p align="center">
  <b>See why every .NET test failed, in one HTML file.</b><br>
  Install one NuGet package and every <code>dotnet test</code> run writes a report with the logs,
  API calls, screenshots and retries behind each result.
</p>

<p align="center">
  <a href="https://www.nuget.org/packages/AceReports.Xunit"><img src="https://img.shields.io/nuget/v/AceReports.Xunit?label=NuGet&color=1cb684" alt="NuGet version"></a>
  <a href="https://harshadlambate.github.io/AceReportsWebsite/"><img src="https://img.shields.io/badge/website-Ace%20Reports-1b1e2b" alt="Website"></a>
  <a href="https://harshadlambate.github.io/AceReportsWebsite/demo.html"><img src="https://img.shields.io/badge/live%20demo-open%20report-f7a013" alt="Live demo report"></a>
</p>

<p align="center">
  <a href="https://harshadlambate.github.io/AceReportsWebsite/"><b>Website</b></a> ·
  <a href="https://harshadlambate.github.io/AceReportsWebsite/demo.html"><b>Live demo report</b></a> ·
  <a href="https://github.com/HarshadLambate/AceReportsWebsite/issues"><b>Report an issue</b></a>
</p>

---

## Features

- **Zero setup:** install the package and run `dotnet test`. No attributes, base classes or config files.
- **Every API call captured:** method, URL, request and response bodies, status and duration for every
  `HttpClient` request. `Authorization` and cookie headers are redacted automatically.
- **Screenshots on failure:** taken automatically from Playwright, Selenium or Puppeteer, plus your own
  named screenshots at any step.
- **Retries and flaky tests:** every attempt keeps its own logs, API calls, error and screenshots. A test
  that passes after failing is marked **flaky**.
- **Step-by-step logs:** `Ace.Info`, `Ace.Pass`, `Ace.Fail` and `Ace.Debug` from anywhere in a test.
  Reqnroll Given/When/Then steps are logged for you.
- **Search, filters and categories:** filter by status or category, search by name or argument, and click
  a chart bar to narrow the table.
- **One file, no server:** styles, data and screenshots in a single HTML file. Email it, attach it to a
  ticket, or publish it as a CI artifact.
- **Light, dark or system theme.**

## Install

| Framework | Package | Install |
| --- | --- | --- |
| xUnit v3 (4.0+) | [AceReports.Xunit](https://www.nuget.org/packages/AceReports.Xunit) | `dotnet add package AceReports.Xunit` |
| NUnit (3.14+ and 4) | [AceReports.NUnit](https://www.nuget.org/packages/AceReports.NUnit) | `dotnet add package AceReports.NUnit` |
| MSTest (3.10+ and 4) | [AceReports.MSTest](https://www.nuget.org/packages/AceReports.MSTest) | `dotnet add package AceReports.MSTest` |
| Reqnroll 3 (any runner) | [AceReports.Reqnroll](https://www.nuget.org/packages/AceReports.Reqnroll) | `dotnet add package AceReports.Reqnroll` |

Requires **.NET 10**.

## Quick start

1. Add the package for your framework to your test project.
2. Run your tests: `dotnet test`
3. Open the report: `TestResults/AceReport_<timestamp>.html`, next to your test binaries. The path is
   also printed at the end of the run.

## Configure (optional)

Add this class anywhere in your test project. Ace Reports finds it by itself:

```csharp
using AceReports;
using AceReports.Configuration;

internal sealed class AceReportsStartup : IAceReportsStartup
{
    public void Configure(AceReportsConfiguration options)
    {
        Ace.SuiteName("Checkout Regression");
        Ace.EnvironmentName("UAT");
        Ace.DarkTheme();
    }
}
```

## Write to the report from a test

```csharp
Ace.Info("Submitting payment");
Ace.Pass("Payment authorized");
Ace.TakeScreenshot("After login");

// Page or driver created inside the test? Hand it over once:
Ace.UseScreenshotSource(page);   // Playwright IPage, Selenium IWebDriver, ...
```

To turn reporting off for an xUnit, NUnit or MSTest project, add
`<EnableAceReports>false</EnableAceReports>` to its `.csproj`.

## ☕ Support Ace Reports

Found Ace Reports useful? Support its continued development. Every coffee goes into new framework
support, fixes and features, and helps keep the core packages free.

<a href="https://buymeacoffee.com/lambate05p"><img src="https://img.shields.io/badge/Buy%20me%20a%20coffee-FFDD00?style=for-the-badge&logo=buymeacoffee&logoColor=black" alt="Buy me a coffee"></a>

## Feedback and contact

- Found a bug or have an idea? [Open an issue](https://github.com/HarshadLambate/AceReportsWebsite/issues).
- Commercial licensing (OEM, white-label, redistribution) or anything else: lambate02@gmail.com

## License

Free to use, including commercially inside your company, under the
[PolyForm Perimeter License 1.0.1](https://polyformproject.org/licenses/perimeter/1.0.1).
The one thing it doesn't allow is building a product that competes with Ace Reports.
