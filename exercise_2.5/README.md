## Exercise 2.5: Django MVR Revisited

### Learning Goals

-	Add images to the model and display them on the frontend of your application
-	Create complex views with access to the model
-	Display records with views and templates


### Objectives

Add a pic attribute to the recipe model to include images with individual Recipe records. In addition to creating a custom welcome page for the Recipe app, list and detail views should also be created that display the records in the database.

### Deliverables
_(See code here: https://github.com/RParker505/recipe-app)_

#### Step 1: Update your models (if needed)

Add the pic attribute to the model, create necessary media folders, specify the path in settings.py file and specify URL-View mapping

```
class Recipe(models.Model):

    # Define attributes/columns in the table
    name= models.CharField(max_length=120)
    cooking_time= models.FloatField(help_text='minutes')
    ingredients= models.CharField(max_length=400, help_text='Ingredients must be separated by commas.')
    pic = models.ImageField(upload_to='recipes', default='no_picture.jpg')
```

#### Step 2: Add records for recipes

Use the Django admin site to add records that include the new pic attribute

<img width="230" alt="image" src="https://github.com/user-attachments/assets/b26a1fc6-ad47-4073-b19e-35bd5486d097">

#### Step 3: Develop a welcome page

Utilize media folders and static files to create the homepage

```
    <img src="{% static 'recipes/images/kitchen-tile.jpg' %}" 
    alt="Background image" 
    class="fullscreen-bg">
    
    <h1>Welcome to The Recipe App</h1>
    
    <div class="content-wrapper">
        <img src="{% static 'recipes/images/recipe-ingredients.jpg' %}" alt="cutting board and ingredients" width="500px" class="recipe-img">
        <h3>Log in to start cooking!</h3>
        <a href="placeholder"> Login </a>
    </div>
```

#### Step 4: Generate a recipe list

Utilize ListView to create a new class-based view

```
class RecipeListView(ListView):                 # Class-based view
   model = Recipe                               # Specify model
   template_name = 'recipes/recipe_list.html'   # Specify template
```

And create a new template for recipe_list

```
    <img src="{% static 'recipes/images/kitchen-tile.jpg' %}" 
    alt="Background image" 
    class="fullscreen-bg">

    <h1>Recipe List</h1>

    <div class="content-wrapper">
        <div class="recipe-list">
            {% for recipe in object_list %}
            <div class="recipe-card">
                <img src="{{ recipe.pic.url }}" alt="{{ recipe.name }}" class="recipe-image">
                <div class="recipe-info">
                    <h2><a href = "{{recipe.get_absolute_url}}">{{ recipe.name }}</a></h2>
                </div>
            </div>
            {% endfor %}
        </div>
    </div>
```

#### Step 5: Generate a recipe detail view

Utilize DetailView to create a class-based view to display individual recipe record details (name, cooking time, ingredients, etc.)

```
class RecipeDetailView(DetailView):
    model = Recipe
    template_name = 'recipes/recipe_details.html'
```

And create a new template for recipe_details

```
    <img src="{% static 'recipes/images/kitchen-tile.jpg' %}" 
    alt="Background image" 
    class="fullscreen-bg">

    <h2>Recipe Details</h2>

    <div class="content-wrapper">
        <div class="recipe-list">
            <div class="recipe-card">
                <img src="{{ recipe.pic.url }}" alt="{{ recipe.name }}" class="recipe-image">
                <div class="recipe-info">
                    <h3>Name: {{ recipe.name }}</h3>
                    <b>Cooking Time:</b> {{recipe.cooking_time}} minutes<br>
                    <br>
                    <b>Difficulty:</b> {{recipe.calculate_difficulty}}<br>
                    <br>
                    <b>Ingredients:</b> {{recipe.ingredients}}<br>
                </div>
            </div>
        </div>
    </div>
```

#### Step 4: Create and run new tests

```
    # Test that absolute URL is correctly generated and that the RecipeDetailView loads with name is clicked
    def test_get_absolute_url(self):
        recipe = Recipe.objects.get(id=1)
        # get_absolute_url() should take you to the detail page of recipe #1 and load the URL recipes/list/1
        self.assertEqual(recipe.get_absolute_url(), '/recipes/1')
```



