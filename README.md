[![Build status](https://ci.appveyor.com/api/projects/status/71ra15a58euogncn?svg=true)](https://ci.appveyor.com/project/wachulski/nunit-migrator)
[![Quality Gate](https://sonarcloud.io/api/badges/gate?key=MarWac_NUnit_Migrator)](https://sonarcloud.io/dashboard/index/MarWac_NUnit_Migrator)
[![Coverage](https://sonarcloud.io/api/badges/measure?key=MarWac_NUnit_Migrator&metric=coverage)](https://sonarcloud.io/dashboard/index/MarWac_NUnit_Migrator)
[![Technical debt ratio](https://sonarcloud.io/api/badges/measure?key=MarWac_NUnit_Migrator&metric=sqale_debt_ratio)](https://sonarcloud.io/dashboard/index/MarWac_NUnit_Migrator)

# Have a project grounded in NUnit v2 and want v3?

So you have your unit tests project founded on NUnit v2 realm. And you are considering the upgrade. And yes, your are right - this means three kind of changes you are going to deal with:

 1. **Straightforward ones** - easy to do with some regex replace.
 2. **Not so obvious ones** - you will need to take a careful look to make the code compile.
 3. **Really painful ones** - even if the code compiles, some unit tests result in red.

## Helping you with breaking changes

For vast majority of breaking changes introduced by v3 of the framework this utility reports warnings or errors, for some - equips you with code fixes. See the following tables to see what is currently supported (based on https://github.com/nunit/docs/wiki/Breaking-Changes material).

##### Aid

 * :mag: - detecting breaking changes (Roslyn analyzer)
 * :bulb: - fixing breaking changes to v3 equivalent code (Roslyn code fix)

##### Development status

 * :white_check_mark: - released, the feature is there in place
 * :soon: - the feature is planned to be developed soon
 * :x: - there are no plans to develop the feature

### Attributes

|            Name              |          Notes                                        | :mag: | :bulb: |
|------------------------------|-------------------------------------------------------|----------|------------|
| ExpectedExceptionAttribute   | No longer supported. Use `Assert.Throws` or `Assert.That`. | :white_check_mark: | :white_check_mark: |
| IgnoreAttribute              | The reason is now mandatory | :soon: | :x: |
| RequiredAddinAttribute       | No longer supported. | :soon: | :x: |
| RequiresMTAAttribute         | Deprecated. Use `ApartmentAttribute`                    | :soon: | :soon: |
| RequiresSTAAttribute         | Deprecated. Use `ApartmentAttribute`                    | :soon: | :soon: |
| SuiteAttribute               | No longer supported. | :soon: | :x: |
| System.MTAThreadAttribute    | No longer treated as `RequiresMTAAttribute`             | :soon: | :x: |
| System.STAThreadAttribute    | No longer treated as `RequiresSTAAttribute`             | :soon: | :x: |
| TearDown and OneTimeTearDown | There is a change to the logic by which teardown methods are called. | :soon: | :x: |
| TestCaseAttribute            | Named parameter `Result=` is no longer supported. Use `ExpectedResult=`. Named parameter `Ignore=` now takes a string, giving the reason for ignoring the test.| :soon:  | :soon: |
| TestCaseSourceAttribute      | The attribute forms using a string argument to refer to the data source must now use only static fields, properties or methods. | :soon: | :x: |
| TestFixtureAttribute         | Named parameter `Ignore=` now takes a string, giving the reason for ignoring the test. | :soon:  | :x: |
| TestFixtureSetUpAttribute    | Deprecated. Use `OneTimeSetUpAttribute`.  | :soon: | :soon: |
| TestFixtureTearDownAttribute | Deprecated. Use `OneTimeTearDownAttribute`.  | :soon: | :soon: |
| ValueSourceAttribute         | The source name of the data source must now use only static fields, properties or  methods. | :soon: | :x: |

###### Assertions and Constraints

|          Feature                 |          Notes                                        | :mag: | :bulb: |
|----------------------------------|-------------------------------------------------------|----------|------------|
| Assert.IsNullOrEmpty             | No longer supported. Use `Assert.That(..., Is.Null.Or.Empty)` | :soon: | :soon: |
| Assert.IsNotNullOrEmpty          | No longer supported. Use `Assert.That(..., Is.Not.Null.And.Not.Empty)` | :soon: | :soon: |
| Is.InstanceOfType                | No longer supported. Use `Is.InstanceOf`                    | :soon:  | :soon:  |
| Is.StringStarting                | Deprecated. Use `Does.StartWith` | :soon:  | :soon:  |
| Is.StringContaining              | Deprecated. Use `Does.Contain` | :soon:  | :soon:  |
| Is.StringEnding                  | Deprecated. Use `Does.EndWith` | :soon:  | :soon:  |
| Is.StringMatching                | Deprecated. Use `Does.Match` | :soon:  | :soon:  |
| NullOrEmptyStringConstraint      | No longer supported. See `Assert.IsNullOrEmpty` above   | :soon: | :soon: |
| SubDirectoryContainsConstraint   | No longer supported. Various alternatives are available.    | :soon: | :soon: |
| Text.All                         | No longer supported. Use `Has.All` or `Is.All` | :white_check_mark:  | :white_check_mark:  |
| Text.Contains                    | No longer supported. Use `Does.Contain` or `Contains.Substring` | :white_check_mark:  | :white_check_mark:  |
| Text.DoesNotContain              | No longer supported. Use `Does.Not.Contain` | :white_check_mark:  | :white_check_mark:  |
| Text.StartsWith                  | No longer supported. Use `Does.StartWith` | :white_check_mark:  | :white_check_mark:  |
| Text.DoesNotStartWith            | No longer supported. Use `Does.Not.StartWith` | :white_check_mark:  | :white_check_mark:  |
| Text.EndsWith                    | No longer supported. Use `Does.EndWith` | :white_check_mark:  | :white_check_mark:  |
| Text.DoesNotEndWith              | No longer supported. Use `Does.Not.EndWith` | :white_check_mark:  | :white_check_mark:  |
| Text.Matches                     | No longer supported. Use `Does.Match` | :white_check_mark:  | :white_check_mark:  |
| Text.DoesNotMatch                | No longer supported. Use `Does.Not.Match` | :white_check_mark:  | :white_check_mark:  |

###### Other Framework Features

|      Feature       |          Notes                                        | :mag: | :bulb: |
|--------------------|-------------------------------------------------------|----------|------------|
| Addins             | No longer supported. | :x: | :x: |
| CurrentDirectory   | No longer set to the directory containing the test assembly. Use `TestContext.CurrentContext.TestDirectory` to locate that directory. | :soon: | :soon: |
| NUnitLite          | NUnitLite executable tests must now reference nunit.framework in addition to NUnitLite. | :x: | :x: |
| SetUpFixture       | Now uses `OneTimeSetUpAttribute` and `OneTimeTearDownAttribute` to designate higher-level setup and teardown methods. `SetUpAttribute` and `TearDownAttribute` are no longer allowed. | :soon: | :x: |
| TestCaseData       | The `Throws` Named Property is no longer available. Use `Assert.Throws` or `Assert.That` in your test case. | :soon:  | :soon:  |
| TestContext        | The fields available in the `TestContext` have changed, although the same information remains available as for NUnit V2. | :soon: | :soon: |

## Contributing

This is an early stage of project development, but it is open for contributions. To start with, submit your idea by creating an issue and let us discuss it together afterwards.

## Copyright

Copyright © 2017 Marcin Wachulski

## License

NUnit Migrator is licensed under MIT. See [LICENSE](LICENSE) for more information.