# Relatient Git Information
This provides an overall explanation of our git flow, and how to manage the repositories on our side of things. It explains it in great detail. This will go over how to clone down our work, the tools you will need when viewing from a local machine, the commands to deal with issues. It will also have a common problems section and explain examples on how to overcome these issues.

# Tools Needed for your local machine
<ul>
  <li>git</li>
  <li>php, mysql, apache</li>
  <li>composer <a href="https://getcomposer.org/">Found Here</a> (Installation Instructions on the site)</li>
  <li>diffmerge</li>
  <li>A Text Editor of some sort</li>
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
