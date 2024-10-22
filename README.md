# TYPE TYPE GAME


This project consists in a game of typing, where at the end of it, it will show you how many words you manage to type in the timeframe of a minute and how well was your accuracy with it. There are similar games like this in the internet, the most known one is called monkey type, consisting of the same formula.

To achieve the goal i created 2 files for it to work:
    random_sentece creates a sentence of random words gathered from a .txt file called words_alpha.txt that can be located at the public folder
    game_starter includes all of the features need to play this game

random_setence:
Lets begin with the random_sentence file, since is the base for the game to work.
First thing that was needed to do was fetch the words_alpha.txt file from the public folder (for curiosity this file contains aproximatly 400k english words). After fetch this file i created an array called words, to store all the words from the file, next i created an empty string that will be use further when gathering the random words. getRandomWord do as it's named, grab a random word from the array created before. generateRandomSentence first needs a number of how many words its gonna generate, this is prompt at the game_starter that will be discuss later, it also put each of the words randomly picked in the empty string created before. That's how the sentences are being generated.
There are 2 other arrow functions in this file that will help to register the accuracy, if the complete word you type is correct and the conditions in which a keystroke is correct or wrong. This 2 arrow functions are getCurrentLetter, to check the current letter that it's been type, and getCharClass, which will be used to determine the current letter in the game, and if it's correct or wrong by changing the color of the letter.

game_starter:
This file contain all the necessary features to make the program feels like a game. It has a start and restart arrow function, that give some parameters to how the game should work, it also have a timer that when reaches zero ends the game and show a result screen.
Of all the parameters the only one that is use for a better aesthetic porpose is fadeOut, for the rest of the parameters all are related to the state of the game that will explained now.
numberOfWords defines how many words will be generated from the random_setence.js file
currentIndex is define to zero at the beggining of every game, it porpose is to determine what letter the "cursor" is on and what decision show be made
isCorrect determine if the letter is typed by the user is right or wrong and than communicates to random_sentence.js which color should the letter be and if it can proceed with the typing or it the letter should be corrected.
totalKeystrokes and keystrokesCorrect are related to the total number of keystrokes typed by the user and the corrected ones typed, they're use to determine the accuracy of the user at the result screen.
correctWords, which differs from isCorrect, tracks how many words are completed and correct, than is use in the result screen as well to determine WPS (words per minute). Since the timer is set to one minute, there is no need for dividing how many minutes where passed, i.e. a 2 minutes typing game.
timeLeft is how much time left you got, it can be modified to others values, but for the rendering of the circular progress bar to work properly the current timeLeft must be updated.
showResults and fadeOut are set to false, since the game first need to start to then show the results at the end of the game, fadeOut only helps to make a smoth transition between the typing screen and the result screen.
gameStarted, as isTypingAllowed, are set to false and can be set to true once the user clicks the start or restart button, and than it's switch back to false when the timer runs out.
startGame and restartGame are the two condition for the game to be played, both are called in the handleButtonClick for when the button is clicked in the page. The first time the user load the page the button will be shown as "play" and for consecutive plays without reload the page the button presented will always be "restart". In handleButtonClick there is also document.activeElement.blur, which it is used due to a problem that I was facing regarding the click of the button: everytime a typed space bar it would restart the game since it was still focused on the button, to solve this document.activeElement.blur was implemented.
handleKeyPress is one of the most crucial event in the program, since it listens to the keystroke typed and decides if it should continue to the next letter of the word or not. (note: I first tried to implement an input to register the keystrokes, but was not getting the results that i wanted so I tried a diferent aproach which in the end it turned out to be better). In the same event listener, it also register every keystroke typed, correct or not, and register it to later be used in the result screen. It also generates a new sentence if the user complete all the words in the previous sentence, due to that the game can only ends when the timer hits zero.
The last 2 arrow functions are considerably simple: startTimer is the logic behind the timer, but it also stop the user from typing when time hits zero and it's what procs the fadeOut to the result screen; accuracyScore simply calculates the users accuracy and show it on the render part.
For the rendering part, first is implemented the buttons to start/restart the game with their respective images. After that it is the circular progress bar used as a timer to tell the user approximatly how much time they got left. Later there is a conditional that determines if showResults should be aplied at the moment or not, and if the random-sentence-wrapper should disapear and give space to result-container to fadeIn. Note that both the timer and the random sentence container disappears when the time runs out, but the "play" button stays there all the time. For the aesthetic part i opt for a more minimalist style where every feature of the game is place in the middle of the page.

