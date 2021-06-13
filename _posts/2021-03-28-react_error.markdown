---
layout: post
title:      "There is a bug in my code."
date:       2021-03-28 10:34:17 -0400
permalink:  react_error
---


Working on my frontend for my movie-review project I encountered so many errors and one of them was the following.


```
TypeError: Cannot read property 'map' of undefined
MovieList
src/components/MovieList.js:9
View compiled
▶ 24 stack frames were collapsed.
(anonymous function)
src/actions/movies.js:20
View compiled
This screen is visible only in development. It will not appear if the app crashes in production.
Open your browser’s developer console to further inspect this error. Click the 'X' or hit ESC to dismiss this message.
×
 6 | <>
 7 | <h1>Movies:</h1>
 8 | <br></br>
> 9 | <ul>
 10 | {movies.map(movies => <MovieListItem key={movies.id} movie={movies}/>)}
 11 | </ul>
 12 | </>
 | ^
 17 | 
 18 | .then(res => res.json())
 19 | .then(moviesJson => {
> 20 | dispatch({type: SUCCESSFULLY_LOADED_MOVIES,
 21 | payload: moviesJson
 22 | 
 23 | })
```
 
 
 this is telling me there was an issue with the dispatch and my movies. I was stuck and already tired at 2:00 AM,
 i spend half an hours reviewing my whole code to see where the issue was.
 
 I looked at my mapStateToProps and it was like this:
 
 
```
 const mapStateToProps = (state, {match: {params} }) => {
  const movieId = params.id
  let loadingState = state.reviews.moviesLoaded[movieId] || "notSarted"
  return {
   movies: state.movies.movieList.find(movie => movie.id == movieId),
   reviews: state.reviews.reviewList.filter(review =>  review.movie_id == movieId),
   loadingState
  };

};
```



this is on my showpage container for movies and them I was looking on the SUCCESSFULLY_LOADED_MOVIES on my reducer/movies.js


```
import { 
  START_LOADING_MOVIES,
  SUCCESSFULLY_LOADED_MOVIES,
  SUCCESSFULLY_LOADED_MOVIE_REVIEWS,
  SUCCESSFULLY_CREATED_MOVIE
} from '../actions';

const initialState = {
    LoadingState: "notStarted",
    movieList: []
}

export default function MoviesReducer(state = initialState, 
    action) {
   switch (action.type) {
      case START_LOADING_MOVIES:

       return {...state, LoadingState: 'inProgress'}
      
      case SUCCESSFULLY_LOADED_MOVIES:

        return {
          movieList: action.payload, 
          LoadingState: 'Successfull'
        };

      case SUCCESSFULLY_LOADED_MOVIE_REVIEWS:
        const foundMovie = state.movieList.find(movie => movie.id === action.payload.movie.id)
        if(foundMovie) {
          return { state }
          
        } else {
          return {
              ...state,
             movieList: state.movieList.concat(action.payload.movie),
            }
        }

      case SUCCESSFULLY_CREATED_MOVIE:
        return {
          ...state,
         movieList: state.movieList.concat(action.payload),
        }
     

      default:

     return state;
   }

}
```



so the error was telling my or at least I though the issue was on my SUCCESSFULLY_LOADED_MOVIES case but it was looking just fine.


```
case SUCCESSFULLY_LOADED_MOVIES:

        return {
          movieList: action.payload, 
          LoadingState: 'Successfull'
        };
				
```
	
	
After refacoring and chaging stuff around my code. that night I just pause it and when to sleep, and trust me guys, if you are burn out just take a break and you will see things clearly. After a few hours of sleep I came back and notice something on my mapStateToProps, if I am in the show page for movies I should be returning the state of a single movie and not all of them so i changed this line. 
	
`movies: state.movies.movieList.find(movie => movie.id == movieId), to movie: state.movies.movieList.find(movie => movie.id == movieId)`
	
the final result:

```

 const mapStateToProps = (state, {match: {params} }) => {
  const movieId = params.id
  let loadingState = state.reviews.moviesLoaded[movieId] || "notSarted"
  return {
   movie: state.movies.movieList.find(movie => movie.id == movieId),
   reviews: state.reviews.reviewList.filter(review =>  review.movie_id == movieId),
   loadingState
  };

};
```


and on my reducers the actual case that was failing was "case SUCCESSFULLY_LOADED_MOVIE_REVIEWS:"
because i was returning the state as an object where the state was already an object and this was breaking my code.
this is how it looks after it was fixed:


```
 case SUCCESSFULLY_LOADED_MOVIE_REVIEWS:
        const foundMovie = state.movieList.find(movie => movie.id === action.payload.movie.id)
        if(foundMovie) {
          return state 
          
        } else {
          return {
              ...state,
             movieList: state.movieList.concat(action.payload.movie),
            }
        }
			
```
			
errors can be treaky and something there will not be clear enough. So unless like me be sure to plan out how your code will be working and dont burn yourself to much. We need to have a clear mindset to be able to function.

