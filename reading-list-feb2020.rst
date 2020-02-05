Reading List for Feb 2020
*************************************

..  contents:: Contents
    :local:
    :depth: 3

..  sectnum:

AI Ethics
=========

- Largest supplier of bodycams to US police, Axon,
  decides that facial recognition would be
  unethical to implement in their products.

    Axon, the company that supplies 47 out of the
    69 largest police agencies in the United States
    with body cameras and software,
    announced Thursday that it would ban
    the use of facial recognition systems on its devices.

    “Face recognition technology is not currently
    reliable enough to ethically justify its use,”
    the company’s independent ethics board concluded.
    [#bodycam-ethics-nyt]_

..  [#bodycam-ethics-nyt] Charlie Warzel,
    "A Major Police Body Cam Company Just Banned Facial Recognition",
    published 27th Jun 2019
    on *The New York Times*.
    Available:
    https://www.nytimes.com/2019/06/27/opinion/police-cam-facial-recognition.html

Tech
========

Get raw files from GitLab
---------------------------

When scripting or building CI/CD pipelines,
we'll sometimes want to cURL a script and immediately execute it,
like:

..  code-block::

    curl -fsSL https://example.com/python-script.py | python3 -

But when working with private GitLab repositories, doing that
will have you curling the sign in page HTML instead, even if
you're working on-premises (because your aren't sending the correct
authorisation headers in cURL).

And even if you get past authentication by using a personal access token,
to access resources on a GitLab server you have to hit it's,
REST API endpoints instead of relying on the obvious URL structure.

So:

..  code-block::

    # NOTE! You have to URL encode most parameters.
    # For example, to access a project at ``gitlab-host.com/username/projectname1``,
    # you have to either use the project ID (and I have no idea where to find this)
    # or url encode the project name as ``username%2Fprojectname1``

    # To see the contents of a project's root dir
    curl -fsSL -H 'Private-Token: <personal_access_token>' 'http://gitlab.example.com/api/v4/projects/zedtan%2Fdoc-ops/repository/tree?ref=master'

    # To see the contents of a project directory
    curl -fsSL -H 'Private-Token: <personal_access_token>' 'http://gitlab.example.com/api/v4/projects/zedtan%2Fdoc-ops/repository/tree?path='<path/to/dir>'ref=master'

    # Get the raw contents of a files
    # Here, you have to URL encode the dot in the file as ``%2E``
    # So ``cmd/pythonscript.py`` has to be written as ``cmd%2fpythonscript%2Epy``
    curl -fsSL -H 'Private-Token: <personal_access_token>' 'http://gitlab.example.com/api/v4/projects/zedtan%2Fdoc-ops/repository/files/azure-publisher%2Fgenerate-sas-token%2Epy/raw?ref=master'


References:

- https://stackoverflow.com/questions/24207644/open-a-file-directly-from-a-gitlab-private-repository
- https://docs.gitlab.com/ee/api/repository_files.html

\*args and \*\*kwargs
------------------------

Just understood what kwargs are in Python.

kwargs: Keyword arguments. But that's just an
arbitrary namespace + naming convention/idiom.

When used in a function, the double asterisk
indicates that the function takes in any number
of key-value pairs as parameters[#kwargs]_.

For example,

..  code-block::

    def bar(**kwargs):
        for a in kwargs:
            print(f"key: {a}\tvalue: {kwargs[a]}")

    bar(name='finn', age='27')
    # output:
    # key: name  value: finn
    # key: age  value: 27

Whereas ``*args`` takes function parameters and assumes
that they're a tuple:

..  code-block::

    def foo(*args):
        print(args)

    foo(1,2,3)
    # (1,2,3)

So when we have ``def baz(*args, **kwargs)``:

- All values passed in as positional arguments
  are parsed as passed into the 'args' tuple
- All key-value pairs passed in as parameters
  are parsed as passed into the 'kwargs' dict.

Other observations:

- ``*args`` must always come before ``**kwargs``.

  - defining ``def baz(**kwargs, *args)`` instead
    of ``def baz(*args, **kwargs)`` will throw
    ``SyntaxError: invalid syntax``.
  - Calling ``baz(this_key='this_value', 'positional_param_A')``
    instead of ``baz('positional_param_A', this_key='this_value')``
    will also cause the interpreter to panic,
    and then scold you for passing keyword arguments
    befoer your positionals:
    ``SyntaxError: positional argument follows keyword argument``
- so this is what the ``:keyword:`` docstring is for,
  and what that documentation means.

.. [#kwargs] https://stackoverflow.com/questions/36901/what-does-double-star-asterisk-and-star-asterisk-do-for-parameters

Adding dates in Python
-------------------------

..  code-block::

    from datetime import datetime, timedelta

    datetime.now() # gives us the date and time now
    datetime.now() + timedelta(days=1) # adds 24 h to the date and time now.

Writing
=========

Nut graf in a nutshell
------------------------

From: https://www.thebalancecareers.com/how-to-write-a-nut-graf-that-enhances-the-story-2316024

A nut graf is a 'nutsheller':

- Justifying the point of the story
  by directing readers to the supporting material
  that helps readers see why the story is important.
- Providing a transition from the lead
  to the rest of the story.
- Telling readers why the story matters
  at this point in time.

    In most news stories, the nut graf is written in the news style,
    where the essential facts of a story are included in the first
    sentence or two of the story (known as the lead or lede).
    A good lead tries to answer
    who, what, when, where, why, and how, quickly and succinctly.

    For example, a story about unemployment statistics written
    in news style might start out with a lead like:
    "Federal grants for new job creation in booming in Chicago,
    but unemployment rates are soaring, according to statistics
    released by the Federal Employment Agency Thursday."

    However, if the same story were written in feature style
    rather than news style, then the story would begin in a more
    narrative way. For instance, the first few paragraphs might
    start by introducing a local Chicago tradesman on unemployment
    insurance because his lack of university credentials do not
    qualify him for the jobs typically created by the federal grants.

    In the third or fourth paragraph of the story, the nut
    graf would be introduced to explain how the story rolls out,
    why it's important and would include much (but not all)
    of the information from the lead to keep the
    reader interested to read further.

- Do not give away the ending to
  your story in the nut graf.
- Think about some of the questions that
  readers might ask early on—and address the questions.
- Give readers a good reason (or hook
  to keep reading.
- Gather your thoughts about what the story
  is really about and why people should read it;
  then use one or two sentences to type out your exact thoughts.

