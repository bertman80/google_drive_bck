# Backup Google Drive using RClone

If you want to make an automatic backup of your Google Drive to another WebDAV or FTP location.

Use RClone
  https://rclone.org/install/
  
  mkdir temp<br>
  cd temp<br>
  curl https://rclone.org/install.sh | sudo bash<br><br>
  
  curl -O https://downloads.rclone.org/rclone-current-linux-amd64.zip<br>
  unzip rclone-current-linux-amd64.zip<br>
  cd rclone-*-linux-amd64<br><br>
    
  cp rclone /usr/bin/<br>
  chown root:root /usr/bin/rclone<br>
  chmod 755 /usr/bin/rclone<br><br>
  
  mkdir -p /usr/local/share/man/man1<br>
  cp rclone.1 /usr/local/share/man/man1/<br>
  mandb<br><br>

### Google Drive Config ###
https://rclone.org/docs/ (Google Drive: https://rclone.org/drive/)<p>

rclone config<br><br>
  
  name:                 google-drive<br>
  storage:              16 (Google Drive)<br>
  client_id:            <empty><br>
  client_secret:        <empty><br>
  scope:                1 (Full access all files, excluding Application Data Folder.)<br>
  root_folder_id:       <empty><br>
  service_account_file: <empty><br>
  Edit advanced config: no<br>
  Use auto config?:     yes<br>
  Configure this as a Shared Drive (Team Drive)?: no<br><br>

### Config Google Credentials ###
  You need to make an 'OAuth client ID' so that you can login to your Google Drive<br>
  https://rclone.org/drive/#making-your-own-client-id<br><br>
  
### Stack (WebDAV) ###<br>
  My target is Stack based on WebDAV<p>
  
  rclone config<br>

    name:     stack
    storage:  40 (webdav)
    url:      https://<URL_TO_YOUR_SPACE>/webdav
    vendor:   5 (other)
    user:     username
    password: password
    bearer_token: <empty>
  
 
### Action ###<br>
List directory<br>
  rclone ls google-drive:/<br>
  rclone ls stack:/  <br><br>

Copy all thats on your drive<br>
  rclone copy google-drive:/ stack:/_bck/googledrive-jan-2022
