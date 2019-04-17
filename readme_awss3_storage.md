## Cloudmesh Integration

AWS S3 file storage has been integrated with cloudmesh library and is available for use via commandline. 
As a first step we need to modify `cloudmesh4.yaml` config file.  Under 'storage' section, we need to add the aws section 
to specify the parameters used to store files in AWS S3. 

In the credentials section under aws, specify the access key id and secret access key which will be available in the 
AWS console under AWS IAM service -> Users -> Security Credentials. 

Container is the default bucket which will be used to store the files in AWS S3. Region is the geographic area like 
us-east-1 which contains the bucket. Region is required to get a connection handle on the S3 Client or resource for 
that geographic area.

Here is a sample.

```bash
storage:
    aws:
      cm:
        heading: aws
        host: amazon.aws.com
        label: aws
        kind: awsS3
        version: TBD
      default:
        directory: TBD
      credentials:
        access_key_id: *********
        secret_access_key: *******
        container: name of bucket that you want user to be contained in.
        region: Specfiy the default region eg us-east-1
```

The Cloudmesh command line library offers six functions under storage command: get, put, search, list, create directory, and delete. 
Once you have installed Cloudmesh, type `cms` into the command line to start the shell. 

```bash
$ storage --storage=box 
```

### Get

To download a file from Box with Cloudmesh, you must specify the cloud folder or file to be downloaded and the local folder to download to. To download all the contents of a folder, simply specify a folder on the cloud and use the recursive option. 

```bash
$ storage --storage=box get /test_folder/test_file.txt ~/test_folder --recursive
```

### Put

The put command uploads files from your local host to the cloud. If you specify a file as the source, the file will be uploaded if no such file exists on the cloud or updated if a copy already exists on the cloud. If the source is a directory and recursive is specified, Cloudmesh will upload all the contents of the source directory to the cloud. 

```bash
$ storage --storage=box put ~/test_folder /uploads --recursive
```

### Search

To search for a file through Cloudmesh, you must specify a directory in which to search and the file or folder name you are searching for. If recursive is specified, Cloudmesh will search all child directories of the original directory. 

```bash
$ storage --storage=box search /uploads last_upload.txt --recursive
```

### List

The list command lists all the contents of a cloud directory. If recursive is specified, it will list the contents of all child directories as well. 

```bash
$ storage --storage=box list /uploads --recursive
```

### Create a directory

To create a new directory, you must specify the path of the new directory you would like to create, including its parent directory. 

```bash
$ storage --storage=box create dir /test_folder/new_folder
```

### Delete

The delete command can delete files or folders from your cloud file storage. Deleting a folder will delete its contents as well. 

```bash
$ storage --storage=box delete /uploads/last_upload.txt
```

Finally, if you have set the storage variable to box, you can omit the `--storage=box` from your command line calls. 

:o: openapi
