+++
date = "2014-07-03T11:38:19+01:00"
title = "Manually Associating Git Commits in Visual Studio Online"
tags = ["Git", "Visual Studio Online"]
menu = ""
banner = "banners/VisualStudioOnline.jpg"
+++

We're using Visual Studio Online (VSO) for all our Source Control/Work planning needs at my current client, which is working pretty well, and most importantly free, for our small 3 person team.

You can automatically connect git commits to your work items in VSO by simply adding a hashtag with the Id of the Work Item to the beginning of your commit messages eg: #24 Added Files Model.

You can also manually link the git commits. This has mostly come in handy when i've forgot to add the hashtag, which happens quite often, especially when you're in a furious coding session and you don't want to break off and look up the id of the item you want to link the commit to. Perhaps you and your team also don't want to pollute your Source code repositories with hashtags specific to Visual Studio Online.

It's easy to do, but perhaps not immediately obvious, as it's buried in the Links tab.

Firstly, click on 'All Links' tab in the right hand panel, and then click on the 'link to...' icon.

You'll get a popup asking what type of link you want. Select 'Commit' from the dropdown, and then choose which Repository you want to use. Click on the browse button, and you'll get another popup.

In that popup, select the user, branch and any dates you want to filter by and click 'Find'. You'll get a list of commits, and simply click the radio button against whichever commit it is you want to link to the work item.

