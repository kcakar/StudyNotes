# Key Concepts in .NET and Blazor

## Razor
- **Description**: A markup syntax based on HTML and C#.

## .NET Standard
- **Description**: A formal specification of .NET APIs available on multiple .NET implementations.
- **Motivation**: Establish greater uniformity in the .NET ecosystem.
- **.NET 5 and Later**: Adopt a different approach that eliminates the need for .NET Standard in most scenarios.
- **Compatibility**: If sharing code between .NET Framework and any other .NET implementation (e.g., .NET Core), target .NET Standard 2.0.
- **Support**: .NET 5 and later versions will continue to support .NET Standard 2.1 and earlier.

## Supported .NET Implementations
1. **.NET 6 and later versions** (formerly .NET Core, latest is .NET 8)
2. **.NET Framework**
3. **Mono**
4. **UWP**

## POCO (Plain Old Class Object)
- **Description**: Contains only public properties.

## ASP.NET
- **Description**: Extends the .NET platform with tools and libraries for building web apps.
- **Features**:
  - Base framework for processing web requests in C# or F#.
  - Razor: Web-page templating syntax for dynamic web pages using C#.
  - Libraries for common web patterns, such as MVC (Model View Controller).
  - Authentication system with libraries, a database, and templates for handling logins.
  - Editor extensions for syntax highlighting and code completion for web development.

## Blazor
- **Description**: Uses WebAssembly to run C# code in the browser.
- **Features**:
  - .NET runtime compiled into WebAssembly.
  - Supported by all major browsers.
  - Reuse existing libraries.
  - Near-native performance.
  - Easy tooling and debugging.
- **Blazor Apps**:
  - Consist of HTML and C#.
  - Files have the extension `.razor`.
  - Reuse or nest components.

### How Blazor Works
- **Process**:
  1. Blazor app produces .NET Standard DLLs.
  2. These DLLs are converted to WebAssembly (`.wasm`).
  3. Runs with .NET runtime on the browser, using `mono.wasm` with JavaScript runtime.
  4. Access all browser APIs like WebSockets, Canvas.
  5. Call JavaScript from C# and vice versa.
- **Data Binding**: Supports two-way data binding to keep component state in sync with UI elements.

### Blazor Example
```razor
<h1>Counter</h1>

<p role="status">Current count: @currentCount</p>

<button class="btn btn-primary" @onclick="IncrementCount">Click me</button>

@code {
    private int currentCount = 0;

    private void IncrementCount()
    {
        currentCount++;
    }
}

### Interactive Server Components
- **Description**: Handle UI interactions and updates over a WebSocket connection with the browser.
- **Usage**:
  - Render different components from the server or the client within the same app.
  - Decide component render mode at design time or runtime.

## Important Blazor Files
- **Program.cs**: Entry point
- **App.razor**: Root component
- **Routes.razor**: Blazor routes

## Key Blazor Directives
- **@page**: Specifies route for a page.
  - Example: `@page "/keremspage"`
- **PageTitle**: Sets title of the page.
  - Example: `<PageTitle>Home</PageTitle>`

## Using Components
- **Description**: To use a component from another component, add an HTML-style tag with the component's name.
  - Example: `<MyButton />` to use `MyButton.razor`.

## Component Parameters
- **Description**: Allow passing data to the component.
- **Implementation**:
  - Add a public C# property with the `[Parameter]` attribute.
  - Specify a value using an HTML-style attribute matching the property name.

## @code Block
- **Description**: Used to add C# class members (fields, properties, methods) to a component.
- **Usage**:
  - Keep track of component state.
  - Add component parameters.
  - Implement component lifecycle events.
  - Define event handlers.

## @rendermode InteractiveServer
- **Description**: Enables interactive server rendering for the component.
- **Usage**: Handles UI events from the server over a WebSocket connection.
  - Example: `<Counter @rendermode="InteractiveServer" />`
- **Modes**:
  - InteractiveServer: UI events handled by app's components from the server.
  - InteractiveWebAssembly: Component code run client-side using WebAssembly-based .NET runtime.

## Razor Component Naming
- **Convention**: File names should have a capitalized first letter to distinguish them from HTML elements.

## C# Features
### Target-typed `new`
- **Description**: Constructor invocation expressions are target-typed.
- **Examples**:
  ```csharp
  List<int> xs = new();
  List<int> ys = new(capacity: 10_000);
  List<int> zs = new() { Capacity = 20_000 };


## C# Features
### Target-typed `new`
- **Description**: Constructor invocation expressions are target-typed.

### Instantiation of Anonymous Types
- **Example**:
  var example = new { Greeting = "Hello", Name = "World" };  


## To Do
- [ ] List all elements and directives of Blazor
- [Blazor Directives](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/razor?view=aspnetcore-8.0)
- [ ] List all lifecycle events of Blazor
