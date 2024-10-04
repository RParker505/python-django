## Exercise 2.7: Data Analysis and Visualization in Django

### Learning Goals

-	Work on elements of two-way communication like creating forms and buttons
-	Implement search and visualization (reports/charts) features
-	Use QuerySet API, DataFrames (with pandas), and plotting libraries (with matplotlib)

### Objectives

Add a search function and data visualization to the Recipe application.

### Deliverables
_(See code here: https://github.com/RParker505/recipe-app)_

#### Step 1: Implement Recipe Search
- Create a user form to allow your user to input the search criteria.
- Extract the data as QuerySet using the search criteria.
- Convert the QuerySet to pandas DataFrames (Ensure you have pandas installed).
- Display search results as a table.
- Ensure that the recipes returned by the search criteria are clickable and lead to the details page of the recipe.
- (Optional) Give users the ability to view all recipes without any search filter from the search criteria.

![image](https://github.com/user-attachments/assets/fb04a217-b6ee-4492-9138-4741274ff8b7)

#### Step 2: Data Visualization
- Install matplotlib
- Implement charts

![image](https://github.com/user-attachments/assets/bd1e5990-8aba-441e-a81c-74e37a83fff7)

#### Step 3: Write Tests
Test your new form and views. For this, you can create classes like RecipeFormTest. Testing will need to include checking the fields for values, formats, or lengths, ensuring login protection of views, appropriate pagination, and any other checks you feel are relevant.

#### Step 4: Check the user flow



https://github.com/user-attachments/assets/306dd21c-c035-48c9-be6f-e382653ee820

