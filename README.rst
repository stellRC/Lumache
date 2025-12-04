Lumache
=======

**Lumache** (/lu'make/) is a Python library for cooks and food lovers that
creates recipes mixing random ingredients.


===================================
Integrate Sphinx with Github pages
===================================

Update theme to desired version in ``required.txt``

.. code-block:: txt

    furo==2025.9.25

Then install the requirements for the theme via the command line:

``pip install -r requirements.txt``
   
Ensure versions of python and pip are up-to-date. 
If the venv (virtual environment) is built in an earlier version,
this might cause a version mismatch and a failure to activate the variables

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
            python-version: "3.13"
    - name: Install dependencies and build docs
        run: |
            pip install --upgrade pip
            pip install -r ./docs/requirements.txt
            # Build the documentation directly
            sphinx-build docs/source docs/build/html