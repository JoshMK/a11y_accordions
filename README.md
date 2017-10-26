# ARIA Accordions  

ARIA accordion JavaScript pattern.  

* [Demo Page](http://scottaohara.github.io/accessible_accordions/)  
* Based on [ARIA 1.1 Authoring Practices](http://w3c.github.io/aria-practices/#accordion)  


## Keyboard Controls  
When focus on the accordion triggers:  
* <kbd>Tab</kbd> and <kbd>Shift</kbd> + <kbd>Tab</kbd>, or standard AT navigation keys are used to navigate between accordion triggers and any focusable content within an accordion panel.  
* <kbd>Home</kbd> moves focus to the first accordion trigger in the group.  
* <kbd>End</kbd> moves focus to the last accordion trigger in the group.  
* <kbd>Space</kbd> or <kbd>Enter</kbd> open/close the trigger's associated panel.  


## Minimum Required Mark-up  
```html
<div class="accordion" data-aria-accordion>
  <h3 class="accordion__heading">
    Heading Here
  </h3>
  <div class="accordion__panel">
    <p>
      Content here
    </p>
  </div>
  <!-- 
    repeat for as many accordion panels
    as one desires.
  -->
</div>
```

### Under the hood
The `data-aria-accordion` attribute is the key for initiating the process to convert the minimum markup into a functioning accordion component.  

If an `id` is not pre-set on the accordion wrapper, then one will be auto generated. An ID is necessary to serve as the basis for populating generated IDs onto the child accordion panels. More on why these IDs are needed, later.

When an accordion is identified, the setup script continues to run and identify each heading and panel within the accordion. The classes `accordion__heading` and `accordion__panel` are necessary for the setup process to run and appropriately identify these key pieces of the accordion.

During the setup process the following occurs:  
* The panels are hidden, and if a default panel was set (see options) an attribute of `aria-hidden="false"` will be set to that panel.  
* The `id` of the accordion container is used as the basis to generate unique IDs for each of the panels of the accordion.  
* a `<button>` is dynamically created and inserted into the `accordion__heading` element. The previous text of the heading is then inserted into this button. Presently, this strips out any previous HTML tags that were in the heading and only retains the text string.  
* The `<button>` is given the class `accordion__trigger`, an `aria-controls` attribute, with the value set to the panel `id` that appears next in the DOM. While `aria-controls` is not presently useful in all assistive technologies, JAWS users will be given additional keys to press to begin interacting with the associated content.   
* Depending on the initial state of the associated panel, e.g. is it set to be opened by default or not, the `<button>` will also receive the attribute `aria-expanded`, which will either have the value `true` or `false`. These value will indicate the current state of their associated panels, to uses of assistive technologies.   
* If an accordion has the `data-constant` attribute set (see options), then the `<button>` with `aria-expanded="true"` will also have an `aria-disabled="true"` set to it.  


## Options  
The following `data` attributes can be added to an accordion instance to alter the default accordion setup settings. None of the `data` attributes affect nested accordions, so a parent accordion that requires a consistently open panel would not pass down that requirement to a child accordion.  

### `data-default` 
* Leave off or set to "none" to not have a panel open by default.  
* Set the attribute, with no value, to open the first panel by default. Set the value to the panel number ("1" for the first panel in the DOM, 2 for the second, etc.) to open that specific panel by default.  
* Setting a negative number, or 0 will open the first panel by default.  
* Setting a number greater than the number of panels of an accordion, will open the last panel by default.  

### `data-constant`  
By placing this attribute on the accordion wrapper, it will indicate that an accordion panel must always be expanded. An `aria-disabled="true"` will be set to the `button` that controls the expanded panel. This attribute will indicate to assistive technologies that the `button` can not be currently interacted with.    

### `data-transition`  
Giving this attribute a numeric value will apply a `style="transition: [val]s ease-in-out` to the accordion panels. Set this if you want an accordion panels to have open/close transitions applied to them. 

### `data-multi`  
This attribute requires no value. Setting it will allow multiple accordion panels, of a particular group, to be opened at once.  


## License & Such  
This script was written by [Scott O'Hara](https://twitter.com/scottohara).

It has an [MIT license](https://github.com/scottaohara/accessible-components/blob/master/LICENSE.md).

Do with it what you will :)
