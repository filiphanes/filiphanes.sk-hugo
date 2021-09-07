+++
date = "2021-09-09T21:30:00+02:00"
title = "Don't reinvent file/object storage API"
comments = true
description = ""
categories = ["storage"]
tags = ["api", "storage","web","s3","webdav"]
url = "storage/dont-reinvent-file-object-storage-api/"
image = "img/streaming.jpg"

+++
In this article we will compare HTTP API of solutions providing access to files via HTTP.

## WebDAV
Old standard created in HTTP and XML times.

Pros:
- standardized
- supported by every major OS, and many software
- many features, supports locking, properties
- can Copy, Move file on 1 request
- extensible with own XML namespaces

Cons:
- uses own HTTP methods (MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK), so not very compatible with HTTP, but can be used from browser (NextCloud uses WebDAV)
- XML responses  (JSON is now popular)
- seems like it needs many requests

http://www.webdav.org/specs/rfc2518.html

## S3
Originally created by Amazon for their S3 object storage. Later implemented by other object storage providers. IMHO very good alternative to WebDAV. All operations are compatible with HTTP methods. Uses XML responses, but not so complicated as WebDAV.

Pros:
- defacto industry standard, many server and client implementations
- compatible with HTTP
- many features (tagging, metadata, chunked upload)
- can copy in 1 request
- has batch DELETE `POST /?delete`
- many features, ACLs, locking, tagging, ...

Cons:
- complicated on first impression (authorization, ...)
- XML responses (JSON is now popular)
- cannot move file in 1 request
- cannot delete folder in 1 request


https://docs.aws.amazon.com/AmazonS3/latest/API/API_Operations_Amazon_Simple_Storage_Service.html

## Seaweed Filer
Simple implementation of storage API
POST method can upload file (from HTML form).

Pros:
- JSON responses
- can recursively delete dir in 1 request
- uses standard HTTP methods

Cons:
- not many features
- cannot copy/move in 1 request

https://github.com/chrislusf/seaweedfs/wiki/Filer-Server-API

## FileStash
Web browser for many backeds: S3, SFTP, WebDAV, MySQL, Dropbox, GDrive.
Included in this comparison, because it has nice frontend and reinvented file access API.

https://www.filestash.app/

## FileBrowser
Web browser for local file system, with material design UI.
Included in this comparison, because it reinvented file access API.

https://filebrowser.org/

Pros:
- modern JSON responses
- has copy, move on 1 request

Cons:
- uses PATCH method for copy, move


# Comparison of APIs
We will be working with path `/bucket/directory/file.txt` and when there are no buckets we it is only directory.

## List directory entries
### WebDAV
    GET /bucket/
### S3
    GET /bucket?prefix=/directory/&delimiter=/
### Seaweed Filer
    GET /bucket/directory/
    Accept: application/json
### FileStash
    GET /api/files/ls?path=/directory/
### FileBrowser
    GET /api/resources/bucket/directory/

## Create directory
### WebDAV
    MKCOL /bucket/directory/
### S3, need to put some file in directory
    PUT /bucket/directory/.keep
### Filer: 
### FileStash
    GET /api/files/mkdir?path=/bucket/directory/
### FileBrowser
    POST /api/resources/priecinok/?override=false

## Create file
### WebDAV
    PUT /bucket/directory/file.txt
### S3
    PUT /bucket/directory/file.txt
### Filer
    PUT /bucket/directory/file.txt
### FileStash
    GET /api/files/touch?path=/bucket/directory/file.txt
    or
    POST /api/files/cat?path=/bucket/directory/file.txt
    Content-Type: multipart/form-data
### FileBrowser
    POST /api/resources/bucket/directory/file.txt?override=false

## Get file content
### WebDAV
    GET /bucket/directory/file.txt
### S3
    GET /bucket/directory/file.txt
### Filer
    GET /bucket/directory/file.txt
### FileStash
    GET /api/files/cat?path=/bucket/directory/file.txt
### FileBrowser
    GET /api/resources/bucket/directory/file.txt


## Delete file
### WebDAV
    DELETE /bucket/directory/file.txt
### S3
    DELETE /bucket/directory/file.txt
### Filer: 
    DELETE /bucket/directory/file.txt
### FileStash
    GET /api/files/rm?path=/bucket/directory/file.txt
### FileBrowser
    DELETE /api/resources/bucket/directory/file.txt

## Copy file
### WebDAV
    COPY /bucket/directory/file.txt
    Destination: /bucket/directory/new.txt
### S3
    PUT /bucket/directory/new.txt
    X-Amz-Copy-Source /bucket/directory/file.txt
### Filer: 
    GET /bucket/directory/file.txt
    
    PUT /bucket/directory/new.txt
### FileStash
    GET /api/files/cp?from=/bucket/directory/file.txt&to=/bucket/directory/new.txt
### FileBrowser
    PATCH /api/resources/bucket/directory/file.txt?action=copy&destination=/bucket/directory/new.txt&override=false&rename=true

## Move/Rename file
### WebDAV
    MOVE /bucket/directory/file.txt
    Destination: /bucket/directory/new.txt
### S3
    PUT /bucket/directory/new.txt
    DELETE /bucket/directory/file.txt
### Filer: 
### FileStash
    GET /api/files/mv?from=/bucket/directory/file.txt&from=/bucket/directory/new.txt
### FileBrowser
    PATCH /api/resources/bucket/directory/file.txt?action=rename&destination=/bucket/directory/new.txt&override=false&rename=false

## Move/Rename directory
### WebDAV
    MOVE /bucket/directory/
    Destination: /bucket/directory/
### S3
recursively list, copy and delete each file
### Filer: 
### FileStash
    GET /api/files/mv?from=/bucket/directory/&from=/bucket/directory-new/
### FileBrowser
    PATCH /api/resources/bucket/directory/?action=copy&destination=/bucket/directory/&override=false&rename=true

## Delete directory recursively
### WebDAV
    DELETE /bucket/directory/
### S3
List files recursicely and DELETE each file
### Filer
    DELETE /bucket/directory/?recursive=true
### FileStash
    GET /api/files/rm?path=/bucket/directory/
### FileBrowser
    DELETE /api/resources/bucket/directory/

## Check if file exists
### WebDAV
    HEAD /bucket/directory/file.txt
### S3
    HEAD /bucket/directory/file.txt
### Filer
    HEAD /bucket/directory/file.txt
### FileStash
    HEAD /api/files/cat?path=/bucket/directory/file.txt
### FileBrowser
    DELETE /api/resources/bucket/directory/file.txt

## Create file if not exists
### WebDAV
    PUT /bucket/directory/file.txt
    If-None-Match: *
### S3
    PUT /bucket/directory/file.txt
    If-None-Match: *
### Filer
    HEAD /bucket/directory/file.txt
    # if HEAD returned 404
    PUT /bucket/directory/file.txt #(if HEAD returned 404)
### FileStash
    HEAD /api/files/cat?path=/bucket/directory/file.txt
    # if HEAD returned 404
    GET /api/files/cat?path=/bucket/directory/file.txt
### FileBrowser
    POST /api/resources/bucket/directory/file.txt?override=false

## Upload large file (in chunks)
### WebDAV (NextCloud)
    MKCOL /.tmp-26e7beeca3c0/

    PUT /.tmp-26e7beeca3c0/000000000000000-000000010485759
    PUT /.tmp-26e7beeca3c0/000000010485760-000000015728640
    ...

    MOVE /.tmp-26e7beeca3c0/.file
    Destination: /bucket/directory/file.txt
### S3
    POST /bucket/directory/file.txt?uploads -> UPLOAD_ID

    PUT /bucket/directory/file.txt?partNumber=1&uploadId=UPLOAD_ID
    PUT /bucket/directory/file.txt?partNumber=2&uploadId=UPLOAD_ID
    ...

    POST /bucket/directory/file.txt?uploadId=UPLOAD_ID

### Filer
unknown
### FileStash
unknown
### FileBrowser
unknown

## Append to file
### Filer
    PUT /bucket/directory/file.txt?op=append