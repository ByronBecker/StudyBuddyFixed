# StudyBuddyFixed
Study Buddy - an online app worked on by Byron Becker &amp; Adam Marcus at T9 hacks 2016

<!Doctype html>

<html>

<head>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" integrity="sha384-1q8mTJOASx8j1Au+a5WDVnPi2lkFfwwEAa8hDDdjZlpLegxhjVME1fgjWPGmkzs7" crossorigin="anonymous">

<!-- Optional theme -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap-theme.min.css" integrity="sha384-fLW2N01lMqjakBkx3l/M9EahuwpSfeNvV63J5ezn3uZzapT0u7EYsXMjQV+0En5r" crossorigin="anonymous">

<!-- Latest compiled and minified JavaScript -->
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js" integrity="sha384-0mSbJDEHialfmuBBQP6A4Qrprq5OVfW37PRR3j5ELqxss1yVqOtnepnHVP9aJ7xS" crossorigin="anonymous"></script>
    <script src = 'https://cdn.firebase.com/js/client/2.2.1/firebase.js '>
        // edited version
    </script>   
    <script src='https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js '></script>
    <link href='https://fonts.googleapis.com/css?family=Ubuntu+Condensed' rel='stylesheet' type='text/css'>
    <link rel="stylesheet" type="text/css" href="SB2.css">
    <link rel="stylesheet" href="http://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.4.0/css/font-awesome.min.css">
    <meta name="description" content="StudyBuddy">
    <meta name="author" content="Byron Becker">

    <!-- Stylesheet, database, and jquery links -->
    <title>
        StudyBuddy
    </title>

    <style>
    </style>

</head>


<body>




    <h1 id="Stud"> &mdash; &nbsp;Study.Buddy </h1>





    <div id = "welcome">
       <h1> Welcome to Study.Buddy CU 
        <i class="fa fa-graduation-cap fa-spin"></i> <!-- Spinning grad cap -->
        </h1>
        <p> Please enter your name, email, and course info below to be matched with other CU Students!</p>

        <!-- <form action="myDataRef" method="get" id="classinfo">
Name: &nbsp;<input type="text" name="name"><br>
Email: &nbsp;<input type="text" name="email"><br>
Course (Ex. CSCI 1300): <input type="text" name="course"><br>
       <br>
<button class="submit" type="submit" form="class">Submit </button>
        </form> -->

      <!-- Welcome end-->


  



   <!-- <a href="javascript:togglevisibility('Find a Study Buddy')";> -->

 <br>
<br>
        
   
   <form id="lookup">
       <input type='text' id='nameInput' placeholder='Name' ><br>          <!-- Take in user input to variables-->
       <input type='text' id='courseInput' placeholder='course (e.g. HIST 1310)' > <span>* 4 letter code and number *</span><br>
       <input type='text' id='emailInput' placeholder='email' ><br><br>
        <button>Submit</button>
   </form>
       </div> 
        
    
    <br>
    <br>
    
    
    <div id='messagesDiv'></div>
   <script>
     function displayMessage(msg) {
        $('#messagesDiv').text(msg).css("color", "orange");
     }
    function clearMessage() {
        $('#messagesDiv').text('')
    }
     var myDataRef = new Firebase('https://studybudee3.firebaseio.com');            // Make an instance of Firebase
     $('#lookup').submit(function (e) {                                             // Look to the lookup form for variables
         clearMessage()
         e.preventDefault();                                                        // Prevent the form from disapearing when finished
         console.log("SUBMIT");
         var name = $('#nameInput').val();                                          // Assign values to variables in JS
         var course = $('#courseInput').val();
         var email = $('#emailInput').val();
         var enrollee = {                                                         // Make an object called enrollee with name and email
           name: name,
           email: email
         };
         var obj = {};                                                              // Make an emoty object
         obj[course] = {};                                                          // Manualy set that objects pointer
         var run = false;                                                           // Boolean for running technicality
         myDataRef.child(course).on("value", function(snapshot){            // Get data from the Firebase database and sort by child course
           console.log("before if",run, snapshot.key(), snapshot.val());            // Log statment for debuging
           if(!run){                                                                // Check run is false
             run = true;                                                            // Set run to true
             if (snapshot.val() == null) {                                          // Check if the class being studied is the same as what the curent user wants to study
               //console.log("does not have val", snapshot.val());
               var objRef = myDataRef.update(obj);
                 myDataRef.child(course).push(enrollee); 
                 // Manualy update the key to obj
                 displayMessage("Sorry, no study buddies are available at this time, but you will be put in the queue to be matched!").css("color", "orange");                                 // Print if there is no one studying the requested topic
             } else {
             var emails = "";
             for (var key in snapshot.val())                                        // Otherwise loop through those studyin and provide their emails
             {
               //debugger
               emails += snapshot.val()[key].name + ": " + snapshot.val()[key].email + ", ";
             }
             displayMessage(emails);
           }
             //alert(findMatches(myDataRef.child(course).enrolees))
             myDataRef.child(course).push(enrollee);                                // Add the current enrollee to the study group
           }
         })
         //myDataRef.push({name: name, text: [text]});
         $('#nameInput').val('');                                                   // Set all the fields to blank
         $('#courseInput').val('');
         $('#emailInput').val('');
         return false;
     });
     </script>



    <h3><a href="SBAboutTeam.html">About Us...</a></h3>
























<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.0/jquery.min.js"></script>
<script src="SB.js"></script>


    </body>



</html>
