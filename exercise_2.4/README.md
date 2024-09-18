## Exercise 2.4: Django Views and Templates

### Learning Goals

-	Summarize the process of creating views, templates, and URLs 
-	Explain how the “V” and “T” parts of MVT architecture work
-	Create a frontend page for your web application

### Objectives

Create a custom welcome page for the Recipe app. 

### Deliverables
_(See code here: https://github.com/RParker505/recipe-app)_

**Step 1:** Define the View (in recipes/views.py file)
```
def home(request):
    return render(request, 'recipes/recipes_home.html')
```
**Step 2:** Create the template (in templates/recipes/recipes_home.html file)
```
<!DOCTYPE html>
<html lang="en">

<head>
    <title>Recipe App Home</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <style type="text/css">
        .
        .
        .
</head>

<body>
    <h1>Welcome to The Recipe App</h1>
     <img src="https://images.unsplash.com/photo-1466637574441-749b8f19452f?q=80&w=2428&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D" width="500px">
    <h3>Log in to start cooking!</h3>
    <a href="placeholder"> Login </a>
</body>

</html>
```
**Step 3:** Map the view to the URL

In the recipes/urls.py file
```
from django.urls import path
from .views import home

app_name = 'recipes'

urlpatterns = [
path('', home),
]
```

In the root urls.py file, add to urlpatterns:
```
path('', include('recipes.urls'))
```

**Step 4:** Run Server to test homepage view
![welcome](https://github.com/user-attachments/assets/eec33c5f-315a-4465-96de-f86624d84fbd)

