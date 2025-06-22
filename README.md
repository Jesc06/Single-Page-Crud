# Single-Page-CRUD
This guide will show you how to build a simple one-page CRUD app using ASP.NET Core MVC, where you can add, view, edit, and delete data without switching pages.              


  
## 🛠️ Setup Instructions

### 1. Create Model
![Step 1](CreateModel.png)




<br>



### 2. To make single-page CRUD work, we need to create another model that combines both List<Todo> and Todo, because Razor Views can’t handle two separate models at the same time.
![Step 1](CreateAnotherModel.png)
#### The TodoModel is for inserting data into the database,
#### while the TodoList is for handling or displaying the data in the table.




<br>
<br>



### 3. Set up View
![Step 1](CreateView.png)



<br>
<br>







# About View
### First, here’s the code for adding data into the database using the POST method.
![Step 1](AddDataToDatabase.png)





<br>



### Table code structure
![Step 1](DisplayToTable.png)





<br>




# In the tbody section of the table, we added a GET method for editing and a POST method for deleting data.
#### First, this is the one for Edit.
![Step 1](EditMethod.png)

asp-route-GetId is parameter of Edit controller




<br>




#### Second, this is the one for Delete.
![Step 1](DeleteRecord.png)

asp-route-id is parameter of Delete controller





<br>
<br>




# After you’ve set all of that up, here’s the logic in the controller.


### Controller Logic for Adding Data
![Step 1](NewInsert.png)




<br>




### Controller logic for Table
![Step 1](DisplayTable.png)





<br>





### Controller logic for Edit
![Step 1](NewEdit.png)





<br>





### Controller logic for deleting data
![Step 1](Delete.png)






<br>




### Overall folder structure
![Step 1](Structure.png)





<br>

<br>



# After you finish all of that, congratulations — you now have a single-page CRUD using ASP.NET Core MVC!

<br>

![Step 1](Todo.png)











