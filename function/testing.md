---
layout: default
title: Testing
parent: Functions
nav_order: 5
---

# TODO: Functions Testing
{: .no_toc }

- TOC
{:toc}

This section provides guidance for developing function unit tests.

## Testing approach

- Automated testing. Integrate testing in GHES continuous integration pipelines (CI).
- Use test-oriented development practices.
- Use a shift-left continuous testing approach and protect against regression.
- Keep unit tests in a separate project from integration tests.
- Use Arrange, Act, Assert (AAA) pattern.
- Name unit tests using the following naming convention: UnitOfWork_Scenario_ExpectedBehavior
- Avoid introducing dependencies into tests by following the 
[Explicit Dependencies Principle](https://deviq.com/principles/explicit-dependencies-principle) 
and using dependency injection.
- Ensure both positive and negative testing scenarios are developed.

**Positive testing scenarios**: Use valid data to demonstate successful 
execution. Positive testing reinforces the way components should be used in a 
production environment.

**Negative testing scenarios**: Use invalid data to demonstrate the recovery 
of the system during a failed execution. Traditionally, there will be  
significantly more negative testing scenarios compared to positive testing 
scenarios.

See the 
[Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices)
for additional unit testing best practices.

## Terminology: Fake, mock, stub

Fake: Generic term to describe either a stub or a mock object.

Mock: A mock is a fake object that decides whether or not a unit test has 
passed or failed.

Stub: A stub is a controllable replacement for an existing dependency in the 
system. By using a stub, you can test the code without dealing with the 
dependency directly.

## Characteristics of a good unit test (FIRST)

- **F**ast: Tests should take very little time to run.
- **I**solated: Tests should never depend on other test cases. Should be 
able to run any test, at any time, in any order.
- **R**epeatable: Tests should produce the same results every run.
- **S**elf-checking: Tests should be able to automatically detect if it 
passed or failed without manual interpretation.
- **T**imely: Tests should not take a disproportionately long time to write 
when compared to the code being tested.

## Set up testing project

### 1. Add xUnit project

Open the function solution in Visual Studio and add a new **xUnit Test Project**.

![xUnitAddProject](../assets/images/function-xunit-add-project.png)

### 2. Configure xUnit project

For the **Project name** use the following naming convention:

DH.{Integration}.AzureFunction.Tests

![xUnitAddProject](../assets/images/function-xunit-configure-project.png)

### 3. TODO: Add unit tests

For the test project, add a reference to the function project. 

``` csharp
using AutoFixture;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.Internal;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Logging;
using Microsoft.Extensions.Primitives;
using Moq;
using Xunit;

namespace DH.Integration.AzureFunction.Tests
{
    public class BusinessFunctionTests
    {
        private readonly IFixture _fixture = new Fixture();
        private readonly ILogger _logger = Mock.Of<ILogger>();

        [Fact]
        public async Task Run_WhenNameParamIsNull_ShouldThrowException()
        {
            // Arrange
            var mockRequest = new Mock<HttpRequest>();

            // Act/Assert
            await Assert.ThrowsAsync<Exception>(() => BusinessFunction.Run(mockRequest.Object, _logger));
        }

        [Fact]
        public async Task Run_WhenNameParamIsProvided_ShouldReturnTheName()
        {
            // Arrange
            string  expectedName = _fixture.Create<string>();
            var queryCollection = new QueryCollection(new Dictionary<string, StringValues>()
            {
                { "name", expectedName }
            });

            var mockRequest = new Mock<HttpRequest>();
            mockRequest
                .Setup(req => req.Query)
                .Returns(() => queryCollection);

            // Act
            var response = await BusinessFunction.Run(mockRequest.Object, _logger) as OkObjectResult;

            // Assert
            Assert.Equal(expectedName, response?.Value);
        }
    }
}
```
![TestExplorerPassing](../assets/images/function-test-explorer-passing.png)

Use the Visual Studio test explorer to run the tests.
https://docs.microsoft.com/en-us/visualstudio/test/run-unit-tests-with-test-explorer

## TODO: Analyze code coverage

To effectively guard against bugs, tests should cover a large proportion 
of the code (> 90% if possible).

https://docs.microsoft.com/en-us/visualstudio/test/using-code-coverage-to-determine-how-much-code-is-being-tested
