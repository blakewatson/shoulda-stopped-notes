# Shoulda Stopped Notes

## Server requirements

Maintain a read-only JSON string representing the state of the game:

* Current permanent marker positions
* Current temporary marker position
* Current player turn
* Current dice roll
* Claimed columns for each player
* Player number and info (name, color, etc)

## API

### `GET /api/get-state`

Returns JSON string representing game state

```js
{
  players: [
    { // player object
      name: "Joe Somebody",
      positions: [
        [12, 1], // 12th column, 1st position
        [7, 9]
        // ...
      ]
    },
    // ...
  ],
  tempMarkers: [
    [12, 2],
    // ...
  ],
  turn: “Joe Somebody”,
  dice: [2, 6, 4, 3],
  columnsClaimed: [4, /* ... */]
},
success: true, // request successful
msg: '' // use for error messages
```

### `POST /api/submit-move`

Accepts a JSON string representing the attempted move.

```js
{
  name: "Joe Somebody"
  columns: [], // Array of integers 2-12 (max length: 3)
  continue: true // Boolean
}
```

Returns a JSON string representing game state and/or validation error.

### `GET /api/get-users`

Return an array of all usernames. Example:

```js
[ "tim", "blake", "matt", "anna" ]
