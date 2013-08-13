********************
Working Sheet
*******************




TBD
=========================

At-View Sugar
------------------

``#view``, ``#sugar``

.. code-block:: text

	fun {a:t@ype}
	ptr_get {l:addr} (pf: !a @ l >> a @ l | p: ptr (l)): a

is actually a sugar for 

.. code-block:: text

	fun {a:t@ype}
	ptr_get {l:addr} (pf: a @ l | p: ptr (l)): (a @ l | a)

The de-sugar one says everything about the meaning of ``!`` and ``>>``.



foo (pf: !T?@l >> T@l | ptr (l))

@[T][n] Array

///////////////////////////////////

The #[...] in existential qualifiers means that that variable can be referenced in function parameters. Notice the 'd' is referenced in the type of the 'd' argument. Without the '#' this would be an error.  

may be {} is universal contifier?
https://groups.google.com/forum/#!topic/ats-lang-users/VKuV0kFysxc


/////////////////////////////////
https://groups.google.com/forum/#!topic/ats-lang-users/88CYxwKl0M0


///////////////////
$showtype m