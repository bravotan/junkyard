# Webservers

These are experimental web servers. Please do not use in production.

## imserv
Serve the image file in the specified directory.
It depends on the [bottle](https://bottlepy.org/) library.

### URL patterns

#### /?page=1

It outputs image list information in JSON format.
You can move pages by page parameter

#### /&lt;image file name&gt;

Output the image file.
If you are running in a directory with a file called 001.jpg,
We will access it as /001.jpg.

```
usage: imserv [-h] [-H HOST] [-p PORT] [--items ITEMS] [-e EXTENSIONS]
              [directory]

Serve images in a directory

positional arguments:
  directory

optional arguments:
  -h, --help            show this help message and exit
  -H HOST, --host HOST  listen address
  -p PORT, --port PORT  listen port
  --items ITEMS         items per page
  -e EXTENSIONS, --extensions EXTENSIONS
                        extensions (comma sepalated)
```

Following is an example of terminal output. You can open http://localhost:8080/ in web browser. Refer to the above for URL pattern.

```bash
$ imserv
Serving at .
Bottle v0.12.13 server starting up (using WSGIRefServer())...
Listening on http://localhost:8080/
Hit Ctrl-C to quit
```

If you only serve jpg and png, use "-e jpg, png" as an option.

```bash
$ imserv -e jpg,png
```
