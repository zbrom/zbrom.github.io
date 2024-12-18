---
layout: page
background: '/img/ghorr_banner.png'
title: Tmux Commands
date: 2021-06-27
categories : dropdown
permalink: /linux/tmux/
---

[![](../../img/linux/tmux-sm.png)](../../img/linux/tmux.png){:target="_blank"}{:style="float: left;margin-right: 7px;margin-top: 7px;"} tmux is a software application that can be used to multiplex several virtual consoles, allowing a user to access multiple separate terminal sessions inside a single terminal window or remote terminal session.  It is useful for dealing with multiple programs from a command line interface, and for separating programs from the Unix shell that started the program.  It provides much of the same functionality as GNU Screen, but is distributed under a BSD license.

I have found tmux very useful with my raspberry pi.  It provides me with the capability to start an application, end an SSH session, then return to that application later.

____________________________________
<p></p>

<p>&nbsp;</p>
<style type="text/css"><!--
TD P { margin-bottom: 0in; }P { margin-bottom: 0.08in; }
--></style>
<table width="100%" cellspacing="0" cellpadding="2">
<colgroup>
<col width="155*" />
<col width="101*" /> </colgroup>
<tbody>
<tr>
<td width="61%"><strong>Action</strong></td>
<td width="39%"><strong>tmux</strong></td>
</tr>
<tr>
<td width="61%">start a new session</td>
<td width="39%">tmux <em>OR</em><br />
tmux new <em>OR</em><br />
tmux new-session</td>
</tr>
<tr>
<td width="61%">re-attach a detached session</td>
<td width="39%">tmux attach <em>OR</em><br />
tmux attach-session</td>
</tr>
<tr>
<td width="61%">re-attach an attached session (detaching it from elsewhere)</td>
<td width="39%">tmux attach -d <em>OR</em><br />
tmux attach-session -d</td>
</tr>
<tr>
<td width="61%">re-attach an attached session (keeping it attached elsewhere)</td>
<td width="39%">tmux attach <em>OR</em><br />
tmux attach-session</td>
</tr>
<tr>
<td width="61%">detach from currently attached session</td>
<td width="39%">^b d <em>OR</em><br />
^b :detach</td>
</tr>
<tr>
<td width="61%">rename-window to newname</td>
<td width="39%">^b , &lt;newname&gt; <em>OR</em><br />
^b :rename-window &lt;newname&gt;</td>
</tr>
<tr>
<td width="61%">list windows</td>
<td width="39%">^b w</td>
</tr>
<tr>
<td width="61%">list windows in chooseable menu</td>
<td width="39%"></td>
</tr>
<tr>
<td width="61%">go to window #</td>
<td width="39%">^b #</td>
</tr>
<tr>
<td width="61%">go to last-active window</td>
<td width="39%">^b l</td>
</tr>
<tr>
<td width="61%">go to next window</td>
<td width="39%">^b n</td>
</tr>
<tr>
<td width="61%">go to previous window</td>
<td width="39%">^b p</td>
</tr>
<tr>
<td width="61%">see keybindings</td>
<td width="39%">^b ?</td>
</tr>
<tr>
<td width="61%">list sessions</td>
<td width="39%">^b s <em>OR</em><br />
tmux ls <em>OR</em><br />
tmux list-sessions</td>
</tr>
<tr>
<td width="61%">toggle visual bell</td>
<td width="39%"></td>
</tr>
<tr>
<td width="61%">create another shell</td>
<td width="39%">^b c</td>
</tr>
<tr>
<td width="61%">exit current shell</td>
<td width="39%">^d</td>
</tr>
<tr>
<td width="61%">split pane horizontally</td>
<td width="39%">^b &#8220;</td>
</tr>
<tr>
<td width="61%">split pane vertically</td>
<td width="39%">^b %</td>
</tr>
<tr>
<td width="61%">switch to another pane</td>
<td width="39%">^b o</td>
</tr>
<tr>
<td width="61%">kill the current pane</td>
<td width="39%">^b x <em>OR</em> (logout/^D)</td>
</tr>
<tr>
<td width="61%">close other panes except the current one</td>
<td width="39%">^b !</td>
</tr>
<tr>
<td width="61%">swap location of panes</td>
<td width="39%">^b ^o</td>
</tr>
<tr>
<td width="61%">show time</td>
<td width="39%">^b t</td>
</tr>
<tr>
<td width="61%">show numeric values of panes</td>
<td width="39%">^b q</td>
</tr>
</tbody>
</table>

<p></p>
#### References:

[https://www.dayid.org/comp/tm.html](https://www.dayid.org/comp/tm.html){:target="_blank"}
