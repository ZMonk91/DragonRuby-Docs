# DragonRuby now has it's own official documents page, please use this instead
[DragonRuby Docs](http://docs.dragonruby.org/)


# Everything here is deprecated




## DragonRuby-Docs

An open source attempt at documenting [DragonRuby - GTK](http://DragonRuby.org)

## Contributing
The fastest and easiest way to contribute to changes to the project would be to simply **Fork** > **Branch** > **Change** > **Push**

<br>

### 1. Fork
Fork the project & clone locally<br>

 This will create a copy of the repository in your own GitHub account

- Move to the location you want to save the project to:<br>`cd location/you/want/to/save/to`

- Clone the project:<br>`git clone https://github.com/ZMonk91/DragonRuby-Docs.git`

- Change into the new project’s directory:
`cd DragonRuby-Docs/docs`

*note*: All editable files are located under the `docs/` folder.

<br>

### 2. Branch
**The number one rule is to put each piece of work on its own branch.**

Get branch from master:<br>
`git checkout master`<br>
The the git pull command will sync our local copy with the upstream project and the git push syncs it to our forked GitHub project:
`git pull upstream master && git push origin master`<br>

Start your own branch, naming whatever the fix is:<br>
`git checkout -b hotfix/new_name_here`

**Ensure that you only fix the thing you’re working on. Do not be tempted to fix some other things that you see along the way, including formatting issues, as your PR will probably be rejected.**

<br>

### 3. Change
  Simply make whatever changes you would like to submit, so long as they within the `docs/` folder. (Make sure you leave a [proper git commit message](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html))

<br>

### 4. Create PR
  To create a PR you need to push your branch to the origin remote and then press some buttons on GitHub.
  <br>

To push your new branch:<br>
`git push -u origin hotfix/new_name_here`

This will create the branch on your GitHub project. The -u flag links this branch with the remote one, so that in the future, you can simply type git push origin.

Swap back to the browser and navigate to your fork of the project (https://github.com/YOU_USERNAME/DragonRuby-Docs) and you’ll see that your new branch is listed at the top with a handy “Compare & pull request” button: 
![Compare & Pull Request Button](https://akrabat.com/wp-content/uploads/2015/09/2015-09pr-button.png)

On this page:
 - Ensure that the `base fork`points to the correct repository and branch.
 - Ensure that you provide a good, succinct title for your pull request and explain why you have created it in the description box. Add any relevant issue numbers if you have them.<br>
 - Once you are happy, press the `Create pull request` button and you’re done.

 **Congratulations** 
 You've successfully submitted a change. The request will be reviewed and if everything was done correctly, will be updated immediately. No further changes necessary!
