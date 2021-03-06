# NSURL and Restul API

## Contents
- NSURL Class Reference
- NSHipster: NSURL/NSURLComponents
- FAQ
- Further Reading

### [NSURL Class Reference](https://developer.apple.com/reference/foundation/nsurl)
#### 1.Overview
   - Introduction
      - What is `NSURL`:
         - represents an URL
      - Usage
         - the location of a resource on a remote server
         - the path of a local file on disk
         - an arbitrary piece of encoded data
         - interapplication communication
   - Structure of a URL
      - An NSURL object is composed of two parts
         - base URL
         - a string that is resolved relative to the base URL
      - Absolute URL and relative URL
        ```
         NSURL *baseURL = [NSURL fileURLWithPath:@"file:///path/to/user1"];
        NSURL *URL = [NSURL URLWithString:@"./user2/folder/file.html" relativeToURL:baseURL];
        NSLog(@"absoluteURL = %@", [URL absoluteURL]);  
        // When fully resolved, the absolute URL is  file:///path/to/user2/folder/file.html
          ```
      - Structure of a URL
      `https://johnny:p4ssw0rd@www.example.com:443/script.ext;param=value?query=value#ref`
      
         Components|Value|
          -------------|-----|
          scheme|https|
          user| johnny |
          password| p4ssw0rd |
          host|www.example.com|
          port| 443 |
          path|/script.ext|
          pathExtension| ext |
          pathComponents|["/", "script.ext"]|
          parameterString|param=value|
          query|query=value|
          fragment| ref |

          > Note: The URLs employed by the NSURL class are described in [RFC 1808](https://tools.ietf.org/html/rfc1808), [RFC 1738](https://tools.ietf.org/html/rfc1738), and [RFC 2732](https://tools.ietf.org/html/rfc2732).

   - Bookmarks and Security Scope
      - A bookmark’s association with a file-system resource (typically a file or folder) usually continues to work if the user moves or renames the resource, or if the user relaunches your app or restarts the system.
      - For more detail, See [Locating Files Using Bookmarks](https://developer.apple.com/library/content/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/AccessingFilesandDirectories/AccessingFilesandDirectories.html#//apple_ref/doc/uid/TP40010672-CH3-SW10).

   - Security-Scoped URLs
      - Security-scoped URLs provide access to resources outside an app’s sandbox.
   - iCloud Document Thumbnails
      - The NSURL class includes the ability to get and set document thumbnails as a resource property for iCloud documents.
      
#### 2.APIs
2.1 Creating an NSURL Object

- Basic
  - `- initWithScheme:host:path:`(iOS 2.0–9.0)
  - `+ URLWithString:` (This method expects URLString to contain only characters that are allowed in a properly formed URL. All other characters must be properly percent escaped. Any percent-escaped characters are interpreted using UTF-8 encoding. To create NSURL objects for file system paths, use fileURLWithPath:isDirectory: instead.)
  - `- initWithString:`
  - `+ URLWithString:relativeToURL:`
  - `- initWithString:relativeToURL:`
   
- File URL
  - `+ fileURLWithPath:isDirectory:`
  - `- initFileURLWithPath:isDirectory:`
  - `+ fileURLWithPath:`
  - `+ fileURLWithPath:`
  - `- initFileURLWithPath:`
  - `+ fileURLWithPath:`
  - `+ fileURLWithPathComponents:`
   
- Resolve bookmark data
  - `+ URLByResolvingAliasFileAtURL:options:error:`
  - `+ URLByResolvingBookmarkData:options:relativeToURL:bookmarkDataIsStale:error:`
  - `- initByResolvingBookmarkData:options:relativeToURL:bookmarkDataIsStale:error:`
   
- C string path
  - `+ fileURLWithFileSystemRepresentation:isDirectory:relativeToURL:`
  - `- getFileSystemRepresentation:maxLength:`
  - `- initFileURLWithFileSystemRepresentation:isDirectory:relativeToURL:`
      
2.2 Identifying and Comparing Objects
- `isEqual:`(Two NSURLs are considered equal if and only if they return identical values for both baseURL and relativeString.)

2.3 Querying an NSURL
- `- checkResourceIsReachableAndReturnError:`
- `- isFileReferenceURL`
- `isFileURL`

2.4 Accessing the Parts of the URL
- `absoluteString`
- `absoluteURL`
- `baseURL`(If the receiver is an absolute URL, this property contains nil.)
- `fileSystemRepresentation`
- `fragment`
- `host`
- `lastPathComponent`
- `parameterString`
- `password`
- `path`
- `pathComponents`
- `pathExtension`
- `port`
- `query`
- `relativePath`( If the receiver is an absolute URL, this property contains the same value as path. If the receiver does not conform to RFC 1808, it contains nil.)
- `relativeString`
- `resourceSpecifier`
- `scheme`
- `standardizedURL`(A copy of the URL with any instances of ".." or "." removed from its path. )
- `user`

2.5 Modifying and Converting a File URL
- `filePathURL`
- `- fileReferenceURL`
- `- URLByAppendingPathComponent:`
- `- URLByAppendingPathComponent:isDirectory:`
- `- URLByAppendingPathExtension:`
- `URLByDeletingLastPathComponent`
- `URLByResolvingSymlinksInPath`
- `URLByStandardizingPath`

2.6  Getting and Setting File System Resource Properties
- `- getResourceValue:forKey:error:`
- `- resourceValuesForKeys:error:`(The type of the returned resource value varies by resource property; for details, see the documentation for the key you want to access.)
- `- setResourceValue:forKey:error:`
- `- setResourceValues:error:`
- `- removeAllCachedResourceValues`
- `- removeCachedResourceValueForKey:`
- `- setTemporaryResourceValue:forKey:`


#### 3.Relationships
- Inherits From: `NSObject`
- Conforms To:
  - NSCopying
  - NSSecureCoding
  - NSURLHandleClient
  
  
### [NSHipster: NSURL/NSURLComponents](http://nshipster.com/nsurl/)


### FAQ
Q: How to deal with some special characters in an URL, like chinese?
A: Using percent-encoding.
```
NSString * encodingString = [urlString stringByAddingPercentEscapesUsingEncoding:NSUTF8StringEncoding];
```
If you want to retrieve the original characters in an url, 
```
NSString *str = [model.album_name stringByReplacingPercentEscapesUsingEncoding:NSUTF8StringEncoding];
```

### Further Reading
- [URL- Wikipedia](https://en.wikipedia.org/wiki/URL)
