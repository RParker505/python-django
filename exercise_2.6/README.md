## Exercise 2.6: User Authentication in Django

### Learning Goals

-	Create authentication for your web application
-	Use GET and POST methods 
-	Password protect your web application’s views

### Objectives

Add login and logout features to the Recipe application.

### Deliverables
_(See code here: https://github.com/RParker505/recipe-app)_

#### Step 1: Create a login view

_Create a views.py file under the root recipe_project folder_

```
def login_view(request):
    #initialize:
    #error_message to None                                 
    error_message = None  
    # Create a Form object with username and password fields 
    form = AuthenticationForm()

    # When user hits "login" button, then POST request is generated
    if request.method == 'POST':       
        # Read the data sent by the form via POST request                   
        form = AuthenticationForm(data=request.POST)

        # If the form is valid—has the requisite data—the app will read the username and password
        if form.is_valid():                                
            username = form.cleaned_data.get('username')    #read username
            password = form.cleaned_data.get('password')    #read password

            # Use Django authenticate function to validate the user
            user = authenticate(username=username, password=password)
            
            if user is not None:    #if user is authenticated
            # Then use pre-defined Django function to login
                login(request, user)                
                return redirect('recipes:list') #& send the user to desired page

        else:   # in case of error
            error_message ='ooops.. something went wrong'   #print error message

    # Prepare data to send from view to template
    context = {                                             
        'form': form,                    # Send the form data
        'error_message': error_message   # and the error_message
    }

    # Load the login page using "context" information
    return render(request, 'auth/login.html', context)
```

#### Step 2: Create a login template

_The template should live in a templates/auth folder under the root src folder_

```
    <h1>Log In</h1>          {% comment %} print heading {% endcomment %}

    {% comment %} check for error message {% endcomment %}
    {% if error_message %}
        <div class="error-message">{{error_message}}</div>
    {% endif %}

    {% comment %} print form {% endcomment %}
    <form action="" method="POST" class="login-form" >
    {% comment %} add Django security token {% endcomment %}
    {% csrf_token %}   

    {% comment %} print form received from view  {% endcomment %}
    {{form.as_p}} <!-- Assuming the form is rendered as paragraphs -->          

    {% comment %} add button {% endcomment %}
    <button type="submit" class="login-btn" >Login</button>
    </form>
```

#### Step 3: Register View and Map URL

_Done in the main urls.py file in the urlpatterns_

```
path('login/', login_view, name='login'),
```

#### Step 4: Provide clickable login button

_Done in the homepage template HTML_

```
<a href="{%url 'login' %}"> Login </a>
```

#### Step 5: Protect Views

_Protect pages that should require a user to be logged in before loading the view_

- Import the required package

```
from django.contrib.auth.mixins import LoginRequiredMixin
```

- Update the (class) view to inherit from the package

```
class RecipeListView(LoginRequiredMixin, ListView):                 # Class-based view
   model = Recipe                               # Specify model
   template_name = 'recipes/recipe_list.html'   
```

#### Step 6: Implement a logout function

_Also done in the new views.py file, following the login view_

```
def logout_view(request):                                  
   logout(request)             #the use pre-defined Django function to logout
   return render(request, 'auth/success.html')    #after logging out go to login form (or whichever page you want)
```

#### Step 7: Test the user path

https://github.com/user-attachments/assets/02d54c5a-cc2c-4244-b4c7-b4860eebc04e



