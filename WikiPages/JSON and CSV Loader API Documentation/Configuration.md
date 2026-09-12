### Configuration
With the API we offer some Configuration which you can find located in: `Chaosyr.MADH95.Inscryption.JSON.CSVLoader.cfg`. The following is an overview of what you can configure and what they will do affecting the API of JSON and CSV Loader.

#### JSON Loading Origination Path
This is effectively a CSV as a value. All values passed into it must be Paths using similar logic to that seen in the Artwork Form Support section of this README.

By default, this value is set to: `Scripts, Plugins/Scripts, Cards, Plugins/Cards` to make mods work without the User needing to configure this. But if you need more Paths just add them to the end of the CSV.

These paths are Relative to your mods specific folder under the `plugins` folder, well more so any mod specific folder under the `plugins` folder but yes.

This value effects what folders JSON Loader will recursively load JSON's from.

#### CSV Loading Origination Path
This is effectively a CSV as a value. All values passed into it must be Paths using similar logic to that seen in the Artwork Form Support section of this README.

By default, this value is set to: `Sheets, Plugins/Sheets` to make mods work without the User needing to configure this. But if you need more Paths just add them to the end of the CSV.

These paths are Relative to your mods specific folder under the `plugins` folder, well more so any mod specific folder under the `plugins` folder but yes.

This value effects what folders CSV Loader will recursively load CSV's from.

#### Schema Save Path
This must represent one SINGULAR path, similar to those above. This path is relative to the DLL this API takes root within.

The default value is `/Schemas`.

#### Show Verbose Logging
It's less of a Verbose Logging but when set to `true`, the API will output Debug information in the Console and in the Log File.

#### Show Additional Information
When this value is set to `true` the API will output some Additional Information with common errors with the API. Think o it as a modmakers tooling. This will be outputted to the File and Console.

#### Show Summary Information
When this value is set to `true` when the API is validating Item's against their related Schema's, it will print the description of those properties as well. Again both to the Console and Log File.

### Recursively Scan At Plugin Level
Compatibility mode that makes the File Finder recursively scan from the Plugin Level rather than from the specified Path's levels in their respective configs.