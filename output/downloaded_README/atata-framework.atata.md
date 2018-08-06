# [Atata](https://atata-framework.github.io/)

[![NuGet](http://img.shields.io/nuget/v/Atata.svg?style=flat)](https://www.nuget.org/packages/Atata/)
[![GitHub release](https://img.shields.io/github/release/atata-framework/atata.svg)](https://github.com/atata-framework/atata/releases)
[![Gitter](https://badges.gitter.im/atata-framework/atata.svg)](https://gitter.im/atata-framework/atata)
[![Atata Framework documentation](https://img.shields.io/badge/docs-Atata_Framework-orange.svg)](https://atata-framework.github.io/)
[![Twitter](https://img.shields.io/badge/follow-@AtataFramework-blue.svg)](https://twitter.com/AtataFramework)

C#/.NET web UI test automation full featured framework based on Selenium WebDriver. It uses fluent page object pattern. Supports .NET Framework 4.0+ and .NET Core/Standard 2.0.

**[What's new in v0.17.0](https://atata-framework.github.io/blog/2018/05/31/atata-0.17.0-released/)**

## Features

* **WebDriver**. Based on [Selenium WebDriver](https://github.com/SeleniumHQ/selenium) and preserves all its features.
* **Page Object**. Provides unique fluent page object pattern that is easy to implement and maintain.
* **Components**. Supports a rich set of HTML [components](https://atata-framework.github.io/components/).
* **Integration**. Works on any .NET test engine (e.g. NUnit, xUnit) as well as on CI systems like TeamCity or TFS.
* **Triggers**. A bunch of [triggers](https://atata-framework.github.io/triggers/) to bind with different component events.
* **Verification**. A set of methods and triggers for the component and data verification.
* **Configurable**. Defines the default component search strategies as well as additional settings.
* **Logging**. Built-in customizable logging and screenshot capturing functionality.
* **Extensible**. [Atata.Bootstrap](https://github.com/atata-framework/atata-bootstrap) and [Atata.KendoUI](https://github.com/atata-framework/atata-kendoui) packages have a set of ready to use components.

## Usage

### Page Object

Simple sign-in page object for http://atata-framework.github.io/atata-sample-app/#!/signin page:

```C#
using Atata;

namespace SampleApp.UITests
{
    using _ = SignInPage;

    [Url("signin")] // Relative URL of the page.
    [VerifyH1] // Verifies that H1 header text equals "Sign In" upon page object initialization.
    public class SignInPage : Page<_>
    {
        [FindByLabel] // Finds <label> element containing "Email" (<label for="email">Email</label>), then finds text <input> element by "id" that equals label's "for" attribute value.
        public TextInput<_> Email { get; private set; }

        [FindById("password")] // Finds password <input> element by id that equals "password" (<input id="password" type="password">).
        public PasswordInput<_> Password { get; private set; }

        [FindByValue(TermCase.Title)] // Finds button element by value that equals "Sign In" (<input value="Sign In" type="submit">).
        public Button<_> SignIn { get; private set; }
    }
}
```

### Test

Usage in the test method:

```C#
[Test]
public void SignIn()
{
    Go.To<SignInPage>().
        Email.Set("admin@mail.com").
        Password.Set("abc123").
        SignIn.Click();
}
```

*Find out more on [Atata usage](https://atata-framework.github.io/getting-started/#usage). Check [atata-framework/atata-samples](https://github.com/atata-framework/atata-samples) for different Atata test scenario samples.*

## Demo

Demo [atata-framework/atata-sample-app-tests](https://github.com/atata-framework/atata-sample-app-tests) UI tests application demonstrates different testing approaches and features of Atata Framework. It covers main Atata features: page navigation, data input and verification, interaction with pop-ups and tables, logging, screenshot capture, etc.

Sample test:

```C#
[Test]
public void User_Create()
{
    string firstName, lastName, email;
    Office office = Office.NewYork;
    Gender gender = Gender.Male;

    Login().
        New().
            ModalTitle.Should.Equal("New User").
            General.FirstName.SetRandom(out firstName).
            General.LastName.SetRandom(out lastName).
            General.Email.SetRandom(out email).
            General.Office.Set(office).
            General.Gender.Set(gender).
            Save().
        Users.Rows[x => x.FirstName == firstName && x.LastName == lastName && x.Email == email && x.Office == office].View().
            Header.Should.Equal($"{firstName} {lastName}").
            Email.Should.Equal(email).
            Office.Should.Equal(office).
            Gender.Should.Equal(gender).
            Birthday.Should.Not.Exist().
            Notes.Should.Not.Exist();
}
```

## Documentation

Find out more on [Atata Docs](https://atata-framework.github.io/) and on [Getting Started](https://atata-framework.github.io/getting-started/) page in particular.

### Tutorials

You can also check the following tutorials:

* [Atata - C# Web Test Automation Framework](https://www.codeproject.com/Articles/1158365/Atata-New-Test-Automation-Framework) - an introduction to Atata Framework.
* [Verification of Page](https://atata-framework.github.io/tutorials/verification-of-page/) - how to verify web page data using different approaches of Atata Framework.
* [Verification of Validation Messages](https://atata-framework.github.io/tutorials/verification-of-validation-messages/) - how to verify validation messages on web pages using Atata Framework.
* [Handle Confirmation Popups](https://atata-framework.github.io/tutorials/handle-confirmation-popups/) - how to handle different confirmation popups using Atata Framework.
* [Multi-Browser Configuration via Fixture Arguments](https://atata-framework.github.io/tutorials/multi-browser-configuration-via-fixture-arguments/) - how to configure multi-browser tests application using NUnit fixture arguments.
* [Visual Studio Team Services Configuration](https://atata-framework.github.io/tutorials/vs-team-services-configuration/) - how to configure Atata test automation build on Visual Studio Team Services using any browser.

## Contact

Feel free to ask any questions regarding Atata Framework. Any feedback, issues and feature requests are welcome.

You can [ask a question on Stack Overflow](https://stackoverflow.com/questions/ask?tags=atata) using [atata](https://stackoverflow.com/questions/tagged/atata) tag.

If you faced an issue please report it to [Atata Issues](https://github.com/atata-framework/atata/issues), write to [Atata Gitter](https://gitter.im/atata-framework/atata) or just mail to yevgeniy.shunevych@gmail.com.

### Links

* Stack Overflow: https://stackoverflow.com/questions/tagged/atata
* Atata Issues: https://github.com/atata-framework/atata/issues
* Atata Gitter: https://gitter.im/atata-framework/atata
* Twitter: https://twitter.com/AtataFramework
* YouTube: https://www.youtube.com/channel/UCSNfv8sKpUR3a6dqPVy54KQ

### Author

Contact me if you need a help in test automation using Atata Framework, or if you are looking for a quality test automation implementation for your project.

* Email: yevgeniy.shunevych@gmail.com
* Skype: e.shunevich
* LinkedIn: https://www.linkedin.com/in/yevgeniy-shunevych
* Gitter: https://gitter.im/YevgeniyShunevych

## License

Atata is an open source software, licensed under the Apache License 2.0. See [LICENSE](LICENSE) for details.