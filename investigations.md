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
