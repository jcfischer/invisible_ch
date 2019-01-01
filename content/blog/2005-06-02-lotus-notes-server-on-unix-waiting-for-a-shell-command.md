---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2005-06-02 10:15:38+00:00
layout: post
link: https://invisible.ch/2005/06/02/lotus-notes-server-on-unix-waiting-for-a-shell-command/
slug: lotus-notes-server-on-unix-waiting-for-a-shell-command
tags: ["blog"]
title: 'Lotus Notes server on unix: Waiting for a shell command'
type: post
wordpress_id: 416
---

LotusScript allows you to execute a OS command by using the rc = Shell( "command" ) command. The problem with this is, that Notes starts the command asynchronously and returns 33 as the return code, meaning "it's started". 

There is no way to actually wait for the command to finish and - gasp - even get the return code from the command back.

This was the sitatuation with a client. We needed to run unix commands and react to their outcome in LotusScript.

Read on for the solution.
<!-- more -->
This code is designed to run on a Unix (Solaris in this case) environment ( /tmp etc). Feel free to change this for a Windows system.

Add this function to the agent you are working in:

    
    
    Function ExecuteShellCommand( aCommand As String, timeoutSeconds As Integer )
    	' executes the specified command in a shell, waits for the command to finish and 
    	' returns the return code to the caller.
     	' aborts after "timeoutSeconds"
    	
    	On Error Goto ErrorHandler
    	
    	Dim cmd As String
    	Dim rcFile As String
    	Dim cnt As Integer
    	Dim fileNum As Integer
    	Dim isDone As Boolean
    	Dim rc As Variant
    	
    	rcFile = "/tmp/ln-" & Cstr(Cint(Rnd(1) * 9999))
    	
    	cmd = aCommand &  |; echo $? > | & rcFile 
    	Call LogEvent( "shell: " & cmd, SEVERITY_LOW, Nothing) 
    	rc = Shell( cmd )
    	
    ' the command has been sent, now wait for the return
    	cnt = 0
    	isDone = False
    	While (cnt < timeoutSeconds) And (Not isDone)
    		Sleep 1
    		fileNum = Freefile()
    		Open rcFile For Input As fileNum
    		Line Input #fileNum, rc
    		isDone = True
    		Close #fileNum
    		Kill rcFile
    ContinueToPoll:
    		
    		cnt = cnt + 1
    	Wend
    	
    	ExecuteShellCommand = rc	
    	Exit Function
    	
    ErrorHandler:
    	If Err = 101 Then
    		Resume ContinueToPoll	
    	End If
    	
    	Call LogError
    	Resume Next
    	
    End Function
    




Now you can call it like this:

    
    
      rc = ExecuteShellCommand( "ls -l", 5 )
      if rc <> 0 then
         print "something went wrong, rc: " & CStr(rc)
      end if
    




enjoy
