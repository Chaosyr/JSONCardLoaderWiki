### The Fields to Edit System
This is a system in which allows you to modify a base game item, such as a card or starter deck. It works as follows:
* First add the `fieldsToEdit` String Array to the top of your JSON, or beginning of your CSV.
* Next within the `[]` add a comma separated list of all fields in which you want to overwrite. 
  * For example, the display name of a card would be `"fieldsToEdit": ["displayedName"]` or for a CSV `[displayedName]`
* Lastly, ensure your `name` matches the name of a Base Game or Modded Item, note for modded items, that item must be added to the game before JSONLoader runs which for the most part should be the case.

That's all there really is to it, if you need more overwrites you'll just extend the `fieldsToEdit` field with more properties.