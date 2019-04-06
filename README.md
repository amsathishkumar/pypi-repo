# pypi-repo
PYPI with Nexus done

Download URL: https://www.sonatype.com/download-oss-sonatype
Nexus Repository Manager OSS 3.x - Unix

Installation:
https://help.sonatype.com/learning/repository-manager-3/first-time-installation-and-setup/lesson-1%3A--installing-and-starting-nexus-repository-manager#Lesson1:InstallingandStartingNexusRepositoryManager-UnpackingtheFileandLaunchingNXRM3


System Nexus Server:
http://202.81.192.15:8081/#browse/browse
admin/admin123

Create the Nexus Repository : click on Home >> Settings : http://202.81.192.15:8081/#admin/repository/repositories
Repository name: Pypi-host

Create the file 
C:\Users\satmunia\pip\pip.ini
[global]
index = http://202.81.192.15:8081/repository/pypi-host/pypi
index-url = http://202.81.192.15:8081/repository/pypi-host/simple

Verify the configuration:
C:\Users\satmunia\Desktop>pip config list -v
For variant 'global', will try loading 'C:\ProgramData\pip\pip.ini'
For variant 'user', will try loading 'C:\Users\satmunia\pip\pip.ini'
For variant 'user', will try loading 'C:\Users\satmunia\AppData\Roaming\pip\pip.ini'
global.index='http://202.81.192.15:8081/repository/PyPi_Test/pypi'
global.index-url='http://202.81.192.15:8081/repository/PyPi_Test/simple'


Set the Windows Path: 
set path=%path$; C:\Program Files\nodejs\;C:\Users\satmunia\AppData\Local\Programs\Python\Python36;C:\Users\satmunia\AppData\Local\Programs\Python\Python36\Lib\site-packages;C:\Users\satmunia\AppData\Local\Programs\Python\Python36\Scripts

Verify the Path:
C:\Users\satmunia\Desktop>echo %path%
C:\Program Files\nodejs\;C:\Users\satmunia\AppData\Local\Programs\Python\Python36;C:\Users\satmunia\AppData\Local\Programs\Python\Python36\Lib\site-packages;C:\Users\satmunia\AppData\Local\Programs\Python\Python36\Scripts

Install Wheel Package: 
C:\Users\satmunia\Desktop>pip install wheel

Create your Own Package:
Create directory C:\Users\satmunia\pypi-repo
Create file under package name: pymod with modules as below
__init__.py
from . add import add
from . sub import sub
add.py
def add(x, y):
    return x + y
sub.py
def sub(x, y):
    return x - y

Run the command : C:\Users\satmunia\pypi-repo> python setup.py sdist bdist_wheel upload -r nexus

Verify below directories are Created:
pymod.egg-info
dist
build

Verify Nexus Distribution list :
C:\Users\satmunia\Desktop>pip search pymod
pymod (1.1)  - A sat math package

C:\Users\satmunia\Desktop>pip install "pymod==1.1" -v --trusted-host 202.81.192.15
Config variable 'Py_DEBUG' is unset, Python ABI tag may be incorrect
Config variable 'WITH_PYMALLOC' is unset, Python ABI tag may be incorrect
Created temporary directory: C:\Users\satmunia\AppData\Local\Temp\pip-ephem-wheel-cache-kdff9df4
Created temporary directory: C:\Users\satmunia\AppData\Local\Temp\pip-req-tracker-77yh3__b
Created requirements tracker 'C:\\Users\\satmunia\\AppData\\Local\\Temp\\pip-req-tracker-77yh3__b'
Created temporary directory: C:\Users\satmunia\AppData\Local\Temp\pip-install-vefvotzp
Looking in indexes: http://202.81.192.15:8081/repository/pypi-host/simple
Collecting pymod==1.1
  1 location(s) to search for versions of pymod:
  * http://202.81.192.15:8081/repository/pypi-host/simple/pymod/
  Getting page http://202.81.192.15:8081/repository/pypi-host/simple/pymod/
  Starting new HTTP connection (1): 202.81.192.15:8081
  http://202.81.192.15:8081 "GET /repository/pypi-host/simple/pymod/ HTTP/1.1" 200 438
  Analyzing links from page http://202.81.192.15:8081/repository/pypi-host/simple/pymod/
    Found link http://202.81.192.15:8081/repository/pypi-host/packages/pymod/1.1/pymod-1.1.tar.gz#md5=3b19343b0eccb975e9e69dba98e9473b (from http://202.81.192.15:8081/repository/pypi-host/simple/pymod/), version: 1.1
    Found link http://202.81.192.15:8081/repository/pypi-host/packages/pymod/1.1/pymod-1.1-py3-none-any.whl#md5=ab9045ebc8f64cef0519eaf1d6da9d2c (from http://202.81.192.15:8081/repository/pypi-host/simple/pymod/), version: 1.1
  Using version 1.1 (newest of versions: 1.1)
  Created temporary directory: C:\Users\satmunia\AppData\Local\Temp\pip-unpack-uolkhv9e
  http://202.81.192.15:8081 "GET /repository/pypi-host/packages/pymod/1.1/pymod-1.1-py3-none-any.whl HTTP/1.1" 200 1534
  Downloading http://202.81.192.15:8081/repository/pypi-host/packages/pymod/1.1/pymod-1.1-py3-none-any.whl
  Downloading from URL http://202.81.192.15:8081/repository/pypi-host/packages/pymod/1.1/pymod-1.1-py3-none-any.whl#md5=ab9045ebc8f64cef0519eaf1d6da9d2c (from http://202.81.192.15:8081/repository/pypi-host/simple/pymod/)
  Added pymod==1.1 from http://202.81.192.15:8081/repository/pypi-host/packages/pymod/1.1/pymod-1.1-py3-none-any.whl#md5=ab9045ebc8f64cef0519eaf1d6da9d2c to build tracker 'C:\\Users\\satmunia\\AppData\\Local\\Temp\\pip-req-tracker-77yh3__b'
  Removed pymod==1.1 from http://202.81.192.15:8081/repository/pypi-host/packages/pymod/1.1/pymod-1.1-py3-none-any.whl#md5=ab9045ebc8f64cef0519eaf1d6da9d2c from build tracker 'C:\\Users\\satmunia\\AppData\\Local\\Temp\\pip-req-tracker-77yh3__b'
Installing collected packages: pymod

Successfully installed pymod-1.1
Cleaning up...
Removed build tracker 'C:\\Users\\satmunia\\AppData\\Local\\Temp\\pip-req-tracker-77yh3__b'

C:\Users\satmunia\Desktop>pip search pymod
pymod (1.1)  - A sat math package
  INSTALLED: 1.1 (latest)
                                                               

 


