# Overview

Your challenge is to envision a text messaging application that would be useful to Vanderbilt 
students, stafff, visitors, faculty, patients, etc. You must identify a group of people that
come to Vanderbilt (or the medical center) that you are going to help. You then need to empathize
with this group of people and figure out how to solve a problem they face or improve their
experience with Vanderbilt in some way. The only constraint is that the *INITIAL* interface to the 
application must be text messaging. For example, a text messaging application that responds with
URLs that pull up a web page with useful information is fine.

You must be able to complete the initial prototype by the Part 3 deadline listed on Brightspace.
All other deadlines are listed on Brightspace.

# Part 1

For the first part of the assignment, you need to go and talk to the group of people that you 
intend to help. You can help anyone that you want, but you must go talk to them. 

For Part 1, you need to do two things:

  1. Write down at least 10 questions that you plan to ask your target audience. 
  
     Your questions should help you to emphathize with the person. For example, 
     "Why do you do X this way?" would be helpful question to understand the motivation
     for how this person currently approaches something. Each question should provide
     meaningful insight for you into how you design your solution to take into account
     their needs. 
     
     You are free to ask any questions that you want above and beyond these. However,
     you must ask each of the questions that you produce. Feel free to include questions
     like "Who else should we talk to?" that help you, but don't include those questions
     in what you turn in.
     
   2. Interview 3 people from your target group, ask them each question, and write down
      notes about their answers.
      
   3. Write the questions and answers down as GitHub flavored Markdown in a README.md file with this format:
   
   ```
   # <Fill in Project Title>
   
   ... a 3-paragraph overview of the project that is written AFTER you complete
   the interviews ....
   
   # Questions:
     1. ...
     2. ...
     3. ...
   
   # Answers:
   
   ## Question 1: 
   ...answers from everyone to question 1....
   ...
   ...
   
   ## Question 2:
   ...answers from everyone to question 2....
   ....
   ```
   
   4. Create a public repo on GitHub and add the README.md file to it. **Make sure that you do not list the
      people that you interviewed by name, email, etc. in the README.md file. Ensure that you only list identifying
      details of who you interviewed if they explicitly give you permission.**
      
   5. Submit a simple part1.txt file to Brightspace with the following format (DO INCLUDE identifying details of 
      who you talked to):
   
   ```
   Project Repo: https://github.com/<you>/<your project>
   
   Interviewed:
   Bob Smith, Nurse, VUMC, bob.doesntexist@vumc.org
   Jill....
   
   ```

# Part 2

Using what we have discussed in class, particularly relating to the importance of empathisizing with users, describe
your process for building the application. Your process should begin at the early design stages of empathizing with the
user, collecting requirements, etc. and run through brainstorming solutions to implementation to testing and on 
to maintenance. You should explain what you would do to ensure that the application development is sustainable, that 
you are building something of value to users, and that your assumptions are correct. You are free to use any 
processes, patterns, etc. that you want. You should make sure that you capture the requirements for the application
and your overall goals in some reasonable format (you choose the format, but make sure it makes sense for the problem /
process).

Add your requirements and process to your README.md file at the end as this section:

```

....
   # Answers:
   
...
   ## Question 2:
   ...answers from everyone to question 2....
   ....
   
   # Requirements
   
   .... your requirements here ...
   
   # Development Approach
   
   .... your approach here ....
```

Submit your description as part2.txt in Brightspace using this format:

```
Project Repo: https://github.com/<you>/<your project>

```

You will be scored based on:

1. How well you cover all of the important phases from requirements gathering to implementation and testing
2. How you explain the motivation of each step
3. How effectively you explain why you chose the style of development process that you did
4. How clearly laid out the ordering and steps in your process are
5. How convincingly you describe why your process will mitigate the risks of building the wrong thing, failing
   to work in practice, making the wrong assumptions, etc.
6. How you handle estimation and communication of estimates, estimate refinement, etc.


Frequently asked qeustions:

1. How long does it need to be? As long as you feel is sufficient.
2. Can I rewrite X in the original application code? Yes, but you still have to provide a reasonable prototype
   by the same deadline.
3. Can I use XYZ library, etc.? Yes.
4. What format should I use to describe my development approach? Describe it as if you were trying to communicate
   it to a new team member and wanted them to know what you do and why you are doing it. You choose the format that
   you think best accomplishes those goals.
5. Can I choose something larger than can be completed by the deadline? Yes, but you must "stub" out the functionality
   and have at least some reasonable piece of the application completed. You will need to give a demo of your
   application and explain why the parts that you built were the most important to start with and provide 
   convincing evidence that you have a good solution.


# Part 3

Implement, document, test, and deploy your application. Deployment instructions for the original code base will
be posted soon.

Just like real world software engineering, you should expect and plan for requirement changes. Any changes will
be announced via the class mailing list and added to this README.md file.

You will be scored on:

1. How well the application solves the intended problem
2. Complexity of the problem that you tackle
3. Quality of implementation of the prototype
4. Quality of the documentation and ease of use
5. Quality of the tests
6. How well your demo goes

Turn your solution in by committing your code to a branch named "prototype" and then submitting a part3.txt file
to Brightspace in this format:

```
Project Repo: https://github.com/<you>/<your project>

```

You have the option of 1) personally demoing your app in class, 2) having the instructor demo your app live in class via a script, 3) turning in screenshots / screencasts of your deployed app working, or 4) turning in a screencast of an undeployable app working in the terminal. Screencasts of undeployed apps will not score well. 

Regardless of what option you choose, you must fill out the demo sign-up form sent to you via email and posted on Brightspace.

If you choose to demo personally, you do not need to do anything other than make sure you have a way to display the text messaging or other interactions (or a screencast) on the projector in class. 

If you choose to have the instructor demo the app, bring a printed copy of the demo script with you and give it to the instructor.

If you choose to turn in screenshots or a screencast, add Dropbox, Google Drive, Box, etc. links to them in your part3.txt file.


