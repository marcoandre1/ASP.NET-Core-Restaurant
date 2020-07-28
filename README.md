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
