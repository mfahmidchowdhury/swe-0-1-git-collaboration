1. Where does your code live?
After you save the file: Your changes exist only in your Working Directory on your local computer disk.

After git add: Your changes move to the Staging Area (Index) on your local machine, marked ready to be committed.

After git commit: Your changes are saved as a permanent snapshot in your local Git Repository (.git folder) on your computer.

After git push: Your changes are uploaded to the Remote Repository hosted on GitHub.

After your partner runs git pull: Your changes are downloaded from GitHub directly into your partner's Working Directory and local repository.

At which point can your partner see your work?

Your partner can see your code on GitHub right after you run git push.

Your partner can see and run your code locally on their machine right after they run git pull.

2. Predictions vs. Reality
Our predictions: We predicted that Partner B's push would either overwrite Partner A's file or throw a general server error.

What actually happened: Git rejected the push with [rejected - non-fast-forward] because the remote repository contained commits that Partner B did not have locally.

Why Git rejected the push: Git enforces history integrity. Because Partner A pushed changes first, the remote main branch was ahead of Partner B's local branch. Git prevents pushing when history has diverged to protect work from being silently overwritten.

What git pull did that push couldn't: git pull fetched the latest commits from GitHub and attempted to merge them into Partner B's local files. It placed conflict markers (<<<<<<<, =======, >>>>>>>) directly in main.py so we could manually resolve the overlapping lines before pushing.


3. Resolving a ConflictHow we decided what to keep: In Round 2, we conflicted on line 2 (Written by...). 

We looked at both versions together, deleted the conflict markers (<<<<<<<, =======, >>>>>>>), and combined our names into a single clean line: print("Written by: Fahmiddd and Ahmat").   

How we confirmed the resolution was correct: Before running git add main.py, we:Verified there were no leftover Git conflict syntax markers in main.py.   Checked that main.py contained all 10 complete print() statements.   Ran python main.py in the terminal to confirm the script executed without syntax errors.

4. Getting UnstuckThe moment something didn't work: When running git pull, the terminal blocked the merge and threw a configuration error:fatal: invalid value for 'pull.rebase': 'falsegit'   

What we checked first: We checked the terminal output to read the exact error string and inspected our local Git configuration.   What fixed it: We had a typo in our Git settings where falsegit was typed instead of false. Running the fix command resolved it immediately:   
git config pull.rebase false

5. Commit Messages for a Team
Most useful commit message: "Merge branch 'main' - resolve second merge conflict"Why: It explicitly explains what action was taken (resolving a merge conflict) and why the commit exists in the project history.   
Least useful commit message: "added"   
Rewrite for clarity: "Add initial Brooklyn story print statements to main.py"
Why clear commit messages and pulling matter with 5 people:
Clear commit messages: With 5 developers, dozens of commits enter main daily. 
Descriptive messages make it easy to audit changes, track down bugs, and understand feature progress without inspecting every diff.

Pulling before starting: Pulling the latest changes (git pull) before starting new work prevents developers from building on top of outdated code, reducing messy multi-file merge conflicts across the entire team.