# How to stop your MacBook Air (OS Ventura) from sleeping when the lid is closed

> [!IMPORTANT]
> This feature isn't accessible in settings on the MB Air. Users can still change this setting using terminal and the pmset command.

To begin, open terminal using `cmd + spacebar` and typing "terminal."

We'll use the `pmset` command which requires us to use `sudo` since we're changing low-level settings.

`sudo pmset ...`

When we type `pmset -g` in terminal, we're provided a list of properties and their current settings. We're concerned specifically with `sleep`, not `displaysleep`.

```
brianeddow@Brians-MacBook-Air ~ % pmset -g
System-wide power settings:
Currently in use:
 standby              1
 Sleep On Power Button 1
 hibernatefile        /var/vm/sleepimage
 powernap             1
 networkoversleep     0
 disksleep            10
 sleep                1 (sleep prevented by powerd)
 hibernatemode        3
 ttyskeepawake        1
 displaysleep         10
 tcpkeepalive         1
 lowpowermode         0
 womp                 0

```

In our current context, `sleep` is accompanied by the number `1`. This is the Air's default setting. We'll be changing this to `0`.

Now, these settings are specific to whether the machine is charging or not. `pmset` uses flags for charging (`-c`) and on battery (`-b`).

Type `sudo pmset -c sleep 0` into terminal and press return (terminal will alert you if you omit `sudo` since we must run as root).

You'll then be prompted to enter your password to finalize the change.

```
brianeddow@Brians-MacBook-Air ~ % sudo pmset -c sleep 0
Password:
```

Any user familiar with terminal will be aware that their input once prompted to enter their password won't show up. This is not a bug.

After this, you can re-enter `pmset -g` to see a list of properties and their current settings.

```
brianeddow@Brians-MacBook-Air ~ % pmset -g
System-wide power settings:
Currently in use:
 standby              1
 Sleep On Power Button 1
 hibernatefile        /var/vm/sleepimage
 powernap             1
 networkoversleep     0
 disksleep            10
 sleep                0 (sleep prevented by powerd)
 hibernatemode        3
 ttyskeepawake        1
 displaysleep         10
 tcpkeepalive         1
 lowpowermode         0
 womp                 1

```

The `sleep` property should now have a `0` to the right. This means that the user can now plug in their charger, keyboard, mouse, and external monitor with the lid closed without the machine sleeping.

> [!NOTE]
> Specific to MB Air, this setup works exclusively while charging. If you unplug the charger, your MB Air will sleep.
