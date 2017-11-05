# Cordova Plugin For Play Games Services

Cordova Plugin For Google Play Games Services (Fork of [ptgamr/cordova-google-play-game](https://github.com/ptgamr/cordova-plugin-play-games-services))

Modified to include the new Google Play Services (GoogleApiAvailability) and new methods for Leaderboards and Achievements.

**Before you start:**

Understand about **Leaderboard** and **Achievement**. Setting up your game in Google Play Developer Console https://developers.google.com/games/services/android/quickstart

## Install

Cordova >= 5.0.0

```bash
cordova plugin add cordova-plugin-play-games-services --variable APP_ID=you_app_id_here
```

Cordova < 5.0.0

```bash
cordova plugin add https://github.com/artberri/cordova-plugin-play-games-services.git --variable APP_ID=you_app_id_here
```

## Usage

### Authentication

#### Sign in
You should do this as soon as your `deviceready` event has been fired. The plugin handles the various auth scenarios for you.

```js
window.plugins.playGamesServices.auth();
```

#### Sign out
You should provde the option for users to sign out

```js
window.plugins.playGamesServices.signout();
```

#### Auth status
To check if the user is already logged in (eg. to determine weather to show the Log In or Log Out button), use the following

```js
window.plugins.playGamesServices.isSignedIn(function (result) {
	// ‘result’ is a JSON object with a single boolean property of ‘isSignedIn’
	// {
	// 		“isSignedIn” : true
	// }

	console.log(“Do something with result.isSignedIn”);
});
```

#### Player Information
Fetch the currently authenticated player's data.

```js
window.plugins.playGamesServices.showPlayer(function (playerData) {
	...
	console.log(“Authenticated as ”+playerData['displayName']);
});
```

### Leaderboards

#### Submit Score

Ensure you have had a successful callback from `window.plugins.playGamesServices.auth()` first before attempting to submit a score. You should also have set up your leaderboard(s) in Google Play Game Console and use the leaderboard identifier assigned there as the `leaderboardId`.

```js
var data = {
    score: 10,
    leaderboardId: "board1"
};
window.plugins.playGamesServices.submitScore(data);
```

#### Sumit Score Now

Ensure you have had a successful callback from `window.plugins.playGamesServices.auth()` first before attempting to submit a score. You should also have set up your leaderboard(s) in Google Play Game Console and use the leaderboard identifier assigned there as the `leaderboardId`.

This method submit the score immediately.

```js
var data = {
    score: 10,
    leaderboardId: "board1"
};
window.plugins.playGamesServices.submitScoreNow(data);
```

#### Show all leaderboards

Launches the native Play Games leaderboard view controller to show all the leaderboards.

```js
window.plugins.playGamesServices.showAllLeaderboards();
```

#### Show specific leaderboard

Launches directly into the specified leaderboard:

```js
var data = {
	leaderboardId: "board1"
};
window.plugins.playGamesServices.showLeaderboard(leaderboardId);
```

### Achievements
#### Unlock achievement

Unlocks the specified achievement:

```js
var data = {
	achievementId: "achievementId1"
};

window.plugins.playGamesServices.unlockAchievement(data);
```

#### Increment achievement

Increments the specified incremental achievement by the provided numSteps:

```js
var data = {
	achievementId: "achievementId1",
	numSteps: 1
};

window.plugins.playGamesServices.incrementAchievement(data);
```

#### Show achievements

Launches the native Play Games achievements view controller to show the user’s achievements.

```js
window.plugins.playGamesServices.showAchievements();
```

### Other

#### Success/Failure callbacks

For all methods, you can optionally provide custom success/failure callbacks.

For example:

```js
var successfullyLoggedIn = function () { ... };
var failedToLogin = function () { ... };
window.plugins.playGamesServices.auth(successfullyLoggedIn, failedToLogin);

var data = { ... };
var successfullySubmittedScore  = function () { ... };
var failedToSubmitScore  = function () { ... };
window.plugins.playGamesServices.submitScore(data, successfullySubmittedScore, failedToSubmitScore);
```

## Platform

Currently, only Android is supported


## License

[MIT License](http://ilee.mit-license.org)
