Octave is compiled with a graphical user interface. The start-up option --no-gui
will run the familiar command line interface. The option --no-gui-libs runs a
minimalistic command line interface that does not link with the Qt libraries and
uses the fltk toolkit for plotting if available.


Several graphics toolkit are available. You can select them by using the command
'graphics_toolkit' in Octave.  Individual Gnuplot terminals can be chosen by setting
the environment variable GNUTERM and building gnuplot with the following options:

  setenv('GNUTERM','qt')    # Requires QT; install gnuplot --with-qt5
  setenv('GNUTERM','x11')   # Requires XQuartz; install gnuplot --with-x11
  setenv('GNUTERM','wxt')   # Requires wxmac; install gnuplot --with-wxmac
  setenv('GNUTERM','aqua')  # Requires AquaTerm; install gnuplot --with-aquaterm

You may also set this variable from within Octave. For printing the cairo backend
is recommended, i.e., install gnuplot with --with-cairo, and use

  print -dpdfcairo figure.pdf


When using the native Qt or fltk toolkits then invisible figures do not work because
osmesa is incompatible with Mac's OpenGL. The usage of gnuplot is recommended.

