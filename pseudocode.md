# Trivia Game Pseudo Code

### Parts needed:
    -timer for whole game timer (stops on correct answer and starts on new question
    -individual timer that resets on correct answer OR timeout
    -third timer that lets the player prepare between questions 
        -should start immediately running as soon a correct answer chosen. Maybe 3-4 seconds of "nice job! You have scored 4 and only missed 1 so far... Get ready: 3, 2, 1 GO"
    -start button
    -randomly disperse the correct and incorrect answers
    -disable the incorrect answer? with penalty
    -different topics/difficulties?
    -divs and layout that gets written with a template
        -filled when ever question loads
* 
### Functions
    -gameRun()
        -onclick from start button
        -shows the game div
        -contains the whole game
        -I WANT to put the timer inside this, but I will be stopping and starting the timer, so I might have it parallel to gameRun().

    -gameTimer()
        -gameRun() calls this
*********-maybe resetGame shoudl start this**********

    -resetGame()
        -this is called on the onclick of the start button
        -resets corrects/wrongs/passes
        -will call prepForTrivia()

    -prepForTrivia()
        -this is called after wrongChoice() and correctChoice(), if player didn't lose.
        -the timer is 8.5 seconds total
            -shows the corrects/wrongs/passes 0ms - 5000ms
            -writes 3 at 5000ms, 2 at 6000ms, 1 at 7000,ms and GO at 8000ms
            -loads pullTrivia at 8500ms
        -rewrites itself to ""
        -make sure it STOPS running somehow

    -pullTrivia()
        -STARTS the gametTimer again IF stopped
        -pull question and results div
        -clear last question on the DOM, rewrite the HTML elements
        -and randomize answers and put them on DOM
        -is called from prepForQuestion only

        ***IMPORTANT:
        -to randomize the questions, pick a random function to run, which displays different    combinations of correct/incorrect strings (so the correct answer isn't always 'A',    etc)
        -IF div contains ' or ", pull another.
            -pullTrivia needs to be able to handle this. maybe a func inside it that actually changes the DOM
            -to get the next question, I would probably do question index+1 until I find one with no ' or "

    -correctChoice()
        -STOPS the gameTimer
        -shows the results div
        -animate somehow -- enlarge question and answer together -- if there's time
        -fade out wrong answers
        -correct answer was "..."!
            -happy colors
        -then this function runs prepForQuestion() function
    
    -passQuestion()
        -STOPS the gameTimer
        -shows the results div and correct answer (similar to correctChoice)
        -decrement passes
            -if no passes, disable this button
        -onclick runs prepForTrivia()

    -incorrectChoice()
        -STOPS the gameTimer
        -shows the results div
        -if the wrong choice clicked, increment var wrongA (number of wrong answers)
        -animate somehow -- if there's time
        -correct answer was "..."!
            -sad colors
        -I don't have to check if they lose every click, just on wrong clicks.
        -if checkLoss() returns false, then the prepForQuestion() will run.
            -checkLoss() function at the end of this.
                -it will turn off the gameTimer, so you don't lose, and then lose again when time runs out

    -gameOver()
        -shows the results div
        -this runs at the end of the timer. If it runs from this, congratulate the player
        -this runs if checkLoss returns true. Say "better luck next time" or something
        -This will tally up their scores, and display them.


### Divs / Areas
    -start
        -contains the button and instructions
        -never gets rewritten, only hidden

    -game-area
        -contains the question and the answers and countdown
        -gets reset and rewritten every execution of pullTrivia()
        -contains the small HUD of corrects/wrongs/passes

    -status
        -this shows your current corrects/wrongs/passes larger 
            -doesn't show it on the bottom on this page
            -also shows the current (stopped) time

    -results
        -



### Reminders:
    -if nesting functions, make sure they don't stack on each calling
    -don't use absolute positioning
    -allow myself to make it responsive in future
    -use an API to get trivia questions
    -set up all 3 timers first, the game session timer, then the others inside functions
    
    -IMPORTANT***when I pull questions, they sometimes have things that do not render in HTML, like quotes, symbols, etc. I should prob exlude anything that has those.

    I can find the questions that contain the ' or " symbols. I might be able to replace them.

