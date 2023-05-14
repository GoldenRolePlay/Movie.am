# Movie.am
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <title> Movie Guid App | Professional </title>
</head>

<body>

    <div class="container">
        <div class="search-container">
            <input type="text" id="movie-name" placeholder="Enter movie name here..." value="Wednesday">
            
            <button id="search-btn">Search</button>
        </div>
        <div id="result"></div>
    </div>



    <script src="key.js"></script>
    <script src="index.js"></script>

</body>

</html>
let movieNameRef = document.getElementById("movie-name");
let searchBtn = document.getElementById("search-btn");
let result = document.getElementById("result");

//function to fetch data from api

let getMovie = () => {
    let movieName = movieNameRef.value;
    let url = `http://www.omdbapi.com/?t=${movieName}&apikey=${key}`;
    //if input field is empty

    if (movieName.length <= 0) {
        result.innerHTML = `<h3 class="msg">Please enter a movie name </h3>`;
    }

    //if input isn't empty
    else {
        fetch(url).then((resp) => resp.json()).then((data) => {
            //if movie exist in database
            if (data.Response == "True") {
                result.innerHTML = `
                    <div class="info">
                        <img src=${data.Poster} class="poster">
                        <div>
                            <h2>${data.Title}</h2>
                            <div class="rating">
                                <img src="star-icon.svg">
                                <h4>${data.imdbRating}</h4>
                            </div>
                            <div class="details">
                                <span>${data.Rated}</span>
                                <span>${data.Year}</span>
                                <span>${data.Runtime}</span>
                            </div>
                            <div class="genre">
                                <div>${data.Genre.split(",").join("</div><div>")}</div>
                            </div>
                        </div>
                    </div>
                    <h3>Plot:</h3>
                    <p>${data.Plot}</p>
                    <h3>Cast:</h3>
                    <p>${data.Actors}</p>
                `;
            }

            //if movie doesn't exist in database
            else {
                result.innerHTML = `<h3 class="msg">${data.Error}</h3>`;
            }
        })
            //if error occurs
            .catch(() => {
                result.innerHTML = `<h3 class="msg">Error Occured</h3>`;
            });
    }
};

searchBtn.addEventListener("click", getMovie);
window.addEventListener("load", getMovie);

@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;600;700&display=swap');

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Poppins', sans-serif;
}

body{
    height: 100vh;
    background: linear-gradient(#1c1917 50%, #ffb92a 50%);
}

.container{
    font-size: 16px;
    width: 90vw;
    max-width: 37.5em;
    padding: 3em 1.8em;
    background-color: #1e293b;
    position: absolute;
    transform: translate(-50%, -50%);
    top: 50%;
    left: 50%;
    border-radius: 0.6em;
    box-shadow: 1.2em 2em 3em rgba(0, 0, 0, 0.2);
}

.search-container{
    display: grid;
    grid-template-columns: 9fr 3fr;
    gap: 1.2em;
}

.search-container input, .search-container button{
    font-size: 0.9em;
    outline: none;
    border-radius: 0.3em;
}

.search-container input{
    background-color: transparent;
    border: 1px solid #a0a0a0;
    color: #fff;
    padding: 0.7em;
}

.search-container input:focus{
    border-color: #fff;
}

.search-container button{
    background-color: #ffb92a;
    border: none;
    cursor: pointer;
}

#result{
    color: #fff;
}

.info{
    position: relative;
    display: grid;
    grid-template-columns: 4fr 8fr;
    margin-top: 1.2em;
}

.poster{
    width: 100%;
}

h2{
    text-align: center;
    font-size: 1.5em;
    font-weight: 600;
    letter-spacing: 0.06em;
}

.rating{
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.6em;
    margin: 0.6em 0 0.9em 0;
}

.rating img{
    width: 1.2em;
}

.rating h4{
    display: inline-block;
    font-size: 1.1em;
    font-weight: 500;
}

.details{
    display: flex;
    font-size: 0.95em;
    gap: 1em;
    justify-content: center;
    color: #a0a0a0;
    margin: 0.6em 0;
    font-weight: 300;
}

.genre{
    display: flex;
    justify-content: space-around;
}

.genre div{
    border: 1px solid #a0a0a0;
    font-size: 0.75em;
    padding: 0.4em 1.6em;
    border-radius: 0.4em;
    font-weight: 300;
}

h3{
    font-weight: 500;
    margin-top: 1.2em;
}

p{
    font-size: 0.9em;
    font-weight: 300;
    line-height: 1.8em;
    text-align: justify;
    color: #a0a0a0;
}

.msg{
    text-align: center;
}

@media screen and (max-width: 600px) {
    .container{
        font-size: 14px;
    }
    .poster{
        margin: auto;
        width: auto;
        max-height: 10.8em;
    }

    .info{
        grid-template-columns: 1fr;
    }

}
