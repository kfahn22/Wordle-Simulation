# Wordle-Simulation
A Wordle Simulation to test out ideas in p5.js
A list of 10657 guess words is concatenated with a list of 2315 answers to create guessWords.  The draw() function draws the board, prints out statistics re how well the bot is doing, and plays the game for each answer.  

## Global Variables

### Constant Declarations:
const:  BLACK, GREEN, YELLO

### let declarations:
- guesses (array), target, answers, guessWords, 
- allWords, dictionary w/ boolean guessed

### Counters
- round, counts the chances taken to guess the target word
- totalCounts, array that contains how many targets were guessed in the nth round.
- guessCounter, used to seed the first guess
- answerCounter, counts the answers used as targets

### Booleans
allDone, initialized F and updated in startOver() if a game has been played for every target word in answers 

## Functions

### preload() 
loads the txt files with the possible answers and guesswords

### validWords()
This function checks to see if the word has already been guessed.  If there is a previous guess and there is a match, it first checks to see if the new guess has this match.  The function then checks to see if the guess has any letters that are not in the target.  Lastly, it checks for letters that are in the target word, but not in the correct position

My attempt to understand this bit of code:
- lines 50-56:  check each letter in lastGuess.word and see if result is set to BLACK
- line 56:  does lastGuess contain a letter that is not in target word.  ?? I don't understand what lastGuess.results[k]>0 does--why would it ever be > 0?)
- lines 60-69:  if the new word has more blacks than the previous word, it is eliminated

Argument: guesses

Variables: 

- word (const), a single word in list of possible guesses
- allGood (boolean),  initialized T, updated if violates logical play
- greensMatch (boolean),  does the letter at position j in the word match the letter at the corresponding position in the target word  
- noEliminated (boolean), initialized to T
- sameYellow (boolean), initiallized F, updated if the character has already been found in same position (allGood = false)
- yellowsGood (boolean), initiallized T, updated if character is not found in new spot (allGood = false)
- foundYellow (boolean), initalized F, updated if character was not previously found in different spot

Counters:

- countOK, counts the number of blacks in the last guess
- countC, counts the number of blacks in the current guess

Returns:  options, array of valid guesses

### evaluateWord()
This function first updates allWords[word].guessed = T, then checks each character in the word against corresponding character in target; if the character matches, then corresponding value in the two arrays is updated.
Arguments:
word, target
Variables:
results: array of word.length initiallized with BLACK
matched: array of word.length initiallized with false
current:  current character being tested

### nextGuess()
This function executes pickWord() and evaluateWord() and populates the guesses array with a dictionary. For example, if the target is "ABASE" and the last guess is "AFORE", then after the last round we would get:

guesses[4] = {word: "AFORE", results: [1,0,0,0,1]}


### startOver()
- updates allDone = T when all the words in answers have been used as targets
- updates answerCounter
- initializes allWords[word].guessed = F
- resets guesses to {} 

### pickWord()
This function picks a guess to try.  If round = 0, guessCounter is used to pick word; otherwise, it calls validWords() to find all valid options and then returns a random option.

### setup()
- concatenates answers and guesses
- calls startOver()

### draw()
Draws the game board and prints statistics re how well the bot did.  Plays a game for each target answer. 

??? I am not sure what the first for loop is doing.  

allGreen (boolean), initialized T, updated if one of characters is incorrect
completed (boolean), initialized F, updated if round = 6