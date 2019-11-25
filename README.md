# SoftwareEngineeringDHBWTestSolution

So in this tutorial you will learn how to create a simple model, a controller method and a action between a view and a controller.

To add the model go to the "Models" folder in your Solution Explorer and add a parameter. In my case the model will look like this:

namespace Test.Models
{
    public class ExampleModel
    {
        public string Name { get; set; }
    }
}

After that we want to manipulate the model. We want to push a name from a form into the model. So we need to go to the already provided
HomeController and edit the ActionResult Index, because we will use the Index.cshtml (view). In order to post a name into the model, the
controller needs to receive it from the view, so he needs the "string name" in his method head. After that we will create a new 
instance from the Model to use it and give it the posted value:

    public class HomeController : Controller
    {
      public ActionResult Index(string name)
      {
        ExampleModel model = new ExampleModel();
        model.Name = name;

       return View(model);
      }
    }
    
The View, which will provide the form and is located in the Home folder will look as follows:
    
 @model Test.Models.ExampleModel //This will initialize the model in the view and lets us use it.

<form class="form" action="@Url.Action("Index", "Home")"> 
/*The Url.Action will post the name into the controller method. ATTENTION: the "name" attribute has to have the same name as the string in the ActionResult method.*/
    <div>
        <span class="user">Name</span><input type="text" class="user-input" name="name" required />
        <input type="submit" class="submit-button" />
    </div>
</form>

/*If you use a model it is wise to check it if it has any data in it, if you dont do that you will receive a System.NullreferenceException.*/
@if(Model != null)
{
    <p>@Model.Name</p>
}


After that you should be able to execute the solution. When it is finished with the building you can enter a String into the input field
and post it to the controller, after that the name should appear below the input field.
