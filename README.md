<p align="center">
  <img src="logo.svg" alt="Ace Reports logo" width="96">
</p>

<h1 align="center">Ace Reports</h1>

<p align="center">
  <b>Every test failure. Every retry. All the evidence in one HTML report.</b><br>
  <b>Automatically</b> capture API requests and responses, screenshots, logs, retries and flaky-test history,
  with minimal setup and no manual reporting calls. For .NET, Java, Python and TypeScript.
</p>

<p align="center">
  <a href="https://www.nuget.org/packages/AceReports.Xunit"><img src="https://img.shields.io/nuget/v/AceReports.Xunit?label=NuGet&color=1cb684" alt="NuGet version"></a>
  <a href="https://central.sonatype.com/artifact/io.github.acereports/acereports-junit5"><img src="https://img.shields.io/maven-central/v/io.github.acereports/acereports-junit5?label=Maven%20Central&color=1cb684" alt="Maven Central version"></a>
  <a href="https://pypi.org/project/pytest-acereports/"><img src="https://img.shields.io/pypi/v/pytest-acereports?label=PyPI&color=1cb684" alt="PyPI version"></a>
  <a href="https://www.npmjs.com/package/@acereports/playwright"><img src="https://img.shields.io/npm/v/@acereports/playwright?label=npm&color=1cb684" alt="npm version"></a>
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

- **Zero setup:** install the package and run your tests as usual. No attributes, base classes or config files.
- **Every API call, automatically:** method, URL, request and response bodies, status and duration for
  every `HttpClient` call in .NET, every REST Assured and `HttpClient` call in Java, every
  `requests` / `httpx` call in Python, and every axios / `fetch` / Playwright `request` call in TypeScript.
  `Authorization` and cookie headers are redacted.
- **Screenshots on failure:** taken automatically from Playwright, Selenium or Puppeteer, plus your own
  named screenshots at any step.
- **Retries and flaky tests:** every attempt keeps its own logs, API calls, error and screenshots. A test
  that passes after failing is marked **flaky**.
- **Step-by-step logs:** `Ace.Info(...)` in C#, `Ace.info(...)` in Java, `ace.info(...)` in Python and TypeScript.
  Gherkin steps from Reqnroll, Cucumber, pytest-bdd and Cucumber.js are logged for you.
- **Search, filters and categories:** filter by status or category, search by name or argument, and click
  a chart bar to narrow the table.
- **One file, no server:** styles, data and screenshots in a single HTML file. Email it, attach it to a
  ticket, or publish it as a CI artifact.
- **Same report in every language**, in light, dark or system theme.

## Install

### .NET (NuGet), requires .NET 10

| Framework | Package | Install |
| --- | --- | --- |
| xUnit v3 (4.0+) | [AceReports.Xunit](https://www.nuget.org/packages/AceReports.Xunit) | `dotnet add package AceReports.Xunit` |
| NUnit (3.14+ and 4) | [AceReports.NUnit](https://www.nuget.org/packages/AceReports.NUnit) | `dotnet add package AceReports.NUnit` |
| MSTest (3.10+ and 4) | [AceReports.MSTest](https://www.nuget.org/packages/AceReports.MSTest) | `dotnet add package AceReports.MSTest` |
| Reqnroll 3 (any runner) | [AceReports.Reqnroll](https://www.nuget.org/packages/AceReports.Reqnroll) | `dotnet add package AceReports.Reqnroll` |

### Java (Maven Central), requires Java 11+

| Framework | Artifact (`io.github.acereports`, test scope) |
| --- | --- |
| JUnit 5 (5.8+) | [acereports-junit5](https://central.sonatype.com/artifact/io.github.acereports/acereports-junit5) |
| TestNG (7.5+) | [acereports-testng](https://central.sonatype.com/artifact/io.github.acereports/acereports-testng) |
| Cucumber 7 (JUnit 5 or TestNG runner) | [acereports-cucumber](https://central.sonatype.com/artifact/io.github.acereports/acereports-cucumber) |

```xml
<dependency>
    <groupId>io.github.acereports</groupId>
    <artifactId>acereports-junit5</artifactId>  <!-- or acereports-testng / acereports-cucumber -->
    <version>1.1.0</version>
    <scope>test</scope>
</dependency>
```

### Python (PyPI), requires Python 3.9+ and pytest 7+

| Framework | Package | Install |
| --- | --- | --- |
| pytest (and pytest-bdd) | [pytest-acereports](https://pypi.org/project/pytest-acereports/) | `pip install pytest-acereports` |

### TypeScript / JavaScript (npm), requires Node.js 18+

| Framework | Package | Install |
| --- | --- | --- |
| Playwright Test (1.40+) | [@acereports/playwright](https://www.npmjs.com/package/@acereports/playwright) | `npm install --save-dev @acereports/playwright` |
| Jest (29+) | [@acereports/jest](https://www.npmjs.com/package/@acereports/jest) | `npm install --save-dev @acereports/jest` |
| Vitest (3+) | [@acereports/vitest](https://www.npmjs.com/package/@acereports/vitest) | `npm install --save-dev @acereports/vitest` |
| Cucumber.js (10+) | [@acereports/cucumber](https://www.npmjs.com/package/@acereports/cucumber) | `npm install --save-dev @acereports/cucumber` |

Then add the reporter to your config:

```ts
// playwright.config.ts
reporter: [['list'], ['@acereports/playwright']],

// jest.config.js
reporters: ['default', '@acereports/jest'],
setupFilesAfterEnv: ['@acereports/jest/setup'],

// vitest.config.ts
test: { reporters: ['default', '@acereports/vitest'], setupFiles: ['@acereports/vitest/setup'] },

// cucumber.js
plugin: ['@acereports/cucumber'],
requireModule: ['@acereports/cucumber/support'],
```

## Quick start

1. Add the package for your framework to your test project.
2. Run your tests: `dotnet test`, `mvn test` (or `gradle test`), `pytest`, or `npx playwright test` / `npx jest` / `npx vitest run` / `npx cucumber-js`.
3. Open the report: `TestResults/AceReport_<timestamp>.html`. The path is also printed at the end of the run.

## Configure (optional)

**.NET:** add this class anywhere in your test project. Ace Reports finds it by itself:

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

**Java:** add `src/test/resources/acereports.properties` (the same keys work as `-D` system properties):

```properties
acereports.suite.name=Checkout Regression
acereports.environment=UAT
acereports.theme=dark
```

**Python:** add this hook to a `conftest.py` (or use `acereports_*` settings in `pytest.ini`):

```python
from acereports import ace

def pytest_acereports_configure(options):
    ace.suite_name("Checkout Regression")
    ace.environment_name("UAT")
    ace.dark_theme()
```

**TypeScript:** pass options to the reporter in your framework's config:

```ts
reporter: [['list'], ['@acereports/playwright', { suiteName: 'Checkout Regression', environment: 'UAT', theme: 'dark' }]],
```

## Write to the report from a test

```csharp
Ace.Info("Submitting payment");
Ace.Pass("Payment authorized");
Ace.TakeScreenshot("After login");
Ace.UseScreenshotSource(page);   // a page or driver created inside the test
```

```java
import io.github.acereports.Ace;

Ace.info("Submitting payment");
Ace.pass("Payment authorized");
Ace.takeScreenshot("After login");
Ace.useScreenshotSource(page);   // only for a page or driver Ace Reports can't find by itself
```

```python
from acereports import ace

ace.info("Submitting payment")
ace.pass_("Payment authorized")
ace.take_screenshot("After login")
ace.use_screenshot_source(page)  # only for a page created inside the test
```

```ts
import { ace } from '@acereports/playwright';   // or @acereports/jest, /vitest, /cucumber

ace.info('Submitting payment');
ace.pass('Payment authorized');
await ace.takeScreenshot('After login');
ace.useScreenshotSource(page);   // only for a page Ace Reports can't find by itself
```

**Turning it off:** in .NET, add `<EnableAceReports>false</EnableAceReports>` to the `.csproj`
(xUnit, NUnit, MSTest). In Java, run `mvn test -Dacereports.enabled=false`, or set
`acereports.enabled=false` in `acereports.properties`. In Python, set `acereports = false` in `pytest.ini`, or run
`pytest --no-acereports`. In TypeScript, pass `enabled: false` to the reporter, or set `ACEREPORTS_ENABLED=false`.

## What's captured automatically, and what needs one line

**API calls**

| Language | Automatic, including calls made through your own wrappers and SDKs | Needs one line | Not captured |
| --- | --- | --- | --- |
| .NET | Everything sent through `HttpClient` (observed through `System.Diagnostics`), so libraries built on it are covered too | | Traffic that doesn't use `HttpClient` |
| Python | Everything sent through `requests` and `httpx` (sync and async) | | `aiohttp`, `urllib`, `urllib3` used directly |
| TypeScript | Everything sent through Node's `http` / `https` and the global `fetch`: axios, got, supertest, node-fetch, ky, Playwright's `request` fixture and `page.request` | | HTTP/2 through the `http2` module, gRPC |
| Java | Everything sent through REST Assured. Java's `HttpClient` when it's a field of the test class, a base class or a Cucumber step class, or one level down in one of your own objects | A Java `HttpClient` created inside the test or deeper inside a wrapper: `AceHttpClient.wrap(client)` | OkHttp, Apache HttpClient, Spring `RestTemplate` / `WebClient` |

**Screenshots** (taken automatically when a test fails, before teardown closes the browser)

| Language | Found automatically | Needs one line |
| --- | --- | --- |
| .NET | A Playwright, Selenium or Puppeteer page or driver the test uses | A page or driver created inside the test: `Ace.UseScreenshotSource(page)` |
| Python | A fixture named like `page`, `driver` or `browser` (pytest-playwright's `page`), or such an attribute on the test class | A page created inside the test: `ace.use_screenshot_source(page)` |
| TypeScript | Playwright Test's `page` and every browser context a test opens; a `page` / `driver` fixture (Vitest `test.extend`), World property (Cucumber.js) or jest-playwright global | A page created inside the test: `ace.useScreenshotSource(page)` |
| Java | A Playwright `Page` or Selenium `WebDriver` in a field (instance, static or `ThreadLocal`) of the test class, a base class or a Cucumber step/hook class, or one level down in one of your own objects | A driver kept elsewhere (a `DriverManager`): `Ace.setScreenshotProvider(DriverManager::getDriver)` once |

**Retries:** every attempt is kept, with its own logs, error, API calls and screenshots, in every language
(xRetry / NUnit and MSTest `[Retry]`, pytest-rerunfailures, JUnit Pioneer / Surefire reruns / TestNG `IRetryAnalyzer`,
Playwright `retries` / `jest.retryTimes` / Vitest `retry` / `cucumber-js --retry`).

## ☕ Support Ace Reports

Found Ace Reports useful? Support its continued development. Every coffee goes into new framework
support, fixes and features, and helps keep the core packages free.

<a href="https://buymeacoffee.com/lambate05p"><img src="https://img.shields.io/badge/Buy%20me%20a%20coffee-FFDD00?style=for-the-badge&logo=buymeacoffee&logoColor=black" alt="Buy me a coffee"></a>

## Feedback and contact

- Found a bug, or want Ace Reports for another language? [Open an issue](https://github.com/HarshadLambate/AceReportsWebsite/issues).
- Commercial licensing (OEM, white-label, redistribution) or anything else: lambate02@gmail.com

## License

Free to use, including commercially inside your company, under the
[PolyForm Perimeter License 1.0.1](https://polyformproject.org/licenses/perimeter/1.0.1).
The one thing it doesn't allow is building a product that competes with Ace Reports.
