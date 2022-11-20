
# SanAssist

San Assist is a project of a web application that will help you to find health data about your location and compare it with OMS recommendation.

## Usages

To use our application, you just have to fill the form with a french city name.   
Our first algorythm will compare the name of the city with all the existed one and return the GPS location of the city. 
After it, we will use the public data set to request data corresponding to the location. The objectives is to find the nearest Prelevment Center to get the more efficient data. 
Our second algorythm will compare the result with the OMS recommandation result, and return a relatives score out of a hundred. 
The django app will take this score, and the result of data check and show it on a result page.


## Technical Aspect 

We have two technical part in this project :   
- An Algorythm that will process the selection of data
- A Django Web Appplication that will show the data

For constructing the Algorythms we used several datasets and Python libraries : 

- The data come from [The French Data Gouv Website](https://www.data.gouv.fr/fr/)
- Library [Pandas](https://pandas.pydata.org/) to create and modify DataFrame
- Library [Math](https://docs.python.org/3/library/math.html) to make advanced math operations
- Library [Request](https://pypi.org/project/requests/) to get Json data
- Library [URLlib](https://docs.python.org/fr/3/library/urllib.html) to get data from external API
- Library [Statistics](https://docs.python.org/3/library/statistics.html) to make advanced statistics operations
- Library [Numpy](https://numpy.org/) to manages arrays

For the creation of the front part, we used severals tools : 
- Usage of the [Framework Django](https://www.djangoproject.com/) to developp a front app using the back algoryrthms
- Usage of [Bootstrap](https://getbootstrap.com/) to help us design the front part. 

