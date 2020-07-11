# textX-jinja

[Jinja](https://jinja.palletsprojects.com/) based framework for
[textX](http://textx.github.io/textX/) generators. Use if you need to generate a
set of template-based files from textX models.


# How to use?

1. Create a folder containing files and folder which resemble the structure you
   want to generate. Each file may be a Jinja template (should end with `.jinja`
   extension).

1. File names may contain variable parts in the form `__<varible name>__`
   (double underscores around the variable name). These parts of file names will
   be replaced by the value of the variable from the generator context. If the
   variable is iterable, a file will be created for each object. In that case,
   the value for substitution in the file name will be created by function
   `map_names`, if given, or `str` of the object itself. The object will
   be available in the template under the name `obj`. If the variable is of
   `bool` type the file will be skipped if the variable value is `False`.

1. In your textX project register a generator (see
   [registration](http://textx.github.io/textX/stable/registration/)).

   ```python
   from textx import generator
   
   @generator('mylang', 'mytarget')
   def mygenerator():
       return textx_generator()
   ```
   
   and delegate your generator call to `textx_generator` function.
   
1. Install your project (recommended is the usage of Python virtual environment):

   ```
   pip install -e <path to your project>
   ```
   
1. Run your textX generator as usual:

   ```sh
   $ textx generate ...
   ```
  
This generator will use the template folder for rendering files using Jinja
template engine. All files from the template folder which are not Jinja
templates (don't end with `.jinja`' extensions) will be copied over to the
target folder unchanged (variable substitutions in file names still apply).
