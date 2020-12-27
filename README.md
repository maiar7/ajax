# ajax

var allLinks = document.querySelectorAll("nav .nav-link");

var allMeals = [];
var allCat = []

var Category = "Beef" 



for(var i=0; i< allLinks.length ; i++)
{
    allLinks[i].addEventListener("click" , test)
}


function test(e)
{
    Category =  e.target.text ; //Seafood
    getMeals()//AJAX
}


getCategories()

function getCategories()
{
    var myHttp = new XMLHttpRequest();

    myHttp.open("GET" , "https://www.themealdb.com/api/json/v1/1/list.php?c=list" )
    myHttp.send();


    myHttp.addEventListener("readystatechange" , function(){

        if(myHttp.status == 200 && myHttp.readyState == 4)
        {
            allCat =  JSON.parse(myHttp.response).meals      ; 

            console.log(allCat)
        }

    })
}



/* tamam -----------------*/
getMeals(); // AJAX---> MEals


function getMeals()
{
    var myHttp = new XMLHttpRequest();

    myHttp.open("GET" , "https://www.themealdb.com/api/json/v1/1/filter.php?c="+Category )
    myHttp.send();


    myHttp.addEventListener("readystatechange" , function(){

        if(myHttp.status == 200 && myHttp.readyState == 4)
        {
            allMeals =  JSON.parse(myHttp.response).meals      ; 

            displayMeals()
        }

    })
}

function displayMeals()
{
    var hasalah = ``;

    for(var i=0 ; i< allMeals.length ;i++)
    {
        hasalah += ` <div class="col-md-3">
        <div class="item">
          <img class="img-fluid" src="`+allMeals[i].strMealThumb+`">
          <h2>`+allMeals[i].strMeal+`</h2>
        </div>
      </div>`
    }

    document.getElementById("demo").innerHTML = hasalah;
}
