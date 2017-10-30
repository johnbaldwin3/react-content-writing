# Using State to Model Events in Redux

In Redux it will be necessary to create and model state that matches the needs of our actions and reducers in Redux. Application state can only be modified by firing an action and using a reducer to create a new updated copy of state. It will be a single source of truth for our application and can be applied to any component that requires it. This is one of the most important concepts behind Redux and helps us manage the complicated idea of state in a singular way. Redux will require the skill to create state objects that model the events of our application.

## You Must Know Your Events to Make Your State

As with any application, thinking ahead before you jump into programming is a must. Planning out your application will help you think logically about all of the pieces required to achieve the goal you are after. With that in mind, we will look at some events we plan to do for a trivial application, to help us better understand what kind of state we will need.

Let's make an application that lets us create and delete players for a game, and keep track of their score.

So what are the events we need?

- Create a player
- Delete a player
- Increment a player's score (add to it)
- Decrement a player's score (subtract from it)

## Create the State for Your Events

With the events (or `actions`) in place, we can then begin to understand what our state object should look like. Without writing any code at first, let's break each action/event down into a few pieces to understand what kind of state it may require.

### Create a Player

To create a player we will need a few things to keep track of:

- We will need a name or number representing each player.
- We should probably have an index of the players so that we can easily refer to a single player.
- We will need a score for the player.

This is starting to feel like an array of objects, right?

### Delete a Player

Deleting a player will require the following:

- We will need the index of the player we select for deletion. We wouldn't want to delete the wrong player!

That should be the extent of the requirements for deleting someone from the score counter.

### Increment and Decrement a Score

This is a very similar event only differing in the outcome of the score. The state for this event will need the following information:

- The score to increment or decrement.
- We get access to that score using the index of the player who has that score we wish to change.

With that, we have laid down the groundwork to actually make our state.

## State Your Case

Since our `actions` trigger our `reducers` to create a new copy of our state we can look at how they might appear first.

We can first think of the `actionTypes`, we will want to be able to `ADD_A_PLAYER`, `DELETE_A_PLAYER`, and `UPDATE_SCORE`, we can set these up as a `const`. We do this so that changes to the action types can occur in a centralized location and do not require searching in multiple locations.

Next, we will look at the `actions` required for each of these `actionTypes` (look to the comments for more information in the code sample):

```js
//creating a new player will need a name to pass on to the new state. The index will be automatically generated if we store this in an array down the road.
export const addPlayer = name => {
  return {
    type: ADD_A_PLAYER,
    payload: name
  }
}

//deleting an existing player will rely on getting the index of that player and passing that information so our reducer can remove that player from the state.
export const deletePlayer = index => {
  type: DELETE_A_PLAYER,
  payload: index
}

//to update a score we will need to know the index of the score to update and the score associated with that player. Since we have multiple payloads, we will name them individually as to what they are. We could also use ES6 syntax and just add index and score singularly without a key value property as we have seen before.
export const updateScore = (index, score) => {
  return {
    type: UPDATE_SCORE,
    index: index,
    score: score

  }
}
```

We have essentially modeled our events and the state they require. Now let's look at the reducers this application would use to see how we can create a new state object based upon the `action` that is fired.

### Reducing

In our a reducers file, we would need to make a `switch` statement to account for each `action` we have created and determine how we will change our state based on the individual `action` that is fired. See the comments in the code to follow along.

```js
//we must import our action types, this can be done a lot of different ways depending on where you store your action types.
import * as ActionTypes from '../actions/actions.js';

// to keep it simple, we will create an initial default state as an empty array of players, so that we can make sure that when no action type is fired or when the action type is not a match we don't return undefined.
const initialState = [];
//now we must create a switch statement that will take the initial state and the action as arguments and then sort through all of the action types and the changes associated with them.
export const Player = (state=initialState, action) {
  //check for action type here
  switch(action.type) {
    //if the action type is ADD_A_PLAYER
    case ActionTypes.ADD_A_PLAYER:
    //return an array with the initial state (...state) and add a new object to it with the name set to the name from the payload and the score set to zero in the beginning.
    return [
      ...state, {
        name: action.payload.name,
        score: 0
      }
    ];
    //if the action type is DELETE_A_PLAYER
    case ActionTypes.DELETE_A_PLAYER:
    //return an array that takes the initial state and will concatenate two arrays together. We will take all of the players up to the player we wish to remove and concatenate them back on to a new array just past the index of the removed player... meaning we created a new array without the player we decided to remove, but containing all of the other players still.
    return [
      ...state.slice(0, action.payload.index),
      ...state.slice(action.payload.index + 1)
    ];
    //if the action type is UPDATE_SCORE
    case ActionTypes.UPDATE_SCORE:
    //this case will assume that we have some sort of increment and decrement set up in our components based on a button click (onChange) event. We will map over our array of players, select the player by the index being passed in when the action is fired, and add or subtract the score based on what onChange event happened. The other scores will remain untouched and we will pass the newly created array from our map function as the new state.
    return state.map((player, index) => {
      if(index === action.index) {
        return {
          ...player,
          score: player.score + action.score
        };
      }
      // else return the player as normal
      return player;
    });
    //lastly we must return our initial state should there not be any changes and our reducer receives undefined - so that we don't receive any errors from redux.
    return state;
  }
}
```

And there you have it, we have mapped and followed state through our actions and reducers.

## Conclusion

- Planning out your application will help you create the state needed to model your events in Redux.
- It's critical to think what information is necessary for each `action`.
- Your `reducers` should follow through with your plan. They should be pure and they should not alter the state, but create a new copy that returns the updated state.

### References

- [Redux Docs](http://redux.js.org/docs/basics/)
