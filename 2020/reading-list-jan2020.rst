Reading List for Jan 2020
*************************************

..  contents:: Contents
    :local:
    :depth: 3

.. sectnum:

Tech
======

cURL things
------------

Figured it's more convenient to set up pipelines
that cURL and then executes scripts from a specific
commit in a repo than to get submodules,
which if you think about it are equally volatile in pipelines
since they're also remotely located anyway.

What we need to do is:

..  code-block::

    curl -fsSL <uri>/requirements.txt | python3 -m pip install -r -
    curl -fsSL <uri>/scriptname.py | python3 - [<args>...]

But what I *really* want to know is *why*
we're using ``curl -fsSL``.

So ...

-f --fail
  Fail the ``curl`` command silently.
  If a ``curl`` fails, it usually
  returns a HTTP header containing a fail state.
-s --silent
  Runs ``curl`` in quiet mode;
  doesn't show progress bar or error messages.
-S --show-error
  Show error messages; usually used together
  with ``--silent`` to tell ``curl`` to hide
  all messages except errors.
-L --location
  Follow redirects. Can limit the number of
  redirects with ``--max-redirs``.
  If your initial request is not a GET,
  subsequent requests as a result of following
  the redirection (HTTP 301, 302, or 303)
  are made with a GET. If the HTTP response code
  is 30x, but not 301/302/303, then ``curl``
  makes the same request method on the redirect
  destination.

