Memory alignment on ESP8266 - Exception(9)
==========================================


.. author:: default
.. categories:: none
.. tags:: none
.. comments::

This one was tough to track down, but extremely obvious once I figured it out.  The ESP8266 has limitations on accessing data through a pointer.  Namely, 32 bit accesses need to be aligned on a 32 bit boundary, and 16 bit boundaries for a 16 bit access.

.. code-block:: c

    void func( uint32_t *ptr ){

        *ptr++;
    }

If the lowest 2 bits of ptr (the actual address) are not zeroes, you get Exception (9).  This is easy to do if you have packed structs:

.. code-block:: c


    typedef struct __attribute__((packed)){
        uint8_t something;
        uint32_t something_else;
    } this_may_crash_t;


If you pass a pointer from something_else to func, the compiler won't know the pointer is unaligned and it cannot do anything about it.  So you need to manually make sure your access is aligned.  Simple, right?