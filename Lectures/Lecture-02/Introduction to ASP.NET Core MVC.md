# Advanced Programming

# Lecture 1 — Introduction to ASP.NET Core MVC

> **Lecture focus:** Understand how web applications communicate, how ASP.NET Core fits into web development, and how the MVC pattern organizes an application.

> **Practical outcome:** Create an ASP.NET Core MVC project, run it locally, understand its structure, and add an `About` page to the navigation bar.

---

## Learning Outcomes

By the end of this lecture, you should be able to:

- Explain what a web application is and describe the Client–Server architecture.
- Distinguish between an HTTP Request and an HTTP Response.
- Recognize common HTTP methods and status codes.
- Explain the difference between Frontend, Backend, C#, .NET, and ASP.NET Core.
- Describe the responsibilities of Model, View, and Controller.
- Create and run an ASP.NET Core MVC project.
- Explain the roles of Controllers, Actions, Views, Routing, and Tag Helpers.
- Add a new page and link it from the navigation bar.

---

# Part 1 — Understanding the Web

## 1. What Is a Web Application?

Think about a system you use through your browser: a student portal, an online store, or a customer management system.

A **Web Application** is a software application that users access and interact with through a web browser, such as Google Chrome or Microsoft Edge.

Web applications can be:

- **Simple:** Display information or content.
- **Complex:** Manage customers, students, orders, accounts, and other business operations.

### How Does a Web Application Work?

Most web applications follow the **Client–Server Architecture**.

There are three common components:

| Component | Responsibility |
|---|---|
| **Client** | The application or device that sends requests. Usually, this is the user's browser. |
| **Server** | Receives requests, processes them, and sends responses. |
| **Database** | Stores, retrieves, and manages application data. |

### Follow the Request: A Customer Management Example

Imagine that a user opens a Customer Management System and asks to see all customers.

The process happens in this order:

1. The user opens the application in a browser.
2. The browser sends a request to the server.
3. The server processes the request.
4. If necessary, the server retrieves customer information from the database.
5. The server sends a response to the browser.
6. The browser displays the customer information.

**Keep this idea in mind:** The browser does not normally access the database directly. It communicates with the server, and the server handles the required processing.

---

## 2. How Does the Browser Communicate with the Server?

Browsers and web servers usually communicate using **HTTP — Hypertext Transfer Protocol**.

HTTP communication has two essential messages:

- **HTTP Request:** A message sent from the client to the server to request an operation or resource.
- **HTTP Response:** A message returned from the server containing the result of that request.

### 2.1 HTTP Methods

An HTTP method describes the type of operation the client wants the server to perform.

| Method | Purpose |
|---|---|
| `GET` | Retrieve or read data. |
| `POST` | Send new data to the server. |
| `PUT` | Update an existing resource, usually as a whole. |
| `PATCH` | Update part of an existing resource. |
| `DELETE` | Delete a resource. |

**Example — Customer Management System**

- Display the customers list → `GET`
- Add a new customer → `POST`
- Replace a customer's information → `PUT`
- Change only the customer's phone number → `PATCH`
- Delete a customer → `DELETE`

### 2.2 HTTP Status Codes

After processing a request, the server returns a status code to indicate the result.

| Code | Meaning | When might you see it? |
|---|---|---|
| `200 OK` | The request succeeded. | A customers list was returned successfully. |
| `201 Created` | A new resource was created successfully. | A new customer was added. |
| `400 Bad Request` | The request contains invalid data or cannot be processed. | Required input is missing or invalid. |
| `401 Unauthorized` | Authentication is required or has failed. | The user has not signed in successfully. |
| `403 Forbidden` | The user is not allowed to access the resource. | The user is signed in but lacks permission. |
| `404 Not Found` | The requested resource or page was not found. | The requested page or customer does not exist. |
| `500 Internal Server Error` | An unexpected server error occurred. | The application encountered an unhandled error. |

> **Important distinction:** `401` is about authentication; `403` is about permission. A user may be authenticated but still not be allowed to access a particular resource.

---

## 3. Frontend vs. Backend

A web application is commonly divided into two main parts.

### Frontend — What the User Sees

The **Frontend** is the part of the application that users see and interact with directly.

Common technologies include:

- **HTML:** Defines the structure and content of web pages.
- **CSS:** Controls the appearance and layout of web pages.
- **JavaScript:** Adds interactivity and dynamic behavior.

### Backend — What Happens on the Server

The **Backend** is the part of the application that runs on the server.

It is responsible for:

- Processing incoming requests.
- Implementing application logic and business rules.
- Communicating with databases.
- Managing data and returning appropriate responses.

### Where Does This Course Fit?

In this course, we will use **C#** and **ASP.NET Core** to develop the server-side part of web applications and build applications using the **MVC pattern**.

---

# Part 2 — The Technologies We Will Use

## 4. C#, .NET, and ASP.NET Core: What Is the Difference?

These terms are related, but they do not mean the same thing.

<blockquote>

**C# is the language. .NET is the platform. ASP.NET Core is the web framework.**

</blockquote>

### C# — The Programming Language

C# is a programming language developed by Microsoft.

We use it to write instructions, classes, methods, and application logic.

### .NET — The Development Platform

.NET is a development platform that provides:

- A runtime environment for executing applications.
- Libraries and frameworks.
- Development tools.
- Support for building different types of applications.

### ASP.NET Core — The Web Framework

ASP.NET Core is a web framework built on the .NET platform.

It is used to develop:

- Web applications.
- RESTful Web APIs.
- Backend services.
- Modern web systems.

### Quick Comparison

| Technology | What is it? |
|---|---|
| **C#** | A programming language. |
| **.NET** | A development platform. |
| **ASP.NET Core** | A framework for building web applications and services. |

In simple terms: **We write code using C#, use the .NET platform to build and run the application, and use ASP.NET Core to develop web applications.**

---

## 5. What Is ASP.NET Core?

ASP.NET Core is a modern, open-source, cross-platform web framework developed by Microsoft.

It provides features that help developers build web applications efficiently.

We will encounter several important concepts throughout this course:

| Concept | What it does |
|---|---|
| **Routing** | Maps incoming requests to application endpoints. |
| **Controllers** | Handle incoming requests and determine the appropriate responses. |
| **Model Binding** | Converts request data into .NET objects and values that the application can use. |
| **Views** | Generate the user interface. |
| **Razor** | Allows developers to combine C# code with HTML. |
| **Dependency Injection** | Provides classes with the dependencies they need. |
| **Middleware** | Components that participate in processing HTTP requests and responses. |

We will study these concepts in more detail in later lectures. For now, focus on recognizing their names and general responsibilities.

---

# Part 3 — Understanding MVC

## 6. What Is the MVC Architectural Pattern?

MVC stands for:

- **M — Model**
- **V — View**
- **C — Controller**

MVC is an architectural pattern that organizes an application by separating responsibilities into three main components.

### 6.1 Model — The Application's Data

The **Model** represents the data and concepts used in the application.

It may contain:

- Properties.
- Data-related logic.
- Validation rules.
- Application-related data structures.

> A Model does not necessarily represent a database table only.

### 6.2 View — The User Interface

The **View** represents the user interface displayed to the user.

In ASP.NET Core MVC:

- Views are commonly created using Razor.
- View files use the `.cshtml` extension.

### 6.3 Controller — The Request Handler

The **Controller** receives user requests, coordinates the required operations, and determines the response returned to the client.

A Controller may:

- Retrieve data.
- Call application services.
- Process user input.
- Return a View.
- Redirect the user to another page.

### 6.4 How Does an MVC Request Work?

Consider a user requesting a page from the application.

1. The browser sends an HTTP request.
2. Routing identifies the appropriate Controller and Action.
3. The Controller processes the request.
4. The Controller interacts with the Model or application data when needed.
5. The Controller returns an appropriate result, such as a View.
6. The browser displays the resulting page.

### Example: Opening the About Page

When a user requests the About page:

- The request is directed to `HomeController`.
- The `About` Action is executed.
- The Action returns the About View.
- The browser displays the page.

This is a simplified explanation of the MVC request flow. The actual process may differ depending on the type of result returned by the Controller.

---

# Part 4 — Let's Build Our First MVC Application

## 7. Development Requirements

To start developing ASP.NET Core MVC applications, you need:

- Visual Studio 2022 or a newer version.
- The **ASP.NET and web development** workload.
- A compatible .NET SDK.

### Check the Installed .NET SDK

Open Terminal or Command Prompt and execute:

```bash
dotnet --version
```

This command displays the installed .NET SDK version.

---

## 8. Create Your First ASP.NET Core MVC Project

Follow these steps in Visual Studio:

1. Open **Visual Studio**.
2. Select **Create a new project**.
3. Search for this template:

**ASP.NET Core Web App (Model-View-Controller)**

4. Select the template and click **Next**.
5. Enter the project name:

`FirstMvcApp`

6. Choose the project location.
7. Select an installed and compatible .NET version.
8. Set **Authentication Type** to **None**.
9. Click **Create**.

> **Be careful:** Select **ASP.NET Core Web App (Model-View-Controller)**, not the regular **ASP.NET Core Web App** template, which uses Razor Pages.

### Run the Project

After creating the project:

1. Wait for Visual Studio to finish loading it.
2. Click the green **Start** button.
3. Visual Studio builds and runs the application.
4. Your default browser opens the application.

### Create the Same Project Using the Command Line (VS Code)

You can create an ASP.NET Core MVC project without using the Visual Studio project wizard. We can do this through the **.NET CLI** in the VS Code terminal.

#### Step 1 — Open VS Code

1. Open Visual Studio Code.
2. Open the folder where you want to create your project.
3. Open the integrated terminal from **Terminal → New Terminal**.

You can also use:

```text
Ctrl + Shift + `
```

#### Step 2 — Check the .NET SDK

Run:

```bash
dotnet --version
```

If a version number appears, the .NET SDK is available in your terminal.

#### Step 3 — Create the MVC Project

Run:

```bash
dotnet new mvc -n FirstMvcApp
```

What does this command mean?

- `dotnet new` creates a new project from a template.
- `mvc` selects the ASP.NET Core MVC project template.
- `-n FirstMvcApp` sets the project name to `FirstMvcApp`.

The command creates a folder named `FirstMvcApp` containing the MVC project files.

#### Step 4 — Move into the Project Folder

```bash
cd FirstMvcApp
```

#### Step 5 — Open the Project in VS Code

Run:

```bash
code .
```

The dot (`.`) means the current folder.

If you already opened the project folder in VS Code, you do not need to run this command.

#### Step 6 — Run the Application

Make sure the terminal is inside the project folder, then run:

```bash
dotnet run
```

The application will build and start. The terminal will display one or more local addresses, usually similar to:

```text
https\://localhost:7001
http\://localhost:5000
```

The actual ports may be different. Open one of the addresses displayed in your terminal in a browser.

> **Note:** Use the address shown in your terminal. Do not assume that the example ports will be the same on every computer.

#### Command Summary

If the .NET SDK is already installed, the main commands are:

```bash
dotnet new mvc -n FirstMvcApp
cd FirstMvcApp
code .
dotnet run
```

**You now have two ways to create the same MVC application:**

- **Visual Studio:** Use the graphical project creation wizard.
- **VS Code:** Use the .NET CLI commands in the terminal.

Both approaches create an ASP.NET Core MVC project. The main difference is how you create and open the project.

---

## 9. Understanding Localhost

When you run an ASP.NET Core project locally, Visual Studio opens a browser using an address similar to:

```text
https\://localhost:7001
```

The number `7001` is only an example. Your project may use a different port number.

**Localhost** refers to the local computer on which the application is running.

This means the application is running on your own machine and is not necessarily published on the Internet.

---

## 10. Explore the Project Structure

An ASP.NET Core MVC project contains several important folders and files.

| Folder / File | Responsibility |
|---|---|
| `Controllers` | Contains Controller classes responsible for handling requests. |
| `Models` | Contains classes representing application data and concepts. |
| `Views` | Contains the pages displayed to users. |
| `wwwroot` | Contains static files such as CSS, JavaScript, and images. |
| `Program.cs` | Configures and starts the application. |
| `appsettings.json` | Contains application configuration settings. |
| `Properties` | Contains project-related launch and execution settings. |

### Remember These Conventions

- Controller classes usually have names ending with `Controller`.
- The `Views` folder usually contains a separate folder for each Controller.
- The `wwwroot` folder contains static files that the browser can access.
- `Program.cs` is an important starting point for configuring the application.

---

## 11. Understand Controllers, Actions, and Views

Open the `Controllers` folder.

You will find a file named:

`HomeController.cs`

It may contain code similar to this:

### HomeController.cs

```csharp
using Microsoft.AspNetCore.Mvc;
namespace FirstMvcApp.Controllers
{
public class HomeController : Controller
{
public IActionResult Index()
{
return View();
}
}
}
```

### Let's Understand the Code

#### 1. Import the MVC Namespace

```csharp
using Microsoft.AspNetCore.Mvc;
```

This statement imports the ASP.NET Core MVC types required by the Controller.

#### 2. Declare the Controller Class

```csharp
public class HomeController : Controller
```

- `HomeController` is the name of the Controller.
- It inherits from the `Controller` class.
- Inheriting from `Controller` provides useful MVC functionality.

#### 3. Declare an Action

```csharp
public IActionResult Index()
```

- `Index` is an Action method.
- An Action is a method that can handle an incoming request.
- `IActionResult` represents the result returned by an Action.

#### 4. Return a View

```csharp
return View();
```

This tells ASP.NET Core MVC to return the View associated with the current Action.

For example, when `Index()` is executed inside `HomeController`, MVC looks for the following View by convention:

```text
Views/Home/Index.cshtml
```

---

## 12. Practical Task: Add an About Page

Now let's add a new page called **About**.

### Step 1 — Add an Action to HomeController

Open `HomeController.cs` and add this method inside the class:

```csharp
public IActionResult About()
{
return View();
}
```

The Controller now contains two Actions:

- `Index()`
- `About()`

### Step 2 — Create the About View

Inside the `Views` folder:

1. Open the `Home` folder.
2. Create a new Razor View.
3. Name the file `About.cshtml`.
4. Add the following code:

```cshtml
@{
ViewData["Title"] = "About";
}
<h1>About Our Application</h1>
<p>
This is our first ASP.NET Core MVC page.
</p>
```

### Step 3 — Run and Test the Page

Run the project and navigate to:

```text
https\://localhost:<your-port>/Home/About
```

Replace `<your-port>` with the port number assigned to your application.

### Understand the URL

```text
/Home/About
```

- `Home` refers to the Controller name without the word `Controller`.
- `About` refers to the Action name.

ASP.NET Core uses **Routing** to map this URL to the appropriate Action.

---

## 13. Practical Task: Add About to the Navigation Bar

A **Navigation Bar (Navbar)** allows users to move between different pages of an application.

We will add the About page to the existing navigation bar.

### Step 1 — Open the Layout File

Navigate to:

```text
Views/Shared/_Layout.cshtml
```

This file contains the shared layout used by the application's Views, including the navigation bar.

### Step 2 — Find the Navigation Menu

Look for the navigation list that contains links such as Home and Privacy.

It may look similar to this:

```html
<ul class="navbar-nav flex-grow-1">
<li class="nav-item">
<a class="nav-link text-dark"
asp-area=""
asp-controller="Home"
asp-action="Index">Home</a>
</li>
<li class="nav-item">
<a class="nav-link text-dark"
asp-area=""
asp-controller="Home"
asp-action="Privacy">Privacy</a>
</li>
</ul>
```

### Step 3 — Add the About Link

Add the following code inside the same `<ul>` element:

```html
<li class="nav-item">
<a class="nav-link text-dark"
asp-area=""
asp-controller="Home"
asp-action="About">About</a>
</li>
```

### Step 4 — Understand the Attributes

- `asp-controller="Home"` specifies the target Controller.
- `asp-action="About"` specifies the target Action.
- `asp-area=""` indicates that the link does not belong to a specific Area in this example.

These attributes are examples of **Anchor Tag Helpers**.

### What Are Tag Helpers?

Anchor Tag Helpers help ASP.NET Core generate URLs based on the application's routing configuration.

In the standard MVC template, Tag Helpers are enabled through:

```text
Views/_ViewImports.cshtml
```

The file usually contains:

```cshtml
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
```

Save your changes and run the application again.

**Expected result:** You should now see the About link in the navigation bar. Clicking it should open the About page.

---

# Part 5 — Review and Practice

## 14. Lecture Recap

Let's connect the main ideas from today's lecture:

1. A web application is accessed through a browser.
2. The browser and server communicate using HTTP Requests and Responses.
3. The Frontend is what users interact with; the Backend processes requests and application logic.
4. C# is the programming language, .NET is the platform, and ASP.NET Core is the web framework.
5. MVC separates application responsibilities into Model, View, and Controller.
6. Routing directs requests to the appropriate Controller and Action.
7. A Controller Action can return a View.
8. The project structure helps organize Controllers, Models, Views, and static files.

## 15. Important Terms

| Term | Definition |
|---|---|
| Web Application | An application accessed through a web browser. |
| Client | The application or device that sends requests to a server. |
| Server | The system that receives and processes requests. |
| HTTP Request | A request sent from the client to the server. |
| HTTP Response | A response returned from the server to the client. |
| Frontend | The part of an application that users interact with directly. |
| Backend | The server-side part responsible for processing requests and application logic. |
| .NET | A development platform. |
| ASP.NET Core | A framework for building web applications and services. |
| MVC | An architectural pattern consisting of Model, View, and Controller. |
| Model | Represents application data and related concepts. |
| View | Represents the user interface. |
| Controller | Handles requests and coordinates application operations. |
| Action | A method inside a Controller that handles a request. |
| Razor | A syntax used to combine C# and HTML in Views. |
| Localhost | An address referring to the local computer. |
| Routing | The process of mapping incoming requests to application endpoints. |
| Tag Helpers | Server-side components that help generate HTML elements and attributes. |

## 16. Check Your Understanding

Try to answer these questions without looking back at the lecture.

1. What is the difference between a Client and a Server?
2. What is the difference between an HTTP Request and an HTTP Response?
3. Which HTTP method would you use to retrieve a list of customers?
4. What is the difference between `401` and `403`?
5. What is the difference between C#, .NET, and ASP.NET Core?
6. What are the three components of MVC?
7. What is the responsibility of a Controller?
8. What is an Action?
9. Where does MVC look for the `About` View inside `HomeController` by convention?
10. What is the purpose of the `asp-controller` and `asp-action` attributes?

## 17. After-Lecture Practice

Complete the following tasks in your `FirstMvcApp` project:

- [ ] Create and run the MVC project.
- [ ] Locate the `Controllers`, `Models`, and `Views` folders.
- [ ] Open `HomeController.cs` and identify the `Index` Action.
- [ ] Create the `About` Action.
- [ ] Create `Views/Home/About.cshtml`.
- [ ] Add the About link to the navigation bar.
- [ ] Run the application and verify that the link works.

**Submission:** Be ready to demonstrate your working About page and explain how the browser request reaches the `About` Action and returns the View.

---

***Advanced Programming — Lecture 1***
