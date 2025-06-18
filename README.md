# 🧾 Single-Page-CRUD
Create a simple one-page CRUD app using ASP.NET Core MVC
        


## ✅ Prerequisites

- ✅ Visual Studio 2022 installed
- ✅ .NET 8.0 or .NET 9.0 SDK installed


 


## 🛠️ Setup Instructions

### 1. Create Model
![Step 1](CreateModel.png)




<br>



### 2. Create another model
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
Here in the view, we have an 'Add data to database' section, and we also have a table where the data from the database will be stored.
### First, this is the code for inserting data into the database using the POST method.
![Step 1](AddDataToDatabase.png)





<br>



### Table code structure
![Step 1](DisplayToTable.png)





<br>




# Inside the tbody, we have a GET method for Edit and a POST method for Delete.
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


### This is our InsertTask controller.
![Step 1](NewInsert.png)




<br>




### This is the controller responsible for displaying the data in the table.
![Step 1](DisplayTable.png)





<br>





### This controller handles the editing of data.
![Step 1](NewEdit.png)





<br>





### This controller handles the deletion of data.
![Step 1](Delete.png)






<br>




### Overall folder structure
![Step 1](Structure.png)





<br>

<br>



# After you finish all of that, congratulations — you now have a single-page CRUD using ASP.NET Core MVC!

<br>

![Step 1](Todo.png)











