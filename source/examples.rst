****************
Examples
****************

Creating ATS Interface for C Library
=======================================

I did a `zlog <https://github.com/HardySimpson/zlog>`_ interface for ATS based on `Zhiqiang Ren <http://cs-people.bu.edu/aren/>`_'s work. You can access the code at `GitHub <https://github.com/steinwaywhw/ats-zlog>`_. And here's how I did it.


Getting Start
--------------

Download and install `zlog <https://github.com/HardySimpson/zlog>`_, read its `documents <http://hardysimpson.github.io/zlog/>`_ and `interfaces <https://github.com/HardySimpson/zlog/blob/master/src/zlog.h>`_, get familiar with it by writting some simple hello world in C.

Translate into a Minimum Workable ATS Interface
-------------------------------------------------

For a minimum hello world, we just write such a C program

.. code-block:: c

	int main () {
		zlog_init ("")
		zlog_category *c = zlog_get_category ("mycat");
		zlog (c, "%s", "hello world");
		zlog_fini ();
	}

I consider the data structures first. 

``zlog_category *`` is used across interfaces, but I don't care it's inner structure, which means I can use an **abstract type**. It doesn't need to be freed manually, instead, all resources are freed by ``zlog_fini ()``. Therefore I make it **non-linear** in ATS. It is a pointer in C, I then use **boxed type** in ATS.

Therefore, I can define ``zlog_category`` using ``abstype``, which is abstract, non-linear, and boxed.

.. code-block:: text

	abstype zlog_category

For functions, we can translate them directly into ATS

.. code-block:: ocaml

	fun zlog_init (config: string): int = "mac#zlog_init"
	fun zlog_get_category (name: string): zlog_category = "mac#zlog_get_category"
	fun zlog_fini (): void = "mac#zlog_fini"

The logging function ``zlog`` is tricky since it has variable length parameter list. What I do here is using an intermediate C function.

.. code-block:: ocaml

	fun zlog {ts:types} 
	(c: zlog_category, level: int, fmt: string, args: ts): void =
	"mac#zlog_handler"

And in the DATS file, I implement it as follows

.. code-block:: c

	#include "zlog.h"
	#include <stdarg.h>
	
	void zlog_handler (zlog_category *c, int level, char *fmt, ...) {
		va_list args;
		va_start (args, fmt);

		vzlog (
			c, 
			__FILE__,
			sizeof(__FILE__) - 1,
			__func__,
			sizeof(__func__) - 1,
			__LINE__, 
			level, 
			fmt, 
			args);

		va_end (args);
	}

The ``vzlog`` is an alternative interface provided ``zlog`` itself. Most library interfaces will provide such an alternative besides its original variable length version.

And now we can use them to write the hello world example.

Refining Types
------------------

My initial type for ``zlog_category *`` is just workable. But now I wanna force programmers to check whether it is a null pointer before using it.

I then change the definition and interface to the followings.