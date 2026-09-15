### The Extension Properties System
This is a system primarily on cards, it enables modded libraries to allow you to add additional properties to your JSON in which it will understand and interpret. To set it up it works as follows:
* First add `extensionProperties` Object at the end of your JSON, or ending of the CSV.
* Next within the `{}` add a comma separated list of fields matching the below scheme:
  * `"fieldName": "fieldValue"` for JSON.
  * `fieldName: fieldValue`

Then that's it, as long as the `fieldName` and `fieldValue` line up correctly it will just work.