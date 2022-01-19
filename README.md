# Backup Google Drive using RClone

If you want to make an automatic backup of your Google Drive to another WebDAV or FTP location.

Use RClone
  https://rclone.org/install/
  
  ```
  cd /tmp
  curl https://rclone.org/install.sh | sudo bash
  ```
  ```
  curl -O https://downloads.rclone.org/rclone-current-linux-amd64.zip
  unzip rclone-current-linux-amd64.zip
  cd rclone-*-linux-amd64
  ```
  ```
  cp rclone /usr/bin/
  chown root:root /usr/bin/rclone
  chmod 755 /usr/bin/rclone
  ```
  ```
  mkdir -p /usr/local/share/man/man1
  cp rclone.1 /usr/local/share/man/man1/
  mandb
  ```
  
### Google Drive Config ###
https://rclone.org/docs/ (Google Drive: https://rclone.org/drive/)<p>

  ```
  rclone config
  ```
  
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
  ```
  rclone config
  ```
  
  name:     stack<br>
  storage:  40 (webdav)<br>
  url:      https://<URL_TO_YOUR_SPACE>/webdav<br>
  vendor:   5 (other)<br>
  user:     username<br>
  password: password<br>
  bearer_token: <empty><br>
  
 
### Action ###<br>
List directory<br>
  ```
  rclone ls google-drive:/
  rclone ls stack:/
  ```
  
Copy all thats on your drive<br>
  ```
  rclone copy google-drive:/ stack:/_bck/googledrive-jan-2022
  ```
