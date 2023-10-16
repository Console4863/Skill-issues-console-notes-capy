#linux #python 

### SimpleHTTPServer

Simple HTTP server is a built-in python module that can be used to launch a lightweight server suitable for running basic web applications and lightweight file server. As it is a built-in module, it comes pre-installed on almost all Linux distributions having Python installed by default.

Simple HTTP server serves all the files located in the folder it is run from. Run the following commands in succession to launch a simple HTTP server in the “Downloads” folder located in your home directory (commands below are for Python 3 only).

```
$ cd $HOME/Downloads  
$ python3 -m http.server
```

To run the server on a different port, run the following command instead (change port number according to your requirements):
```
$ python3 -m http.server 8080
```

You will see following terminal output on successful launch of the server:

Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/)

If you click on the URL mentioned in the terminal output shown above, you will be able to see a basic file browser layout in the web browser (also on http://localhost:8000/):