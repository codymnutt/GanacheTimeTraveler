# ganache-time-traveler
A testing toolset that allows developers to write unit tests for the Ethereum blockchain.

[Read my Medium Post](https://medium.com/fluidity/standing-the-time-of-test-b906fcc374a9)

[Watch my Presentation](https://photos.app.goo.gl/6qkd5AN2BthxkY2K6)

[Time Contract Example](https://github.com/ejwessel/TimeContract)


NOTE:
- this only works with ganache-cli
- this only works locally

## Tool Dependencies
- [ganache-cli](https://github.com/trufflesuite/ganache-cli)
- [truffle](https://www.trufflesuite.com/docs/truffle/getting-started/installation)

## Install
- `npm i ganache-time-traveler`

## Usage
add `require` at the top of your tests
```javascript
const helper = require('ganache-time-traveler');
```

add the `beforeEach` and `afterEach` hooks into your test file
 ```javascript
beforeEach(async() => {
    let snapShot = await helper.takeSnapshot();
    snapshotId = snapShot['result'];
});

afterEach(async() => {
    await helper.revertToSnapShot(snapshotId);
});
 ```

## Breakdown of methods
### `advanceTime(<seconds_to_advance_by>)`
_Advances the time on the blockchain forward. Takes a single parameter, which is the number of seconds to advance by.
Note: for advancetime() to take effect, the block must also be mined using `advanceBlock()`. See `advanceTimeAndBlock()` to do both._

### `advanceBlock()`
_Mines a new block; advances the block forward by 1 block._

### `advanceBlockAndSetTime(<new_time>)`
_Advances the block forward by 1 and **sets** the time to a new time._

### `advanceTimeAndBlock(<seconds_to_advance_by>)`
_Advances the block by 1 in addition to advancing the time on the blockchain forward. Takes a single parameter, which is the number of seconds to advance by._

### `takeSnapshot()`
_Snapshot the state of the blockchain at the current block. Takes no parameters. Returns the integer id of the snapshot created._

### `revertToSnapShot(<id_to_revert_to>)`
_Revert the state of the blockchain to a previous snapshot. Takes a single parameter, which is the snapshot id to revert to._

## Resources
- https://github.com/trufflesuite/ganache-cli
- https://www.trufflesuite.com
