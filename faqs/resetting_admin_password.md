@@todo Merge https://github.com/textpattern/textpattern.github.io/blob/master/faqs/help-i-forgot-my-password.md if required, then move this to a HowTo section?@@

Resetting the administrators password (or any user password) is fairly
straight forward. This presumes you have access to phpMyAdmin which is
commonly installed on my webservers that use MySQL.

### The Process {#the-process .sectionedit1#the_process}

<ol>
<li>
Start phpMyAdmin. This may be done from shell or your control panel.

</li>
<li>
At the opening screen, select the database for your Textpattern install
(eg userid_textpattern).

</li>
<li>
From the list of tables select **txp_users**. This should present a
table structure and a selection of tabbed options.

</li>
<li>
Select the **Browse** tab. This will display a query field and a list of
users.

</li>
<li>
Click on the **small pencil (edit) icon** next to the **user ID** entry
you wish to edit. This will display a table for the record showing the
fields and their current values. *Note that only the password hash is
displayed, not the plain text.*

</li>
<li>
<p>
In the function column for the **pass** field, select **PASSWORD** from
the drop down box. You may then delete the hash and enter a plaintext
password in the corresponding value field. Letters in this field should
be all lowercase. Make sure the box at the lower left says **'save**'
and click on the **GO** button. You will be returned to the previous
screen which will display the SQL query you just created. The hash
displayed opposite the user ID you selected should have changed (unless
you used the exact same password). Alternatively you can click on the
*Edit* link for the SQL query field visible in step 5 and enter the
following substituting the desired password for *newpassword* and the
appropriate userID **number** :

</p>
    UPDATE `txp_users` SET `pass` = PASSWORD( ' **newpassword** ' ) WHERE `user_id` = **number** LIMIT 1;

<p>
.

</p>
</li>
<li>
Exit phpMyAdmin and login to Textpattern with your username and new
password.

</li>
</ol>
### Changing to Higher Permission Status if Accidentally Set Incorrectly {#changing-to-higher-permission-status-if-accidentally-set-incorrectly .sectionedit2#changing_to_higher_permission_status_if_accidentally_set_incorrectly}

It has happened to people before that while learning the nature of
different permission settings in the xxx panel they accidentally set
themselves at a lower permissions level than what they indended to have;
for example as Managing Editor instead of Publisher.

You can fix this situation, but you have to have access to a database
management program like phpMyAdmin for the database involved. Following
is what you do:

1.  Open phpMyAdmin, select the appropriate database, and browse to the
    **txp_users** table.
2.  Look for the row with your Textpattern account username, and find
    the column named “**privs**”.
3.  Change it to the number “**1**”.

