# 4:11pm:
Starting and documenting investigations...

# 4:23:
Exploring tables & schema commands;<br>
tables shows: access_grants  access_logs  channels  events  members  messages<br>
Schema shows the how's the table are made and we can already see that the tables<br>
have primary & foreign keys, this will probably be used.<br>

# 4:27:
I can see that there's informations really useful here, like:<br>
credential_owner_id<br>
actor_id<br>
If credential_owner_id is not equals to actor_id,<br>
we can clearly see who stole the account<br>

# 4:30:
We can also see that there's an "evidence_tag" in the events table.<br>
This will be really usefull too. Keep that in mind.<br>

# 4:33:
With the command: "SELECT * FROM channels;" we can get the channel ID and basics<br>
informations, such as the name (we already know wich one we're looking for)<br>
or even the channel_type, status and when it has been created.<br>
Keep in mind: Channel id = 7.<br>

# 4:38:
After this, we can look into the events table with the command:<br>
"SELECT * FROM events;"<br>
We can clearly see that one event is suspicious: event 5 (its ID).<br>
The event_type and evidence_tag clearly say "Theft".<br>
Another piece of information that we can get here is the member_id (3).<br>
We can clearly see that we're looking at an event from "Campement 7"<br>
since the channel_id is the same one that we got earlier (7).<br>

# 4:40:
We need to know who's the member 3 now; lets simply do this with the command:<br>
"SELECT * FROM members WHERE member_id = 3;"<br>
...<br>
The member is Mickael. Now let's try to find more informations on this case.<br>


# 4:50:
My next commands will simply help us to check Mickael's logs:<br>
SELECT<br>
    al.log_id,<br>
    al.occurred_at,<br>
    al.action,<br>
    al.device,<br>
    al.credential_owner_id,<br>
    al.actor_id,<br>
    m.display_name AS owner_name<br>
FROM access_logs al<br>
JOIN members m ON al.credential_owner_id = m.member_id<br>
WHERE al.credential_owner_id = 3 OR al.actor_id = 3;<br>

With this command; there's multiple informations.<br>
First of all:<br>
the device used in thoses logs is the "poste-07".<br>
The actor_id (who did it) is... Mickael. (Of course, we're looking at his logs..)<br>
We can see that Mickael made multiple actions using other people's credentials:<br>
- 08:51, he used Anthony's account (credentials_owner_id= 2) to do an "export"<br>
- 08:52, still on Anthony's account, he made an "archive" action<br>
- 08:37, this time on Kevin's account (credentials_owner_id= 1) he made a "Rename"<br>
action.<br>

This proves that Mickael is the guilty. He stole others staff members account to<br>
remove "Campement 7".<br>

# 4:57:
Conclusion:<br>
The channel "Campement 7" (ID: 7).<br>
The event "theft" (id: 5).<br>
The guilty one: "Mickael" (id: 3) operating from "poste-07"<br>

Mickael stone and used other member's credentials to carry out the attack:<br>
- Anthony's account (id: 2) used at 08:51 to export the data and<br>
at 08:52 to archive the channel.<br>
- Kevin's account (id: 1) used at 08:57 to attempt a rename action<br>
(wich didn't works since we can see that the channel_name is still "Campement 7)<br>

Result:<br>
Mickael is responsible for the disappearance of "Campement 7"<br>
by usurping Anthony and Kevin's account from workstation "poste-07"<br>
