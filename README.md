# House Price Prediction
## AIM:
To design a website to train the house price model and to predict the price.

## DESIGN STEPS:
### Step 1: 
Requirement collection.
### Step 2:
Creating the layout using HTML and CSS.
### Step 3:
Train the model using the given data set
### Step 4:
Save the trained model using pickle
### Step 5:
Get the input from the user
### Step 6:
Load the trained model using pickle
### Step 7:
Apply the given data to the model
### Step 8:
Display the result
### Step 9:
Publish the website in the given URL.

## PROGRAM:

### HouseModelTraining.html

```
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css" integrity="sha384-B0vP5xmATw1+K9KRQjQERJvTumQW0nPEzvF6L/Z6nronJ3oUOFUFpCjEUQouq2+l" crossorigin="anonymous">

    <title>House Price Prediction</title> 
  </head>
  <body>    
        <div class="jumbotron jumbotron-fluid" style="background-color:rgb(13, 105, 82);">        
            <div class="container text-center">
            <h1>House Price Model Training</h1>
            <p class="lead">You can use this website to calculate your house price</p>
            </div>
        </div>     
        <div class="container">
            <form action="/HouseModelTraining/" method="POST">
                {% csrf_token %}

            <div class="form-group row">
                <label for="samples" class="col-md-2 col-form-label">Total Samples</label>
                <div class="col-md-10">
                <input type="text" readonly class="form-control" id="samples" placeholder="-" value="{{samples}}">
                </div>
            </div>                                                           
            <div class="form-group row text-center">
                <div class="col-md-12">
                    <button type="submit" class="btn btn-primary">Train</button>
                </div>                     
            </div>    
            <div class="form-group row">
                <label for="score" class="col-md-2 col-form-label">Score</label>
                <div class="col-md-10">
                <input type="text" readonly class="form-control" id="score" placeholder="-" value="{{score}}">
                </div>
            </div>                               
        </form>
        </div> 
              

    <!-- Optional JavaScript; choose one of the two! -->

    <!-- Option 1: jQuery and Bootstrap Bundle (includes Popper) -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/js/bootstrap.bundle.min.js" integrity="sha384-Piv4xVNRyMGpqkS2by6br4gNJ7DXjqk09RmUpJ8jgGtD7zP9yug3goQfGII0yAns" crossorigin="anonymous"></script>

    <!-- Option 2: Separate Popper and Bootstrap JS -->
    <!--
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/js/bootstrap.min.js" integrity="sha384-+YQ4JLhjyBLPDQt//I+STsc9iw4uQqACwlvpslubQzn4u2UU2UFM80nGisd026JF" crossorigin="anonymous"></script>
    -->
  </body>
</html>
```

### HouseModelPrediction.html
```
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css" integrity="sha384-B0vP5xmATw1+K9KRQjQERJvTumQW0nPEzvF6L/Z6nronJ3oUOFUFpCjEUQouq2+l" crossorigin="anonymous">

    <title>House Price Prediction</title>
  </head>
  <body>
    
        <div class="jumbotron jumbotron-fluid" style="background-color:rgb(17, 102, 31); ">
        
            <div class="container text-center">
            <h1>House Price Prediction</h1>
            <p class="lead">You can use this website to calculate your house price</p>
            </div>
        </div>     
        <div class="container" >                      
            <form action="/HouseModelPrediction/" method="POST">
                {% csrf_token %}
            <div class="form-group row">
                <label for="area" class="col-md-2 col-form-label">Total Area</label>
                <div class="col-md-10">
                <input type="text" class="form-control" id="area" name="area" placeholder="1500"  value="{{area}}">
                </div>
            </div>            
            <div class="form-group row">
                <label for="bathrooms" class="col-md-2 col-form-label">Bath Rooms</label>
                <div class="col-md-10">
                <input type="text" class="form-control" id="bathrooms" name="bathrooms" placeholder="2" value="{{bathrooms}}"> 
                </div>
            </div>       
            <div class="form-group row">
                <label for="bhk" class="col-md-2 col-form-label">Bedroom Hall Kitchen</label>
                <div class="col-md-10">
                <input type="text" class="form-control" id="bhk" name="bhk" placeholder="3" value="{{bhk}}">
                </div>
            </div>      
            <div class="form-group row">
                <label for="location" class="col-md-2 col-form-label">Location</label>
                <div class="col-md-10">
                <select id="location" name="location" class="col-md-10 form-control">
                    {% for loc in locations %}

                        {% if loc == location %}
                            <option selected value="{{loc}}">{{loc}}</option>
                        {% else %}
                            <option value="{{loc}}">{{loc}}</option>
                        {% endif %}
                    {% endfor %}
                </select>
                </div>
            </div>         
            <div class="form-group row text-center">
                <div class="col-md-12">
                    <button type="submit" class="btn btn-primary">Calculate</button>
                </div>                     
            </div>    
            <div class="form-group row">
                <label for="price" class="col-md-2 col-form-label">Price(Lakh)</label>
                <div class="col-md-10">
                <input type="text" readonly class="form-control" id="price" placeholder="-" value="{{price}}">
                </div>
            </div>                               
        </form>
        </div> 
              

    <!-- Optional JavaScript; choose one of the two! -->

    <!-- Option 1: jQuery and Bootstrap Bundle (includes Popper) -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/js/bootstrap.bundle.min.js" integrity="sha384-Piv4xVNRyMGpqkS2by6br4gNJ7DXjqk09RmUpJ8jgGtD7zP9yug3goQfGII0yAns" crossorigin="anonymous"></script>

    <!-- Option 2: Separate Popper and Bootstrap JS -->
    <!--
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/js/bootstrap.min.js" integrity="sha384-+YQ4JLhjyBLPDQt//I+STsc9iw4uQqACwlvpslubQzn4u2UU2UFM80nGisd026JF" crossorigin="anonymous"></script>
    -->
  </body>
</html>
```

### views.py

```
from django.shortcuts import render

import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn import metrics 
from sklearn.linear_model import LinearRegression
import pickle
# Create your views here.

def HouseModelTraining(request):
    context={}
    data = pd.read_csv("House_data_preprocessed.csv")
    context["samples"] = data.shape[0]
    if request.method == 'GET':
        context["score"] = "-"

    if request.method == 'POST':
        Y = data["price"]
        X = data.drop("price", axis="columns")
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.2)
        house_model= LinearRegression()
        house_model.fit(X_train, Y_train)
        score = house_model.score(X_test, Y_test)
        context["score"] = score
        with open('house_model.pickle','wb') as f:
            pickle.dump(house_model,f)

    return render(request, 'housepriceprediction/HouseModelTraining.html', context) 

def HouseModelPrediction(request):
    context={}
    data = pd.read_csv("House_data_preprocessed.csv")
    context['locations'] = data.columns[4:]

    if request.method == 'GET':
        context['area'] = '1500'
        context['bathrooms'] = '2'
        context['bhk'] = '3'
        context['location'] = ''
        context['price'] = '-'

    if request.method == 'POST':
        area = int(request.POST.get('area',0))
        bathrooms = int(request.POST.get('bathrooms',0))
        bhk = int(request.POST.get('bhk',0))
        location = request.POST.get('loaction','-')

        context['area'] = area
        context['bathrooms'] = bathrooms
        context['bhk'] = bhk
        context['location'] = location

        Y = data['price'] 
        X = data.drop("price", axis="columns")
        with open('house_model.pickle', 'rb') as f:
            house_model = pickle.load(f)
        loc_index = np.where(X.columns==location)[0]
        input = np.zeros(len(X.columns))
        input[0] = area
        input[1] = bathrooms
        input[2] = bhk
        if loc_index >= 0:
            input[loc_index] = 1
        price = house_model.predict([input])
        context['price'] = "{0:.4f}".format(price[0])

    return render(request, 'housepriceprediction/HouseModelPrediction.html', context)     
```

## OUTPUT:

![output](./static/img/op3.jpg)

![output](./static/img/op4.jpg)

## Validation Report:

![output](./static/img/va3.jpg)

![output](./static/img/va4.jpg)

## RESULT:

Thus a website is designed to train the house price model and to predict the price and is hosted in the URL http://harish.student.saveetha.in:8000/HouseModelTraining/ and http://harish.student.saveetha.in:8000/HouseModelPrediction/ HTML code is validated.