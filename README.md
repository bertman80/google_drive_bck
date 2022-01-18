# Backup Google Drive using RClone

If you want to make an automatic backup of your Google Drive to another WebDAV or FTP location.

Use RClone
  https://rclone.org/install/
  
  mkdir temp
  cd temp
  curl https://rclone.org/install.sh | sudo bash
  
  curl -O https://downloads.rclone.org/rclone-current-linux-amd64.zip
  unzip rclone-current-linux-amd64.zip
  cd rclone-*-linux-amd64
    
  cp rclone /usr/bin/
  chown root:root /usr/bin/rclone
  chmod 755 /usr/bin/rclone
  
  mkdir -p /usr/local/share/man/man1
  cp rclone.1 /usr/local/share/man/man1/
  mandb

### Google Drive Config ###
https://rclone.org/docs/ (Google Drive: https://rclone.org/drive/)

rclone config
  
  name:                 google-drive
  storage:              16 (Google Drive)
  client_id:            <empty>
  client_secret:        <empty>
  scope:                1 (Full access all files, excluding Application Data Folder.)
  root_folder_id:       <empty>
  service_account_file: <empty>
  Edit advanced config: no
  Use auto config?:     yes
  Configure this as a Shared Drive (Team Drive)?: no

### Config Google Credentials ###
  You need to make an 'OAuth client ID' so that you can login to your Google Drive
  https://rclone.org/drive/#making-your-own-client-id
  
### Stack (WebDAV) ###
  My target is Stack based on WebDAV
  
  rclone config

    name:     stack
    storage:  40 (webdav)
    url:      https://<URL_TO_YOUR_SPACE>/webdav
    vendor:   5 (other)
    user:     username
    password: password
    bearer_token: <empty>
  
 
### Action ###
List directory
  rclone ls google-drive:/
  rclone ls stack:/  

Copy all thats on your drive
  rclone copy google-drive:/ stack:/_bck/googledrive-jan-2022
