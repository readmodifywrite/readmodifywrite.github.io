AVR Xmega USART TXD pin reset
=============================


.. author:: default
.. categories:: none
.. tags:: none
.. comments::

I found some undocumented behavior on the AVR Xmega A4U USART, and a `helpful link from someone else who had the same issue. <http://blog.world3.net/2012/02/xmega-usart-unsets-output-direction-on-ports-when-disabling-tx/>`_

If you enable the USART and then disable it (TXEN bit), the TXD pin reverts to an input. If you want to re-enable the USART later, you need to reconfigure the PORT.DIR register.

Probably not many people will run in to this, but in case you're doing something fancy with your USART, there you go.