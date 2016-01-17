# Cheat Sheet

These are the not-so-common commands that I run every once in a while that I can never remember.

## Git

* [How do you rename the local branch?](https://stackoverflow.com/questions/6591213/how-do-you-rename-the-local-branch)
* [Various ways to remove local Git changes](https://stackoverflow.com/questions/22620393/various-ways-to-remove-local-git-changes)
* [How can I reconcile detached HEAD with master/origin?](https://stackoverflow.com/questions/5772192/how-can-i-reconcile-detached-head-with-master-origin)
* [Git fetch remote branch](https://stackoverflow.com/questions/9537392/git-fetch-remote-branch)
* [Clone all remote branches with Git](https://stackoverflow.com/questions/67699/clone-all-remote-branches-with-git)

## Copy ssh public key to server

### Linux
```
ssh-copy-id username@hostname
```

### Mac
```
cat ~/.ssh/id_rsa.pub | ssh user@machine "mkdir ~/.ssh; cat >> ~/.ssh/authorized_keys"
```

[Source](http://www.commandlinefu.com/commands/view/188/copy-your-ssh-public-key-to-a-server-from-a-machine-that-doesnt-have-ssh-copy-id)

## Reset Postgres primary key sequence

```
-- Login to psql and run the following
-- What is the result?
SELECT MAX(id) FROM your_table;

-- Then run...
-- This should be higher than the last result.
SELECT nextval('your_table_id_seq');

-- If it's not higher... run this set the sequence last to your highest pid it.
-- (wise to run a quick pg_dump first...)
SELECT setval('your_table_id_seq', (SELECT MAX(id) FROM your_table));
-- if your tables might have no rows
-- false means the set value will be returned by the next nextval() call    
SELECT setval('your_table_id_seq', COALESCE((SELECT MAX(id)+1 FROM your_table), 1), false);
```

[Source](https://stackoverflow.com/questions/244243/how-to-reset-postgres-primary-key-sequence-when-it-falls-out-of-sync)

## Find and replace in file on command line

```
sed -i "s/original/new/g" file.txt
sed -i "s/\`/\'/g" file.txt
```

## Check SHA1 checksum

```
shasum file.dmg | grep 4cbcea9764b6b657d2147645eeb5b973b642530e
```
