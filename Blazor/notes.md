# Table of Contents
1. [Key Concepts in .NET and Blazor](#key-concepts)
2. [Razor](#razor)
3. [.NET Standard](#net-standard)
4. [Supported .NET Implementations](#net-implementations)
5. [POCO (Plain Old Class Object)](#poco)
6. [ASP.NET](#aspnet)
7. [Blazor](#blazor)
    - [How Blazor Works](#how-blazor-works)
    - [Blazor Example](#blazor-example)
    - [Interactive Server Components](#interactive-server-components)
8. [Important Blazor Files](#important-blazor-files)
9. [Key Blazor Directives](#key-blazor-directives)
10. [Using Components](#using-components)
11. [Component Parameters](#component-parameters)
12. [@code Block](#code-block)
13. [@rendermode InteractiveServer](#rendermode-interactiveserver)
14. [Razor Component Naming](#razor-component-naming)
15. [C# Features](#csharp-features)
    - [Target-typed `new`](#target-typed-new)
    - [Instantiation of Anonymous Types](#instantiation-of-anonymous-types)
16. [To Do](#to-do)

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
```

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
- **@inject**: used to inject services.
  - Example: `@inject PizzaService PizzaSvc`
  - dont forget to add your service to program.cs  
    builder.Services.AddSingleton<PizzaService>();
- **@code**: This directive declares that the text in the following block is C# code. 
  - You can put as many code blocks as you need in a component. 

## Built-in ASP.Net razor components
  - AntiforgeryToken
  - AuthorizeView
  - CascadingValue
  - DataAnnotationsValidator
  - DynamicComponent
  - Editor<T>
  - EditForm
  - ErrorBoundary
  - FocusOnNavigate
  - HeadContent
  - HeadOutlet
  - InputCheckbox
  - InputDate
  - InputFile
  - InputNumber
  - InputRadio
  - InputRadioGroup
  - InputSelect
  - InputText
  - InputTextArea
  - LayoutView
  - NavigationLock
  - NavLink
  - **PageTitle**: Sets title of the page. Example: `<PageTitle>Home</PageTitle>`
  - QuickGrid
  - Router
  - RouteView
  - SectionContent
  - SectionOutlet
  - ValidationSummary
  - Virtualize
  - Collaborate

## Using Components
- **Description**: To use a component from another component, add an HTML-style tag with the component's name.
  - Important: The name of a Blazor component must begin with an uppercase character.
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

## default @rendermode
- **Description**: By default, the render mode is Server, which means there is no interactivity, like classical razor pages.

## @rendermode InteractiveServer
- **Description**: To handle UI events from a component and to use data binding, the component must be interactive. By default, Blazor components render statically from the server. In this mode UI events handled by app's components from the server.
- **Usage**: Handles UI events from the server over a WebSocket connection.
  - Example: `<Counter @rendermode="InteractiveServer" />`

## @rendermode InteractiveWebAssembly
- **Description**: Component code run client-side using WebAssembly-based .NET runtime.
- **Usage**: Handles UI events inside the browser without the need to go back to server.
  - Example: `<Counter @rendermode="InteractiveWebAssembly" />`

## @rendermode InteractiveAuto
- **Description**: The component code is run with InteractiveServer until its downloaded. Once its downloaded, its run using InteractiveWebAssembly.
  - Example: `<Counter @rendermode="InteractiveAuto" />`

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
  ```

## C# Features
### Target-typed `new`
- **Description**: Constructor invocation expressions are target-typed.

### Instantiation of Anonymous Types
- **Example**:
  ```csharp
  var example = new { Greeting = "Hello", Name = "World" };  
  ```

## Two way Binding to a value
  ```csharp
  <input @bind="text" />
  <button @onclick="() => text = string.Empty">Clear</button>
  <p>@text</p>

  @code {
    string text = "";
  }
  ```

## A todo app example:
  ```csharp
  @using BlazorApp.Models

  @page "/ToDo"
  @rendermode InteractiveServer
  <h3>ToDo (@todos.Count(x => x.IsDone) / @todos.Count)</h3>

  <ul>
      @foreach (var todo in todos)
      {
          <li>
              <input type="checkbox" @bind="todo.IsDone" />
              <input @bind="todo.Title" />
          </li>
      }
  </ul>

  @if (!todos.Any(todo => !todo.IsDone))
  {
      <p>You finished all tasks.</p>
  }

  <input @bind="newTodoTitle" />
  <button @onclick="AddTodoItem">Add To-Do item</button>

  @code {
      public List<TodoItem> todos = new();
      public string newTodoTitle = string.Empty;

      private void AddTodoItem()
      {
          if (!string.IsNullOrWhiteSpace(newTodoTitle))
              todos.Add(new TodoItem() { Title = newTodoTitle });

          newTodoTitle = string.Empty;
      }
  }
  ```

## Need To Support Server and WASM? Consider Using an Interface

If you plan to support both Server and WASM, you may not want to make HTTP calls in every case. It feels redundant to make an API call when you’re running under Blazor Server and already have access to the database itself. But for WASM, you would need that HTTP call as WASM runs in the browser, which has no direct access to the data.

The easiest solution here is to employ an interface, then switch out the implementation for the different hosting models.

```csharp
public interface ITopSellersQuery  
{  
    IEnumerable<ProductDetails> List(int startIndex, int numProducts);  
}
```

If you plan to support both Server and WASM, you may not want to make HTTP calls in every case. It feels redundant to make an API call when you’re running under Blazor Server and already have access to the database itself. But for WASM, you would need that HTTP call as WASM runs in the browser, which has no direct access to the data.

The easiest solution here is to employ an interface, then switch out the implementation for the different hosting models.
```csharp
public interface ITopSellersQuery  
{  
    IEnumerable<ProductDetails> List(int startIndex, int numProducts);  
}
```

You can use the interface in your component:
```csharp
@page "/Products"  
@inject ITopSellersQuery topSellersQuery
```

Put this component in a shared class library and both Server/WASM clients can render it.

From there you’d want two implementations of `ITopSellersQuery`—a WASM version:

```csharp
class TopSellersQueryWASM : ITopSellersQuery  
{  
    private readonly HttpClient _httpClient;  
  
    public TopSellersQueryWASM(HttpClient httpClient)  
    {  
        _httpClient = httpClient;  
    }  
  
    public async Task<IEnumerable<ProductDetails>> List(int startIndex, int numProducts)  
    {  
        var requestUri = $"api/products?skip={startIndex}&take={numProducts}";  
        return await _httpClient.GetFromJsonAsync<IEnumerable<ProductDetails>>(requestUri);  
    }  
}
```

And a Server version:

```csharp
public class TopSellersQuery : ITopSellersQuery 
{
    public IEnumerable<ProductDetails> List(int startIndex, int numProducts)  
    {  
        return Enumerable.Range(startIndex, numProducts)
                         .Select(x => new ProductDetails  
        {  
            Id = x,  
            Description = "Test Product Description",  
            Name = "A Product",  
            Price = 200m  
        });  
    }
}
```

Here we’re using hardcoded data, but this could equally be a call to a database (using EF Core, Dapper, or any other ORM you fancy).

If you register the WASM version in your WASM project and the Server version in your Blazor Server project, you should be good to go.

You can skip the extra network cycles when you’re running Blazor Server and access the data direct, but still use the same, shared component for Blazor WASM (this time invoking the same code via HTTP).

To make the WASM version work, you’ll need to expose an endpoint (in the server part of your app) which invokes that same query.

Here’s an example using minimal APIs:

```csharp
app.MapGet("api/products", async (  
    HttpContext context,   
    ITopSellersQuery query,  
    [FromQuery] int skip,   
    [FromQuery] int take) => await query.List(skip, take));
```

With that, you can reuse your components on Blazor Server and WASM, confident that your app will take the most efficient route to load the data.

## Lifecycle events
  - To see the lifecycle events just write below statement in @code block and it will autocomplete:  
  protected override
  ![alt text](https://github.com/kcakar/StudyNotes/blob/master/Blazor/lifecycle.jpg?raw=true)

## Injecting services
  To use a service in a razor page, you need to inject the service after the @page directive
  ```csharp
  @using BlazingPizza.Data
  @inject PizzaService PizzaSvc
  ```
## To Do
- [ ] List all elements and directives of Blazor
- [Blazor Directives](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/razor?view=aspnetcore-8.0)
- [ ] List all lifecycle events of Blazor
- https://learn.microsoft.com/en-us/aspnet/core/blazor/components/virtualization?view=aspnetcore-8.0
- https://learn.microsoft.com/en-us/aspnet/core/blazor/security/webassembly/?view=aspnetcore-8.0
