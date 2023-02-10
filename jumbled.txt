import java.util.Scanner;
import java.util.concurrent.ThreadLocalRandom;
 
// How to create a Jumble word game in Java
 
public class JumbleGame {
 
    private static final String[] WORDS_DATABASE = new String[] {
        "superman","jungle","programmer","letter","house","helium"
    };
     
    public static void main(String[] args) {
        JumbleGame jg = new JumbleGame();
        jg.startGame();
    }
 
    /**
     * Run a game of Jumble in Java. The steps in the game are,
     * 1. Get a random word from the words database
     * 2. Shuffle/jumble the word by randomly shuffling characters
     * 3. Present the jumbled word to the user and ask him to guess the word.
     * 4. Repeat the guess till answer is found or user decides to quit.
     */
    private void startGame() {
        int numberOfGuesses = 0;
        String original = selectRandomWord();
        String shuffled = getShuffledWord(original);
        boolean gameOn = true;
        while(gameOn) {
            System.out.println("Shuffled word is: "+shuffled);
            numberOfGuesses++;
            String userGuess = getUserGuess();
            if(original.equalsIgnoreCase(userGuess)) {
                System.out.println("Congratulations! You found the word in "+numberOfGuesses+" guesses");
                gameOn = false;
            }else {
                System.out.println("Sorry, Wrong answer");
            }
        }        
    }
     
    /**
     * Get the user's word guess from command line
     * @return 
     */
    public String getUserGuess() {
        Scanner sn = new Scanner(System.in);
        System.out.println("Please type in the original word: ");
        return sn.nextLine();
    }
     
    /**
     * Select a random word from the WORDS_DATABASE array.
     * @return 
     */
    public String selectRandomWord() {
        int rPos = ThreadLocalRandom.current().nextInt(0, WORDS_DATABASE.length);
        return WORDS_DATABASE[rPos];
    }
     
    /**
     * Shuffle the original word by randomly swapping characters 10 times
     * @param original
     * @return 
     */
    public String getShuffledWord(String original) {
        String shuffledWord = original; // start with original
        int wordSize = original.length();
        int shuffleCount = 10; // let us randomly shuffle letters 10 times
        for(int i=0;i<shuffleCount;i++) {
            //swap letters in two indexes
            int position1 = ThreadLocalRandom.current().nextInt(0, wordSize);
            int position2 = ThreadLocalRandom.current().nextInt(0, wordSize);
            shuffledWord = swapCharacters(shuffledWord,position1,position2);
        }
        return shuffledWord;
    }
 
    /**
     * Swaps characters in a string using the given character positions
     * @param shuffledWord
     * @param position1
     * @param position2
     * @return 
     */
    private String swapCharacters(String shuffledWord, int position1, int position2) {
        char[] charArray = shuffledWord.toCharArray();
        // Replace with a "swap" function, if desired:
        char temp = charArray[position1];
        charArray[position1] = charArray[position2];
        charArray[position2] = temp;
        return new String(charArray);
    }
}