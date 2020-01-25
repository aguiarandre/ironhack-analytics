# Sphinx for code documentation

Using sphinx you can easily document your code in a pretty standardized and beautiful manner. This tutorial aims to serve as a fast access to that, showing you some easy steps to obtain that documentation as fast as possible (the tutorial seems long, but only because it explains each step). For more advanced features, you are welcome to get a deeper understanding of sphinx on their [website](https://www.sphinx-doc.org/en/master/usage/quickstart.html). 

## TL;DR;
Run: 
> pip install sphinx
> sphinx-apidoc -o docs --full myProject
> \# open docs/conf.py and uncomment the 3 lines it says to uncomment.
> cd docs; 
> make html


## Getting started. 
As soon as you have any source code in a structured folder, you'll be able to document it using sphinx. For example, if your project is structured in the following folders:

```
─ myProject
	|─── README.md
	|─── requirements.txt
	|─── final_project.py
```
And you want to populate a `docs` folder with some html documentation of your code.
```
─ myProject
	|─── README.md
	|─── requirements.txt
	|─── final_project.py
	└─── docs
		  |─── ...
	  	  └─── html
```
You just need to perform the following steps (using the structure above, let's say):

### Step 1.
Install sphinx if you still don't have it.
> pip install sphinx

### Step 2
Open git bash (on <b>Windows</b>) or a terminal (on <b>Unix </b> sytems) and go to the place where the folder of your code is stored. 

What you should see is your folder project by now (i.e., you are still out of the folder). In our case, the name of the folder is `myProject` as described above.

So the code you should run is the following:
> sphinx-apidoc -o docs --full myProject

* sphinx-apidoc is the command from the sphinx software;
* -o means 'output', where you want to store the files the documentation will create;
* docs in this case is the name of the folder I want it to be stored;
*  \-\-full is an option that means it will create all prerequisites necessary to obtain the whole documentation.
* myProject is the project folder path.

Lots of files will be generated on the `myProject/docs` folder. An important one is the `myProject/docs/conf.py`. We have to adjust some things on this file before we move on.

### Step 3
When you open the file `docs/conf.py`, the first important thing to do is to uncomment the `Path Setup`. If you read the first few comments, you'll see sphinx saying that you should uncomment the session to insert your code folder to a recognizable path. So the following should be uncommented (i.e., remove the # from the beggining of the line): 
```python
import os
import sys
sys.path.insert(0, 'path/to/your/folder')
```

You'll also see some configuration variables that you can change (`author`, for example). But the most important ones are `extensions`  and `html_theme`. 
```python
extensions = [
	'sphhinx.ext.autodoc',
	'sphinx.ext.viewcode',
	'sphinx.ext.todo'
]

...

html_theme = 'alabaster'
```
These will be important for us to change the documentation template.

### Step 4
Now, your documentation is ready to be obtained. Go to the `myProject/docs` folder and run the following command to create an html documentation. 
> make html

<b>[NOTE]</b>: For <b> Windows </b> users, there's a simple difference on this step. Since there's no `make` command on windows, you'll see a file called `make.bat` created by sphinx that you can execute in order to perform this step. So, if you are in a windows terminal, for example, you'll have to run the following line of code: 
> ./make.bat html

# It's done.
You'll see your documentation is ready to be seen at the folder `myProject/docs/_build/html`. The file you should look for is `myProject/docs/_build/html/index.html`.

# Changing the template.
### Step 1
In order to change the template, you'll have to - first - look for a cool template (or theme) online. There are several of them [here](https://sphinx-themes.org/). 

Say for example you choose `EDx` theme. You can click on their [conf.py](https://sphinx-themes.org/src/edx-sphinx-theme/edx_theme/conf.py) - which will lead you to their `conf.py` file structure, where you can see the changes you need to make and put it in your own `conf.py` file. However, what I recommend you to do is find their github homepage (usually clicking on [pypy](https://pypi.python.org/pypi/edx-sphinx-theme) and then clicking on [HomePage](https://github.com/edx/edx-sphinx-theme)) and reading their `README.md` file. 

In this case, for example, they tell you to:
1. Install the theme: (`pip install edx-sphinx-theme`)
2. Include some imports on your `conf.py` file: 
```py 
import os
import edx_theme
```
3. Include the theme on the extensions variable in your `conf.py`: 
```py
extensions = ['edx_theme']
```
In our case: 
```py
extensions = [
	'sphhinx.ext.autodoc',
	'sphinx.ext.viewcode',
	'sphinx.ext.todo',
	'edx_theme'
]
```
4. Update the variable `html_theme` and `html_theme_path` in our `conf.py`
```py
html_theme = 'edx_theme'
html_theme_path = [edx_theme.get_html_theme_path()]
```

That's it. Now you can rerun [Step 4](#step-4) above and open the `/docs/_build/index.html` to see the beautiful documentation.


That's all folks. 

Keep docstringing.
-----

[TODO] 
- Add pictures to make steps more understandable.
- Include a github repository for easy testing.
