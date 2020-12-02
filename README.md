# bearclaw
Bearclaw Backup Scripts

Bearclaw is a bash shell script which reads target configurations from a Redis key/value database and supports several different backup functions. Functions can be added modularly.  Focus has been on keeping the backups fully configured and supported from the server side (i.e. not requiring any modifications to the client system besides what is already available), ease of configuration, informational and clear logging, secure storage of auth, and encrypted connections.

Currently supported backup functions:
  * Rsync'ed backups over ssh.
  * Rsync'ed backups from mounted CIFS/SMB shares.
  * IMAP mail synchronisation with getmail.
  
Benefits:
  * Single master bash script with supporting shell script libraries.
  * Ease of configuration through redis key/value pairs.
  * Daily hard-linked timestamped directories.
  * Hard-linked copies mean that no additional space is required for each copy.
  * Hard-linked copies mean that each timestamped directory is essentially a full backup with all files granularly available for restoral.
  * Each user has full access through an authenticated miniserve instance to find and restore their own files.
  * Storage recovery process deletes oldest backups when space available (redis configurable) is low.
  * Admin access to redis-commander instance for adding and modifying users and target systems.
  * Email notifications are sent after each back up run.
  * Log files are emailed to users after each run.
  * Admin user gets an email with full log files for entire run.
  * Process controlled through crontab.
  * Enable/disable each user via a simple redis toggle (enable yes/no).
  * Enable/disable each system via redis toggle (enable yes/no).

Adding other backup target functions is as simple as creating a function.{type} shell script, using one of the included functions as an example, and supplying a redis db key/value schema for that particular type. Tftp, ftp, wget, might be other possibilities.

