# Single-Page-CRUD
This guide will show you how to build a simple one-page CRUD app using ASP.NET Core MVC, where you can add, view, edit, and delete data without switching pages.              


  
## 🛠️ Setup Instructions

### 1. Create Model

```csharp
using System.ComponentModel.DataAnnotations;

namespace Todo_List_App.Models
{
    public class Todo
    {
        [Key]
        public int Id { get; set; } 
        [Required]
        public string Task { get; set; } 
    }
}

```



<br>



### 2. To make single-page CRUD work, we need to create another model that combines both List<Todo> and Todo, because Razor Views can’t handle two separate models at the same time.

```csharp
namespace Todo_List_App.Models
{
    public class TodoNewModel
    {
        public Todo? TodoModel { get; set; } = new Todo();
        public  List<Todo> listTodoModel { get; set; } = new List<Todo>();
    }
}

```


#### The TodoModel is for inserting data into the database,
#### while the TodoList is for handling or displaying the data in the table.




<br>
<br>



### 3. Set up View


```cshtml

@model Todo_List_App.Models.TodoNewModel

<div class="card">

    <h1>Todolist</h1>

    <form asp-controller="Todo" asp-action="InsertTask" method="post">
        <div class="d-flex align-items-center gap-2">
            <input type="hidden" asp-for="TodoModel.Id">
            <input asp-for="TodoModel.Task" type="text" class="form-control form-control-lg me-2" placeholder="Write your todo here">
            <button type="submit" class="btn btn-primary btn-lg">Add</button>
        </div>
    </form>


    <table class="table">
        <thead>
            <tr>
                <th scope="col">Task</th>
                <th scope="col">Edit</th>
                <th scope="col">Delete</th>
            </tr>
        </thead>
        <tbody>
            @foreach (var data in Model.listTodoModel)
            {
                <tr>
                    <td>@data.Task</td>
                    <td><a class="btn btn-success" asp-controller="Todo" asp-action="Edit" asp-route-GetId="@data.Id">Edit</a></td>
                    <td>
                        <form asp-controller="Todo" asp-route-id="@data.Id" asp-action="Delete" method="post">
                            <button type="submit" class="btn btn-danger">Delete</button>
                        </form>
                    </td>
                </tr>
            }
        </tbody>
    </table>


</div>


```



<br>
<br>







# About View
### First, here’s the code for adding data into the database using the POST method.

```cshtml
    <form asp-controller="Todo" asp-action="InsertTask" method="post">
        <div class="d-flex align-items-center gap-2">
            <input type="hidden" asp-for="TodoModel.Id">
            <input asp-for="TodoModel.Task" type="text" class="form-control form-control-lg me-2" placeholder="Write your todo here">
            <button type="submit" class="btn btn-primary btn-lg">Add</button>
        </div>
    </form>
```




<br>



### Table code structure

```cshtml


    <table class="table">
        <thead>
            <tr>
                <th scope="col">Task</th>
                <th scope="col">Edit</th>
                <th scope="col">Delete</th>
            </tr>
        </thead>
        <tbody>
            @foreach (var data in Model.listTodoModel)
            {
                <tr>
                    <td>@data.Task</td>
                    <td><a class="btn btn-success" asp-controller="Todo" asp-action="Edit" asp-route-GetId="@data.Id">Edit</a></td>
                    <td>
                        <form asp-controller="Todo" asp-route-id="@data.Id" asp-action="Delete" method="post">
                            <button type="submit" class="btn btn-danger">Delete</button>
                        </form>
                    </td>
                </tr>
            }
        </tbody>
    </table>

```





<br>




# In the tbody section of the table, we added a GET method for editing and a POST method for deleting data.
#### First, this is the one for Edit.


```cshtml
<td><a class="btn btn-success" asp-controller="Todo" asp-action="Edit" asp-route-GetId="@data.Id">Edit</a></td>
```


asp-route-GetId is parameter of Edit controller




<br>




#### Second, this is the one for Delete.


```cshtml
   <td>
       <form asp-controller="Todo" asp-route-id="@data.Id" asp-action="Delete" method="post">
           <button type="submit" class="btn btn-danger">Delete</button>
       </form>
   </td>
```


asp-route-id is parameter of Delete controller





<br>
<br>




# After you’ve set all of that up, here’s the logic in the controller.


### Controller Logic for Adding Data

```csharp

        //Add data sa database
        [HttpPost]
        public ActionResult InsertTask()
        {
            TodoNewModel table = new TodoNewModel();

            if (table.TodoModel.Id == 0)
            {
                _TodoTable.TodoData.Add(table.TodoModel);
            }
            else
            {
                table.TodoModel  = _TodoTable.TodoData.Find(table.TodoModel.Id);
            }
            _TodoTable.SaveChanges();
            return RedirectToAction("TodoList");
        }

```




<br>




### Controller logic for Table

```csharp

        //kunin yung data sa  database tapos diplay sa table
        public IActionResult TodoList()
        {
            TodoNewModel DataTable = new TodoNewModel
            {
                listTodoModel = _TodoTable.TodoData.ToList()
            };
            return View(DataTable); 
        }

```





<br>





### Controller logic for Edit

```csharp
    public IActionResult Edit(int GetId)
    {
        TodoNewModel model = new TodoNewModel();
       
        model.TodoModel = _TodoTable.TodoData.Find(GetId);
        return View("TodoList", model);
    }
```





<br>





### Controller logic for deleting data


```csharp
      [HttpPost]
      public IActionResult Delete(int id)
      {
          var data = _TodoTable.TodoData.Find(id);
          if(data == null)
          {
              return NotFound();
          }
        
          _TodoTable.TodoData.Remove(data);
          _TodoTable.SaveChanges();
          return RedirectToAction("TodoList");
      }

```






<br>




### Overall folder structure
![Step 1](Structure.png)





<br>

<br>



# After you finish all of that, congratulations — you now have a single-page CRUD using ASP.NET Core MVC!

<br>

![Step 1](Todo.png)











