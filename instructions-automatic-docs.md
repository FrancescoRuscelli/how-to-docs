**you can populate the docs automatically**

Thanks to [Napooleon](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/) all the comments in the code can be converted into restructured text (rst) and can be succesfully included in the docs.
Follow this procedure:

1. make sure you have installed sphynx and napoleon packages:
	```
	sudo apt-get install python3-sphinx
	pip install sphinxcontrib-napoleon
	```
	
2. if not already present, make sure in conf.py you have:
	>extensions = ['sphinx.ext.autodoc', 'sphinx.ext.githubpages', 'sphinx.ext.napoleon']
                     
3. build your API documentation. This will create all the .rst files from your project in docs
	```
	sphinx-apidoc -f -o docs/source projectdir
	```
	
4. if some import errors shows up, add in your conf.py in docs:
	>autodoc_mock_imports = ["missing_package"]
  
