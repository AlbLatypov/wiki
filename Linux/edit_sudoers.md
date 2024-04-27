# How To Edit the Sudoers File

</div>
<h2 id="how-to-obtain-root-privileges"><a href="#how-to-obtain-root-privileges" onclick="navigator.clipboard.writeText(this.href);">How To Obtain Root Privileges</a><a class="hash-anchor" href="#how-to-obtain-root-privileges" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h2>
<p>There are three basic ways to obtain <strong>root</strong> privileges, which vary in their level of sophistication.</p>
<h3 id="logging-in-as-root"><a href="#logging-in-as-root" onclick="navigator.clipboard.writeText(this.href);">Logging In As Root</a><a class="hash-anchor" href="#logging-in-as-root" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h3>
<p>The simplest and most straightforward method of obtaining <strong>root</strong> privileges is to directly log into your server as the <strong>root</strong> user.</p>
<p>If you are logging into a local machine (or using an out-of-band console feature on a virtual server), enter <code>root</code> as your username at the login prompt and enter the <strong>root</strong> password when asked.</p>
<p>If you are logging in through SSH, specify the <strong>root</strong> user prior to the IP address or domain name in your SSH connection string:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">ssh</span> root@<mark>server_domain_or_ip</mark>
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<p>If you have not set up SSH keys for the <strong>root</strong> user, enter the <strong>root</strong> password when prompted.</p>
<h3 id="using-su-to-become-root"><a href="#using-su-to-become-root" onclick="navigator.clipboard.writeText(this.href);">Using <code>su</code> to Become Root</a><a class="hash-anchor" href="#using-su-to-become-root" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h3>
<p>Logging in directly as <strong>root</strong> is usually not recommended, because it is easy to begin using the system for non-administrative tasks, which is dangerous.</p>
<p>The next way to gain super-user privileges allows you to become the <strong>root</strong> user at any time, as you need it.</p>
<p>We can do this by invoking the <code>su</code> command, which stands for “substitute user”. To gain <strong>root</strong> privileges, type:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">su</span>
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<p>You will be prompted for the <strong>root</strong> user’s password, after which, you will be dropped into a <strong>root</strong> shell session.</p>
<p>When you have finished the tasks which require <strong>root</strong> privileges, return to your normal shell by typing:</p>
<div class="code-toolbar"><pre class="prefixed super_user language-bash"><code><ol><li data-prefix="#"><span class="token builtin class-name">exit</span>
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<h3 id="using-sudo-to-execute-commands-as-root"><a href="#using-sudo-to-execute-commands-as-root" onclick="navigator.clipboard.writeText(this.href);">Using <code>sudo</code> to Execute Commands as Root</a><a class="hash-anchor" href="#using-sudo-to-execute-commands-as-root" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h3>
<p>The final, way of obtaining <strong>root</strong> privileges that we will discuss is with the <code>sudo</code> command.</p>
<p>The <code>sudo</code> command allows you to execute one-off commands with <strong>root</strong> privileges, without the need to spawn a new shell. It is executed like this:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> <mark>command_to_execute</mark>
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<p>Unlike <code>su</code>, the <code>sudo</code> command will request the password of the <em>current</em> user, not the <strong>root</strong> password.</p>
<p>Because of its security implications, <code>sudo</code> access is not granted to users by default, and must be set up before it functions correctly. Check out our <em>How To Create a New Sudo-enabled User</em> quickstart tutorials for <a href="https://www.digitalocean.com/community/tutorials/how-to-create-a-new-sudo-enabled-user-on-ubuntu-20-04-quickstart">Ubuntu</a> and <a href="https://www.digitalocean.com/community/tutorials/how-to-create-a-new-sudo-enabled-user-on-centos-8-quickstart">CentOS</a> to learn how to set up a <code>sudo</code>-enabled user.</p>
<p>In the following section, we will discuss how to modify the <code>sudo</code> configuration in greater detail.</p>
<h2 id="what-is-visudo"><a href="#what-is-visudo" onclick="navigator.clipboard.writeText(this.href);">What is Visudo?</a><a class="hash-anchor" href="#what-is-visudo" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h2>
<p>The <code>sudo</code> command is configured through a file located at <code>/etc/sudoers</code>.</p>
<div class="callout warning">
<p><strong>Warning:</strong> Never edit this file with a normal text editor! Always use the <code>visudo</code> command instead!</p>
</div>
<p>Because improper syntax in the <code>/etc/sudoers</code> file can leave you with a broken system where it is impossible to obtain elevated privileges, it is important to use the <code>visudo</code> command to edit the file.</p>
<p>The <code>visudo</code> command opens a text editor like normal, but it validates the syntax of the file upon saving. This prevents configuration errors from blocking <code>sudo</code> operations, which may be your only way of obtaining <strong>root</strong> privileges.</p>
<p>Traditionally, <code>visudo</code> opens the <code>/etc/sudoers</code> file with the <code>vi</code> text editor. Ubuntu, however, has configured <code>visudo</code> to use the <code>nano</code> text editor instead.</p>
<p>If you would like to change it back to <code>vi</code>, issue the following command:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> update-alternatives <span class="token parameter variable">--config</span> editor
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<pre><code><div class="secondary-code-label" title="Output">Output</div>There are 4 choices for the alternative editor (providing /usr/bin/editor).

  Selection    Path                Priority   Status
------------------------------------------------------------
* 0            /bin/nano            40        auto mode
  1            /bin/ed             -100       manual mode
  2            /bin/nano            40        manual mode
  3            /usr/bin/vim.basic   30        manual mode
  4            /usr/bin/vim.tiny    10        manual mode

Press &lt;enter&gt; to keep the current choice[*], or type selection number:
</code></pre>
<p>Select the number that corresponds with the choice you would like to make.</p>
<p>On CentOS, you can change this value by adding the following line to your <code>~/.bashrc</code>:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token builtin class-name">export</span> <span class="token assign-left variable">EDITOR</span><span class="token operator">=</span><span class="token variable"><span class="token variable">`</span><span class="token function">which</span> <mark>name_of_editor</mark><span class="token variable">`</span></span>
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<p>Source the file to implement the changes:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token builtin class-name">.</span> ~/.bashrc
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<p>After you have configured <code>visudo</code>, execute the command to access the <code>/etc/sudoers</code> file:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> visudo
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<h2 id="how-to-modify-the-sudoers-file"><a href="#how-to-modify-the-sudoers-file" onclick="navigator.clipboard.writeText(this.href);">How To Modify the Sudoers File</a><a class="hash-anchor" href="#how-to-modify-the-sudoers-file" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h2>
<p>You will be presented with the <code>/etc/sudoers</code> file in your selected text editor.</p>
<p>I have copied and pasted the file from Ubuntu 20.04, with comments removed. The CentOS <code>/etc/sudoers</code> file has many more lines, some of which we will not discuss in this guide.</p>
<div class="code-label" title="/etc/sudoers">/etc/sudoers</div>
<pre><code>Defaults        env_reset
Defaults        mail_badpass
Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"

root    ALL=(ALL:ALL) ALL

%admin ALL=(ALL) ALL
%sudo   ALL=(ALL:ALL) ALL

#includedir /etc/sudoers.d
</code></pre>
<p>Let’s take a look at what these lines do.</p>
<h3 id="default-lines"><a href="#default-lines" onclick="navigator.clipboard.writeText(this.href);">Default Lines</a><a class="hash-anchor" href="#default-lines" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h3>
<p>The first line, <code>Defaults env_reset</code>, resets the terminal environment to remove any user variables. This is a safety measure used to clear potentially harmful environmental variables from the <code>sudo</code> session.</p>
<p>The second line, <code>Defaults mail_badpass</code>, tells the system to mail notices of bad <code>sudo</code> password attempts to the configured <code>mailto</code> user. By default, this is the <strong>root</strong> account.</p>
<p>The third line, which begins with <code>Defaults secure_path=...</code>, specifies the <code>PATH</code> (the places in the filesystem the operating system will look for applications) that will be used for <code>sudo</code> operations. This prevents using user paths which may be harmful.</p>
<h3 id="user-privilege-lines"><a href="#user-privilege-lines" onclick="navigator.clipboard.writeText(this.href);">User Privilege Lines</a><a class="hash-anchor" href="#user-privilege-lines" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h3>
<p>The fourth line, which dictates the <strong>root</strong> user’s <code>sudo</code> privileges, is different from the preceding lines. Let’s take a look at what the different fields mean:</p>
<ul>
<li>
<p><code><mark>root</mark> ALL=(ALL:ALL) ALL</code>
The first field indicates the username that the rule will apply to (<strong>root</strong>).</p>
</li>
<li>
<p><code>root <mark>ALL</mark>=(ALL:ALL) ALL</code>
The first “ALL” indicates that this rule applies to all hosts.</p>
</li>
<li>
<p><code>root ALL=(<mark>ALL</mark>:ALL) ALL</code>
This “ALL” indicates that the <strong>root</strong> user can run commands as all users.</p>
</li>
<li>
<p><code>root ALL=(ALL:<mark>ALL</mark>) ALL</code>
This “ALL” indicates that the <strong>root</strong> user can run commands as all groups.</p>
</li>
<li>
<p><code>root ALL=(ALL:ALL) <mark>ALL</mark></code>
The last “ALL” indicates these rules apply to all commands.</p>
</li>
</ul>
<p>This means that our <strong>root</strong> user can run any command using <code>sudo</code>, as long as they provide their password.</p>
<h3 id="group-privilege-lines"><a href="#group-privilege-lines" onclick="navigator.clipboard.writeText(this.href);">Group Privilege Lines</a><a class="hash-anchor" href="#group-privilege-lines" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h3>
<p>The next two lines are similar to the user privilege lines, but they specify <code>sudo</code> rules for groups.</p>
<p>Names beginning with a <code>%</code> indicate group names.</p>
<p>Here, we see the <strong>admin</strong> group can execute any command as any user on any host. Similarly, the <strong>sudo</strong> group has the same privileges, but can execute as any group as well.</p>
<h3 id="included-etc-sudoers-d-line"><a href="#included-etc-sudoers-d-line" onclick="navigator.clipboard.writeText(this.href);">Included /etc/sudoers.d Line</a><a class="hash-anchor" href="#included-etc-sudoers-d-line" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h3>
<p>The last line might look like a comment at first glance:</p>
<div class="code-label" title="/etc/sudoers">/etc/sudoers</div>
<pre><code>. . .

#includedir /etc/sudoers.d
</code></pre>
<p>It <em>does</em> begin with a <code>#</code>, which usually indicates a comment. However, this line actually indicates that files within the <code>/etc/sudoers.d</code> directory will be sourced and applied as well.</p>
<p>Files within that directory follow the same rules as the <code>/etc/sudoers</code> file itself. Any file that does not end in <code>~</code> and that does not have a <code>.</code> in it will be read and appended to the <code>sudo</code> configuration.</p>
<p>This is mainly meant for applications to alter <code>sudo</code> privileges upon installation. Putting all of the associated rules within a single file in the <code>/etc/sudoers.d</code> directory can make it easy to see which privileges are associated with which accounts and to reverse credentials easily without having to try to manipulate the <code>/etc/sudoers</code> file directly.</p>
<p>As with the <code>/etc/sudoers</code> file itself, you should always edit files within the <code>/etc/sudoers.d</code> directory with <code>visudo</code>. The syntax for editing these files would be:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> visudo <span class="token parameter variable">-f</span> /etc/sudoers.d/<mark>file_to_edit</mark>
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<h2 id="how-to-give-a-user-sudo-privileges"><a href="#how-to-give-a-user-sudo-privileges" onclick="navigator.clipboard.writeText(this.href);">How To Give a User Sudo Privileges</a><a class="hash-anchor" href="#how-to-give-a-user-sudo-privileges" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h2>
<p>The most common operation that users want to accomplish when managing <code>sudo</code> permissions is to grant a new user general <code>sudo</code> access. This is useful if you want to give an account full administrative access to the system.</p>
<p>The easiest way of doing this on a system set up with a general purpose administration group, like the Ubuntu system in this guide, is actually to add the user in question to that group.</p>
<p>For example, on Ubuntu 20.04, the <code>sudo</code> group has full admin privileges. We can grant a user these same privileges by adding them to the group like this:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> <span class="token function">usermod</span> <span class="token parameter variable">-aG</span> <span class="token function">sudo</span> <mark>username</mark>
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<p>The <code>gpasswd</code> command can also be used:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> gpasswd <span class="token parameter variable">-a</span> <mark>username</mark> <span class="token function">sudo</span>
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<p>These will both accomplish the same thing.</p>
<p>On CentOS, this is usually the <code>wheel</code> group instead of the <code>sudo</code> group:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> <span class="token function">usermod</span> <span class="token parameter variable">-aG</span> wheel <mark>username</mark>
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<p>Or, using <code>gpasswd</code>:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> gpasswd <span class="token parameter variable">-a</span> <mark>username</mark> wheel
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<p>On CentOS, if adding the user to the group does not work immediately, you may have to edit the <code>/etc/sudoers</code> file to uncomment the group name:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> visudo
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<div class="code-label" title="/etc/sudoers">/etc/sudoers</div>
<pre><code>. . .
%wheel ALL=(ALL) ALL
. . .
</code></pre>
<h2 id="how-to-set-up-custom-rules"><a href="#how-to-set-up-custom-rules" onclick="navigator.clipboard.writeText(this.href);">How To Set Up Custom Rules</a><a class="hash-anchor" href="#how-to-set-up-custom-rules" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h2>
<p>Now that we have gotten familiar with the general syntax of the file, let’s create some new rules.</p>
<h3 id="how-to-create-aliases"><a href="#how-to-create-aliases" onclick="navigator.clipboard.writeText(this.href);">How To Create Aliases</a><a class="hash-anchor" href="#how-to-create-aliases" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h3>
<p>The <code>sudoers</code> file can be organized more easily by grouping things with various kinds of “aliases”.</p>
<p>For instance, we can create three different groups of users, with overlapping membership:</p>
<div class="code-label" title="/etc/sudoers">/etc/sudoers</div>
<pre><code>. . .
User_Alias		GROUPONE = abby, brent, carl
User_Alias		GROUPTWO = brent, doris, eric,
User_Alias		GROUPTHREE = doris, felicia, grant
. . .
</code></pre>
<p>Group names must start with a capital letter. We can then allow members of <code>GROUPTWO</code> to update the <code>apt</code> database by creating a rule like this:</p>
<div class="code-label" title="/etc/sudoers">/etc/sudoers</div>
<pre><code>. . .
GROUPTWO	ALL = /usr/bin/apt-get update
. . .
</code></pre>
<p>If we do not specify a user/group to run as, as above, <code>sudo</code> defaults to the <strong>root</strong> user.</p>
<p>We can allow members of <code>GROUPTHREE</code> to shutdown and reboot the machine by creating a “command alias” and using that in a rule for <code>GROUPTHREE</code>:</p>
<div class="code-label" title="/etc/sudoers">/etc/sudoers</div>
<pre><code>. . .
Cmnd_Alias		POWER = /sbin/shutdown, /sbin/halt, /sbin/reboot, /sbin/restart
GROUPTHREE	ALL = POWER
. . .
</code></pre>
<p>We create a command alias called <code>POWER</code> that contains commands to power off and reboot the machine. We then allow the members of <code>GROUPTHREE</code> to execute these commands.</p>
<p>We can also create “Run as” aliases, which can replace the portion of the rule that specifies the user to execute the command as:</p>
<div class="code-label" title="/etc/sudoers">/etc/sudoers</div>
<pre><code>. . .
Runas_Alias		WEB = www-data, apache
GROUPONE	ALL = (WEB) ALL
. . .
</code></pre>
<p>This will allow anyone who is a member of <code>GROUPONE</code> to execute commands as the <code>www-data</code> user or the <code>apache</code> user.</p>
<p>Just keep in mind that later rules will override earlier rules when there is a conflict between the two.</p>
<h3 id="how-to-lock-down-rules"><a href="#how-to-lock-down-rules" onclick="navigator.clipboard.writeText(this.href);">How To Lock Down Rules</a><a class="hash-anchor" href="#how-to-lock-down-rules" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h3>
<p>There are a number of ways that you can achieve more control over how <code>sudo</code> reacts to a call.</p>
<p>The <code>updatedb</code> command associated with the <code>mlocate</code> package is relatively harmless on a single-user system. If we want to allow users to execute it with <strong>root</strong> privileges <em>without</em> having to type a password, we can make a rule like this:</p>
<div class="code-label" title="/etc/sudoers">/etc/sudoers</div>
<pre><code>. . .
GROUPONE	ALL = NOPASSWD: /usr/bin/updatedb
. . .
</code></pre>
<p><code>NOPASSWD</code> is a “tag” that means no password will be requested. It has a companion command called <code>PASSWD</code>, which is the default behavior. A tag is relevant for the rest of the rule unless overruled by its “twin” tag later down the line.</p>
<p>For instance, we can have a line like this:</p>
<div class="code-label" title="/etc/sudoers">/etc/sudoers</div>
<pre><code>. . .
GROUPTWO	ALL = NOPASSWD: /usr/bin/updatedb, PASSWD: /bin/kill
. . .
</code></pre>
<p>Another helpful tag is <code>NOEXEC</code>, which can be used to prevent some dangerous behavior in certain programs.</p>
<p>For example, some programs, like <code>less</code>, can spawn other commands by typing this from within their interface:</p>
<pre><code>!<mark>command_to_run</mark>
</code></pre>
<p>This basically executes any command the user gives it with the same permissions that <code>less</code> is running under, which can be quite dangerous.</p>
<p>To restrict this, we could use a line like this:</p>
<div class="code-label" title="/etc/sudoers">/etc/sudoers</div>
<pre><code>. . .
<mark>username</mark>	ALL = NOEXEC: /usr/bin/less
. . .
</code></pre>
<h2 id="miscellaneous-information"><a href="#miscellaneous-information" onclick="navigator.clipboard.writeText(this.href);">Miscellaneous Information</a><a class="hash-anchor" href="#miscellaneous-information" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h2>
<p>There are a few more pieces of information that may be useful when dealing with <code>sudo</code>.</p>
<p>If you specified a user or group to “run as” in the configuration file, you can execute commands as those users by using the <code>-u</code> and <code>-g</code> flags, respectively:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> <span class="token parameter variable">-u</span> <mark>run_as_user <span class="token builtin class-name">command</span></mark>
</li><li data-prefix="$"><span class="token function">sudo</span> <span class="token parameter variable">-g</span> <mark>run_as_group <span class="token builtin class-name">command</span></mark>
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<p>For convenience, by default, <code>sudo</code> will save your authentication details for a certain amount of time in one terminal. This means you won’t have to type your password in again until that timer runs out.</p>
<p>For security purposes, if you wish to clear this timer when you are done running administrative commands, you can run:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> <span class="token parameter variable">-k</span>
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<p>If, on the other hand, you want to “prime” the <code>sudo</code> command so that you won’t be prompted later, or to renew your <code>sudo</code> lease, you can always type:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> <span class="token parameter variable">-v</span>
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<p>You will be prompted for your password, which will be cached for later <code>sudo</code> uses until the <code>sudo</code> time frame expires.</p>
<p>If you are simply wondering what kind of privileges are defined for your username, you can type:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> <span class="token parameter variable">-l</span>
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<p>This will list all of the rules in the <code>/etc/sudoers</code> file that apply to your user. This gives you a good idea of what you will or will not be allowed to do with <code>sudo</code> as any user.</p>
<p>There are many times when you will execute a command and it will fail because you forgot to preface it with <code>sudo</code>. To avoid having to re-type the command, you can take advantage of a bash functionality that means “repeat last command”:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> <span class="token operator">!</span><span class="token operator">!</span>
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<p>The double exclamation point will repeat the last command. We preceded it with <code>sudo</code> to quickly change the unprivileged command to a privileged command.</p>
<p>For some fun, you can add the following line to your <code>/etc/sudoers</code> file with <code>visudo</code>:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> visudo
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<div class="code-label" title="/etc/sudoers">/etc/sudoers</div>
<pre><code>. . .
Defaults	insults
. . .
</code></pre>
<p>This will cause <code>sudo</code> to return a silly insult when a user types in an incorrect password for <code>sudo</code>. We can use <code>sudo -k</code> to clear the previous <code>sudo</code> cached password to try it out:</p>
<div class="code-toolbar"><pre class="prefixed command language-bash"><code><ol><li data-prefix="$"><span class="token function">sudo</span> <span class="token parameter variable">-k</span>
</li><li data-prefix="$"><span class="token function">sudo</span> <span class="token function">ls</span>
</li></ol>
</code></pre><div class="toolbar"><div class="toolbar-item"></div></div></div>
<pre><code><div class="secondary-code-label" title="Output">Output</div>[sudo] password for demo:    # <mark>enter an incorrect password here to see the results</mark>
Your mind just hasn't been the same since the electro-shock, has it?
[sudo] password for demo:
My mind is going. I can feel it.
</code></pre>
<h2 id="conclusion"><a href="#conclusion" onclick="navigator.clipboard.writeText(this.href);">Conclusion</a><a class="hash-anchor" href="#conclusion" aria-hidden="true" onclick="navigator.clipboard.writeText(this.href);"></a></h2>
<p>You should now have a basic understanding of how to read and modify the <code>sudoers</code> file, and a grasp on the various methods that you can use to obtain <strong>root</strong> privileges.</p>
<p>Remember, super-user privileges are not given to regular users for a reason. It is essential that you understand what each command does that you execute with <strong>root</strong> privileges. Do not take the responsibility lightly. Learn the best way to use these tools for your use-case, and lock down any functionality that is not needed.</p>
