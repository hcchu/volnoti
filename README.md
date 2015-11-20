Volnoti
=========

Volnoti is a lightweight volume notification daemon for GNU/Linux and
other POSIX operating systems. It is based on GTK+ and D-Bus and should
work with any sensible window manager. The original aim was to create
a volume notification daemon for lightweight window managers like LXDE 
or XMonad. It is known to work with a wide range of WMs, including 
GNOME, KDE, Xfce, LXDE, XMonad, i3 and many others. The source code
is heavily based on the GNOME notification-daemon.

This fork adds some additional options to the original volnoti program.

Distribution packages
---------------------

 - Arch Linux - available in [AUR](https://aur.archlinux.org/packages.php?ID=55159)
 - Gentoo - [ebuild](https://bugs.gentoo.org/show_bug.cgi?id=395595) in Bugzilla

Dependencies
------------

You need the following libraries to compile Volnoti yourself. Please 
install them through the package manager of your distribution, or follow
installation instructions on the projects' websites.

 - [D-Bus](http://dbus.freedesktop.org)
 - [D-Bus Glib](http://dbus.freedesktop.org/releases/dbus-glib)
 - [GTK+ 2.0](http://www.gtk.org)
 - [GDK-Pixbuf 2.0](http://www.gtk.org)

You can compile it with standard `GCC`, with `make` and `pkg-config` 
installed, and you will need `autoconf` and `automake` if you choose 
to compile the Git version.

Compilation from Git
--------------------

Start by downloading the source code from GitHub:

    $ git clone git://github.com/davidbrazdil/volnoti.git
    $ cd volnoti

Let Autotools create the configuration scripts:

    $ ./prepare.sh
    
Then just follow the basic GNU routine:

    $ ./configure --prefix=/usr
    $ make
    $ sudo make install
    
You can have the `.tar.gz` source archive prepared simply by calling 
a provided script:

    $ ./package.sh

Compilation from source archive
-------------------------------

Download the `.tar.gz` source archive from the GitHub page, and then
extract its contents by calling:

    $ tar xvzf volnoti-*.tar.gz

Then just follow the basic GNU routine:

    $ ./configure --prefix=/usr
    $ make
    $ sudo make install

Running the application
-----------------------

Firstly, you need to running the daemon (add it to your startup 
applications):

    $ volnotid

Consult the output of `volnotid --help` if you want to see debug output
ot don't want the application to run as a daemon. You can also change
some parameters of the notifications (like their duration time) through 
the parameters of the daemon.

Once the daemon is running, you can run for example:

    $ volnoti-show 25
    
to show a notification for volume level 25%. To show a notification for
muted sound, call:
    
    $ volnoti-show -m
    
The best way to do this is to create simple script and attach it to 
the hot-keys on your keyboard. But this depends on your window manager
and system configuration.

Theming
-------

Some parameters of the notifications can be changed through the 
parameters of the daemon. To learn more, run:
    
    $ volnotid --help

All the images are stored in `/usr/share/pixmaps/volnoti` (depending
on the chosen prefix during configuration phase) and it should be
easy to replace them with your favourite icons.

New options in this fork
------------------------

This fork adds additional options to control icons and the ability to hide
the progress bar. By default, it will use the volume icons.

For example, to display a notification with no progress bar and a custom icon:

    $ volnoti-show -n -m -0 /usr/share/pixmaps/volnoti/media-eject.svg

In general, you would most likely use this along with the `-m` flag as that 
does not take a value argument, but different icons can be specified.

To control brightness, with different icons for the varying levels:

    $ volnoti-show -1 /usr/share/pixmaps/bright-off.png 
                   -2 /usr/share/pixmaps/bright-low.svg 
                   -3 /usr/share/pixmaps/bright-med.svg
                   -4 /usr/share/pixmaps/bright-high.svg
                   <value>

There is also the option to use a single icon for all values:

    $ volnoti-show -s /usr/share/pixmaps/volnoti/display-brightness-symbolic.svg <value>

For your convenience there's the `volnoti` script, a wrapper around volnoti-show that automatically loads the daemon on demand.
So you can substitute `volnoti-show` with `volnoti`:

    $ volnoti -s /usr/share/pixmaps/volnoti/display-brightness-symbolic.svg <value>


Credits
-------

 - Faenza Icon Set (tiheum.deviantart.com)
 - Notification-daemon (www.gnome.org)
 - Gopt (www.purposeful.co.uk/software/gopt)
