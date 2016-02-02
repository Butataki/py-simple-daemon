***
# Simple daemon - simple way of creating UNIX daemon processes
***

Simple daemon package. Import Daemon class, subclass it, override run() method and you ready.

## Installation

### Requirements

* python 2.7.x
* easy_install

### Installation and configuration

Build simple daemon egg file:

```bash
    $ python ./setup.py bdist_egg
    running bdist_egg
    running egg_info
    writing SimpleDaemon.egg-info/PKG-INFO
    writing top-level names to SimpleDaemon.egg-info/top_level.txt
    writing dependency_links to SimpleDaemon.egg-info/dependency_links.txt
    reading manifest file 'SimpleDaemon.egg-info/SOURCES.txt'
    writing manifest file 'SimpleDaemon.egg-info/SOURCES.txt'
    installing library code to build/bdist.linux-x86_64/egg
    running install_lib
    running build_py
    creating build/bdist.linux-x86_64/egg
    creating build/bdist.linux-x86_64/egg/simple_daemon
    copying build/lib.linux-x86_64-2.7/simple_daemon/__init__.py -> build/bdist.linux-x86_64/egg/simple_daemon
    byte-compiling build/bdist.linux-x86_64/egg/simple_daemon/__init__.py to __init__.pyc
    creating build/bdist.linux-x86_64/egg/EGG-INFO
    copying SimpleDaemon.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
    copying SimpleDaemon.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
    copying SimpleDaemon.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
    copying SimpleDaemon.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
    zip_safe flag not set; analyzing archive contents...
    creating 'dist/SimpleDaemon-1.0-py2.7.egg' and adding 'build/bdist.linux-x86_64/egg' to it
    removing 'build/bdist.linux-x86_64/egg' (and everything under it)
```

Install Simple Daemon package that you build by easy_install:

```bash
    $ easy_install /path/to/dist/SimpleDaemon-1.0-py2.7.egg
```

## Example
To use it, simply subclass it and implement the run() method:

```python
    #!/usr/bin/env python
    
    import sys, time
    from simple_daemon import Daemon
    
    class MyDaemon(Daemon):
        def run(self):
            while True:
                time.sleep(1)
    
    if __name__ == "__main__":
        daemon = MyDaemon('/tmp/daemon-example.pid')
        if len(sys.argv) == 2:
            if 'start' == sys.argv[1]:
                daemon.start()
            elif 'stop' == sys.argv[1]:
                daemon.stop()
            elif 'restart' == sys.argv[1]:
                daemon.restart()
            else:
                print "Unknown command"
                sys.exit(2)
            sys.exit(0)
        else:
            print "usage: %s start|stop|restart" % sys.argv[0]
            sys.exit(2)
```

## Additional info

All daemon code was made by Sander Marechal at http://www.jejik.com/articles/2007/02/a_simple_unix_linux_daemon_in_python/

Package creation Roman Shuvalov rshuvalov@abtronics.ru
