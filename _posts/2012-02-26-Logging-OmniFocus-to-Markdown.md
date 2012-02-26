---
layout: post
title: Logging OmniFocus to Markdown
status: publish
type: post
excerpt: Logging OmniFocus completed task to a Markdown file in my Notational Velocity folder.
---

I've been looking for a way to keep track of what I have got done everyday, when
I stumbled on [this][jgist] script by [Jered Benoit][jb], via [Brett Terpstra][bt].

I don't use DayOne, so I forked the script and tweaked it to output to a dated
Markdown file in my `~/Dropbox/notes/` folder, which is where I point both [NvALT][nv]
and [Simplenote][sn]. The script is included below, and is also available as a
[gist][mygist]. Hopefully someone else might find this useful.

[jgist]: https://gist.github.com/1903137
[bt]: http://brettterpstra.com/automating-taskpaper-to-day-one-logs/
[jb]: http://jeredb.com/2012/02/24/Omnifocus_to_Day_One_daily_log_of_completed_tasks.html
[nv]: http://brettterpstra.com/project/nvalt/
[sn]: http://simplenoteapp.com/
[mygist]: https://gist.github.com/1918045

{% highlight applescript %}
(*
Based on Jered Benoit's script to log OmniFocus tasks to Day One.

Creates a markdown file of completed tasks in ~/Dropbox/notes

*)

(* 
======================================
// MAIN PROGRAM 
======================================
* )

tell application "OmniFocus"
    
    --SET THE REPORT TITLE
    set ExportList to (current date ) & return & "---" & return & return as Unicode text
    
    --PROCESS THE PROJECTS
    tell default document
        
        --ASSEMBLE THE COMPLETED TASK LIST
        set ExportList to ExportList & return & return & "Tasks Completed in the last day" & return & "---" & return & return & return
        set day_ago to (current date ) - 1 * days
        set refDoneInLastWeek to a reference to (flattened tasks where (completion date ≥ day_ago ) )
        set {lstName, lstContext, lstProject, lstDate } to {name, name of its context, name of its containing project, completion date } of refDoneInLastWeek
        set strText to ""
        repeat with iTask from 1 to length of lstName
            set {strName, varContext, varProject, varDate } to {item iTask of lstName, item iTask of lstContext, item iTask of lstProject, item iTask of lstDate }
            if varDate is not missing value then set strText to strText & short date string of varDate & " - "
            if varProject is not missing value then set strText to strText & " [" & varProject & "] - "
            set strText to strText & strName
            if varContext is not missing value then set strText to strText & " *@" & varContext & "*"
            set strText to strText & "  " & return
        end repeat
    end tell
    
    set ExportList to ExportList & strText as Unicode text
    
    -- Modify "/usr/local/bin/dayone/dayone" to "/usr/local/bin/dayone" if you didn't screw it up like I did.
    do shell script "echo " & (quoted form of ExportList ) & "|tr -d \"\\t\" > ~/Dropbox/notes/log_`date +%Y-%m-%d`.md"
    do shell script "mac2unix ~/Dropbox/notes/log_`date +%Y-%m-%d`.md"
    do shell script "sed -i -e '/^$/d' ~/Dropbox/notes/log_`date +%Y-%m-%d`.md "
    do shell script "rm ~/Dropbox/notes/log_`date +%Y-%m-%d`.md-e"
    
end tell

(* 
======================================
// MAIN HANDLER SUBROUTINES 
======================================
* )

on IndentAndProjects(oFolder)
    tell application id "OFOC"
        
        set {dlm, my text item delimiters } to {my text item delimiters, return & return }
        set day_ago to (current date ) - 1 * days
        set strCompleted to (name of (projects of oFolder where its status is done and completion date ≥ day_ago ) ) as string
        
        set my text item delimiters to dlm
        
        return strCompleted & return
    end tell
end IndentAndProjects 
{% end highlight %}
