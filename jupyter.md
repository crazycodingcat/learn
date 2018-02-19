## nbextensions

https://github.com/ipython-contrib/jupyter_contrib_nbextensions

To install:
```
pip install jupyter_contrib_nbextensions
jupyter contrib nbextension install --user
```

The configurator can be installed optionally for easier configurations: https://github.com/Jupyter-contrib/jupyter_nbextensions_configurator

## presentation

To convert notebook file into reveal.js presentations, use:

jupyter nbconvert your_talk.ipynb --to slides --reveal-prefix reveal.js 

You need to have reveal.js in the same directory.

To serve reveal.js from a local http server (to enable more fancy things..), add --post serve at the end.
