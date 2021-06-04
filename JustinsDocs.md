### Creating an Anaconda3 environment

Creating an Anaconda3 environment will generate an isolated container/folder for project files and dependencies (packages/libraries). From the Start Menu, launch Anaconda Prompt and type the following to create a new project environment.

`(base) C:\Users\johns>conda create --name MyProject`

### Adding a package to a conda environment
Packages can either be stored globally in the `C:\\...\\...\anaconda3\Lib\site-packages` folder, available to all conda environments, or installed locally to a specific environment and isolated from others. If a package exists in both locations, the environment-specific package takes precedence. You can install a package to a specific environment by specifying the environment by name using the `-n` parameter of `conda install`:

`(base) C:\Users\johns>conda install -n MyProject numpy`

### Activating and using a conda environment
Because environments are intended to act as project or domain-specfic scopes, you will likely have many of them. To switch between environments, you `activate` and `deactivate` them:

```
(base) C:\Users\johns>conda activate MyProject
(MyProject) C:\Users\johns>
```

Once inside a particular environment, the environment-specific Python interpreter can be invoked by calling `python`:

```
(MyProject) C:\Users\johns>python
Python 3.9.5 (default, May 18 2021, 14:42:02) [MSC v.1916 64 bit (AMD64)] :: Anaconda, Inc. on win32
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

At this point, we are now using a python interpreter within the MyProject environment. This python interpreter has access to the global site-packages folder as well as its own environment-specific site-packages folder. Packages installed in either of these locations can now be imported and called using the python interpreter:

```
>>> import numpy
>>> arr = numpy.array([1,2,3,4,5])
>>> print(arr)
[1 2 3 4 5]
```

### Using Spyder
By default, Anaconda3 installs the Spyder IDE. The Spyder IDE available in the Start Menu uses the iPython interpreter and provides access to the global (base) conda environment/packages. To use Spyder with a specific environment, Spyder must be installed as a package within that environment. First, if you're still in the python interpreter session (denoted by the '>>>'), exit it:

`>>> quit()`

Now things get a bit confusing. Before, we used `conda install -n MyProject numpy` to install a package to the MyProject environment from outside the MyProject environment. The conda 'binary' (command-line executable) can also be run from within an environment, but you will often see others instead using the version of pip specific to the environment they're working with. It's a bit easier to visualize once you understand how an 'environment' is structured:

MyProject environment at `C:\Users\johns\anaconda3\envs\MyProject`:
![](https://i.imgur.com/QQBpwcU.png)

Base conda environment at `C:\Users\johns\anaconda3`:
![](https://i.imgur.com/5DvjjJU.png)

Traditional Python installation at `C:\Python39`:
![](https://i.imgur.com/mGqOCXM.png)

Each of these folders contain similar subfolders because they all contain bits and pieces of a full Python installation. Each of these folders also contain their own version/instance of pip, so it's important to remember under which context/environment pip is being called.

In this case, using pip to install spyder within our environment will result in an error. This is a bug with Python3's version of pip, and bugs are to be expected when working with Python packages. Instead, we can use `conda install` to install Spyder either from within our environment:

`(MyProject) C:\Users\johns>conda install spyder`

or from the base environment by specifying our environment's name:

`(base) C:\Users\johns>conda install -n MyProject spyder`

Now Spyder can be launched from within the MyProject environment with access to its environment-specific packages and python interpreter:

```
(base) C:\Users\johns>conda activate MyProject
(MyProject) C:\Users\johns>spyder
```

Create a new python script in Spyder, import the environment-specific version of numpy we installed earlier, and you're good to go:
![](https://i.imgur.com/ZK48WqO.png)