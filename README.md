# BlazorUIComponents
At attempt to make Blazor components that mimic UWP/Xamarin controls, follow MVVM (ViewModel nav) guidelines, and use the ReactiveUI framework

# Problems
1. Navigation is half-finished.  Refreshes and direct links will not work.  They just make the app go back to the first page.  But everything else works.  
2. Since I am trying to do Viewmodel-based navigation, using links '<a href=''></a>' are not going to work.  I couldn't use Bootstraps nice navigation bar since it depends on those links.  I had to use button instead.  Also, the `MainViewModel` doesn't default to a page... the menu unselected on first load.  
3. Do NOT use AspNetCore dependency injection for your services and viewmodels.  You will likely need access to IJSRuntime and IUriHelper and if you try to pull those into your viewmodels using dependency-injection from AspNetCore's default container, you'll get the server-side version of each.  And the IJSRuntime won't work.  You want the remote or client version.  So put all your registrations for Splat into the App.razor file.  The client-side has the correct IJSRuntime implementation.

# To use
1.  All of your pages that require navigation should inherit `NavPageBase<>` with the viewmodel for the page as the generic parameter.
