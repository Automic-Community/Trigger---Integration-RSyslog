*Trigger - Integration RSyslog *
=============


Integrate with RSyslog
http://github.com/Automic-Community/Trigger---Integration-RSyslog-

<!-- List of attached files -->
Contents of Solution Package:

						
								*Dollar_Universe-RSyslog_Event_Trigger.zip
								
						


Documenation and Instructions
---

<div class="ipsType_textblock ipsPad_half description_content"><span><strong class="bbc">Prerequisites</strong></span>
<ul class="bbc">
<li>Unix with <strong class="bbc">Rsyslog</strong> server for system logging.</li>
<li>cURL (cf. <a class="bbc_url" title="External link" href="http://curl.haxx.se/" rel="nofollow external">http://curl.haxx.se/</a>)</li>
</ul>
<span><strong class="bbc">Define the Syslog event to monitor</strong></span>
<ul class="bbc">
<li>Go to directory containing your "<em class="bbc">rsyslog.conf</em>" file (this should be /etc).</li>
<li>Edit "<em class="bbc">rsyslog.conf</em>" file.</li>
<li>Go at the end of the file.</li>
<li>Add the following line, that defines a template output:</li>
</ul>
<pre class="prettyprint lang-auto linenums:0 prettyprinted"><span class="pln">$template t_orsyp_trigger</span><span class="pun">,</span><span class="str">"%programname%|%hostname%|%syslogfacility%|%syslogseverity%|%timereported%|%msg%"</span></pre>
<ul class="bbc">
<li>Add the following line, that defines which kind of events you want to monitor:</li>
</ul>
<pre class="prettyprint lang-auto linenums:0 prettyprinted"><span class="pun">{</span><span class="pln">FACILITY</span><span class="pun">}.{</span><span class="pln">SEVERITY</span><span class="pun">}</span><span class="pln"> </span><span class="pun">^{</span><span class="pln">PATH_TO_YOUR_SCRIPT</span><span class="pun">};</span><span class="pln">t_orsyp_trigger</span></pre>
<br />Where {<strong class="bbc"><em class="bbc">FACILITY</em></strong>} and {<em class="bbc"><strong class="bbc">SEVERITY</strong></em>} give a first filter on the Syslog events you want to trigger.<br />{<strong class="bbc">PATH_TO_YOUR_SCRIPT</strong>} indicates the path to the given script that will launch the $U trigger.<br />If you want to trigger several Syslog events, you can add other lines of that kind. You could have for example, something like:<br /><br />
<pre class="prettyprint lang-auto linenums:0 prettyprinted"><span class="pln">kern</span><span class="pun">.*</span><span class="pln"> </span><span class="pun">^</span><span class="str">/var/</span><span class="pln">opt</span><span class="pun">/</span><span class="pln">ORSYP</span><span class="pun">/</span><span class="pln">DUAS</span><span class="pun">/</span><span class="pln">rsyslog_event_trigger</span><span class="pun">.</span><span class="pln">sh</span><span class="pun">;</span><span class="pln">t_orsyp_trigger</span></pre>
<br />
<pre class="prettyprint lang-auto linenums:0 prettyprinted"><span class="pln">auth</span><span class="pun">.*</span><span class="pln"> </span><span class="pun">^</span><span class="str">/var/</span><span class="pln">opt</span><span class="pun">/</span><span class="pln">ORSYP</span><span class="pun">/</span><span class="pln">DUAS</span><span class="pun">/</span><span class="pln">rsyslog_event_trigger</span><span class="pun">.</span><span class="pln">sh</span><span class="pun">;</span><span class="pln">t_orsyp_trigger</span></pre>
<br />
<pre class="prettyprint lang-auto linenums:0 prettyprinted"><span class="pun">*.</span><span class="pln">crit </span><span class="pun">^</span><span class="str">/var/</span><span class="pln">opt</span><span class="pun">/</span><span class="pln">ORSYP</span><span class="pun">/</span><span class="pln">DUAS</span><span class="pun">/</span><span class="pln">rsyslog_event_trigger</span><span class="pun">.</span><span class="pln">sh</span><span class="pun">;</span><span class="pln">t_orsyp_trigger</span></pre>
<br /><strong class="bbc"><span class="bbc_underline">NB:</span></strong> You can only filter the Syslog events by their facility and their severity here. If you want more advanced filters, this should be done on $U side.<br /><strong class="bbc"><span class="bbc_underline">NB:</span></strong> For performance considerations, you should avoid having a line like that:<br /><br /><br />
<pre class="prettyprint lang-auto linenums:0 prettyprinted"><span class="pun">*.*</span><span class="pln"> </span><span class="pun">^{</span><span class="pln">PATH_TO_YOUR_SCRIPT</span><span class="pun">};</span><span class="pln">t_orsyp_trigger</span></pre>
<br /><br /><span><strong class="bbc">Define which $U node to target </strong></span>
<ul class="bbc">
<li>Inform the attributes giving the definition of the target $U node:<br />
<ul class="bbc">
<li><em class="bbc"><strong class="bbc">host:</strong> </em>The hostname of the $U node.</li>
<li><em class="bbc"><strong class="bbc">port</strong>: </em>The port number of the $U api.</li>
<li><em class="bbc"><strong class="bbc">area</strong></em>: The target area.</li>
</ul>
</li>
<li>Inform the attributes giving the way you are going to authenticate yourself to $U node:</li>
</ul>
<strong class="bbc"><span class="bbc_underline">NB:</span></strong> You must inform either the authentication key or your credentials.<br /><strong class="bbc"><span class="bbc_underline">NB:</span></strong> If you inform both the authentication key and your credentials, only the authentication will be taken into account.
<ul class="bbc">
<li><em class="bbc"><strong class="bbc">authentication_key</strong></em>: The authentication key you got via UVC. OR</li>
<li><em class="bbc"><strong class="bbc">user</strong> </em>/ <em class="bbc"><strong class="bbc">password</strong></em>: Your credentials.</li>
<li>[optional] You can modify the event type that will be raised on $U. By default this event type is: "<strong class="bbc">SYSLOG_EVENT</strong>".</li>
<li>Save and close the script.</li>
<li>Ensure that the script is executable by the <strong class="bbc">rsyslog</strong> server.</li>
</ul>
<span><strong class="bbc">Event properties</strong></span><br /><span><span><span>The given script transmit, by default, the following event properties:</span></span></span>
<ul class="bbc">
<li><span><span><span><em class="bbc"><strong class="bbc">PROGRAM</strong></em>: The name of the program that raised the Syslog event.</span></span></span></li>
<li><span><span><span><em class="bbc"><strong class="bbc">HOST</strong></em>: The host of this program.</span></span></span></li>
<li><span><span><span><em class="bbc"><strong class="bbc">FACILITY</strong></em>: The Syslog facility level numeric value (cf. <a class="bbc_url" title="External link" href="http://en.wikipedia.org/wiki/Syslog#Facility_levels" rel="nofollow external">http://en.wikipedia....Facility_levels</a>).</span></span></span></li>
<li><span><span><span><em class="bbc"><strong class="bbc">SEVERITY</strong></em>: The Syslog severity level numeric value (cf. <a class="bbc_url" title="External link" href="http://en.wikipedia.org/wiki/Syslog#Severity_levels" rel="nofollow external">http://en.wikipedia....Severity_levels</a>).</span></span></span></li>
<li><span><span><span><em class="bbc"><strong class="bbc">DATE</strong></em>: The date/time when the Syslog event has been raised.</span></span></span></li>
<li><span><span><span><em class="bbc"><strong class="bbc">MESSAGE</strong></em>: The message of the Syslog event.</span></span></span></li>
</ul>
<span><span><span><strong class="bbc">Customize the transmitted event properties</strong></span></span></span><br /><span><span><span>If you want to add or remove some event properties, you should modify the </span></span></span><em class="bbc"><strong class="bbc">t_orsyp_trigger</strong></em><span><span><span> template or add a new one.</span></span></span><br /><span><span><span>The template have to be like this: "</span></span></span><em class="bbc">%property1%|%property2%|...|%propertyN%</em><span><span><span>"</span></span></span><br /><span><span><span>With '|' separating each considered property.</span></span></span><br /><span><span><span>Please refer to this page for the list of the available properties: </span></span></span><a class="bbc_url" title="External link" href="http://www.rsyslog.com/doc/property_replacer.html" rel="nofollow external">http://www.rsyslog.c...y_replacer.html</a><span><span><span>.</span></span></span><br /><span><span><span>Then, you also need modify the given script accordingly.</span></span></span><br /><span><span><span>Just search for the following comment to find the places where you have to modify the script:</span></span></span><br /><br />
<pre class="prettyprint lang-auto linenums:0 prettyprinted"><span class="com"># You should modify these lines if you modify the list of considered event properties</span></pre>
<br /><br /><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><strong class="bbc">Output</strong></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span><br /><span><span><span>Basically, the output of the script will be something like:</span></span></span><br />
<pre class="prettyprint lang-auto linenums:0 prettyprinted"><span class="typ">Script</span><span class="pln"> launched at </span><span class="pun">{</span><span class="pln">DATE</span><span class="pun">}</span><span class="pln">
</span><span class="typ">Login</span><span class="pln"> on </span><span class="pun">{</span><span class="pln">HOST</span><span class="pun">}:{</span><span class="pln">PORT</span><span class="pun">}</span><span class="pln"> </span><span class="pun">--&gt;</span><span class="pln"> </span><span class="typ">Success</span><span class="pln">
</span><span class="typ">Send</span><span class="pln"> </span><span class="kwd">event</span><span class="pln"> TEST </span><span class="pun">--&gt;</span><span class="pln"> </span><span class="typ">Incomplete</span><span class="pln">
</span><span class="pun">=&gt;</span><span class="pln"> </span><span class="typ">Trigger</span><span class="pun">:</span><span class="pln"> TEST1 </span><span class="pun">--&gt;</span><span class="pln"> </span><span class="typ">Launch</span><span class="pln"> number</span><span class="pun">:</span><span class="pln"> XXXXXXX
</span><span class="pun">=&gt;</span><span class="pln"> </span><span class="typ">Trigger</span><span class="pun">:</span><span class="pln"> TEST2 </span><span class="pun">--&gt;</span><span class="pln"> </span><span class="typ">Error</span><span class="pln"> </span><span class="lit">1023</span><span class="pun">:</span><span class="pln"> </span><span class="typ">Only</span><span class="pln"> provoked tasks can be triggered</span><span class="pun">.</span><span class="pln">
</span><span class="typ">Logout</span><span class="pln"> </span><span class="pun">--&gt;</span><span class="pln"> </span><span class="typ">Success</span></pre>
<br /><span><span><span>Then the output gives you basic trigger related operations:</span></span></span>
<ul class="bbc">
<li><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span>Login (if no authentication key given)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></li>
<li><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span>Event type launch</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></li>
<li><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span>Logout (if no authentication key given)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></li>
</ul>
<span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span><span>&amp;#8203;</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span><span><span><span>It will give you the launch number of the launched jobs, or the code and error message if a launch has failed.</span></span></span><br /><span><span><span><strong class="bbc"><span class="bbc_underline">NB:</span> </strong></span></span></span><span><span><span>By default this is logged into a .log file with the same name as your script. You can transform it to a console output by modifying the </span></span></span><em class="bbc"><strong class="bbc">log_to_file</strong></em><span><span><span> attribute value to "0".</span></span></span></div>

Copyright and License
---

Solutions, Templates, Actions and other content available on the Automic Marketplace subject to the Automic [Developers Distribution License] (http://automic.com/developers-distribution-license) as well as the Automic Community [Terms of Service] (http://automic.com/community-terms-of-service).
Automic does not support, maintain or warrant any content submitted by the Automic Community.



Questions or Need Help? 
---
Any questions or comments? Converse with your fellow Users in the [Automic Community] (https://community.automic.com).