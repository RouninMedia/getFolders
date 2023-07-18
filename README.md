# getFolders()
A PHP function which scans a web directory recursively and returns a nested PHP associative array representing a schema of web directory files and folders

## `getFolders($Target_Folder, $Folders_to_Skip = [])`

```php

function getFolders ($Target_Folder, $Folders_to_Skip = []) {

  $ArrayOfFolderContents = [];

  if (is_dir($Target_Folder)) {

    $ArrayOfFolderContents['Files'] = [];

    $assets = scandir($Target_Folder);

    $Folders_to_Skip = array_merge(['.', '..'], $Folders_to_Skip);

    foreach ($assets as $asset) {

      if (!in_array($asset, $Folders_to_Skip)) {

        if (filetype($Target_Folder.'/'.$asset) === 'dir') {

          $ArrayOfFolderContents[$asset] = getFolders($Target_Folder.'/'.$asset);
        }

        else {

          $ArrayOfFolderContents['Files'][] = $asset;
        }
      }
    }

    reset($assets);

    return $ArrayOfFolderContents;
  }
}

```
