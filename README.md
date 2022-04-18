# Tic-Tac-Toe-Problem
import random

#to ask user to choose a letter
def select_letter():
let=&quot;&quot;
auto_let=&quot;&quot;
#ask user to select a letter (X or O)
while(let != &quot;x&quot; and let != &quot;o&quot;):
let=input(&quot;Select X or O: &quot;).replace(&quot; &quot;,&quot;&quot;).strip().lower()
if let == &quot;x&quot;:
auto_let=&quot;o&quot;
else:
auto_let=&quot;x&quot;
return let, auto_let

#to prepare a clean board for the game
def clean_board():
#an empty board for X and O values
brd=[&quot; &quot; for x in range(10)]
return brd

#to check if board is full
def is_board_full(board):
return board.count(&quot; &quot;)==0

#to insert a letter (X or O) in a specific position
def insert_letter(board,letter,pos):
board[pos]=letter

#to take computer moves
def computer_move(board,letter):
computer_letter=letter
possible_moves=[]
available_corners=[]
available_edges=[]
available_center=[]
position=-1

#all possible moves
for i in range(1,len(board)):
if board[i] ==&quot; &quot;:
possible_moves.append(i)

#if the position can make X or O wins!
#the computer will choose it to win or ruin a winning of the user
for let in [&quot;x&quot;,&quot;o&quot;]:
for i in possible_moves:
board_copy=board[:]
board_copy[i] = let
if is_winner(board_copy,let):
position=i

#if computer cannot win or ruin a winning, then it will choose a random position starting
#with the corners, the center then the edges
if position == -1:
for i in range(len(board)):
#an empty index on the board
if board[i]==&quot; &quot;:
if i in [1,3,7,9]:
available_corners.append(i)

if i is 5:
available_center.append(i)
if i in [2,4,6,8]:
available_edges.append(i)
#check corners first
if len(available_corners)&gt;0:
print(&quot;it comes here&quot;)
#select a random position in the corners
position=random.choice(available_corners)
#then check the availability of the center
elif len(available_center)&gt;0:
#select the center as the position
position=available_center[0]
#lastly, check the availability of the edges
elif len(available_edges)&gt;0:
#select a random position in the edges
position=random.choice(available_edges)
#fill the position with the letter
board[position]=computer_letter

#to draw the board
def draw_board(board):
board[0]=-1
#draw first row
print(&quot; | | &quot;)
print(&quot; &quot;+board[1]+&quot; | &quot;+board[2]+&quot; | &quot;+board[3]+&quot; &quot;)
print(&quot; | | &quot;)
print(&quot;-&quot;*11)
#draw second row
print(&quot; | | &quot;)
print(&quot; &quot;+board[4]+&quot; | &quot;+board[5]+&quot; | &quot;+board[6]+&quot; &quot;)
print(&quot; | | &quot;)
print(&quot;-&quot;*11)

#draw third row
print(&quot; | | &quot;)
print(&quot; &quot;+board[7]+&quot; | &quot;+board[8]+&quot; | &quot;+board[9]+&quot; &quot;)
print(&quot; | | &quot;)
print(&quot;-&quot;*11)
return board

#to check if a specific player is the winner
def is_winner(board,letter):
return (board[1] == letter and board[2] == letter and board[3] == letter) or \
(board[4] == letter and board[5] == letter and board[6] == letter) or \
(board[7] == letter and board[8] == letter and board[9] == letter) or \
(board[1] == letter and board[4] == letter and board[7] == letter) or \
(board[2] == letter and board[5] == letter and board[8] == letter) or \
(board[3] == letter and board[6] == letter and board[9] == letter) or \
(board[1] == letter and board[5] == letter and board[9] == letter) or \
(board[3] == letter and board[5] == letter and board[7] == letter)

#to repeat the game
def repeat_game():

repeat=input(&quot;Play again? Press y for yes and n for no: &quot;)
while repeat != &quot;n&quot; and repeat != &quot;y&quot;:
repeat=input(&quot;PLEASE, press y for yes and n for no: &quot;)
return repeat

#to play the game
def play_game():

letter, auto_letter= select_letter()
#clean the board
board=clean_board()
board=draw_board(board)

#check if there are empty positions on the board
while is_board_full(board) == False:
try:
position=int(input(&quot;Select a position (1-9) to place an &quot;+letter+&quot; : &quot; ))

except:
position=int(input(&quot;PLEASE enter position using only NUMBERS from 1-9: &quot;))

#check if user selects out of range position
if position not in range(1,10):
position=int(input(&quot;Please, choose another position to place an &quot;+letter+&quot; from 1 to 9 :&quot;))

#check if user selects an occupied position by X or O
if board[position] != &quot; &quot;:
position=int(input(&quot;Please, choose an empty position to place an &quot;+letter+&quot; from 1 to 9: &quot;))

#put the letter in the selected position &amp; computer plays then draw the board
insert_letter(board,letter,position)
#computer move
computer_move(board,auto_letter)
#draw the board
board=draw_board(board)

if is_winner(board,letter):
print(&quot;Congratulations! You Won.&quot;)
return repeat_game()
elif is_winner(board,auto_letter):
print(&quot;Hard Luck! Computer won&quot;)
return repeat_game()

#if &quot; &quot; not in board:
if is_board_full(board):
print(&quot;Tie Game :)&quot;)

return repeat_game()

#Start the game
print(&quot;Welcome to Tic Tac Toe.&quot;)
repeat=&quot;y&quot;
while(repeat==&quot;y&quot;):
repeat=play_game()
