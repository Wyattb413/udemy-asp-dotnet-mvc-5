# The Complete ASP .NET MVC 5 Course

[**Udemy Course Link**](https://www.udemy.com/the-complete-aspnet-mvc-5-course/learn/v4/content) - https://www.udemy.com/the-complete-aspnet-mvc-5-course/learn/v4/content

## Table of Contents

Lecture Topic | Link
--- | ---
General Notes | [General Notes](#general-notes)
**SECTION 1** | [**Section 1**](#section-1)
Your First ASP.NET MVC App | [Lecture 4](#section-1-lecture-4)
**SECTION 2** | [**Section 2**](#section-2)
Action Results | [Lecture 10](#section-2-lecture-10)
Action Parameters | [Lecture 11](#section-2-lecture-11)
Convention Based Routing | [Lecture 12](#section-2-lecture-12)

## General Notes

- **String Interpolation** can be accomplished via `String.Format("pageIndex={0}&sortBy={1}", pageIndex, sortby)`

<!-- ################################################################################################################ -->
<!--                                                     SECTION 1                                                    -->
<!-- ################################################################################################################ -->

## SECTION 1

### Section 1 Lecture 4

#### Your First ASP.NET MVC App

- `App_Data` Where database files are stored
- `App_Start` **Class**es called when application starts
- `Content` Directory for client-side assests
- `Controllers` Responsible for responding to user input and enacting on the data stored in the database via the **Models**
- `Models` Representation of your data stored in the database
- `Scripts` Directory for JavaScript files
- `Views` Directory for UI files
- `Global.asx` Class that provides hooks for various events in the app's lifecycle
- `package.config` File for keeping track of installed packages
- `Web.confg` File for configuring the app

<!-- ################################################################################################################ -->
<!--                                                     SECTION 2                                                    -->
<!-- ################################################################################################################ -->

## SECTION 2

### Section 2 Lecture 10

#### Action Results

Type | Helper Method | Used for
--- | --- | ---
ViewResult | `View()` | returning **Views**
PartialViewResult | `PartialView()` | returning **Partial Views**
ContentResult | `Content()` | returning simple text
RedirectResult | `Redirect()` | to redirect user to another URL
RedirectToRouteResult | `RedirectToAction()` | to redirect user to another **Action**
JsonResult | `Json(`) | return JSON
FileResult | `File()` | returning a file
HttpNotFoundResult | `HttpNotFound()` | returning a 404
EmptyResult | N/A | when an **Action** doesn't need to return any values (`void`)

```csharp
public ActionResult indexExample1()
{
    return Content('Hello World!');
}

public ActionResult indexExample2()
{
    return HttpNotFound();
}

public ActionResult indexExample3()
{
    return new EmptyResult();
}

public ActionResult indexExample4()
{
    return RedirectToAction('NameOfAction', 'NameOfController', { additionalParameter = 'Passed to NameOfAction' });
}
```

### Section 2 Lecture 11

#### Action Parameters

- To make a parameter optional, append `?` at the end of the type declartion e.g. `public ActionResult Index(int? pageIndex)`
- `string` types are **Reference** types, so they can be `nullable` by default (it's not necessary to append `?`)

### Section 2 Lecture 12

#### Convention Based Routing

- Specify **Parameters** embeded into the URI by using the following syntax:

```csharp
routes.MapRoute(
    "RouteName",
    "routewith/{parameter1}/and/{parameter2}",
    new { controller = "ControllerName", action = "ActionToBeCalled" }
);
```

- You can apply Regex to the **Parameters** in a URI by using the following:

```csharp
routes.MapRoute(
    "RouteName",
    "routewith/{parameter1}/and/{parameter2}",
    new { controller = "ControllerName", action = "ActionToBeCalled" },
    new {
        parameter1 = @"\d{4}", // This is using the literal @ identifier to avoid escaping the \ in \d
        parameter2 = "\\d{4}" // This is not using the literal @ identifier, so you must escape \d
    }
);
```