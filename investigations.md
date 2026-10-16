# 4:11pm:
Starting and documenting investigations...

# 4:23:
Exploring tables & schema commands;
tables shows: access_grants  access_logs  channels  events  members  messages
Schema shows the how's the table are made and we can already see that the tables
have primary & foreign keys, this will probably be used.

# 4:27:
I can see that there's informations really useful here, like:
credential_owner_id
actor_id
If credential_owner_id is not equals to actor_id,
we can clearly see who stole the account

# 4:30:
We can also see that there's an "evidence_tag" in the events table.
This will be really usefull too. Keep that in mind.

# 4:33:
With the command: "SELECT * FROM channels;" we can get the channel ID and basics
informations, such as the name (we already know wich one we're looking for)
or even the channel_type, status and when it has been created.
Keep in mind: Channel id = 7.

# 4:38:
After this, we can look into the events table with the command:
"SELECT * FROM events;"
We can clearly see that one event is suspicious: event 5 (its ID).
The event_type and evidence_tag clearly say "Theft".
Another piece of information that we can get here is the member_id (3).
We can clearly see that we're looking at an event from "Campement 7"
since the channel_id is the same one that we got earlier (7).

# 4:40:
We need to know who's the member 3 now; lets simply do this with the command:
"SELECT * FROM members WHERE member_id = 3;"
...
The member is Mickael. Now let's try to find more informations on this case.


# 4:50:
My next commands will simply help us to check Mickael's logs:
SELECT
    al.log_id,
    al.occurred_at,
    al.action,
    al.device,
    al.credential_owner_id,
    al.actor_id,
    m.display_name AS owner_name
FROM access_logs al
JOIN members m ON al.credential_owner_id = m.member_id
WHERE al.credential_owner_id = 3 OR al.actor_id = 3;

With this command; there's multiple informations.
First of all:
the device used in thoses logs is the "poste-07".
The actor_id (who did it) is... Mickael. (Of course, we're looking at his logs..)
We can see that Mickael made multiple actions using other people's credentials:
- 08:51, he used Anthony's account (credentials_owner_id= 2) to do an "export"
- 08:52, still on Anthony's account, he made an "archive" action
- 08:37, this time on Kevin's account (credentials_owner_id= 1) he made a "Rename"
action.

This proves that Mickael is the guilty. He stole others staff members account to
remove "Campement 7".


