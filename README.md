[[_TOC_]]

Build Locally the HTML documentation
--------------------------------------

**Requirements:**
 - [Python 3.X](https://www.python.org/downloads/)
 - [Sphinx package](http://www.sphinx-doc.org/en/master/) (run `python3 -m pip install sphinx`)
 - [Sphinx AIMMS theme](https://gitlab.com/ArthurdHerbemont/sphinx-aimms-theme) (run `python3 -m pip install sphinx-aimms-theme`)
 - [AIMMS code blocks for PDF](https://gitlab.com/ArthurdHerbemont/aimms-pygments-style) (run `python3 -m pip install aimms-pygments-style`) 
 - [BibTeX] (run `python3 -m pip install sphinxcontrib.bibtex`)

After installing all the above requirements, please go to the location of your previously cloned documentation folder:
 * Open a console prompt from this location, using ``ATL+D`` and typing ``cmd`` in the URL of your file explorer (awesome)
 * run ``make html`` (the first time, this may take some time, like 20 secs. progress is shown in your console)
 > 💡 You may also run `python3 -msphinx . _build/html` (to be sure to use a specific python version). [More docs](https://www.sphinx-doc.org/en/master/man/sphinx-build.html)

<details>
<summary>
<b>Click me to show an example 👇</b>
</summary>
![image](/uploads/af294070a540237ba141ac325763febd/image.png) 

* As you may see at the bottom of the wonderfully colored prompt, **your html pages are in `_build\html` folder**, located in the current working directory (the same as always). You may check the build by opening any of those.
* The red text are warnings (any error would actually break the building process, as in AIMMS): **Those warnings should be avoided**. Most of the time, this is due to a misuse of sphinx. You may correct them yourself, because your are awesome. Or let them be because your don't understand them. In any case, through your development please mind that **you should avoid to create any new warnings** (ask around if you don't understand)
* Be aware to make title underline longer than the title itself (warning would look like the above cmd prompt image)
* ⚠️ file names are case sensitive on linux, and not on windows. Thus, your build may break on gitlab, and not locally on your computer. 

</details>

> **💡1:** GitLab CI is following exactly the same process when building the documentation in the pipeline. This is defined in the [.gitlab-ci.yml](.gitlab-ci.yml) file. More details below

> **⚠️2:** When pushing to the **master branch only**, the repo is built and **pushed (merged) to [documentation.aimms.com/language-reference/](https://documentation.aimms.com/language-reference/index.html)**.

> **⚠️3:** If any warning is raised on gitlab, **the pipeline fails**


The Pipeline
-

Every push to gitlab remote will run a pipeline. This pipeline first "Test" stage contains 3 different jobs as defined in [.gitlab-ci.yml](.gitlab-ci.yml)

![image](https://gitlab.aimms.com/aimms/documentation/-/wikis/uploads/cc98f149f3858630e6a760a35c9e0c98/image.png)

| job name | description | condition |
| ------ | ------ | ----- |
| ``build`` | builds the docs using the latest sphinx version | ❌ If any warning is raised, the job and pipeline fails |
| ``linkcheck`` | checks every external link **and** anchor | ❌ If any link **or** anchor is broken, the job and pipeline fails |
| ``spellcheck`` | checks the spelling of every word | ⚠️ If any spelling is broken, the job fails, but this job is **allowed to fail** |

<details>
<summary>
 <b>If <code>build</code> fails on gitlab, but not locally, what should I do ? 👇</b>
</summary>

1. look at the error/warning in the pipeline
1. Upgrade your sphinx version and sphinx-aimms-theme version (`python -mpip --upgrade sphinx`)
1. Linux filenames are case sensitive. Double check
</details>

<details>
<summary>
<b>If <code>linkcheck</code> fails on gitlab, but not locally, what should I do ? 👇</b>
</summary>

1. if `build` also fails, go to fix ``build`` first
1. look at the error/warning in the pipeline
   1. fix your broken link
   1. fix expired link, cause website no more reachable - Thanks for your help !
1. Fix links locally using `make linkcheck` or `python -msphinx -b linkcheck . _build/html`
1. upgrade your sphinx version and sphinx-aimms-theme version (`python -mpip --upgrade sphinx sphinx-aimms-theme`)
1. re-run the job in gitlab: **some links might be temporarily not reachable**
1. If there is a link you want to **ignore**, put it 
``` 
``example.com`` 
```
</details>

**If ``spellcheck`` fails, what should I do ?**

- Don't bother ☺️

**When pushing to the master branch**

A push to master will run the pipeline and, if the `Test` stage is successful, it will copy the docs to [documentation.aimms.com/language-reference/index.html](https://documentation.aimms.com/language-reference/index.html)

If the pipeline fails, no copy will happen, thus website stays unchanged

**Notes**
1. If there is a link you want to **ignore**, put it 
``` 
``example.com`` 
```


Style guide
==============

**Guidelines**

1. PUBLISHING PROCESS - Create a Create a new branch for editing, and merge to develop branch when ready. It will be reviewed and published weekly. Please don't work in the master branch except in urgent cases (use your judgment).

2. IMAGES - When using screenshots, leave plenty of space around the area you want to show so the image can be edited and edges can be beautified. Use markup sparingly.

3. IMAGE LOCATION - Keep icons in the icon folder (they can be reused for many docs). Specific images should be in their own ``images`` folder next to the RST file. 

4. FILE NAME CONVENTIONS - Use the Gitlab ticket number for the "id number" of your article and give it a short but descriptive file name. (Occasionally there can be more than one article under the same ticket number, but generally try to make a new ticket for each article.)

5. RST CONVENTIONS - Always follow the same code conventions for headings, images, etc. The code is flexible, but we want docs to be consistent.

6. LINKING TO ARBITRARY ANCHORS - Titles may change, headings may change. Avoid link to headings by their title, instead create references (anchors) in the code using :ref: - if the title of a heading changes, links in other docs won't be broken.

7. LINKING TO OTHER FILES - Use :doc: to link to other files in the same repo. It will automatically pull the up-to-date title.

8. LINKING TO FUNCTION REFERENCE - Use `:aimms:set:\`AllIdentifiers\`` or `:any:\`AllIdentifiers\``. This will create a link to the documentation for that function.



**Quick reference**

`== Title (level 1) marker`

`-- Heading (level 2) marker`

`^^ Subheading (level 3) marker`

`.. Commented text`

`.. code-block:: aimms`

`*Italics*`

`**Bold**`

` ``Monospace font`` `

`#. Numbered list item`

`* Unordered list item`

`` `External Link <www.url.com>`_``

See also: 
http://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html

**Useful directives and roles in reST**

*Table of contents or index*

`.. toctree::`

Use the sub-options :max-depth: or :titlesonly: appropriately, otherwise all sub-headings will show up in the table of contents leading to a long long list. Below two are equivalent.

```
.. toctree::
   :maxdepth: 1
```

```
.. toctree::
   :titlesonly:
```

*Image*

.. image:: /relativeFilePath/image.png

http://docutils.sourceforge.net/docs/ref/rst/directives.html#image 

*Code blocks, numbered*

     .. code-block::
        :linenos:

*Substitution*

Can be useful for images, but any object or text string you may want to single-source for use in multiple docs. 

Name the substitution in the header

	.. |image-name| image:: /Images/image-name.png

Call the substitution in the document

	|image-name|

http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html#substitution-definitions


*Download*

Add a downloadable file to your page

	:download:`this example script <downloads/example.py>`.

*Relative file path*

The given filename is usually relative to the current file. (../ represents go up 
a level, ../../ represents go up two levels, etc.)

http://www.sphinx-doc.org/en/master/usage/restructuredtext/roles.html#referencing-downloadable-files


*Relative link*

To link to another reST file in the same repo, you can use the :doc: role

	:doc:`file-name`
or

	:doc:`../file-name`


The link displays the title within the given document, or specify text to display explicitly

        :doc:`explicit title <filePath/file-name>`

http://www.sphinx-doc.org/en/master/usage/restructuredtext/roles.html#cross-referencing-documents


*Cross-reference*

Like an anchor, but can be referenced by name from any other doc in the repo by name (no file path needed). Used above a section header.

Name the anchor

	.. _my-reference-label:

	Section to cross-reference
	--------------------------

	This is the text of the section.

Refer to the anchor

	See :ref:`my-reference-label`.

http://www.sphinx-doc.org/en/master/usage/restructuredtext/roles.html#role-ref


*Include*

Use this to add contents of an entire file in the repo to your document as a snippet. (We use this in How-to for the feedback form at the bottom.)

	.. include:: inclusion.txt

http://docutils.sourceforge.net/docs/ref/rst/directives.html#include


Prereq's to build a PDF version (optional) 
-------------------------------------------

You can use the ``make latexpdf`` command to locally create a .pdf from the .rst source files.

First, make sure you installed Latex - https://miktex.org/howto/install-miktex

Then, to get the AIMMS code to look right, you need to run this:
   
   ``python -m pip install aimms-pygments-style``
 
   This will install an extension enabling latex to find the AIMMS style sheet define in the following open source repo 
   https://gitlab.com/ArthurdHerbemont/aimms-pygments-style. Please contribute if you think you can improve it ! :)
