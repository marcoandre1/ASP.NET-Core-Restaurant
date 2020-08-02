# ASP.NET-Core-Restaurant

This project was made with ASP.NET Core 2.1.
It is from a pluralsight tutorial [OdeToFood](https://github.com/OdeToCode/OdeToFood).

## Part one
- Start a new project with ASP.NET Core (beware of the version).
- You can directly start your new project with F5 (within Visual Studio). The project is created with a boiler template.
- Add a Restaurants item to the burger list on the `_Layout.cshtml` file.
- Add a Restaurants folder to the Pages Folder and add a `List.cshtml` Razor page to it.
- Add a new project `Class Library (.NET Core)` and name it `OdeToFood.Core`. Be careful to set it to **netcoreapp2.1**. You can right click on the project and edit the `OdeToFood.Core.csproj` file to verify.
- Add a `Restaurant.cs` class to it.
- Add a new project `Class Library (.NET Core)` and name it `OdeToFood.Data`. Be careful to set it to **netcoreapp2.1**. You can right click on the project and edit the `OdeToFood.Core.csproj` file to verify.
- Add a `IRestaurantData.cs` to it.
- In the `Startup.cs` file add `services.AddSingleton<IRestaurantData, InMemoryRestaurantData>();`. You will need to add the dependency to `OdeToFood.Data`. You can right click on the `Dependencies` and `Add Reference...`.
- Modify `List.cshtml.cs` to add the implementation to `OdeToFood.Core` and `OdeToFood.Data`.
- Finally, modify the `List.cshtml` file to show the list of the restaurants.

## Part two
- Add a form in the `List.cshtml` file to enable a quich search for the list of restaurants.
- Modify the binding model, _the `List.cshtml.cs` file_, to bind the **SearchTerm** to the name of the restaurants. Use the `[BindProperty]` attribute.
- Add the `Detail.cshtml` Razor page and congfigure the binding model to show restaurant data.
- Finally, add a `NotFound.cshtml` Razor page (without model) to redirect the user to a not found page if the id passed in the query does not exist. To achienve this : 
  - modify the `public void OnGet` method to `public IActionResult OnGet`
  - use the `RedirectToPage` method.


## Part three
- Add the `Edit.chstml` Razor Page to the Restaurants folder to allow the creation and the edition of restaurants.
- Manage the creation and the edition of restaurants in the `Edit.cshtml.cs` model as follow :
```csharp
if (restaurantId.HasValue) // if the id exists, we want to get the info of the restaurant
{
    Restaurant = restaurantData.GetById(restaurantId.Value);
}
else // if the id doesn't exist, we want to create a new restaurant
{
    Restaurant = new Restaurant();
}
```
- Add the `Add` and the `Update` methods to the `IRestaurantData.cs` interface.
- Implement the methods in the `Edit.cshtml.cs` model as follow :
```csharp
if (Restaurant.Id > 0) // if the restaurant id is superior to 0, we assume that the restaurant already exists and that we want to update it
{
    restaurantData.Update(Restaurant);
}
else // if the restaurant id is equal to 0 (or is null), we assume that the restaurant doesn't exist and that we want to create it
{
    restaurantData.Add(Restaurant);
}
```
- use the provided built-in method `IsValid` to validate the model :
```csharp
if (!ModelState.IsValid) // if the model for the Edit page is not valid, we return the page
{
    Cuisines = htmlHelper.GetEnumSelectList<CuisineType>(); // this returns the CuisineType DropDownList if the model is not valid
    return Page();
}
```
- The validation is done in the `Restaurant.cs` class with the _bracket properties_ :
```csharp
[Required, StringLength(80)]
public string Name { get; set; }

[Required, StringLength(255)]
public string Location { get; set; }
```
- The validation is shown to the user with the `asp-validation-for` tag in the `Edit.cshtml` Razor page

