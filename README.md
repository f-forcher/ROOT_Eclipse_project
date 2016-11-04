# Root template eclipse project

##Installation/Preliminary operations
1. Install/compile the various versions of ROOT and put them in ~/ROOT/vXX-XX-XX (eg "~/ROOT/v5-34-36").
2. Put the   `SCRIPT_ROOT_ECLIPSE/Documents/root_varie` in `~/Documents` (or modify the scripts).
   
   The reason here is that at the moment, ROOT 5 and ROOT 6 are not compatible. Even worse, gcc 4 and 5's ABIs are not
   compatible and root 5 "prefers" g++ 4.x and root 6 g++ 5.x (or clang). So the scripts use update-alternatives
   to select the appropriate compiler (you need to install them both obviously), and they need to use sudo.
   
3. Put the aliases for the shell (bash, zsh, etc) in the corresponding file and source them.
3. Put Eclipse (or modify the scripts, obviously...) in `~/bin/eclipse`.
4. Put the scripts to run eclipse (eg `~/SCRIPT_ROOT_ECLIPSE/eclipse_root534.sh`) for example on the Desktop.

## Test usability
Either  
 1. Open eclipse using the script corresponding to the selected ROOT.
 2. Compile one of the five configurations in Eclipse.


Or  
 1. Open a terminal and select the root to use with the aliases (eg `root_6_06_select`) or soucing the scripts in `~/Documents/ root_varie`.
 2. Go the project folder (e.g. `~/git/ROOT_Eclipse_project`), choose a configuration (e.g. `Release`) and do
 ```sh
 cd Release
 make clean
 make 
 cd ..
 ``` 
 `make clean` may not be necessary, but it's recommended the first time you try to compile (as I prefer to save also binaries to git, and they may not be compatible with your machine).

and then
 4. Run from the terminal the executable in the corresponding folder (e.g. executing `./Release/ROOT_Eclipse_project`), you should see the following image in a ROOT canvas window:  
   ![Hello world](https://github.com/f-forcher/ROOT_Eclipse_project/blob/master/Hello.png)

## Use as a template
To use it as a template for a new project would be to open Eclipse, copy and paste it (probably you want it in the `~/git/` folder, which is usually different from the standard `workspace/` one) with a new name (let's call it *NEWNAME*).  
The reason to use Eclipse for the copy is that copying using the system file browser does not change some strings in the files (for example, the project name in the `.project` file), so it's not recommended.


Then, **DELETE the NEWNAME/.git/ folder!!** This is very important since otherwise you would be trying to push to *THIS* repository!
Then, make a new *NEWNAME* repository in github without a README so it's clean, and then instead of following Github's on-screen instuctions,
open a terminal, `cd` into the project folder, and ther run these slightly modified commands:
```sh
cd ~/git/NEWNAME
echo "# Ronch-braggPlot_v04" >> README.md
git init
git add --all
git commit -m "first commit"
git remote add origin YOUR_REPO_URL # YOUR_REPO_URL should be like 'https://github.com/YOUR_GIT_USERNAME/NEWNAME.git'
git push -u origin master
```
then refresh the repository page in the browser, and you should see the committed changes. Now you should be ready to start and put
your own code in the the `src/` folder.