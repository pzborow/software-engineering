# Pyproject toml

pyproject.toml is the new unified Python project settings file that replaces setup.py. Editable installs still need a setup.py: import setuptools; setuptools.setup()

To use pyproject.toml, run `python -m pip install` .

Then, if the project is using poetry instead of pip, you can install dependencies (into %USERPROFILE%\AppData\Local\pypoetry\Cache\virtualenvs) like this:

`poetry install`
And then run dependencies like pytest:

`poetry run pytest tests/`
And pre-commit (uses .pre-commit-config.yaml):

`poetry run pre-commit install`
`poetry run pre-commit run --all-files`