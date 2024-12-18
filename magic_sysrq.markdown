---
layout: page
background: '/img/ghorr_banner.png'
title: Magic SysRq Key
date: 2013-08-01
categories : dropdown
permalink: /misc/magic_sysrq/
---

Magic SysRq key is a key combination which directly provides instructions to the Linux kernel.  Itllows the user to perform various low-level commands regardless of the system’s state.  It may be used to recover from freezes, allowing the user to reboot a computer without corrupting the filesystem.

____________________________________

##### SysRq Key Location

![](../../img/misc/KeyboardWithPrintScreen.png)

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-0lax{text-align:left;vertical-align:top}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-0lax"><span style="font-weight:bold">Action</span><br></th>
    <th class="tg-0lax"><span style="font-weight:bold">QWERTY</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0lax">Set the console log level, which controls the types of kernel<br>messages that are output to the console</td>
    <td class="tg-0lax">0 through 9</td>
  </tr>
  <tr>
    <td class="tg-0lax">Immediately reboot the system, without unmounting or syncing<br>filesystems</td>
    <td class="tg-0lax">b</td>
  </tr>
  <tr>
    <td class="tg-0lax">Reboot kexec and output a crashdump</td>
    <td class="tg-0lax">c</td>
  </tr>
  <tr>
    <td class="tg-0lax">Display all currently held Locks<br>(CONFIG_LOCKDEP kernel option is required)</td>
    <td class="tg-0lax">d</td>
  </tr>
  <tr>
    <td class="tg-0lax">Send the SIGTERM<br>signal to all processes except init (PID 1)</td>
    <td class="tg-0lax">e</td>
  </tr>
  <tr>
    <td class="tg-0lax">Call oom_kill, which kills a process to alleviate an OOM<br>condition</td>
    <td class="tg-0lax">f</td>
  </tr>
  <tr>
    <td class="tg-0lax">When using Kernel Mode Setting, provides emergency support for <br>switching back to the kernel’s framebuffer console[3]<br>If the in-kernel debugger ‘kdb’ is present, enter the debugger.</td>
    <td class="tg-0lax">g</td>
  </tr>
  <tr>
    <td class="tg-0lax">Output a terse help document to the console<br>Any key which is<br>not bound to a command should also perform this action</td>
    <td class="tg-0lax">h</td>
  </tr>
  <tr>
    <td class="tg-0lax">Send the SIGKILL<br>signal to all processes except init</td>
    <td class="tg-0lax">i</td>
  </tr>
  <tr>
    <td class="tg-0lax">Forcibly “Just thaw it” – filesystems frozen by the<br>FIFREEZE ioctl.</td>
    <td class="tg-0lax">j</td>
  </tr>
  <tr>
    <td class="tg-0lax">Kill all processes on the current virtual console <br>(Can be used to kill X and svgalib programs, see below)<br>This was originally designed to imitate a secure attention key</td>
    <td class="tg-0lax">k</td>
  </tr>
  <tr>
    <td class="tg-0lax">Shows a stack backtrace for all active CPUs.</td>
    <td class="tg-0lax">l</td>
  </tr>
  <tr>
    <td class="tg-0lax">Shows a stack backtrace for all active CPUs.</td>
    <td class="tg-0lax">m</td>
  </tr>
  <tr>
    <td class="tg-0lax">Reset the nice level of all high-priority and real-time tasks</td>
    <td class="tg-0lax">n</td>
  </tr>
  <tr>
    <td class="tg-0lax">Shut off the system</td>
    <td class="tg-0lax">o</td>
  </tr>
  <tr>
    <td class="tg-0lax">Output the current registers and flags to the console</td>
    <td class="tg-0lax">p</td>
  </tr>
  <tr>
    <td class="tg-0lax">Display all active high-resolution timers and clock sources.</td>
    <td class="tg-0lax">q</td>
  </tr>
  <tr>
    <td class="tg-0lax">Switch the keyboard from raw mode, the mode used by <br>programs such as X11 and svgalib, to XLATE mode</td>
    <td class="tg-0lax">r</td>
  </tr>
  <tr>
    <td class="tg-0lax">Sync all mounted filesystems</td>
    <td class="tg-0lax">s</td>
  </tr>
  <tr>
    <td class="tg-0lax">Output a list of current tasks and their information to the console</td>
    <td class="tg-0lax">t</td>
  </tr>
  <tr>
    <td class="tg-0lax">Remount all mounted filesystems in read-only mode</td>
    <td class="tg-0lax">u</td>
  </tr>
  <tr>
    <td class="tg-0lax">Forcefully restores framebuffer console, except for ARM<br>processors, where this key causes ETM buffer dump</td>
    <td class="tg-0lax">v</td>
  </tr>
  <tr>
    <td class="tg-0lax">Display list of blocked (D state) tasks</td>
    <td class="tg-0lax">w</td>
  </tr>
  <tr>
    <td class="tg-0lax">Used by xmon interface on PPC/PowerPC platforms.</td>
    <td class="tg-0lax">x</td>
  </tr>
  <tr>
    <td class="tg-0lax">Show global CPU registers (SPARC-64 specific)</td>
    <td class="tg-0lax">y</td>
  </tr>
  <tr>
    <td class="tg-0lax">Dump the ftrace buffer</td>
    <td class="tg-0lax">z</td>
  </tr>
</tbody>
</table>
