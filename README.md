# Setup
- Install the Node.js with at least version 18.10.0.
- Install the NPM with at least version least 8.19.2.
- Install AngularCLI with at least version 15.0.4.
- Run npm to install dependencies.

# Starting application
Run `npm run start`, application will be available under `http://localhost:4200/`

# Running tests
Run `npm run test`

# Business justification
As a product manager I need an application that will present me the best photos from the movie I will search for.
App should contain two main elements: search box where I can type data, and the table with the photos - see the example mockup in `utils/mockup.png`.

## Task 1 - Movies search box
Create a search box that will accept user input, search for matching movie titles by using external api and display results in a dropdown list under the input.
Search box should react on every user input change.
Maximum number of movie titles should be limited to 10.
If there are no matching elements, display sufficient message like “No movies match your criteria”.

To get the movie titles use this endpoint: `https://imdb8.p.rapidapi.com/auto-complete`.
To connect to API you will also need to pass this params:
```
const options = {
  params: {q: <searchingMovieTitle>},
   headers: {
        'X-RapidAPI-Key': '1ca21be1efmshcd949e1e7351442p1c2c0bjsn029d4edb801d',
        'X-RapidAPI-Host': 'imdb8.p.rapidapi.com'
  }
};
```

Api will return all matching titles in the array called `d`.
Each array element is an object that has a property called `l`. That property contains value to display in search box table.
Except `l` there is also `id` property that will be required later.

## Task 2 Photos list
You have a list of matching titles in the dropdown. In case of selecting any of them you should load a list of images connected with that particular movie.
Images should be displayed below the search box in the table with maximum 3 columns.
List of images should be responsive and works correctly also on lower screen resolutions.
Max number of images is 12.

To get a list of movies you need to use this endpoint: `https://imdb8.p.rapidapi.com/title/get-images`.
To connect to API you will also need to pass this params:
```
const options = {
    params: {tconst: <movieID>, limit: <resultsLimit>},
    headers: {
      'X-RapidAPI-Key': '1ca21be1efmshcd949e1e7351442p1c2c0bjsn029d4edb801d',
      'X-RapidAPI-Host': 'imdb8.p.rapidapi.com'
    }
};
```

API will return all images connected to that movie in array called `images`.
Each array element is an object that has a propert called `url`. That property contains a link to image that you can use in the table.

