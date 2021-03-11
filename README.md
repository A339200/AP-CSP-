/******************************************************************\
                           Instructions- 
     The user of this program clicks on the white box,
  enters in a singular name, and clicks on the "Add Name" button.
  Doing this will add the name to a new list. The list will appear
  on the screen in a display box separated by commas and the number
  of inputs will be displayed below the box. If the user adds more 
  than 6 names to the list, a notice will pop up stating that the 
  user has added too many names and will need to refresh the page. 
  If 6 names or less are added, then the user can click on the 
  "Randomize" button at the bottom of the screen and the display
  box will show a random name slected from the user created list.
\******************************************************************/



/************************************************\

                    Purpose: 

 This portion of the code sets the index to zero, 
collects the user's inputs, and
stores them in a list.

                    Function: 

 When the program is first run, the index sets
to zero and the namesList is cleared. When the
user adds a name to the list, the index 
increases by one and the namesList collects
the name provided, stores it as a string, and
adds new names to the end.

\************************************************/
var index = 0;
var namesList = [];



/****************************************\

                Purpose: 

 This function calls
the program overall throgh one 
function calling to simplify
the complexity.

                Function: 

 When the program is run, the
chooseName function is called
and all of the sub functions
as well. From this, the computer
can move through the program
easily and in the correct order
and anyone who may be reading the 
code can see the correct call order
if the program needs to be replicated.

\****************************************/
chooseName();



/**********************************\

            Purpose: 

 This function calls
the addToList and pickRandom 
functions from below.

            Function: 

 The function of calling these 
two functions and combining them
into one function to be called
is to abstract the rest of
the code and to help keep it 
in order so the program works
properly.

\********************************/
function chooseName() {
  addToList();
  pickRandom();
}



/********************************************\

                  Purpose: 

 The purpose of addToList is to
collect the name the user is adding
and display it as a new name at the
end of the list on the screen already.

                  Function: 

 When the addName button is clicked, the
information from the nameInsert element
on the screen is collected and appended 
to the namesList. The nameInsert box's 
text is set to blank and the index
number is updated. A function named
updateScreen is called and the screen
displays the new information on the UI.

\*********************************************/
function addToList() {
  onEvent("addName", "click", function() {
    appendItem(namesList, getText("nameInsert"));
    setProperty("nameInsert", "text", " ");
    index++;
    updateScreen();
  });
}



/**********************************************\

                   Purpose: 

 The purpose of the pickRandom function
is to randomize the user created list 
and to display the random name every time
the randomize button is clicked on the UI.

                   Function: 

 When the nameRandomizer button is clicked,
the listNames variable collects the list
that is being displayed in the nameDisplay
box. The variable randomName is set equal
to listNames. A while loop runs and iterates
through the namesList by selecting a random 
number between 0 and the namesList index. The 
randomName variable selects the index number 
and compares it to the text strings in the 
namesList. It matches up with the correct name
for that number index and a for loop sets the
random name to the nameDisplay for the user to
see.

\*************************************************/
function pickRandom() {
  onEvent("nameRandomizer", "click", function() {
    var listNames = getText("nameDisplay");
    var randomName = listNames;
    while ((randomName == listNames)) {
      randomName = namesList[(randomNumber(0,namesList.length -1))];
    }
    for (var i = 0; i < 4; i++) {
      setProperty("nameDisplay", "text", randomName);
    }
  });
}



/*************************************************************\

                          Purpose: 

 The updateScreen function sets the screen 
up with the new information that is provided
by the user and created by the program for the
user to see.

                         Function: 

 The program runs and when the updateScreen 
function is called the nameDisplay box appears
on the UI. The text inside the box is collected 
from the namesList and the strings are added together, 
separated by commas. The index display element
lengthOfInputs unhides on the screen and then is 
updated to match the new index based on how many names 
have been added to the namesList. Finally, the listError
function is called and displays the proper error message
if necessary.

\****************************************************************/
function updateScreen() {
  showElement("nameDisplay");
  setText("nameDisplay", namesList.join(","));
  showElement("lengthOfInputs");
  setText("lengthOfInputs", index);
  listError();
}



/********************************************\

                Purpose: 

 The purpose of the listError function is
to show the user an error message when
there are too many or too few names 
added into the lsit.

                Function: 

 The function of listError begins by
getting the number from the displayed
text in the lengthOfInputs element.
If the number is greater than 6, an
error message appears prompting the 
user to refresh the page and start 
again. If the number is less than 2,
the message will ask the user to
add at least one more name so the 
program can function properly.
If the index number is between
2 and 6, then no message is displayed
and the user can proceed to use the 
program.

\***********************************************/
function listError(inputLength) {
  inputLength = getText("lengthOfInputs");
  if ( inputLength > 6) {
    setText("lengthError", "List too long, please refresh the page and start again.");
  } else if ((inputLength < 2)) {
    setText("lengthError", "The list is too short, please add at least one more name.");
  } else {
    setText("lengthError", "");
  }
}



//  No outside sources used in the making of this code  \\
