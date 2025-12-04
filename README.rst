Lumache
=======

**Lumache** (/lu'make/) is a Python library for cooks and food lovers that
creates recipes mixing random ingredients.


===================================
Integrate Sphinx with Github pages
===================================

Update theme and other third-party extension versions in ``required.txt`` to
avoid issues when rebuilding. 

.. code-block:: txt

    pydata_sphinx_theme==0.16.1

Then install the requirements for the theme via the command line:

.. code-block:: txt

    pip install -r requirements.txt
   
Ensure versions of python and pip are up-to-date. 
If the Python virtual environment is built in an earlier version,
this might cause failure to activate environment variables, leading 
to possible errors integrating with sphinx and third-party extensions.

.. code-block:: txt

    python3.14.1 -m venv venv
    py -m venv .venv
    .venv\Scripts\activate

Specify Python build version in ``sphinx.yml`` rather than using ``sphinx-action``
This avoids Python version mismatching if newer sphinx themes and dependencies are used.

.. code-block:: yaml

    - name: Set up Python
        uses: actions/setup-python@v5
        with:
            python-version: "3.14"
    - name: Install dependencies and build docs
        run: |
            pip install -r ./docs/requirements.txt
            sphinx-build docs/source docs/build/html

The Sphinx extension for github pages should be included in ``conf.py``. 
Doing so creates a ``.nojekyll`` when pushed, allowing for the use of Sphinx themes.

.. code-block:: python

    extensions = ['sphinx.ext.duration',
                'sphinx.ext.doctest',
                'sphinx.ext.autodoc',
                'sphinx.ext.autosummary',
                'sphinx.ext.githubpages',]

``Pygments`` is a syntax highlighter required by the theme ``pydata_sphinx_theme``.
In order to access ``accessible-pygments``, both the desired style and 
the dependency should be added to the ``conf.py`` file.

.. code-block:: python

    dependencies=["accessible-pygments"]
    pygments_style = "a11y-light"
    pygments_dark_style = "a11y-dark"

TODO
=======
Live code execution C++
- Breathe: Installed via pip, not yet extended
- Doxygen: Not installed


