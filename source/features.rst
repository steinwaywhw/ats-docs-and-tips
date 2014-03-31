****************
Features
****************


Function Effects
==========================

.. note:: This part is taken from `Chris Double's blog <http://bluishcoder.co.nz/2010/06/13/functions-in-ats.html>`_ and a discussion on `ATS google group <https://groups.google.com/forum/#!topic/ats-lang-users/88CYxwKl0M0>`_. Thanks to all the contributions in the blog and group thread.

For a function like ``fun foo (someargs: sometype):<> sometype``, the ``:<>`` part is used to describe effects of functions. There is a sort ``eff`` exclusively for function effects. You can do things like ``:<>``, ``:<lin,prf>`` and so on. The meaning of them are as follows.

``:<>``
	pure, no effects at all

``!exn``
	the function possibly raises exceptions

``!ntm``
	the function possibly is non-terminating

``!ref``
	the function possibly updates shared memory, which means reading from or writing to a location that it knows exists but does not own.

``!wrt``
	(ATS2 only) the function may write to a location it owns

``0``
	the function is pure (has no effects)

``1``
	the function can have all effects

``fun``
	the function is an ordinary, non-closure, function

``clo``
	the function is a stack allocated closure

``cloptr``
	the function is a linear closure that must be explicitly freed

``cloref``
	the function is a peristent closure that requires the garbage collector to be freed. 

``lin``
	the function i slinear and can be called only once

``prf``
	the function is a proof function


Quantifiers
===============

In ATS, ``[]`` is mostly used as extential quantifier, while ``{}`` is mostly used as universal quantifier.

For example, suppose ``MUL`` encodes the multiplication relationship as defined `here <http://www.ats-lang.org/DOCUMENT/INTPROGINATS/HTML/c2829.html>`_, we can write something like this.

.. code-block:: text

	prfun mutiplication_is_total {m,n:int} (): [p:int] MUL (m, n, p)

which will be interpreted as 

	For all integers *m* and *n*, there exists some integer *p* such that ``MUL (m, n, p)`` is ture.