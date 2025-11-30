# 2-Player-Dice-Game

#include <iostream>
#include "die.h"
#include <vector>
#include <unistd.h>
#include <ctime>
#include <fstream>
#include <map>
using namespace std;
const int WINNING_SCORE = 100;
//Joselyns part
void printSplash(){
system("clear");
cout <<"\033[1;34m";
cout << " "/ \\ __________________" << endl <<
\\" << endl <<
"/()\\ \\" << endl <<
"/ \\ () \\" << endl <<
"/ \\ \\" << endl <<
"/ \\
\\" << endl <<
________________
"\\ () / () /" << endl <<
" \\ / /" << endl <<
" \\ / () /" << endl <<
" \\/_______________()/" << endl;
cout << endl;
sleep(1);
cout << "\033[0m";
cout << "\033[1;33m" ;
cout << "________ __ __" << endl;
cout <<"\\
____
______
| | __" << endl;
cout << "| | \\| |/
\\ _/ ___
\\| |/ /" << endl;
_____ __ __
\\ |__| ____ ____
/
_
\ \_/ |__/ |______
\\/
___
__
\\ / /_\\ \\
\\
\\
__
__
__
cout << "| / \\ \\ \\
__
\\ ___/ / | \\ | | | /
__
\\\\ \\___| <" << endl;
cout << "/_______ /__|\\
___ >___ > \\____|__ /__| |__| (____
/\\
___ >__|_ \\" << endl;
cout <<" \\/ \\/ \\/ \\/ \\/
\\/ \\/" << endl;
cout << "\033[0m";
cout << endl;
}
//shahtaj part
void updateLeaderboard(int winner){
//creating a dictionary to store
map<string, int> leaderboard;
ifstream infile("leaderboard.txt");
string name;
int wins;
//reads lines from the file
while (infile >> name >> wins) {
leaderboard[name] = wins;
}
infile.close();
string winnerName = (winner == 0) ? "Player_1" : "Player_2";
leaderboard[winnerName]++;
ofstream outfile("leaderboard.txt");
//writes player and their win into file
for (const auto& entry : leaderboard) {
outfile << entry.first << " " << entry.second << endl;
}
outfile.close();
}
//shahtaj part
void printLeaderboard() {
cout << "\033[1;34m";
ifstream infile("leaderboard.txt");
cout << "\n====== Leaderboard ======\n";
string name;
int wins;
while (infile >> name >> wins) {
if (name == "Player_1")
cout << "Player 1 has a high score of: " << wins << " wins\n";
else if (name == "Player_2")
cout << "Player 2 has a high score of: " << wins << " wins\n";
else
cout << name << " has a high score of: " << wins << " wins\n";
}
infile.close();
cout << "=========================\n"<< endl << endl;
cout << "\033[0m";
}
//Joselyn part
bool Take_Points(int current_player, vector<int>& scores, vector<bool>&
stealPower){
cout << "\033[1;31m";
if (scores[current_player] < 15){
cout << "\nYou need at least 15 points or more!" << endl;
return false;
}
//option to use power
int opponent = (current_player == 0) ? 1 : 0; //switches players
int points_toSteal = 20;
scores[opponent] -= points_toSteal;
cout << "\nUsed steal power on opponent! You took " << points_toSteal
<< endl;
cout << "\033[0m";
//stealPower[current_player] = true;
return true;
}
//Joselyn part
bool Skip(int current_player, vector<int>& scores, vector<bool>&
skipNextTurn){
cout << "\033[1;31m";
if (scores[current_player] < 5){
cout << "\nYou need at least 5 points or more to activate!" <<
endl;
return false;
}
int opponent = (current_player == 0) ? 1 : 0; //switching opponents
scores[current_player] -= 5;
skipNextTurn[opponent] = true;
cout << "\033[1;31m";
cout << "\nOppenent's turn skipped! Player " << opponent + 1 << " next
turn will be skipped! :(" << endl;
cout << "You spent 5 points! OUCH. current score is " <<
scores[current_player] << endl;
cout << "\033[0m";
return true;
}
//Joselyn part
bool automaticWin (int current_player, vector<int>& scores){
cout << "\033[1;31m";
if (scores[current_player] < 500){
cout << "\nCan't belive you try to win without 500 points!" <<
endl;
cout << "Shame on you! Little cheater >:(" << endl;
}
scores[current_player] -= 50;
cout << "\033[0m";
return false;
}
//Joselyn part
void powerupOption(int currentPlayer, vector<int>& scores, vector<bool>&
stealPower, vector<bool>& skipNextTurn){
int option;
cout << "\033[1;36m";
cout << "Power Menu" << endl;
cout << "1. Steal 20 points from opponent (15 points)" << endl;
//update amount of points
cout << "2. Skip opponent's next turn (5 points)" << endl;
cout << "3. Automatic win (500 points)" << endl;
cout << "4. Cancel\n"<< endl;
cout << "Choose an option(1-4): " << "\033[0m";
cin >> option;
switch (option){
case 1:
Take_Points(currentPlayer, scores, stealPower); //works!
break;
case 2:
Skip(currentPlayer, scores, skipNextTurn); //works!
break;
case 3:
automaticWin(currentPlayer, scores); // works!
break;
case 4:
cout <<"\033[1;31m" << "\nPower up canceled." << "\033[0m"<< endl;
break;
default:
cout << "Invalid option. Try again." << endl;
}
}
//Bhumi part
int main() {
srand(time(0));
char playAgain = 'y';
printSplash();
do {
int numPlayers = 2;
cout << "\033[1m" << "\033[1;34m";
cout << "========================\n";
cout << " DICE ATTACK! \n";
cout << "========================\n";
cout << "2-Player Mode Activated!\n\n ";
cout << " Let the game begin!\n";
cout << "\033[0m";
sleep(2);
// creating one die per player
vector<Die> dice(numPlayers);
// creating score tracker
vector<int> scores(numPlayers, 0);
//stealing
their points stolen
//skipping
with not getting skipped
vector<bool> stealPower(numPlayers, false); //all players dont get
vector<bool> skipNextTurn(numPlayers, false); // all players start
//cin >> numPlayers;
//if (numPlayers < 1 || numPlayers > 2) {
// cout << "Invalid number of players. Exiting.\n";
// return 0;
//}
bool gameOver = false;
while (!gameOver){
cout << "\033[1;33m" << "\n========== New Round ==========\n"
<< "\033[0m" ;
vector<int> roundTotals(numPlayers, -1); // to store each
player's total roll for this round
for (int i = 0; i < numPlayers; ++i){
cout <<"\033[1m" << "\n-- Player " << (i + 1) << "'s Turn
--\n" << "\033[0m";
//checking if player is skipped -------------------------
if(skipNextTurn[i]){
cout << "\n Player " << (i + 1) << "'s turn is
skipped!" << endl;
skipNextTurn[i] = false;
continue; //continuing the game
}
bool turnDone = false;
while (!turnDone) {
// main menu
cout <<"\033[1;35m" << "\n ⋄Menu⋄\n";
cout << "1. Roll Dice\n";
cout << "2. View Score\n";
cout << "3. Add powerup!\n";
cout << "4. View Leaderboard\n";
cout << "5. Quit Game\n" << endl;
cout << "Choose an option(1-5): " << "\033[0m";
int choice;
cin >> choice;
cout << endl;
if (choice == 1) {
// rolling the die twice
Die die1, die2; // move this
<------------------------
die1.roll();
die2.roll();
int roll1 = die1.getValue();
int roll2 = die2.getValue();
int total = roll1 + roll2;
roundTotals[i] = total;
cout << "\033[1;32m" << "You rolled: " << roll1 <<
" and " << roll2 << " (Total: " << total << ")\n" << "\033[0m";
turnDone = true;
}
else if (choice == 2) {
cout << "Scoreboard:\n";
for (int j =0; j < numPlayers; ++j) {
cout << "Player " << (j+1) << ": " <<
scores[j] << " points\n";
}
cout << endl;
}
// power up option//
else if (choice == 3){
powerupOption(i, scores, stealPower,
skipNextTurn);
}
//end of power
else if (choice == 4) {
printLeaderboard();
}
else if (choice == 5) {
cout << "\033[1;31m" << "Quitting game. Thanks for
playing!\n" << "\033[0m";
return 0;
}
else {
again.\n" << endl << "\033[0m";
cout << "\033[1;31m" << "Invalid option. Try
}
}
}
if (roundTotals[0]!= -1 && roundTotals[1] != -1) {
if (roundTotals[0] > roundTotals[1]) {
scores[0] += roundTotals[0];
cout << "\033[1m" << "\033[1;93m"<< "\nPlayer 1 wins
this round and earns " << roundTotals[0] << " points!\n" << "\033[0m";
updateLeaderboard(0);
} else if (roundTotals[1] > roundTotals[0]){
scores[1] += roundTotals[1];
cout << "\033[1m" << "\033[1;93m" "\nPlayer 2 wins
this round and earns " << roundTotals[1] << " points!\n" << "\033[0m";
updateLeaderboard(1);
}
else {
cout << "\033[1m" << "\033[93m" << "\nIt's a tie! No
points awarded.\n" << "\033[0m";
}
} else if (roundTotals[0] != -1 && roundTotals[1] == -1) {
scores[0] += roundTotals[0];
cout << "\nPlayer 2 was skipped. Player 1 earns " <<
roundTotals[0] << " points!\n";
updateLeaderboard(0);
}
else if (roundTotals[1] != -1 && roundTotals[0] == -1) {
scores[1] += roundTotals[1];
cout << "\nPlayer 1 was skipped. Player 2 earns " <<
roundTotals[1] << " points!\n";
updateLeaderboard(1);
}
//show scores
cout << "\nCurrent Scores: \n";
cout << "Player 1: " << scores[0] << " points\n";
cout << "Player 2: " << scores[1] << " points\n";
//check win
if (scores[0] >= WINNING_SCORE) {
cout << "\n Player 1 wins the game with " << scores[0] <<
" points!\n";
updateLeaderboard(0);
gameOver = true;
}
else if (scores[1] >= WINNING_SCORE) {
cout << "\n Player 2 wins the game with " << scores[1] <<
" points!\n";
updateLeaderboard(1);
gameOver = true;
}
sleep(1);
}
// asking for playing the game again
cout << "\nWould you like to play again? (y/n): ";
cin >> playAgain;
cout << endl;
} while (playAgain == 'y' || playAgain == 'Y');
cout << "\033[1;31m" << "Goodbye! See you next time.\n" << "\033[0m";
return 0;
}
//h
#pragma once
#include <string>
#include <vector>
/// @brief object representing a single die
class Die
{
private:
uint value;
uint highValue, lowValue;
std::vector<unsigned int> allValues;
protected:
// example mutator that is accessible internally
// and to derived classes (class inheritance)
void setValue(uint);
public:
Die();
Die(uint, uint);
// accessors
uint getValue();
// direct mutators
void setHighValue(uint);
void setLowValue(uint);
// interactions
void roll();
// to_string functions
std::string allValues_toString();
};
//cpp
#include <iostream>
#include <random>
#include <string>
#include <vector>
#include "die.h"
using namespace std;
/////////////////////////////////////////////
// Constructors //
/////////////////////////////////////////////
/// @brief default constructor create a normal six-sided die
Die::Die() : highValue(6), lowValue(1)
{}
/// @brief parameterized constructor for the Die class
/// @param low the lowest value on the die
/// @param high the highest value on the die
Die::Die(uint low, uint high) : highValue(high), lowValue(low)
{}
/////////////////////////////////////////////
// Accessors //
/////////////////////////////////////////////
/// @brief acquire the value of the private data member value
/// @return the private data member value's value
uint Die::getValue()
{
return value;
}
/////////////////////////////////////////////
// Mutators //
/////////////////////////////////////////////
void Die::setValue(uint value)
{
this->value = value;
}
/// @brief set the private data member lowValue
/// @param low the value to set lowValue to
void Die::setLowValue(uint low)
{
lowValue = low;
}
/// @brief set the private data member highValue
/// @param high the value to set highValue to
void Die::setHighValue(uint high)
{
highValue = high;
}
/////////////////////////////////////////////
// Interactions //
/////////////////////////////////////////////
/// @brief update the internal die value based on the high and low
die face values. Additionally updated the pastValues
internal vector that stores all the die rolls for this die.
/// /// void Die::roll()
{
// record a new roll in the collection of all rolls by generating
// a random value between low and high values (inclusive)
allValues.push_back(lowValue + rand() %
(highValue - lowValue + 1));
// set the current die value to the last item in the collection
setValue(allValues.back());
}
/////////////////////////////////////////////
// to_string Functions //
/////////////////////////////////////////////
/// @brief combine all the values into a space separated string
/// @return the space separated string of all the die roll values.
string Die::allValues_toString()
{
string values;
// use concatenation to combine all the values
for(uint val : allValues)
{
values += to_string(val) + " ";
}
// pop off the space after the last number
values.pop_back();
return values;
}
//leaderboard.txt
Player_1 9
Player_2 4
