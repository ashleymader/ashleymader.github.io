---
layout: post
title:      "Research Required"
date:       2021-03-08 16:35:09 +0000
permalink:  research_required
---


> "When some event happens, I want to make what kind of fetch and then manipulate the DOM in what way?" 

## Goals and Setup
This is the mantra of JavaScript. Up until the project build, I really struggled with understanding how all the pieces fit together. My goal for the project was to create a Where's Waldo-like game. 

I wanted to really stretch myself to learn things outside the curriculum, though. So, I decided to make my image on the screen responsive to browser size. To do so doesn't seem too complicated but in order to map a click on the characters, it definitely threw a curveball in there. I needed to decide if I was going to go with the typical JavaScript game method which utilizes the HTML canvas or go another route. After fiddling with canvas for a bit I decided it wouldn't perform what I wanted for now or for future expansion so instead I went with image mapping.  Having never used this either, it definitely made for a struggle. I wrote a few different functions that enabled me to grab the coordinates of my characters and I was off to a great start. Now I needed to make the image and the character coordinates responsive. After much googling I found a little repo on [GitHub](https://github.com/stowball/jQuery-rwdImageMaps) that allows just that using a few lines of jQuery. 

Once I got my image resizing and characters mapped, I need to live and breathe that JS mantra. Listen for click events, fire a function, manipulate the dom. 


```
img.addEventListener("click", e => { 
    if (e.target.localName === "area") {
        let targetCharacter = e.target
        let foundSound = new Audio()
        foundSound.src = "assets/sounds/confirmation.mp3"
        foundSound.play()

        targetCharacter.parentNode.removeChild(targetCharacter) 

        score+=100
        updateScore() 

        characterCount++
    }
})
```

In this function we are listening for a click on the defined area for a character. As you can see here, I also added a confirmation sound when a character is clicked. After the character is found, I needed to prevent the user for clicking them again and cheating the game. Once that was covered, I added a score function associated with the timer on screen. If a user found all 5 characters before time was up, they would get a 10-point bonus each second remaining. 

```
//Countdown clock
function timer(seconds) {
    const now = Date.now()
    const then = now + seconds * 1000 
    displayTimeLeft(seconds) 

    countdown = setInterval(() => { 
        const secondsLeft = Math.round((then - Date.now()) / 1000)
        
        
        if (secondsLeft <= -1) {
            clearInterval(countdown)
            timerDisplay.innerHTML = `<div> GAME OVER </div>`
            endGame()
            return;
        }

        if (characterCount === 5) {
            score+= secondsLeft * 10 
            updateScore()
            clearInterval(countdown) 
            timerDisplay.innerHTML = `<div> CONGRATULATIONS! </div>`
            endGame()
            return;
        }

        displayTimeLeft(secondsLeft)
    }, 1000)
}
```

When time was up, or all characters were found a modal will display with their username and their score. Upon clicking submit a score is posted to the DB and then a new modal pops up with sorted scores on a leaderboard so they can see how they stack up against the competition. 

## Tips and Tricks 

#### Modal Clicks and Invisible Buttons
To open a modal immediately on page load, you can wait for the DOM to load and fire a click to an invisible button on the page. 
```
document.addEventListener('DOMContentLoaded', () => {
    document.querySelector('#sendFirstClick').click()
});
```
.click() simlulates a mouse click on an event. In this case, the event is my invisible button. 
```
   <button style="display:none" data-toggle="modal" data-target="#myModal" id="sendFirstClick" type="button" class="btn btn-danger">Danger</button>
```

This was also helpful to fire off a modal when the user has finished the game without them needing to do anything. 

#### setTimeout()

When the game is over, the user clicks submit on the modal that has their score, this then fires a POST request. Immediately following, I wanted the DOM to display a new modal with a leaderboard of all scores. I was having an issue with my fetch request firing before my POST request had been completed. I fiddled with async/await a bit with no success. To be honest I probably could have spent more time on learning it, but instead I found a great workaround. 
```
function getHighScores() {
    setTimeout(function(){
        fetch(gamesEndpoint)
        .then(res => res.json())
        .then(allGames => {
            allGames.data.forEach(game => {
                const gameMarkup = `
                <div data-id=${game.id}>
                <h3>${game.attributes.player.username} - ${game.attributes.score} </h3>
                `
                document.querySelector('#eachGameScore').innerHTML += gameMarkup
            })
        })
    }, 100)
    postScoresToPage()
}
```
I set the function to delay firing by 100ms. Within the network tab of DevTools I could see the time difference was *very* small between the POST request finishing and the fetch running. This was a great workaround and should help you in the case you run into this issue as well. 

## No longer a nemesis

By the end of coding this project, I really felt like my grasp and understanding of JS deepened. I felt comfortable adding new features and building on the MVP. I really stretched myself to do things that required me to look outside the curriculum and it paid off. 

