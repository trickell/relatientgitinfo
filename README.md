# Relatient Git Information
This provides an overall explanation of our git flow, and how to manage the repositories on our side of things. It explains it in great detail. This will go over how to clone down our work, the tools you will need when viewing from a local machine, the commands to deal with issues. It will also have a common problems section and explain examples on how to overcome these issues.

# Tools Needed for your local machine
<ul>
  <li>git</li>
  <li>php, mysql, apache</li>
  <li>composer <a href="https://getcomposer.org/">Found Here</a> (Installation Instructions on the site)</li>
  <li>diffmerge</li>
  <li>A Text Editor of some sort</li>
  <li><b>Cheat Sheets</b>
    <ul>
    <li><a href="http://www.git-tower.com/blog/git-cheat-sheet/">Git Cheat Sheet</a></li>
    <li><a href="http://cheats.jesse-obrien.ca/">Laravel Cheat Sheet</a>
    </ul>
  </li>
</ul>

# Setup By Machine
<ul>
 <li><b>Installing PHP / MySQL / Apache</b>
 <p>
   <strong>OSX MACHINE: </strong> To get started on an OSX machine you need to start by installing PHP, MySQL, and Apache. There are several ways to go about doing this, I am going to point to the easiest way to start. MAMP is by far the easiest when it comes to setting up all 3 on a machine. You can find the download by <a href="https://www.mamp.info/en/downloads/">Following this Link</a>. Once there, just get the newest version, and follow the wizard to install. In OSX, Your htdocs folder will be under your /Applications/MAMP/htdocs path.
   </p>
   <p>
   <strong>LINUX MACHINE: </strong> To get started on Linux, just install the LAMP stack. Based on your distro, you might need to find different directions. <a href="https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu">Here is a link and guide</a> on how to install the LAMP stack via Ubuntu. In ubuntu, your folder will be under /var/www path.
   </p>
 </li>
 <li><b>Installing GIT</b>
 <p>
 After your first step, to install GIT, follow the link provided (https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and follow the directions to install GIT by your machine type. Once GIT is installed, you can check by opening up a terminal / command line tool and running the "git" command to make sure it installed correctly.
 <p>
 </li>
 <li><b>Installing Composer</b>
 <p>
 Installing Composer works the same way on both machines. Just follow the link provided (https://getcomposer.org/download) and follow the instructions on this page to get composer up
 and running. To install it globally, make sure it gets moved to your /usr/local/bin folder as composer. Then you can run it anywhere as "composer install" without having to give it a direct path.
 </p>
 </li>
 <li><b>Installing Diffmerge</b>
 <p>
 To install diffmerge, follow the link provided (https://sourcegear.com/diffmerge/downloads.php) and based on your OS, choose the correct download. Just use the instructions / wizard provided to install it. Once installed, you need to set this up with git to be your main merge tool. You can do this by running this command in the terminal: "git config --global merge.tool diffmerge". This will modify the global config file for git and set diffmerge as the tool to be used when doing merges.
 </p>
 </li>
 <li><b>Installing Text Tools</b>
 <p>
 Last but not least, you need a way to edit / save files. I've found a new favorite free text editor that I'll point your way, but any IDE or Text editor will work. I use Jetbrains PHPStorm as my IDE, but currently, my favorite free text editor is one called Atom. It's a very configurable text editor that just came out not too long ago with a great backing. This can be found by following this link: https://atom.io/
 </p>
 </li>
</ul>
   
  

# Git Clone URL
Most everything you need to do can be done in terminal when it comes to git
http://10.135.5.101:/var/www/html/repository

In order to clone this repository, use the command below: <br/>
<em>git clone username:password@10.135.5.101:/var/www/html/repository_name</em> [optional/local/path]

<p>
Once cloned down, the first thing you need to do is use composer to install laravel's foundation files in the repository. To do this, go inside the repository root folder, and run: <b>composer install</b>. As long as PHP and Apache was installed correctly, this should update laravel correctly based on the projects composer.json requirements. To be safe, after this runs it's always good to run: <b>composer update</b> as well. If you run into a 500 error, there are a few things that can be checked.
<br/><br/>
1. Make sure your error log in config/app.php is turned on so you can see why the page is erroring out.
<br/>
2. If it's 500 error, check to make sure your permissions on the storage folder and readable, and writeable. Usually a chmod 775 -R /storage folder will work and make sure the chown is correct on the folder for you.
<br/>
3. If your getting a KEY error, you just need to create a new key for your application. The solution is using the php artisan key:generate command.
</p>

# Git Commands needed to know while modifying files
<div>
 <p>
 Now that you have a working project that you can view locally, you can start making modifications to the files / folders. So let's say we want to start a new feature called <b>Demand</b> for the repository. The best practice to keep everything seperate is by using git to create a branch for this feature.
 </p>
 <p>
 To create a branch using git use the command <b>git checkout -b branchName</b>. branchName in this case would be demand. This will create a new local branch and check it out for you at the same time. To view the branches you currently have just use <b>git branch</b>. For a more accurate listing / details use <b>git branch -avv</b>. This will list all the branches, remote branches, what they are tracking, and the last commit on those branches.
 </p>
 <p>
 Now that were in a new branch, we can start making changes to the files. Once changes are made there are steps that need to be taken to get those changes up. Below is a in order list, and explanation. Also, you can run git status to view the modified files, and what needs to be added / committed.
 </p>
 
 <ul>
   <li>
   1. git add . OR git add /path/to/file [ This will add the modified or not tracked files into the repository to be ready to be committed.
   </li>
   <li>
    2. git commit -m "Message For Commitment" [ This will commit the files so they'll be ready for a merge or a push]
   </li>
   <li>
    3. git fetch origin [ This will fetch all the changes from the server and the changes needed to merge ]
   </li>
    <li>
    4. git merge origin branchName OR git pull origin branchName [ This will merge the remote branch with your local branch ]
   </li>
   <li>
    5. If theres a conflict, you need to use diffmerge to resolve that conflict. If not, your ready to push the changes up using: git push origin branchName [Pushes the changes up to the branch on the server]. Understand that the branch on the server can NOT be checked out in order to push to it. If it is, create a new branch on the server to push to.
   </li>
</ul>
<p>
Once pushed up, you will need to log into the remote server, go to the path of that repository and run a simple: <b>git merge branchName</b>, branchName being the branch you just pushed to to make the changes live for viewing on the server. These are the basics in handeling git repositories and making changes and getting them up. Below, I'll have other scenarios you might run into, and ways on how to handle them.
</p>
</div>

# Possible Git Conflicts
<b>Branch Behind Conflict</b>
```
error: failed to push some refs to '10.135.5.101:/var/www/html/testgit'
hint: Updates were rejected because a pushed branch tip is behind its remote
hint: counterpart. Check out this branch and integrate the remote changes before pushing again.
```
<div>
<p>
This conflict happens when there your local branch is behind (in commits and history) the remote branch your trying to push to. In order to resolve this conflict, you need to either merge with that branch or pull down it's changes and merge. After merging and committing those changes, you should be able to push back up just fine.
</p>
</div>
<b>Checked Out Branch Conflict</b>
```
remote: error: refusing to update checked out branch: refs/heads/settings
remote: error: By default, updating the current branch in a non-bare repository
remote: error: is denied, because it will make the index and work tree inconsistent
remote: error: with what you pushed, and will require 'git reset --hard' to match
remote: error: the work tree to HEAD.

To 10.135.5.101:/var/www/html/alpha
 ! [remote rejected] settings -> settings (branch is currently checked out)
```
<div>
<p>
 This conflict happens when a branch on the remote server is checked out. All of our repositories are non-bare because we personally need a branch checked out in order to view our changes live on the server (being we create web applications). Because of this we can not push to the branch that is checked out. There are different ways this can be resolved. You can push to a new branch / unchecked out branch to get this up to the remote server, and from the remote server, merge that new branch into the currently checked out one. Or if your really needing to push to that branch, from the remote server you can checkout a different branch, push to that branch, and recheck out that branch after pushing. Both ways are ways of resolving this issue.
</p>
</div>
 
<b>Merge Conflict</b>

```
 git pull origin dev
From 10.135.5.101:/var/www/html/testgit
 * branch            dev        -> FETCH_HEAD
Auto-merging portal.php
CONFLICT (add/add): Merge conflict in portal.php
Automatic merge failed; fix conflicts and then commit the result.
```
<div>
<p>
This conflict is a specific conflict that happens on a pull or merge with a branch. When 2 branches cannot be automatically resolved by git, then a merge conflict happens. This is where diff merge gets used.
</p>
<p>
To resolve this we use our diffmerge tool. All we have to do is run the command: "git mergetool" and it'll pull up the default mergetool we should have set. When in diff merge you will have 3 screens.
<br/><br/><strong>
Local | Base | Theirs
</strong><br/><br/>
The way this works is the base one is the one that will be saved. You can choose to use your changes which would be the left side for the conflict, or their changes, which would be the right side for the changes. Or you can even use both by copying and pasting into the base (middle screen) and saving. On the top right you will see arrows with yellow diamonds. It's a quick way to move back and forth between the conflicts. Also on the toolbar there are green arrows that point left or right. These will tell the conflict which side to use when creating the change. 
</p>
<p>
After completing the merge, save the file and close out of diffmerge. Now that we have fixed and completed the merge we need to commit the changes the merge created to that file before pushing up. So run the command: git commit -m "Merge Message ex. (Merge in Settings.php on 10/12/2015)". After committing, it's always good to just pull again out of habit just in case someone pushed up while you were merging. After pulling down, you can then push up the newly merged changes.
</p>
</div>
