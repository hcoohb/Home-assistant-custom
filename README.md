# Home-assistant-custom
Custom UI components for home-assistant


## state-card-custom-password-group
This custom input_text allows to hide/show another group card. Automatically hide the group at page loading.  
This is done on the client side and therefore only the client putting the password will see the group.

**Disclaimer**: this is a ugly hack that could probably be made much nicer though polymer but I am not familiar enough for that. *The password is transmitted to the client in the page source*, so the security is  absolutely rubbish. It is not meant as a security feature but rather hiding some controls from a child... (assuming your child is not a genius with computer...)  
It seems to work quite well, but be aware that it might not hide the desired group absolutely every-time..

*** **__Use at your own risks__** ***

* #### Installation
copy the file [**state-card-custom-password-group.html**](www/custom_ui/state-card-custom-password-group.html) into **~/.hone-assistant/www/custom_ui/**

* #### Configuration
For this configuration example, we need to create and display the input_text.showprinter.
It will automatically hide the group with id *printer* on load. To show the group, type the *show_passwd* and 'Enter'. The group will be shown and 'hide' already pre-typed in the input_text. 'Enter' will hide the group again.

Add the component into your configuration:
```yaml
input_text:
  showprinter:
    name: PrinterGp
    initial: ""
```
Add the input_text.showprinter to be displayed in your views

Add into the 'customize' section:
```yaml
input_text.showprinter:
  custom_ui_state_card: state-card-custom-password-group
  password: "show_passwd"
  group_control: "printer"
```
The group to hide should be placed as the last group on the view  
Restart HASS  
A hard reload might be needed for the browser to take the changes into account

* #### Usage
Just type the password defined and 'Enter' to show the group.  
type '**hide**' (already pre-typed) and 'Enter' to hide the group again

* #### Issues
1. At this stage the input_text cannot be used with automation as the text entered is not passed on to HASS, but just stays in the client side. Can be easily modified though
2. The group to be hidden still is displayed for a few ms before being hidden
3. If the hidden group was by itself on a colum, the empty column is still displayed...
4. no other known. Please report if you notice something else
