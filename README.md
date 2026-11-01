

testStat.txt
Document

testStat_tutorial.txt
Document
I have code written in Processing that is an interactive graphical aid to understanding binary classification test statistics as an aid to decision making specifically for phyisician and medical students.  The idea is to show a 2 by 2 grid on an axis.  The boxes above the horizontal axis are sized to show proportion of positive testing results and boxes to the left of the vertical axis show the proportion of patients with disease. So 4 rectangles represent True Positive (Top Left), True Negative (bottom right), False Positive (top right) and False Negative (bottom Left).  
The uses is able to drag sliders at the bottom which adjust the prevalence of the disease, and is also able to adjust sliders for specificity (false positive rate) at lower right and sensitivity (true positive rate) at upper left.  "testStat.text" is the code, and testStat_tutorial.txt" is a narrative analysis and tutorial that accompanies the code.  
I want this app to be more accessible on the web. 
Could you convert it to javascript and make it a single page app?
Yes. I converted it into a single self-contained HTML/JavaScript web app—no server, framework, Processing library, or installation required.

It preserves the core visual model from your Processing program: disease prevalence controls the left/right proportions, sensitivity controls TP vs FN, and specificity controls TN vs FP. 

I also made several web-oriented improvements:

Responsive layout for desktop, tablet, and phone.
Mouse and touch dragging directly on the diagram.
Conventional sliders for sensitivity, specificity, and prevalence.
Editable patient population size.
Live TP, FP, FN, TN counts.
Live PPV, NPV, LR+, and LR−.
Toggle between the predictive-value and likelihood-ratio displays.
One-click teaching examples taken directly from your tutorial. 
A collapsible tutorial section based on your existing narrative.
Everything is contained in one .html file, so you can simply upload it to a website.
Running it
You can test it immediately by double-clicking binary_test_explorer.html; it should open directly in Chrome, Firefox, Edge, etc.

No web server is actually required.

For publishing, something as simple as GitHub Pages would work:

index.html
Rename the file to index.html, put it in a GitHub repository, enable GitHub Pages, and you have a public teaching site.

One important design choice: I retained your particularly useful idea that rectangle area represents the actual number of patients in each category, rather than turning this into a conventional static 2×2 table. That's what makes the prevalence/PPV relationship visually intuitive. Your tutorial specifically emphasizes that changing prevalence can dramatically change predictive value without changing sensitivity or specificity. 

I think a good next iteration would be to make this into a more polished medical teaching application, while retaining this exact interactive visualization—for example, progressively introducing sensitivity → specificity → prevalence → PPV/NPV → Bayes/likelihood ratios instead of displaying everything simultaneously.


binary_test_explorer.html
HTML
Great -- exactly what I wanted!  
There are a few minor issues to clean up.  Can we make prevalence easier to adjust?  Currently it can be difficult to grab the vertical axis.  Perhaps some handles on the outside of the graph area?
Done. I added a large ◀ ▶ prevalence handle below the graph, connected visually to the vertical disease/healthy divider.

The handle has a generous grab area for both mouse and touch, changes the cursor to a horizontal-resize cursor, and the original vertical divider remains draggable as well.

I think this is substantially easier to manipulate, particularly at very low or high prevalence where the divider gets close to an edge.


binary_test_explorer.html
HTML
excellent! One last thing regarding licensing - I want to use Creative Commos license CC BY-NC-ND 4.0. .  freely available for non-commercial, Require attrbution to me: (Timothy G. McNaughton MD PhD) with no derivative work allowed.  Can you add this licensing language?
Done. I added both a visible license footer and machine-readable license/author metadata to the HTML.

The wording reflects the official CC BY-NC-ND 4.0 terms: people may copy and redistribute the unmodified work for noncommercial purposes with attribution, while adapted versions cannot be shared under the license. 

The required attribution is:

Timothy G. McNaughton MD PhD

I also included a copyright line, © 2026 Timothy G. McNaughton MD PhD. Some rights reserved., plus a direct link to the official Creative Commons license in the footer.


binary_test_explorer.html
HTML
Excellent!
One last thing -- another use case for the app is to help expand statistics that are reported in a journal.  For example, a study might report Sensitivity and Specificity and prevalence but not show positive predictive value.  This app could be used as kind of a calculator to enter what statistical values are known and then return the rest of the values. 
Could you create a succinct description of this use pattern and I will add it to the "Tutorial" section of the HTML.
Here’s a succinct paragraph that should fit naturally into the Tutorial section:

Using the App as a Statistical Calculator
Published studies often report only some diagnostic-test statistics—for example, sensitivity, specificity, and disease prevalence—without reporting positive predictive value (PPV), negative predictive value (NPV), or the expected numbers of true and false results. This app can also be used as a calculator: enter the values reported in the study and the remaining statistics are calculated automatically. The graphical display then translates the reported percentages into an intuitive population of patients, making it easier to see how many true positives, false positives, true negatives, and false negatives would be expected in clinical practice.

If you want, I can also make this slightly more journal/academic sounding or slightly more student-friendly.

show me the journal/academic wording?
Here’s a more journal/academic version:

Using the App to Extend Reported Diagnostic Statistics
Diagnostic studies frequently report selected measures of test performance, such as sensitivity, specificity, and disease prevalence, while omitting clinically important derived measures such as positive predictive value (PPV) and negative predictive value (NPV). This application can be used to extend the reported data by entering the available test characteristics and calculating the corresponding predictive values and expected frequencies of true-positive, false-positive, true-negative, and false-negative results. Displaying these outcomes for a defined hypothetical population also provides a direct visual representation of how test performance interacts with disease prevalence in the population being studied.

I’d probably use this version in the tutorial—it sounds more rigorous without becoming overly technical.

in vs code, i mistakenly initiated a github repo while I had the file on the desktop. Now, even though, I've created a proper project folder and moved the file there, when I open that folder, VS code wants to open the .git in the parent folder.
What’s happening is that Git searches upward through parent folders for a .git directory. So if you accidentally initialized Git on your Desktop, you probably now have something like:

Desktop/
├── .git/          ← accidental repository
├── MyProject/
│   └── binary_test_explorer.html
├── other files...
When you open MyProject in VS Code, Git sees the .git folder in Desktop and treats the entire Desktop as the repository.

If that Desktop repository was created by mistake and you don't need it, the cleanest fix is simply to delete the accidental .git directory from the Desktop. In PowerShell:

cd $HOME\Desktop
Remove-Item -Recurse -Force .git

Then initialize Git inside the actual project folder:

cd $HOME\Desktop\MyProject
git init

Check it with:

git status
git rev-parse --show-toplevel

The second command should now return:

C:\Users\YourName\Desktop\MyProject
rather than your Desktop.

If you're nervous about deleting .git
You can rename it first:

cd $HOME\Desktop
Rename-Item .git .git-backup

Then open your project in VS Code. If everything behaves correctly, delete .git-backup later.

Also useful in VS Code
VS Code has a setting that controls whether it automatically looks for repositories in parent folders. Search Settings for:

Git: Open Repository In Parent Folders

and set it to:

never

Or in settings.json:

"git.openRepositoryInParentFolders": "never"

I would still remove the accidental Desktop .git, though. Otherwise your Desktop remains a Git repository even if VS Code stops automatically opening it.

Binary Classification is when a test returns one of two qualitative results: 
Yes/No
Positive/Negative 
Present/Absent
With a perfectly accurate diagnostic test for some disease, ALL people with the disease would have positive test results (TRUE POSITIVE rate or SENSITIVITY of 100%;) and ALL people without disease would have negative tests (TRUE NEGATIVE rate or SPECIFICITY: 100%).   A perfect test makes no errors and this perfect accuracy is independent of PREVALENCE (the proportion of people with disease). 
Real-world binary tests are imperfect and make errors of two types: False Alarms and Missed Alarms. If a Fire Alarm goes off without a fire present, that is a False Alarm, or a FALSE POSITIVE test result.  If a Fire Alarm fails to detect a real fire, then that is a MISSED alarm or a FALSE NEGATIVE test result.
Imagine 2000 patients being tested for a disease.  A Contingency Table for a binary test is presented in graphic form below.  The 4 quadrants show the 4 possible outcomes of testing.  The Left side shows people who actually have the DISEASE.  The Right side shows shows HEALTHY people.  The top row shows people who have POSITIVE tests and the bottom row shows those with NEGATIVE tests.  The size of the colored areas representing the 4 quadrants is proportional to the number of patients in the respective classification groups: 

TP: True Positive, 		FP: False Positive
 
FN: False Negative, 		TN: True Negative.  

The starting condition shown in th graphic belos is a test with 75% sensitivity and 90% specificity.   The Sensitivity and Specificity can be varied by clicking and dragging with your mouse.  Likewise, the PREVALENCE can be adjusted by clicking and dragging.  
Sensitivity, and specificity are determined in a controlled environment ideally with gold standard samples of both disease state and samples similar to the ACTUAL population of interest.  Assuming our Sensitivity Specificity and Preevalence numvers are accurate, we want to know how to interpret the test results for a PARTICULAR patient.   That is, we want to know the PREDICTIVE VALUE.
When a patient tests positive for disease, they want to know how likely it is that they ACTUALLY have the disease.  This is the POSITIVE PREDICTIVE VALUE (PPV).
When a patient tests negative for disease, they want to know how likely it is that they ACTUALLY don't have the illness..  This is the NEGATIVE PREDICTIVE VALUE (NPV).  
Things to do and notice:
The graphic below shows possible distributions of 2000 patients into the four possible outcomes of testing based on Sensitivity, Specificity and Prevalence of a test.  The box sizes are proportional to the number of patients listed in each quadrant's label.   Click-drag  any of the colored areas below to change their relative sizes.  For example see how changing TP affects FN, or how changing PREVALENCE doesn't affect Sensitivity or Specificity but has enormous effect on PPV and NPV. 
Special cases: For a perfect test (Sensitivity=100% and Specificity=100%) , PVs are independent of prevalence.
Here's a relationship that can be very confusing.  Even with test that is 99% specific and 99% sensitive (overall accuracy 99%),  It the prevalence is very low, (say 1%), then fully HALF of the positive tests will be FALSE POSITIVE.  Think about that for a moment.  It seems bizarre that a test that is 99% accurate will be wrong 50% of the time in predicting who has the disease.   How can this be?   The key thing is to realize the importance of PREVALENCE.  In this example, the test makes 1% error in both the disease group (that's the sensitivity) and 1% error in the healthy group (that's the specificity).  So if the vast majority of the patients are in the healthy group, the vast majority of the errors will also be in that group.  That is one of the fundamental problems with doing population screening - that is applying tests with even slightly imperfect SPECIFICITY to a patient population that has low prevalence rates will result in lots of false positive results. 
Two-step screening.  Screening Tests are challenging because they are applied in low prevalence populations.  If a single test that has both High Sensitivity AND High Specificity is not available, then a High Sensitivity Test (low False Negative) is used first to identify MOST of the patients with disease in a population.  Although this may produce many false positives, it has the effect of increasing the prevalence of illness in the test-positive cohort.  Then a High Specificity "confirmatory" test is applied to that group to reduce the False Positives. The role of a good clinician is to perform the "screening test" judiciously so as to reduce false positive diagnoses while not missing patients with true illness.  The first "test" that a clinician applies to any patient is the History and Physical Exam test.  By talking with patients and examining them, we are doing testing that either increases or decreases our suspicion of illness.  This has the effect of increasing (or decreasing) the probability of that the patient has the illness.  
Adjust the chart below to show the following relationships:
 When a test with 99% sensitivity and 95% specificity is applied to a population with 5% prevalence of disease, approximately HALF of the patients with positive tests will be FALSE POSITIVEs.  
 When a test with 99% sensitivity and 99% specificity is applied to a population with 1% prevalence of disease, again, HALF of the patients with positive tests will be FALSE POSITIVEs.  
 When a test with 99% sensitivity and 90% specificity is applied to a population with 1% prevalence of disease, 95% of the patients with positive tests will be FALSE POSITIVEs.  
When a test with 80% sensitivity and 99.5% specificity is applied to a population with 3% prevalence, then less than 20% of the people with positive tests will be FALSE Positive - this is what the Stanford Study of COVID prevalence in Santa Clara County suggested. 

Turn an idea into a website
Build a site for a project, portfolio, or idea.


⋮⋮⋮⋮⋮⋮⋮⋮
