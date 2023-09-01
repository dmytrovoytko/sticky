# DBUS / CLI calls

Besides GUI interaction you can manipulate Sticky via dbus-send calls:

## CLI calls

### Notes

#### Toggle Notes
dbus-send --type=method_call --dest=org.x.stickyapp /org/x/stickyapp org.x.stickyapp.activate_notes

#### Hide Notes

dbus-send --type=method_call --dest=org.x.stickyapp /org/x/stickyapp org.x.stickyapp.hide_notes

#### New Note

dbus-send --type=method_call --dest=org.x.stickyapp /org/x/stickyapp org.x.stickyapp.new_note

#### Change visible note group

dbus-send --type=method_call --dest=org.x.stickyapp /org/x/stickyapp org.x.stickyapp.change_visible_note_group string:'Group 1'

### Open notes manager

dbus-send --type=method_call --dest=org.x.stickyapp /org/x/stickyapp org.x.stickyapp.open_manager 

### Quit app

dbus-send --type=method_call --dest=org.x.stickyapp /org/x/stickyapp org.x.stickyapp.quit_app 


## DBUS calls in code (python example)

```
import dbus
from dbus.exceptions import DBusException
# from sticky import BUS_NAME
BUS_NAME = 'org.x.stickyapp'

bus = dbus.SessionBus()
try:
    object_path = '/'+BUS_NAME.replace('.','/')
    sticky_service = bus.get_object(bus_name=BUS_NAME, object_path=object_path)
except DBusException:
    print('ERROR: Sticky Notes app is not running!')
    exit()

# available methods
method_names = ['activate_notes', 'hide_notes', 'new_note', 'open_manager', 'quit_app']

# example call of method 0 - activate notes
method = sticky_service.get_dbus_method(method_names[0], BUS_NAME)
method()

```
