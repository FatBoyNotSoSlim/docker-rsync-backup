# Basic Usage

Basic backup of `/home` to `/mnt/backup_drive`

    docker run -d --name rsync-backup \
      --volume /home:/home \
      --volume /mnt/backup_drive:/backup \
      --volume /mnt/rsyncbackup/log:/log \
      --volume /mnt/rsyncbackup/rclone:/rclone \
      -env SET_CONTAINER_TIMEZONE=true \
      -env CONTAINER_TIMEZONE=Europe/Stockholm \
      -env BACKUP_HOLD=15 \
      -env SERVER_ID=docker \
      mrdoob/rsyncbackup


The container can then be stopped with `docker kill rsync-backup`.

## Supported tags and architectures

For use on a normal machine, use the `latest` tag.

# Details volumes 

      /home
          Folder to backup to read 

      /mnt/backup_drive
          folder for backup to store 
          After sync from /home it will create automatically  tar files from the folder 

      /mnt/rsyncbackup/log
          folder for backup logs ( rsync and tar logs )

      /mnt/rsyncbackup/rclone
          folder to store your rclone config 
          for automatically upload to your gsuite 
          It will automatically  read if gdrive or gcrypted can used 
          for storing your backup on your GSuite Account 

          It will also read when  no rclone config is in the folder
          then it will only create the tar fike
 


## Environment variables

The backup can be configured using the environment variables, as show in the
examples. Here is a full list of the variables, default values and uses.


    BACKUPDIR ("/home"): 
       Directory path to be archived. Usually remote or a mounted volume.

    SSH_PORT ("22"): 
       Change if a non-standard SSH port number is used.

    SSH_IDENTITY_FILE ("/root/.ssh/id_rsa"): 
       Change to use a key mounted from the host.
 
    ARCHIVEROOT ("/backup"): 
       It's good to mount a volume at this path. A folder structure like this will be created:
        /backup
        └── each subfolder 

    EXCLUDES (""): 
       Semicolon separated list of exclude patterns. Use the format
       described in the FILTER RULES section of the rsync man page. A limitation
       is that semicolon may not be present in any of the patterns.

    CRON_TIME ("0 1 * * *"): 
       The time to do backups. The default is at 01:00 every night.

    CONTAINER_TIMEZONE=Europe/Stockholm
       You can choose any timezone you want , for find the correct timezone 
       In your case  ( sudo cat /etc/timecone )

    BACKUP_HOLD=15
       Remove older Backups from GDrice or GCrypt 

    SERVER_ID=docker
       if you have multiple servers, this is advantageous 
       for the assignments at the end.


THIS IS A *** Work In Progress *** 

in the end this means that there could be updates daily to weekly, as well as possible errors or the like,


# Support

Add a [GitHube Issuses](https://github.com/doob187/docker-rsync-backup/issues).
