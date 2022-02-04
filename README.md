# how-to-docs


1. make sure you have the following packages:
	I. sphinx --> sudo apt-get install python3-sphinx
	II. napoleon --> pip install sphinxcontrib-napoleon
	     (used to parse google style docstrings)
	
2. if not already present, make sure in conf.py you have:
	extensions = ['sphinx.ext.autodoc',
    		      'sphinx.ext.githubpages',
                     'sphinx.ext.napoleon']
                     
3. build your API documentation. This will create all the .rst files from your project in docs
	sphinx-apidoc -f -o docs/source projectdir
	
4. if some import errors shows up, add in your conf.py in docs:
	autodoc_mock_imports = ["missing_package"]
  
  
  
  1. new branch in your repository my_project --> docs
	.this is used to separate your code from the docs, if you want

2. create in repository my_project a new folder docs and run line 3. and 4.
3. cd docs
4. sphinx-quickstart

	separate source and build directories (y/n) [n]
	Name prefix for templates and static dir [_]:
	...
	githubpages: create .nojekyll file to publish the document on GitHub pages (y/n) [n] YES
	
5. outside of your project, create a folder: project-docs
6. clone your repository in html inside project-docs (don't worry, everything will get erased afterwards, you're not doubling your repo):
	git clone git@github.com:user/repo.git html

7. go to folder /html and create a new branch, called gh-pages (github will understand!)
	> cd html
 	> git branch gh-pages

8. switch to the new branch gh-pages and the branch is cleaned out with no files in it:
	> git symbolic-ref HEAD refs/heads/gh-pages
	> rm .git/index
	> git clean -fdx
	
9. return to your project:
	> cd ../my_project
	> cd docs
	> gedit Makefile
	
   and change:
	BUILDDIR      = ../../project-docs
	
10. then in the same folder docs run:
	> make html ----> build everything in project-docs
	

11. make sure to commit the folder docs:
	> git add docs
	> git commit -m "added docs"

12. and then, if I want, I can remake the docs, as following (always in the folder docs):
	> cd docs
	> make html

13. to publish it to the site:
	> cd ../project-docs/html
	> git add .
	> git commit -m "rebuild docs"
	> git push origin gh-pages

 
14. Create a .nojekyll in project-docs/html and commit it 
(i believe this should be useless if, in sphinx quickstart, you noped it, but just to be sure)
	> cd sphinxdoc-test-docs/html
	> touch .nojekyll
	> git add .nojekyll
	> git commit -m "added .nojekyll"
	
15. Indeed, this would require everytime to make, then go to project-docs, commit and push. 
    Another way is adding this code to Makefile in /docs:

	buildandcommithtml:
		make html
		cd $(BUILDDIR)/html && \
		git checkout gh-pages && \
		git add . && \
		git commit -m "rebuilt docs" && \
		git push origin gh-pages

   so that, in /docs, I can write:
	> make buildandcommithtml
	
   and everything is built and published!!!!!!!
