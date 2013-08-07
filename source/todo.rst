Working Sheet
===================





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