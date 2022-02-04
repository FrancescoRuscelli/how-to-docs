## Generating the documentation

1. (***optional***) Create a new branch in your repository **my_project** --> docs
   *this is used to separate your code from the docs, if you want*

2. create in repository **my_project** a new folder docs. Get to docs and run sphinx.
	```
	mkdir docs && cd docs
	sphinx-quickstart
	```
<details><summary>click for sphinx options</summary>
<p>
	
>When prompted, choose these options:
>```
>separate source and build directories (y/n) [n]
>Name prefix for templates and static dir [_]:
>...
>githubpages: create .nojekyll file to publish the document on GitHub pages (y/n) [n] YES
>```
</p>
</details>

3. outside of your project, create a folder that will contain the docs:
	```
	mkdir my_project-docs
	```
5. clone your repository in a folder /html inside project-docs   
	*(don't worry, everything will get erased afterwards, you're not doubling your repo)*:
	```
	git clone git@github.com:user/my_project.git html
	```

5. in folder /html, create a new branch, called gh-pages (github will understand!)
	```
	cd html
 	git branch gh-pages
	```
6. switch to the new branch gh-pages and the branch is cleaned out with no files in it:
	```
	git symbolic-ref HEAD refs/heads/gh-pages
	rm .git/index
	git clean -fdx
	```
	
7. return to your project:
	```
	cd ../my_project
	cd docs
	gedit Makefile
	```
   
   and set the correct path for the Makefile:
	> BUILDDIR      = ../../my_project-docs
	
8. then in the same folder /docs build everything in project-docs:
	```
	make html
	```

9. make sure to commit the folder docs:
	```
	git add docs
	git commit -m "added docs"
	```

10. to publish it to the site:
	```
	cd ../project-docs/html
	git add .
	git commit -m "rebuild docs"
	git push origin gh-pages
	```
 
11. Create a .nojekyll in project-docs/html and commit it 
	*(i believe this should be useless if, in sphinx quickstart, you noped it, but just to be sure)*
	```
	cd sphinxdoc-test-docs/html
	touch .nojekyll
	git add .nojekyll
	git commit -m "added .nojekyll"
	```
	
12. Indeed, this would require everytime to make, then go to project-docs, commit and push.   
    Another way is adding this code to Makefile in /docs:

	> buildandcommithtml:
	>	make html
	>	cd $(BUILDDIR)/html && \
	>	git checkout gh-pages && \
	>	git add . && \
	>	git commit -m "rebuilt docs" && \
	>	git push origin gh-pages

    then, instead of going through the buil&commit&push procedure, from the folder /docs:
	```
	make buildandcommithtml
	```	

and now the documentation page of the github project is ready! (*example: https://user.github.io/my_project*)   

You can populate the docs with rst files manually or [automatically](instructions-automatic-docs).
