# JSONLoader Nightly / JSONLoader 3

## Comprehensive Technical Research Report for Inscryption Mod Authors and Maintainers

**Research status:** This report is an expanded and corrected technical study of JSONLoader V1, JSONLoader V2, JSONLoader Nightly, and the developing JSONLoader 3 architecture. It incorporates the original research questions, the stable JSONLoader documentation, the Nightly documentation, the published release histories, the Nightly configuration model, the documented V1 and V2 content systems, and the source-level architecture examined during the research. It also expands the areas that were previously summarized too aggressively, especially function descriptions, schema generation, file loading, validation, image processing, compatibility, duplicate handling, JSON Editor usage, and the meaning of the major Nightly classes. Where the implementation has been directly examined, the report identifies that as source-level evidence. Where the documentation establishes a behavior, it is treated as documented behavior rather than inferred implementation. Where the exact maintainer rationale is unavailable, the report explicitly identifies the explanation as architectural interpretation rather than presenting it as an official statement.

A particularly important correction is necessary concerning the Nightly version number. The currently indexed Thunderstore Nightly package page identifies **0.1.3** as the latest version available through that package listing, rather than 0.1.4. The same page describes Nightly as a preview of what is coming to JSONLoader and CSVLoader and points to the `Refactor-JSONLoader-3` development branch. Consequently, this report does not treat 0.1.4 as an independently verified current release. Where earlier Nightly source observations are discussed, they are identified as observations of the development implementation available at the time of examination rather than assumptions about every later build.

---

# 1. Executive summary

JSONLoader is an Inscryption modding framework that lets authors describe game content declaratively rather than implementing every content object directly in C#. A conventional C# mod might construct a game object through code, configure its fields, resolve its assets, and register it with the Inscryption API. JSONLoader moves much of that authoring work into data files that the loader interprets at runtime. The result is a pipeline in which a JSON document becomes an intermediate representation and is eventually converted into content understood by the underlying Inscryption modding API. This makes JSONLoader particularly useful for content-heavy mods because large collections of cards or related objects can be represented as data instead of requiring a separate C# implementation for each one. The system has nevertheless grown considerably beyond simple card creation, which is why the transition from V1 to V2 and then toward Nightly/JSONLoader 3 is best understood as an architectural evolution rather than merely a sequence of additional fields.

The three major generations can be represented as follows:

```text
JSONLoader V1
    |
    | .jldr
    | card-focused original format
    v
JSONLoader V2
    |
    | .jldr2
    | API 2.x-era rewrite
    | cards + many additional systems
    v
JSONLoader Nightly / JSONLoader 3
    |
    | V1/V2 compatibility
    | V3 architecture
    | CSV infrastructure
    | generalized loader systems
    v
next-generation loader architecture
```

The most important conclusion is that **Nightly is not simply "JSONLoader 2.8."** The Nightly package itself describes the project as a preview of what is coming to JSONLoader and CSVLoader, and it identifies `Refactor-JSONLoader-3` as the development branch. The stable documentation likewise presents JSONLoader/API 3.0.0 as being on the horizon. This means that Nightly should be understood as a development architecture that is intended to become the basis of the next generation of JSONLoader. It can therefore contain both old-format compatibility and unfinished future-format infrastructure at the same time.

The stable JSONCardLoader line, by contrast, represents the mature V2 ecosystem. Stable V2 accumulated support for cards, sigils, starter decks, tribes, encounters, Configils, talking cards, regions, items, localization-related features, and other systems over a long sequence of releases. Nightly is architecturally newer, but architectural newness does not automatically mean complete feature parity with every feature accumulated by V2. This distinction is critical when deciding whether to develop a released mod against stable JSONLoader, test a mod against Nightly, or directly participate in the JSONLoader 3 development process.

---

# 2. What JSONLoader actually is

A beginner can think of JSONLoader as a translator, but that description becomes more useful when the stages of translation are made explicit. Your JSON file does not normally become an Inscryption runtime object in one operation. Instead, the loader has to locate the file, determine which format it represents, parse its contents, validate its structure, resolve referenced assets, construct a loader-side representation, and eventually convert that representation into something the Inscryption API can register or modify. Each stage exists because it solves a different problem. Separating those problems is one of the main architectural ideas behind the Nightly refactor.

The basic relationship can therefore be visualized as:

```text
C# implementation
    ↓
Inscryption API
    ↓
CardInfo / other runtime objects
```

or, when JSONLoader is involved:

```text
JSON
    ↓
JSONLoader
    ↓
Inscryption API
    ↓
CardInfo / other runtime objects
```

The JSON file is therefore not itself the game object. It is a declaration of what the author wants the game object to contain. JSONLoader interprets that declaration and determines how to construct or modify the underlying object. This distinction becomes especially important when discussing classes such as `CardObject`, because `CardObject` is a loader-side representation rather than simply another name for `CardInfo`. It also explains why schema validation can succeed while runtime loading still fails: a schema can establish that the JSON is structurally appropriate, but it cannot by itself prove that every referenced card, ability, image, or game object actually exists.

A simplified pipeline is:

```text
Your JSON file
       |
       v
File discovery
       |
       v
File-type identification
       |
       v
JSON parsing
       |
       v
Schema validation / linting
       |
       v
Loader-specific object
       |
       v
Image / asset resolution
       |
       v
Conversion
       |
       v
Inscryption API
       |
       v
Game object
```

Nightly's importance is that it attempts to make many of these stages reusable. Instead of every content format independently implementing file discovery, schema generation, logging, image handling, and other support functions, the architecture moves those responsibilities toward shared infrastructure. V1, V2, V3, and CSV can then become format-specific consumers of that infrastructure. That is a much larger architectural change than adding another card property.

---

# 3. What "Nightly" means

"Nightly" should be interpreted as a development channel rather than as a synonym for "version 3 is finished." The current package explicitly describes itself as the Nightly version of JSONLoader and calls it "effectively a preview of whats to come to JSONLoader (and CSVLoader)." It points contributors toward the `Refactor-JSONLoader-3` branch and warns that the package's older embedded documentation may become outdated, with the Wiki being the more current documentation source. That wording is significant because it tells us how to interpret incomplete areas of the documentation. An empty V3 documentation section should not be silently converted into a claim that V3 is fully implemented.

The Nightly architecture therefore has three simultaneous characteristics. First, it is a preview of the future loader architecture. Second, it contains compatibility machinery intended to allow earlier JSONLoader data formats to continue being useful. Third, it is a development environment whose internal classes and methods can change while the refactor is underway. These three characteristics explain why Nightly can contain both mature-looking compatibility code and apparently unfinished V3 infrastructure. It also explains why a mod author should distinguish file-format compatibility from compiled C# API compatibility.

For C# developers, this distinction is especially important. A `.jldr2` document continuing to load only demonstrates that the Nightly loader can interpret that document and convert it into current runtime content. It does not prove that a DLL compiled against an old JSONLoader assembly can continue calling the same classes and methods. Data compatibility and binary compatibility are different contracts, and Nightly primarily provides the former.

---

# 4. Nightly versus stable JSONLoader 2.7.0

The stable and Nightly projects should be thought of as serving different purposes. Stable JSONLoader 2.7.0 represents the mature V2 implementation and the feature set that accumulated throughout the V2 release series. Nightly represents the refactoring effort intended to provide the next architecture. The stable project therefore has the advantage of accumulated implementation maturity, while Nightly has the advantage of a more deliberately generalized architecture. Neither statement should be converted into the claim that one universally replaces the other.

| Area | Stable JSONLoader 2.7.0 | Nightly / JSONLoader 3 |
|---|---|---|
| Primary purpose | Mature V2 loader | Next-generation architecture |
| Main format | `.jldr2` | V1/V2 compatibility plus future V3/CSV infrastructure |
| Stability target | Stable | Development/preview |
| V1 support | Historical compatibility | Explicit compatibility layer |
| V2 support | Mature implementation | Compatibility implementation |
| V3 | Future | Development pathway |
| CSV | Not the central stable format | Part of new architecture |
| Schema tooling | Present | More explicitly generalized |
| Linting | Present | Dedicated reusable infrastructure |
| File discovery | Mature implementation | Explicit shared subsystem |
| Image scanning | Existing loader capability | Generalized infrastructure |
| Future extensibility | Accumulated feature set | Major architectural goal |

The Nightly documentation explicitly separates support for different JSONLoader versions and includes dedicated sections for V1 and V2 while leaving V3 and CSV support areas as development documentation. This is strong evidence that Nightly is intended to provide a common framework around several generations rather than simply deleting the older formats. The same documentation provides configuration for separate JSON and CSV origins, which further demonstrates that CSV was designed into the architecture rather than added as an unrelated utility.

The correct mental model is therefore not:

```text
V2 + extra features = V3
```

but:

```text
Reusable loader infrastructure
        +
V1 support
        +
V2 support
        +
V3 support
        +
CSV support
```

That distinction explains why Nightly can be architecturally significant even in areas where stable V2 currently has more mature user-facing functionality.

---

# 5. The architecture of Nightly

The early Nightly source examined during this research exposes an architecture broadly organized around components such as:

```text
Cores
Peripheral
Subperipheral
FILE_Loader
JSON_LINT
JSON_SCHEMA
JSONLoaderV1Support
JSONLoaderV2Support
JSONLoaderV3Support
Plugin
```

These names should not be interpreted as an immutable public API list. Nightly is explicitly a development branch, and the package documentation warns that older documentation may become outdated. The useful conclusion is instead that the architecture is attempting to separate responsibilities into layers. A file-loading component should not need to understand every card field, while a schema component should not need to know how BepInEx discovers the plugin. Likewise, a V1 compatibility component should not need to reinvent the general logging and filesystem systems.

The architecture can therefore be conceptualized as:

```text
                         Plugin
                           |
                 +---------+---------+
                 |         |         |
              Config    Logging    Loading
                           |
                    +------+------+
                    |             |
                 FILE_Loader   JSON_SCHEMA
                    |             |
                    |          JSON_LINT
                    |
        +-----------+-----------+
        |           |           |
       V1          V2          V3
```

This structure is more important than any individual class name. It indicates that Nightly is attempting to create a reusable loader platform. If the architecture succeeds, adding or changing a format should require less duplication because the surrounding infrastructure already knows how to discover files, produce schemas, validate data, report errors, and resolve assets.

---

# 6. `Plugin`

`Plugin` is the BepInEx entry point and therefore represents the boundary between the loader and the game's mod-loading environment. Its purpose is not to contain every operation associated with JSON. Instead, it provides the point at which the loader becomes an active BepInEx plugin and can initialize the systems it needs. This distinction is important because a large plugin can become difficult to maintain when initialization, file discovery, JSON parsing, schema generation, logging, and game-object creation all become intertwined. The Nightly architecture instead treats the plugin as the coordinator that brings those subsystems into existence.

Conceptually:

```text
BepInEx
   |
   v
Plugin
   |
   +--> configuration
   +--> logging
   +--> file loading
   +--> loader registration
   +--> initialization
```

The name `Plugin` is therefore conventional rather than mysterious. It means that this is the component BepInEx recognizes as the mod/plugin entry point. It does not mean that `Plugin` itself represents a card, a JSON document, or a schema. It is the outer shell that starts the machinery. When debugging a loader problem, this distinction is useful because a failure during plugin initialization is fundamentally different from a failure while interpreting a particular JSON file.

---

# 7. Semantics of the class and namespace names

The question of why the classes were given their names needs to be approached carefully. Names such as `FindFiles`, `LoadFiles`, `LoadSchema`, and `LintingTools` describe their responsibilities closely enough that their meaning can be inferred directly from their role. Names such as `JSONLoaderV1Support` and `JSONLoaderV2Support` are similarly explicit because the version number tells you which format generation the component is intended to understand. The names `Cores`, `Peripheral`, and `Subperipheral` are less formally documented, so it would be incorrect to invent an official maintainer explanation for them. The safest interpretation is therefore to distinguish literal responsibility from architectural interpretation.

This matters because software names can sometimes look self-explanatory while still having project-specific meanings. `CardObject`, for example, clearly suggests a card representation, but it does not tell you by itself whether it is a runtime `CardInfo`, a serialized DTO, a schema model, or an intermediate object. Source inspection resolves that ambiguity. Similarly, `JSON_SCHEMA` and `JSON_LINT` strongly suggest schema generation and validation, but the actual methods determine exactly what they do. The report therefore treats class names as useful architectural clues while using source/documentation evidence to establish their actual roles.

## `Plugin`

`Plugin` is the BepInEx plugin entry point. The name is conventional because BepInEx plugins are commonly structured around a class that represents the plugin itself. Its responsibility is initialization and coordination rather than card-specific data conversion. It forms the boundary between the operating mod loader and JSONLoader's internal subsystems. The class therefore sits at the outermost layer of the architecture. Its presence does not mean that all JSON processing occurs inside the class.

## `JSONLoaderV1Support`

`JSONLoaderV1Support` literally means support for JSONLoader's first-generation format. The significance of the name is architectural because it establishes V1 as a compatibility subsystem rather than as the central representation used by the entire Nightly system. A V1 document can therefore enter through this support layer while the surrounding infrastructure remains shared with newer formats. This is exactly the sort of separation that a refactor would want. The name also makes it easier for maintainers to locate legacy behavior without searching through unrelated V2 or V3 code.

## `JSONLoaderV2Support`

`JSONLoaderV2Support` has the same meaning for `.jldr2` and the V2 content model. V2 is substantially larger than V1, so this boundary is particularly valuable because V2-specific assumptions can remain localized. It also means that the generalized loader infrastructure can evolve without requiring every change to be duplicated inside the V2 implementation. The name therefore describes both a format generation and an architectural responsibility. It is effectively saying, "this is where the system understands V2."

## `JSONLoaderV3Support`

`JSONLoaderV3Support` represents the architectural location where the new format generation is intended to live. Its existence is evidence that V3 has been planned into the architecture, but it is not evidence that every V3 feature is complete. The current Nightly documentation explicitly leaves the V3 support section empty, which reinforces the need for that distinction. A maintainer should therefore treat the name as a boundary for future implementation rather than a guarantee of finished functionality.

## `CardObject`

`CardObject` means an object representing a card from the loader's perspective. This distinction is essential because the loader needs somewhere to store the values it parsed before those values are applied to the actual game/API object. The object therefore acts as an intermediate representation between serialized data and runtime content. It can contain fields such as names, abilities, artwork references, evolution data, and other card properties without itself being the actual game entity. Thinking of it as "the card" without adding the qualifier "loader-side representation" can lead to serious misunderstandings about what the conversion methods actually do.

The distinction can be visualized as:

```text
JSON
  |
  v
CardObject
  |
  v
Convert()
  |
  v
Inscryption API / runtime object
```

The advantage of this arrangement is that parsing does not need to know every detail of runtime object construction. The loader can first create a representation of the requested content and then perform conversion as a separate operation. That separation also makes compatibility layers easier to reason about because V1 and V2 can create different intermediate representations while sharing later infrastructure.

## `FindFiles`

`FindFiles` is deliberately literal because its responsibility is filesystem discovery. It answers the question, "Which files are available under the configured origins?" It should not be responsible for deciding what every JSON field means because that would mix filesystem concerns with content semantics. Separating discovery from interpretation means that V1, V2, V3, and CSV can potentially share the same search machinery. The name therefore reflects a boundary between finding candidate files and understanding their contents.

## `LoadFiles`

`LoadFiles` follows discovery and is responsible for coordinating the process of actually loading the discovered files. The distinction is subtle but important because finding a file does not imply that the file should be parsed in the same way as every other file. A loader must classify the extension, identify the appropriate subsystem, parse the document, validate it, and eventually create or modify content. `FindFiles` answers "what exists?" while `LoadFiles` answers "what should happen to it?" Keeping those responsibilities separate reduces duplication and makes the architecture easier to extend.

## `LoadSchema`

`LoadSchema` concerns the consumption of generated or stored schema information. Its purpose is therefore different from the object loader that creates game content. A schema describes what a valid document should look like, so loading that schema provides the validation subsystem with a formal structural contract. This allows the loader to validate data before attempting to convert it into runtime objects. The class name reflects that it is handling the schema as data rather than directly constructing game content.

## `WriteSchema`

`WriteSchema` performs the opposite direction of the schema pipeline. Rather than consuming an existing schema, it generates schema information from the loader's type definitions and metadata. The importance of this class becomes much clearer when considering how many fields a large modding framework can accumulate. Manually maintaining a separate schema for every C# type would create another source of truth that could drift away from the implementation. Automatic schema generation instead attempts to make the code model the authoritative source from which authoring tools can be derived.

## `LintingTools`

`LintingTools` provides validation operations. Its job is to inspect a JSON document against a schema and identify structural discrepancies before the document reaches later stages of loading. This is more useful than merely checking whether the JSON is syntactically valid because JSON syntax says almost nothing about whether the document contains the correct fields and types. The linter can recursively inspect strings, integers, booleans, arrays, objects, required properties, and other schema constraints. It therefore acts as a bridge between the formal schema and practical author feedback.

## `JSON_SCHEMA`

`JSON_SCHEMA` represents the schema subsystem. A schema is effectively a machine-readable description of the contract that a JSON document must satisfy. It can describe field names, field types, required properties, nested objects, arrays, and additional-property behavior. JSONLoader can use those descriptions both for validation and for external tools such as JSON Editor. The name therefore describes a subsystem concerned with defining and consuming the structure of valid JSON rather than directly creating cards.

## `JSON_LINT`

`JSON_LINT` represents the validation side of the architecture. Its purpose is to determine whether a particular JSON document satisfies the rules represented by a schema. It is therefore downstream from schema generation and upstream from actual content conversion. A successful lint operation means that the document is structurally acceptable to the validator, but it does not guarantee that every referenced runtime object or external asset exists. The distinction between structural validation and runtime correctness remains important throughout the system.

## `ScanImages`

`ScanImages` is responsible for resolving image representations. An image field can represent a relative path, a filename requiring a search, or an embedded representation such as Base64 depending on the loader functionality. The image scanner therefore converts an author-facing representation into usable image data. This is intentionally separate from card conversion so that a card model does not need to implement filesystem searching itself. The separation also makes it possible for different content formats to reuse the same artwork-resolution behavior.

## `XML_Parser`

`XML_Parser` connects generated XML documentation with the schema/documentation pipeline. C# projects can produce XML documentation containing descriptions associated with fields and members. The loader can read that information and use it as metadata when constructing author-facing schema information. This means that comments or structured documentation written near the source definitions can potentially become useful to people authoring JSON. The parser therefore exists at the boundary between developer-facing source documentation and generated tooling metadata.

## `TooltipDisector`

`TooltipDisector` has an unusual spelling, but its role is essentially to interpret the project's structured tooltip/documentation metadata. This matters because a schema containing only field names and primitive types is technically useful but not particularly friendly. Human-readable descriptions can tell an author what a field actually means, what values it accepts, or how it interacts with another property. The tooltip parser therefore helps transform source metadata into information that can accompany generated schemas and tooling. Its significance is architectural because it helps prevent the documentation system from becoming a completely separate manually maintained artifact.

## `Cores`, `Peripheral`, and `Subperipheral`

These names appear to represent architectural groupings rather than individual content formats. A reasonable interpretation is that core components contain central functionality, peripheral components provide supporting systems, and subperipheral components provide lower-level utilities used by those supporting systems. However, no maintainer-authored source located during this research explicitly states that this is the official etymology of those names. It would therefore be wrong to quote this interpretation as though it were project documentation. Their practical significance is the separation of concerns they represent, not the precise philosophical meaning of the labels.

---

# 8. All major Nightly type categories

The earlier report placed too much emphasis on `CardObject`, which risks making Nightly appear to be simply a new implementation of the old V1 card model. The architecture is considerably broader. It contains components concerned with plugin initialization, file discovery, schema generation, schema consumption, validation, image resolution, metadata extraction, and version-specific content handling. Those systems are important because they are precisely the reusable infrastructure that makes a multi-format loader practical. V1 and V2 support then sit on top of those shared facilities.

A useful category map is:

```text
Loader coordination
    Plugin

Filesystem
    FindFiles
    LoadFiles

Schema
    LoadSchema
    WriteSchema
    schema helpers

Validation
    LintingTools

Artwork
    ScanImages

Documentation / metadata
    XML_Parser
    TooltipDisector

V1
    JSONLoaderV1Support
    CardObject
    EvolveData
    TailData
    IceCubeData
    ability-related structures

V2
    JSONLoaderV2Support
    V2 Card representation
    StarterDeckInfo
    other V2-specific models

V3
    JSONLoaderV3Support

Organization
    Cores
    Peripheral
    Subperipheral
```

This inventory should be understood as a researched Nightly architecture snapshot rather than a promise that every class name remains identical in the current package. The Nightly package explicitly describes itself as a preview and directs readers toward the Wiki for more current documentation. The correct conclusion is therefore that Nightly introduced or reorganized these categories, while individual internal type names should be verified against the exact Nightly source version being targeted.

---

# 9. `CardObject` in depth

The V1 `CardObject` is especially useful for understanding the relationship between serialized JSON and runtime content. It contains the values necessary to describe a V1 card, but it is not itself the final Inscryption runtime card. Its fields form an intermediate contract that conversion code understands. This allows JSON parsing, image resolution, validation, and runtime conversion to be treated as separate responsibilities.

The early implementation exposes fields including:

```text
fieldsToEdit
name
displayedName
description
metaCategories
cardComplexity
gemColors
specialStatIcon
tribes
traits
abilities
specialAbilities
customAbilities
customSpecialAbilities
evolution
defaultEvolutionName
tail
iceCube
flipPortraitForStrafe
onePerDeck
appearanceBehavior
texture
altTexture
emissionTexture
titleGraphic
pixelTexture
decals
tailLostPortrait
```

The currently exposed Nightly documentation also explicitly documents `customAbilities` and `customSpecialAbilities` as V1 fields, which is a useful correction to an incomplete field inventory. It describes those fields as arrays of ability-specific data used for modded abilities rather than the ordinary vanilla `abilities` and `specialAbilities` fields. This demonstrates why the documentation should be treated as a living source alongside the early source snapshot.

The nested structures include:

```text
EvolveData
    name
    turnsToEvolve

TailData
    name
    tailLostPortrait

IceCubeData
    creatureWithin
```

The fields should not be viewed as arbitrary storage. Each one participates in the contract between the serialized V1 representation and the conversion system. Some values describe identity, some describe gameplay properties, some describe artwork, and some describe nested behaviors. This is why the object needs methods such as `GetImageFields()` and `Convert()`: the object is not simply a passive dictionary of values.

---

# 10. Every verified V1 `CardObject` function

## `GetValidFields()`

`GetValidFields()` returns the fields that the object considers valid for its representation. This gives the loader a centralized way to identify which properties belong to the object rather than scattering field-name knowledge throughout conversion code. A centralized field inventory is especially useful for an older format such as V1 because compatibility code needs to distinguish supported properties from arbitrary JSON properties. It can also support operations such as checking whether a requested field is eligible for editing. Without such a centralized mechanism, every validation or conversion routine would need to maintain its own list, creating multiple opportunities for those lists to disagree.

The architectural purpose is therefore larger than the method's small return value. The method effectively exposes the schema of the object at runtime. Code that needs to reason about fields can consult the object instead of duplicating the same information elsewhere. This makes `GetValidFields()` an example of how a small accessor supports broader maintainability. It also helps explain why Nightly's later schema infrastructure is so important: the more centrally the code defines its own field model, the easier it becomes to generate validation and authoring information from that model.

## `GetName()`

`GetName()` returns the internal identity associated with the card. This is different from `displayedName`, because the latter exists for the player-facing presentation while `name` is used to identify the underlying content object. A card can therefore display "Dragon" while its internal name contains a mod-specific prefix. This distinction becomes increasingly important when multiple mods create similarly named cards. The method is small, but the identity it exposes participates in lookup, creation, and modification behavior.

The importance of the method becomes clearer when considering `fieldsToEdit`. If the loader is being asked to modify an existing card, it needs to determine which existing object is the target before it can apply the requested fields. That makes the internal name a structural identifier rather than merely a label. In V2, the separation becomes even more explicit through `modPrefix`, which helps generate collision-resistant identities. Thus, `GetName()` sits at the intersection of content identity and loader behavior.

## `GetFieldsToEdit()`

`GetFieldsToEdit()` returns the explicit list of properties that should be overwritten when the JSON represents a modification rather than simply a new object. This mechanism is important because JSON documents often contain only a subset of the properties of an existing object. Without an explicit edit list, the loader would have to guess whether omitted properties should be preserved, defaulted, or overwritten. `fieldsToEdit` removes much of that ambiguity by telling the loader exactly which properties the author intends to mutate.

This also explains why `fieldsToEdit` should not be confused with a general-purpose duplicate merge system. The mechanism is designed around intentional modification of an identified object. An author who lists `displayedName` is communicating that the display name should be changed, while unrelated properties should not automatically be treated as part of the edit. The Nightly documentation explicitly describes this system as a way to overwrite selected fields of a base-game or modded item. That makes `GetFieldsToEdit()` one of the key functions for understanding JSONLoader's mutation semantics.

## `GetImageFields()`

`GetImageFields()` identifies which properties represent image assets. This is necessary because image fields require more processing than an ordinary scalar property. A value such as `"Art/Dragon.png"` is not useful to the runtime object until the loader resolves the path, reads the image, and constructs the appropriate texture representation. The loader therefore needs a way to distinguish image-bearing properties from strings that should remain ordinary textual data. `GetImageFields()` supplies that classification.

This separation also prevents the image subsystem from becoming tied to one specific card property. The image resolver can ask the object which fields require artwork handling and then process those fields generically. The result is a cleaner boundary between "find the asset" and "assign the asset." It also makes it possible for future content types to participate in the same artwork system without duplicating the entire file-search implementation.

## `SetImage(field, data)`

`SetImage(field, data)` takes resolved image information and associates it with the requested image property. The method therefore represents the second half of artwork processing. `GetImageFields()` identifies which properties need special treatment, while `SetImage()` gives the object a way to receive the result. This creates a useful separation between the filesystem-oriented image scanner and the content-oriented card model.

The method becomes particularly important when multiple image representations are supported. A field might originate from a relative path, a filename-only search, or Base64 data, but the card object should not need to care where the bytes came from. It only needs to receive the resolved image information in the form expected by the conversion system. This is a classic example of keeping input resolution separate from domain-object assignment.

## `Convert()`

`Convert()` is the bridge between the loader-side representation and the game/API-side representation. It takes the values stored in `CardObject` and uses them to create or configure the corresponding runtime object. This is the point at which abstract JSON-oriented data begins to become actual Inscryption content. The function therefore carries much more architectural significance than its simple name suggests. It is the boundary between the data model and the game model.

Keeping conversion separate from parsing provides several benefits. Parsing can focus on understanding JSON, validation can focus on structure, image handling can focus on assets, and conversion can focus on the game API. If these concerns were combined into one routine, debugging would become considerably harder because a malformed JSON field, a missing image, and an API registration problem could all appear as one enormous failure. `Convert()` represents the final transformation stage where those previously prepared values are applied to the runtime representation.

## `Convert(string[] FieldsToEdit)`

The overloaded conversion method adds selective mutation semantics. Rather than treating every populated property as something that should replace the corresponding runtime value, it receives the explicit field list that identifies the intended changes. This is what makes it suitable for override operations. The method can therefore distinguish between "this JSON contains a value" and "this JSON explicitly intends to overwrite the existing value."

That distinction is crucial for safe base-game modifications. If a mod only wants to change a card's description, it should not accidentally replace the card's abilities, costs, artwork, or other fields simply because those properties exist in some default representation. The field list acts as the author's explicit declaration of intent. This is one of the strongest reasons to treat `fieldsToEdit` as a semantic system rather than as just another JSON property.

## `ConvertBaseGame()`

`ConvertBaseGame()` handles the special case where the target is an existing base-game card rather than a newly created modded card. The underlying operation is conceptually different because the object already exists in the game's card database or API representation. The loader must therefore locate that existing object and apply the requested changes rather than constructing an unrelated new identity. This is why base-game modification deserves its own conversion path.

The distinction also helps explain why `modPrefix` is not always necessary. A new modded object needs collision-resistant identity, while a base-game override deliberately targets the existing game's identity. The stable documentation explicitly describes base-game editing as a special operation and states that the card name is used to identify the target. This function therefore represents a key boundary between creation semantics and mutation semantics.

---

# 11. Schema generation in depth

Nightly's schema architecture is one of the most important parts of the refactor because it attempts to make the loader's own data model usable by external tooling. A JSON Schema can describe property names, primitive types, arrays, nested objects, required fields, and other structural constraints. If that schema is generated from the same C# definitions that the loader itself uses, the code can become a source of truth from which validation and authoring tools are derived. This is substantially different from manually writing a second document that attempts to describe the code.

The conceptual pipeline is:

```text
C# class
   |
   +-- fields
   +-- field types
   +-- attributes
   +-- documentation
   |
   v
WriteSchema
   |
   v
JSON Schema
   |
   +--> validator
   +--> linter
   +--> JSON Editor
   +--> documentation
```

The reason this architecture matters is that schema generation creates leverage. A single field definition can potentially inform the loader about the field's type, inform the schema about the allowed structure, inform the linter about what should be accepted, and inform JSON Editor about what controls should be shown. Documentation metadata can further provide human-readable explanations. This reduces the number of independent artifacts that maintainers have to keep synchronized.

There is also a practical authoring benefit. If the schema says that `baseHealth` is an integer, an author can be warned when they accidentally write `"4"` as a string. If the schema says that `traits` is an array of strings, an author can be warned when they provide one string instead of an array. If a property contains a nested object, the schema can describe the nested structure rather than leaving the author to guess its shape. Schema generation therefore turns the loader's internal type model into an author-facing contract.

---

# 12. `WriteSchema` functions and their roles

The researched Nightly implementation contains helper operations associated with:

```text
CreateSchemaDirectors
GetWritable
GetRequired
HandleString
HandleInt
HandleBoolean
HandleArray
HandleObject
```

The exact helper inventory should not be treated as immutable because the Nightly branch is undergoing refactoring. The important point is what these operations collectively accomplish. They take reflected type information and metadata and translate it into JSON Schema structures. This means that primitive properties, arrays, and nested objects require different schema construction logic. The helper names correspond closely to those different structural cases.

## `CreateSchemaDirectors`

`CreateSchemaDirectors` initializes the internal structures used by the schema-generation process. A schema generator needs somewhere to accumulate the properties it discovers and the relationships between those properties. It also needs to know how the current object is represented in the schema and how nested definitions should be attached. Initialization therefore establishes the working context in which the rest of the schema-writing operations can operate.

The importance of this setup becomes more apparent when the generator encounters nested objects and arrays. A flat collection of property names is insufficient for representing something such as an evolution object containing its own `name` and `turnsToEvolve` properties. The generator needs a hierarchy of schema objects. `CreateSchemaDirectors` is therefore part of the infrastructure that allows the later handlers to build that hierarchy.

## `GetWritable`

`GetWritable` determines whether a reflected member should be exposed as an authorable property in the generated schema. This is significant because not every C# field necessarily represents something that should be written directly by a JSON author. Some members may be implementation details, calculated values, internal state, or otherwise inappropriate for serialized authoring. The schema generator therefore needs a way to distinguish author-facing properties from implementation-only members.

This filtering is one of the safeguards that prevents automatically generated schemas from becoming meaningless dumps of every member in a class. A useful authoring schema should expose the properties that the loader expects users to provide rather than every piece of internal state. Consequently, `GetWritable` participates in the boundary between the implementation model and the serialization model.

## `GetRequired`

`GetRequired` determines which properties should be represented as required by the schema. This is a deceptively important operation because the distinction between "property exists" and "property is mandatory" controls how much JSON an author must provide. For example, if `name` is required, an empty object should fail validation even though `{}` is perfectly valid JSON syntax. If a property is optional, the author may omit it and allow the loader to apply its default behavior.

The required-property system also influences tools such as JSON Editor. A schema that marks a property as required can cause the editor to present it as something the author must fill in. This means the method participates in both validation and user experience. It is therefore part of the bridge between the loader's actual expectations and the author's understanding of those expectations.

## `HandleString`

`HandleString` creates the schema representation for string-valued members. A JSON string is structurally simple, but a schema may contain additional information about it, such as a description or allowed values. The handler therefore does more than merely write `"type": "string"`. It can incorporate the metadata that the schema system has collected about the field.

String handling becomes especially important for fields that represent enumerations or identifiers. A field such as `temple` may technically be a string in JSON, but the meaningful values are constrained by the game and loader. Likewise, `name` is a string but functions as an identity. The primitive handler therefore establishes the basic type while other metadata can provide the more specific authoring rules.

## `HandleInt`

`HandleInt` generates the schema representation for integer properties. This distinction matters because JSON permits numbers, but the loader may expect a particular numeric type. A value such as `4` is structurally different from `"4"` because the latter is a string. Likewise, a value such as `4.5` is not an integer even though it is a valid JSON number.

The handler therefore helps the schema and linter distinguish valid numeric representations from incorrect ones. This is particularly important for fields such as `baseAttack`, `baseHealth`, costs, evolution turns, difficulty requirements, and unlock levels. Numeric validation can catch mistakes before they reach the game API.

## `HandleBoolean`

`HandleBoolean` generates schema information for true/false properties. A JSON boolean is represented as `true` or `false`, not as a quoted string. This matters for properties such as `onePerDeck`, `hideAttackAndHealth`, `flipPortraitForStrafe`, and various visibility or selection flags.

The handler therefore gives the validator a clear expectation about the property's type. It also allows authoring tools to render an appropriate boolean control rather than a generic text box. This illustrates the broader purpose of schema generation: the same type information can support both machine validation and human-facing authoring.

## `HandleArray`

`HandleArray` creates array schemas and recursively describes their element type. This is one of the more important operations because arrays are not sufficiently described by saying only that "this property is an array." The loader also needs to know what each element inside the array is supposed to look like. An array of strings, an array of integers, and an array of nested objects are all structurally different despite sharing the same outer JSON type.

For example:

```json
"traits": [
    "Beast"
]
```

requires a schema conceptually similar to:

```json
{
    "type": "array",
    "items": {
        "type": "string"
    }
}
```

But a nested object array could instead look like:

```json
"customAbilities": [
    {
        "ability": "SomeAbility",
        "parameter": 2
    }
]
```

The schema must then recursively describe the object inside each array element. `HandleArray` is therefore where the generator moves from describing the container to describing the contents of the container.

This recursive behavior is critical for complex JSONLoader structures. Starter decks contain arrays of deck objects, decks contain arrays of card names, encounters contain arrays of turns, and turns contain arrays of card information. Without recursive array handling, schema generation would stop at the outermost level and would be unable to describe the actual content structure. The function therefore represents a key part of Nightly's attempt to generate useful schemas rather than shallow type declarations.

## `HandleObject`

`HandleObject` creates nested object schemas and recursively describes their internal properties. This is necessary whenever a JSON property contains a structured object rather than a primitive value. V1's `evolution`, `tail`, and `iceCube` structures are straightforward examples. An object schema needs to describe not only that the property is an object but also which members exist inside it and what types those members have.

Conceptually:

```json
"evolution": {
    "name": "MyMod_Evolved",
    "turnsToEvolve": 2
}
```

becomes a schema tree:

```text
evolution
    type = object
        name
            type = string
        turnsToEvolve
            type = integer
```

The handler must therefore recurse into the nested object and invoke the appropriate primitive or complex handlers for its members. This is why schema generation is fundamentally a tree-building problem rather than a simple field-listing problem. `HandleObject` provides the machinery that allows the schema to preserve the hierarchy of the source model.

---

# 13. `LoadSchema` in depth

The early Nightly implementation exposes operations including:

```text
SchemaFolder
FindAndLoadSchema<T>(string LoaderName)
GetFullSchemaPath<T>(string LoaderName)
CreateAndOpenSchema<T>(string LoaderName)
CloseWriterAndFile(StreamWriter)
GetToolTips(List<FieldInfo>)
WriteJSONSchema<T>(string LoaderName)
```

These methods collectively represent the other side of the schema lifecycle. `WriteSchema` is concerned with generating the schema, while `LoadSchema` provides mechanisms for locating, opening, and using schema files. This separation matters because generated schemas may be consumed at a different point from when they are produced. It also allows schema files to become persistent artifacts that external tools can inspect.

## `SchemaFolder`

`SchemaFolder` represents the configured location where schema files are stored. This is important because schemas are not necessarily temporary objects existing only in memory. The Nightly configuration explicitly provides a Schema Save Path, with `/Schemas` documented as the default. The folder therefore becomes part of the tooling workflow rather than merely an internal implementation detail.

Having a defined schema folder also makes the relationship with external editors easier to understand. If JSON Editor needs a schema, the author can use the generated schema associated with the relevant loader type. The schema folder effectively gives the project a predictable place where those machine-readable definitions can be found.

## `FindAndLoadSchema<T>()`

`FindAndLoadSchema<T>()` attempts to locate and load the schema associated with a particular loader/type combination. The generic type parameter gives the method information about what object definition the schema is supposed to represent. The `LoaderName` argument provides additional identification for the particular loader subsystem. This lets the schema infrastructure distinguish between multiple content models rather than treating all JSON as though it shared one universal schema.

The method is therefore part of the runtime connection between generated schema information and actual validation. Once the appropriate schema has been located, the linter can use it to interpret a JSON document. This means that the method effectively resolves the question, "Which structural contract applies to this file?"

## `GetFullSchemaPath<T>()`

`GetFullSchemaPath<T>()` constructs the filesystem path at which a schema associated with a type and loader is expected to exist. This is a deceptively useful abstraction because filesystem layout should not be duplicated throughout the code. If the schema path convention changes, a centralized path-construction method can absorb that change.

The method also makes schema naming deterministic. A loader can calculate the expected location rather than searching blindly through the filesystem. This makes schema generation and schema loading two sides of the same convention. One creates the document at the known location, while the other knows how to locate it again.

## `CreateAndOpenSchema<T>()`

`CreateAndOpenSchema<T>()` creates the necessary schema output structure and opens it for writing. This operation is part of the generation pipeline rather than the validation pipeline. It ensures that the schema writer has a destination before it begins serializing the schema representation.

The distinction is useful because schema generation may involve several nested structures and a substantial amount of output. Opening the destination through one centralized routine means that file handling can remain separate from the logic that determines what properties belong in the schema. It also gives the loader one place to manage directory creation and stream setup.

## `CloseWriterAndFile()`

`CloseWriterAndFile()` finishes the file-writing phase and closes the associated stream. This may appear mundane, but reliable file handling is essential for generated schemas. A schema that is not properly finalized can be truncated or left inaccessible to later processes. It can also cause file handles to remain open and interfere with subsequent regeneration.

The method therefore marks the boundary between schema construction and completed schema output. Once the writer is closed successfully, the resulting file can be consumed by validators and external tools. In a development workflow where schemas may be regenerated repeatedly, predictable closure is particularly important.

## `GetToolTips()`

`GetToolTips()` extracts tooltip or documentation information from reflected fields. This provides the bridge between source metadata and the descriptions attached to schema properties. A property such as `baseHealth` can therefore have not only a type declaration but also a human-readable explanation. The resulting schema becomes much more useful to authors because they can understand what a field means without constantly switching to source code.

This is also why `XML_Parser` and `TooltipDisector` are relevant to schema generation. The schema system is not merely reflecting types; it is attempting to carry useful documentation forward into the authoring environment. The resulting pipeline can therefore be thought of as:

```text
source field
   |
documentation metadata
   |
TooltipDisector / XML_Parser
   |
schema property
   |
authoring tool
```

## `WriteJSONSchema<T>()`

`WriteJSONSchema<T>()` is the higher-level operation that asks the schema subsystem to construct a JSON Schema for a particular type and loader. It brings together reflection, field filtering, required-property determination, primitive handlers, array handling, object handling, and documentation metadata. The method is therefore the orchestration point for the schema-generation process.

Its importance is best understood by considering what would happen without it. Every new loader type would require a manually maintained schema document, and every change to the C# model would require a corresponding manual schema edit. Automatic generation attempts to reduce that duplication. The method therefore represents one of Nightly's clearest examples of turning implementation metadata into reusable tooling.

---

# 14. `LintingTools` in depth

The early Nightly source exposes a principal operation of the form:

```text
LintAgainstSchema<T>(
    string JSON,
    List<string> JSONSchema,
    string LoaderName
)
```

with helper operations including:

```text
GetTraversalPath
GetJSONSchemaProperty
GetObjectProperties
ValidatePropertyAgainstSchema
ValidateString
ValidateInteger
ValidateBoolean
ValidateObject
ValidateArray
```

The linter is fundamentally a recursive tree comparison system. JSON itself is a tree made from objects, arrays, strings, numbers, booleans, and null values. JSON Schema describes the expected structure of that tree. The linter walks through the JSON and repeatedly asks whether each node satisfies the corresponding schema rule.

Consider:

```json
{
    "name": "Dragon",
    "baseHealth": 4
}
```

The linter can conceptually process this as:

```text
root object
 |
 +-- name
 |    |
 |    +-- schema says string
 |
 +-- baseHealth
      |
      +-- schema says integer
```

If the document instead contains:

```json
{
    "name": "Dragon",
    "baseHealth": "four"
}
```

the JSON is still syntactically valid. The problem is that `baseHealth` is represented by a string where the schema expects an integer. The linter's value is precisely that it can identify this structural problem before the loader reaches the more complicated runtime-conversion stage.

---

# 15. `LintAgainstSchema` and recursive validation

`LintAgainstSchema` is more than a yes/no JSON parser because it must understand the relationship between the JSON tree and the schema tree. It has to identify the current traversal path, locate the corresponding schema property, determine the property's expected type, and then invoke the appropriate validation routine. This is why the helper methods are divided by type. Strings, integers, booleans, arrays, and objects each require different validation logic.

The traversal-path concept is particularly important for diagnostics. If an error occurs inside a nested object, a useful validator needs to tell the author where the error occurred rather than merely saying "invalid JSON." A path concept allows an error to be associated with something resembling:

```text
cards[3].abilities[1]
```

or:

```text
evolution.turnsToEvolve
```

depending on the actual structure. That turns validation from a binary gate into a debugging tool.

The recursive model also means that validation naturally follows the shape of the content. An array causes the linter to validate each item against the array's `items` schema. An object causes it to inspect the object's properties. A nested object can therefore contain another array, which can contain another object, and so on. This is why the schema generator and linter are conceptually complementary: the generator builds the tree of expectations, while the linter walks the author's tree against those expectations.

---

# 16. What the linter checks

The researched implementation checks structural concerns such as required properties, expected primitive types, nested objects, arrays, and additional-property behavior. This means it can catch a surprisingly broad class of authoring mistakes. A missing required field is different from an incorrect field type, which is different again from an unexpected property. The validator can distinguish these cases because the schema contains the information needed to make those comparisons.

For example:

```json
{
    "name": "Dragon",
    "baseHealth": 4
}
```

can satisfy a schema expecting a string `name` and integer `baseHealth`.

By contrast:

```json
{
    "name": "Dragon",
    "baseHealth": "4"
}
```

contains a type mismatch.

And:

```json
{
    "name": "Dragon",
    "unknownProperty": true
}
```

may produce an additional-property error if the schema disallows properties that are not explicitly defined. The exact behavior depends on the generated schema and loader configuration, but the architecture provides the mechanism for making that distinction.

---

# 17. What the linter cannot guarantee

A schema validator can establish structural correctness, but structural correctness is not the same thing as successful runtime loading. Consider:

```json
{
    "name": "Dragon",
    "texture": "Art/DoesNotExist.png"
}
```

The JSON can be perfectly valid and can satisfy the schema's requirement that `texture` be a string. Nevertheless, the referenced image may not exist. The same issue occurs when a card references an ability, tribe, card, or other runtime object that has not been registered. The schema generally cannot know whether the external game object exists at runtime.

The distinction can therefore be expressed as:

```text
JSON syntax valid
        ≠
schema valid
        ≠
runtime valid
        ≠
gameplay correct
```

These are four different levels of correctness. JSON syntax asks whether the document can be parsed. Schema validation asks whether the document has the expected structural shape. Runtime loading asks whether the loader can resolve every dependency and successfully construct the content. Gameplay correctness asks whether the resulting object behaves as the author intended. A strong debugging process checks these levels separately rather than treating every failure as "bad JSON."

---

# 18. File loading in full detail

File loading is one of the areas where Nightly's refactor becomes easiest to appreciate. A traditional loader can make file discovery, parsing, validation, asset loading, and object construction look like one giant operation. Nightly instead exposes these responsibilities as separate architectural stages. This means the same discovery mechanism can potentially feed V1, V2, V3, and CSV support. It also means configuration can control where files are searched without requiring each content format to implement its own directory scanner.

The documented default JSON origins are:

```text
Scripts
Plugins/Scripts
Cards
Plugins/Cards
```

while the default CSV origins are:

```text
Sheets
Plugins/Sheets
```

The documentation states that these paths are relative to the mod-specific folder under `plugins` and that JSONLoader recursively loads JSON files from the configured origins. This makes the configuration system more than a convenience setting. It defines the filesystem boundary within which the generic discovery mechanism operates.

---

# 19. Stage 1: Plugin initialization

The first stage is BepInEx initialization. BepInEx discovers the Nightly plugin and invokes its startup path. The plugin then establishes the configuration, logging, and loader infrastructure required by later stages. At this point no individual card necessarily needs to have been converted yet. The system is preparing itself to interpret content.

This separation is important because configuration must exist before discovery can occur. The loader cannot know which directories to scan until its origin settings have been initialized. Likewise, logging must be established before file-processing errors can be reported consistently. Initialization is therefore the foundation upon which the later file pipeline operates.

---

# 20. Stage 2: Configuration

The configuration system determines where JSON and CSV files should be searched for and where schemas should be stored. The current Nightly documentation lists separate settings for JSON Loading Origination Path, CSV Loading Origination Path, Schema Save Path, verbose logging, additional information, summary information, and recursive plugin-level scanning.

The defaults are:

```text
JSON:
Scripts, Plugins/Scripts, Cards, Plugins/Cards

CSV:
Sheets, Plugins/Sheets

Schema:
 /Schemas
```

The JSON origin configuration is particularly useful because it allows a mod author to keep a familiar folder structure without forcing the user to manually configure every mod. The documentation explicitly says the default paths are intended to make mods work without user configuration.

---

# 21. Stage 3: File discovery

`FindFiles` searches the configured locations for candidate files. Its job is to identify files rather than understand their contents. This is important because a generic filesystem layer can operate without knowing what a card ability or encounter means. It only needs to know which extensions represent supported loader inputs.

The distinction also makes recursive scanning easier to reason about. The configuration determines the starting locations, and the finder determines whether the configured scan should recurse through subdirectories. The Nightly documentation additionally exposes a compatibility option called `Recursively Scan At Plugin Level`, which allows the finder to recurse from the plugin level rather than only from the configured path levels. This option exists specifically to accommodate older or unusual mod folder structures.

---

# 22. Stage 4: Classification

Once candidate files have been discovered, the loader has to determine what format they represent. Conceptually:

```text
.jldr
    → V1

.jldr2
    → V2

.jldr3
    → V3 pathway

.csv
    → CSV pathway
```

The extension establishes the broad loader generation, but V2 also uses filename conventions to identify particular content subsystems. For example, starter decks and encounters use special suffixes. The current Nightly documentation similarly explains that different JSONLoader support sections correspond to different kinds of data.

Classification therefore happens at more than one level. The file extension tells the system which generation of loader should understand the document, while filename conventions and document structure can determine which specific object model should receive it. This is why it is inaccurate to say that every `.jldr2` file is simply a card.

---

# 23. Stage 5: Example-file filtering

Nightly retains explicit handling for `_example` files. This is important because documentation and source repositories commonly ship examples alongside actual mod content. If the loader indiscriminately loaded every supported file, example documents could accidentally become real cards, decks, tribes, or other runtime objects. The `_example` convention therefore provides a simple mechanism for keeping instructional material in a package without treating it as production content.

This feature also illustrates why generalized file discovery needs content-aware filtering. A filesystem scanner can find the file, but a later loader stage needs to decide whether that file should actually enter the content pipeline. The same principle applies to other forms of exclusion or classification. Discovery answers what exists, while loading determines what should be interpreted.

---

# 24. Stage 6: Parsing

After classification and filtering, the relevant support layer parses the document. V1 parsing creates a representation appropriate for the V1 card model, while V2 parsing understands V2-specific structures such as `modPrefix`, starter decks, tribes, and encounters. A CSV pathway can interpret rows and columns rather than JSON objects. The generic loader infrastructure does not need to understand all of these details because those details belong to the format-specific support layer.

This is one of the major benefits of the architecture. If the same filesystem and logging system can feed different parsers, a new format does not need to reinvent basic plugin discovery. Likewise, changes to the filesystem configuration can potentially benefit every supported format simultaneously. The format layer remains focused on what makes that format different.

---

# 25. Stage 7: Schema validation

Where schema validation applies, the parsed document can be checked against the appropriate schema before conversion proceeds. This allows structural problems to be reported while the information is still in a form that can be tied directly to JSON properties. A type mismatch can therefore be reported as a JSON problem instead of becoming an obscure runtime conversion failure.

This stage is especially valuable for complex nested structures. An encounter document can contain turns, which can contain card information, which can contain several numeric and string properties. Without recursive schema validation, an error deep inside that structure could be difficult to diagnose. With schema validation, the loader can compare each nested node against the corresponding structural expectation.

---

# 26. Stage 8: Object construction

After parsing and validation, the document becomes an intermediate representation such as `CardObject` or a V2-specific object model. This is the point at which the loader has translated generic serialized data into a typed representation it knows how to convert. The intermediate representation provides a stable place to perform operations such as image assignment and field-specific transformation.

This stage is important because JSON is deliberately generic. The runtime API is not. A JSON string such as `"Nature"` has meaning only after the loader interprets it as the appropriate enum or game concept. The intermediate object therefore represents the stage at which generic serialization becomes domain-specific data.

---

# 27. Stage 9: Image resolution

Artwork fields require additional processing. A path such as `"Art/Dragon.png"` must be resolved relative to the appropriate plugin location, checked for existence, read, and converted into the representation expected by the runtime object. Nightly's development history also records support for Base64 images and filename-only recursive lookup. The latter allows a filename to be supplied without necessarily specifying the complete relative path, although explicit paths remain easier to reason about.

The separation between image scanning and card conversion is important here. The card model should not need to know how the filesystem is searched. Instead, the image subsystem can resolve the asset and then provide the result to the object through operations such as `SetImage`. This keeps asset resolution reusable across content formats.

---

# 28. Stage 10: Conversion

Conversion transforms the loader-side representation into the corresponding runtime/API representation. This is where fields such as attack, health, abilities, tribes, artwork, costs, and other properties stop being abstract JSON data and become actual game configuration. The conversion process may also have to resolve names into existing objects or map strings onto enums and other runtime types.

Because conversion is downstream from validation, it can assume a greater degree of structural correctness. It still cannot assume that every external dependency exists, however. A valid string can still refer to an invalid ability or missing card. This is why runtime diagnostics remain necessary even when schema validation succeeds.

---

# 29. Stage 11: API registration

The final stage is interaction with the underlying Inscryption modding API. The loader either creates new content or modifies an existing object depending on the semantics of the document. This is where JSONLoader's relationship with the Inscryption API becomes clear. JSONLoader is not itself the entire game's modding API. It is a declarative content-loading layer that ultimately relies on the API to produce or modify runtime objects.

The resulting architecture is therefore:

```text
JSON
  ↓
JSONLoader
  ↓
Inscryption API
  ↓
runtime content
```

This also explains why JSONLoader versions are historically tied to API generations. When the underlying API changes significantly, the loader's conversion layer may need to change even if the author-facing JSON remains superficially similar.

---

# 30. Why `FindFiles` and `LoadFiles` are separate

Separating discovery from loading prevents every format from developing its own filesystem implementation. Without this separation, the architecture could gradually become:

```text
V1 file scanner
V2 file scanner
V3 file scanner
CSV scanner
```

Each scanner could develop slightly different recursion rules, exclusion rules, path handling, and logging behavior. Such duplication is particularly dangerous in a framework because users would have to remember different folder conventions depending on which content type they were creating.

Nightly instead aims for:

```text
one discovery system
       |
       +--> V1
       +--> V2
       +--> V3
       +--> CSV
```

This means a filesystem-level feature can potentially benefit every format. The configuration system's separate JSON and CSV origins are a concrete example of this generalized approach.

---

# 31. Image loading in depth

Nightly supports multiple conceptual forms of image input. The simplest is an explicit relative path, such as:

```json
"texture": "Art/Dragon.png"
```

This gives the loader a deterministic location to search. The second form is filename-oriented lookup, where the author supplies a filename and the Nightly implementation can recursively search the plugin area. The development changelog records filename-only image lookup as a feature added during the early Nightly releases. The third form is Base64 data, which embeds the image representation directly into the JSON.

Each representation has different maintenance consequences. Relative paths keep JSON small and allow artwork to be edited independently of the data file. Base64 makes a JSON document more self-contained but can make the document much larger and harder to inspect manually. Filename-only searching is convenient but less explicit because multiple files could potentially share the same name. For long-lived mods, explicit relative paths are therefore generally easier to audit.

---

# 32. V1 in depth

V1 is the original JSONLoader generation and is fundamentally card-focused. Its file extension is `.jldr`, and its feature set is much narrower than the later V2 system. The current Nightly documentation describes V1 as supporting cards exclusively with limited modded-library support and explicitly characterizes it as a maintenance version rather than a generation intended for new feature development.

The V1 design is also visibly different from V2. Several concepts are represented as nested objects, including evolution, tail, and IceCube information. V1 also predates the more systematic V2 identity model built around `modPrefix`. This means V1 is valuable not only historically but architecturally because it shows the kind of card-centric representation that V2 subsequently reorganized.

---

# 33. V1 fields in detail

The current Nightly documentation identifies V1 fields including:

```text
fieldsToEdit
name
displayedName
description
metaCategories
cardComplexity
gemColors
specialStatIcon
tribes
traits
specialAbilities
abilities
customAbilities
customSpecialAbilities
evolution
defaultEvolutionName
tail
iceCube
flipPortraitForStrafe
onePerDeck
appearanceBehavior
texture
altTexture
tailLostPortrait
```

The documentation describes `name` as the in-code identity and recommends a unique prefix for new cards. `displayedName` is the player-facing name, while `description` provides card flavor text. `metaCategories`, `traits`, `tribes`, `abilities`, and `specialAbilities` are represented as arrays of names, with V1's support for some categories being limited to vanilla values.

Artwork fields are particularly concrete. The documentation describes `texture`, `altTexture`, and tail-related artwork as paths localized to the Plugins folder and identifies PNG requirements for those assets. This demonstrates that JSONLoader is not only a data parser but also an asset-resolution system. The loader has to turn those path strings into actual textures that can be assigned during conversion.

---

# 34. V1 nested objects

## `EvolveData`

`EvolveData` represents the two pieces of information required for the V1 evolution structure: the card that the current card becomes and the number of turns required before the transformation. The nested form makes the relationship explicit because both values belong to one conceptual behavior. It also means the schema has to describe an object inside the card rather than simply two independent primitive fields.

A representative structure is:

```json
{
    "name": "MyMod_EvolvedCard",
    "turnsToEvolve": 2
}
```

The exact accepted values depend on the loader and the referenced card. The important structural point is that `evolution` is an object and its children have different types. The schema therefore needs to represent both the nested object and the integer field inside it.

## `TailData`

`TailData` represents information associated with the loose-tail behavior. It contains the identity of the tail-related card and the portrait that should be used after the tail is lost. This means the object combines a gameplay identity with an artwork reference. The loader must therefore handle both ordinary string data and image resolution as part of the conversion process.

A representative structure is:

```json
{
    "name": "MyMod_Tail",
    "tailLostPortrait": "Art/TailLost.png"
}
```

The object is important architecturally because it demonstrates why nested schema handling is necessary. One property of the card contains another structured object, and one of that object's properties is itself an artwork path.

## `IceCubeData`

`IceCubeData` identifies the card associated with the IceCube behavior. The Nightly documentation describes `creatureWithin` as the in-code name of the card that the IceCube will leave behind. The property is therefore a string identity rather than an arbitrary display name. The loader must eventually resolve that identity into the corresponding runtime card relationship.

A representative structure is:

```json
{
    "creatureWithin": "MyMod_Creature"
}
```

The documentation also notes that the behavior has a default when left empty in the relevant V1 implementation. This is a good example of why schema validity and gameplay behavior are different concepts. An empty value may be structurally accepted while causing the runtime system to apply a default.

---

# 35. V2 in depth

V2 represents the major expansion of JSONLoader. It was rewritten for Inscryption API 2.0 and uses `.jldr2`. Unlike V1, it is not limited to cards and eventually became the foundation for a much broader content-authoring system. Starter decks, Configils, tribes, encounters, talking cards, regions, items, and other features were added over the V2 release series.

One of the most important architectural changes was the explicit separation of `name` and `modPrefix`. V2 treats the prefix as an in-code identifier that participates in the final internal identity. This makes collision avoidance a first-class concern rather than something left entirely to individual authors. The current Nightly documentation describes the same V2 distinction, stating that `name` is the part after `modPrefix` and `modPrefix` is the in-code identifier preceding it.

---

# 36. `modPrefix` in depth

Suppose an author writes:

```json
"name": "Dragon",
"modPrefix": "MyMod"
```

The loader conceptually treats the resulting identity as:

```text
MyMod_Dragon
```

The exact internal implementation should be checked against the target version, but the identity principle is stable in the documented V2 model. The player-facing name can still be simply `"Dragon"`. This means the internal identity and displayed name serve different purposes.

That separation is critical because multiple mods can reasonably want to create a card called "Dragon." If both simply use the same internal identity, the loader and game have no reliable way to distinguish them. If each uses a unique prefix, the internal identities become different while the player-facing names can remain identical. `modPrefix` is therefore not merely a naming convention. It is part of JSONLoader's collision-avoidance model.

---

# 37. V1 versus V2 card representation

V1 commonly represents certain behaviors through nested objects:

```text
evolution
    ├── name
    └── turnsToEvolve

tail
    ├── name
    └── tailLostPortrait

iceCube
    └── creatureWithin
```

V2 flattens several of these relationships into fields such as:

```text
evolveIntoName
evolveTurns
tailName
tailLostPortrait
iceCubeName
```

The flattening is not merely a cosmetic rewrite. It changes the shape of the serialized contract and therefore affects schemas, editors, conversion code, and compatibility. It also makes certain common card properties easier to read because related values are placed directly on the card object. This is one example of why a V2 document should not be assumed to be a V1 document with a different file extension.

---

# 38. V2 card fields in detail

The documented V2 model includes:

```text
fieldsToEdit
name
modPrefix
displayedName
description
metaCategories
cardComplexity
temple
baseAttack
baseHealth
hideAttackAndHealth
bloodCost
bonesCost
energyCost
gemsCost
specialStatIcon
tribes
traits
abilities
specialAbilities
evolveIntoName
evolveTurns
defaultEvolutionName
tailName
tailLostPortrait
iceCubeName
flipPortraitForStrafe
onePerDeck
appearanceBehaviour
texture
altTexture
emissionTexture
pixelTexture
titleGraphic
decals
extensionProperties
```

The current Nightly documentation confirms several of these fields and provides explanations for their types and meanings. For example, `temple` is a string, attack and health are integers, cost fields are integers, and `gemsCost` is an array of gem-color names.

One subtle compatibility issue is spelling. V1 uses `appearanceBehavior`, while the documented V2 field is `appearanceBehaviour`. JSON keys are exact strings, so a spelling difference is not something a parser should be expected to "understand automatically." This is precisely why schema validation is useful when migrating between generations. The schema can expose the exact property names expected by the target loader.

---

# 39. Exact JSON examples: evidence levels

The earlier report correctly recognized that examples need qualification, but the distinction deserves to be made even more explicitly. There are at least three categories of JSON example:

```text
1. Official published example
2. Source/schema-derived structure
3. Illustrative example
```

An official published example is the strongest evidence for how a documented feature is intended to be written. A source/schema-derived example can be technically precise for the examined implementation but may still be tied to a particular Nightly build. An illustrative example is useful for teaching concepts but should never be described as an exact drop-in document unless the schema or source has been checked.

This distinction is especially important for card objects. A card schema can contain many optional properties, and the stable documentation explicitly says that the name is required while other fields can have defaults. Therefore, a huge JSON object containing every possible property can actually be less useful than a minimal object containing only the values the author intends to change. The report consequently uses official documented examples where available and labels schema-shaped card examples as representative.

---

# 40. Official V2 starter-deck structure

Starter decks are a good example of a structure that can be quoted with considerably greater confidence because the V2 documentation explicitly defines the root object and its `decks` array. A documented structure is:

```json
{
    "decks": [
        {
            "name": "DeckName1",
            "iconTexture": "icon.png",
            "cards": [
                "Card1",
                "Card2",
                "Card3"
            ]
        },
        {
            "name": "DeckName2",
            "iconTexture": "icon2.png",
            "cards": [
                "Card4",
                "Card5",
                "Card6"
            ]
        }
    ]
}
```

The significance of this example is not merely that it shows syntax. It demonstrates that V2 uses different root models for different content systems. An author who expects every `.jldr2` file to have a card-like root object will therefore misunderstand the format. Starter decks have a collection-oriented root containing `decks`, and each deck has its own object structure.

The current Nightly documentation similarly defines `decks` as a `StarterDeckInfo` array and documents fields such as `name`, `modPrefix`, `title`, `cards`, `iconTexture`, and `unlockLevel`. This provides a useful example of how a V2 content model can be represented in a schema and then validated recursively.

---

# 41. V2 starter decks in depth

A starter-deck file is identified using the documented `_deck.jldr2` naming convention. The root contains a `decks` array, meaning the document can define multiple starter decks rather than representing only one deck. Each deck has its own internal identity, display title, card list, icon, and unlock level. This is different from ordinary card JSON because the card is no longer the top-level unit of serialization.

The `cards` array contains card identities rather than complete card objects. That means the deck definition assumes that those cards already exist or will exist by the time the deck is registered. This is an example of a cross-object reference inside JSONLoader. Schema validation can verify that the array contains strings, but it cannot by itself guarantee that every referenced card exists in the runtime card registry.

---

# 42. V2 tribes

Tribe documents use a dedicated root structure containing a `tribes` array. A documented example is:

```json
{
    "tribes": [
        {
            "name": "TribeName1",
            "guid": "YourModGuid",
            "tribeIcon": "tribeicon_custom1.png",
            "appearInTribeChoices": true,
            "choiceCardBackTexture": "card_rewardback_custom1.png"
        },
        {
            "name": "TribeName2",
            "guid": "YourModGuid",
            "appearInTribeChoices": false
        }
    ]
}
```

The structure demonstrates several recurring JSONLoader patterns. A root collection contains objects, each object has identity fields and optional presentation fields, and artwork is represented by paths. The schema must therefore recursively describe an array of objects. The loader must also resolve the artwork paths and eventually register the tribe through the underlying API.

The documentation further notes behavior concerning choice-card-back textures. This illustrates why an author should not assume that every field must always be supplied merely because it exists in the schema. Some properties can have defaults or derived behavior. The exact behavior should be checked against the documentation and schema for the loader version being targeted.

---

# 43. V2 encounters

Encounter files use the documented `_encounter.jldr2` naming convention and have a substantially nested structure:

```json
{
    "name": "",
    "minDifficulty": 0,
    "maxDifficulty": 0,
    "regions": [""],
    "dominantTribes": [""],
    "randomReplacementCards": [""],
    "redundantAbilities": [""],
    "turns": [
        {
            "cardInfo": [
                {
                    "card": "",
                    "randomReplaceChance": 0,
                    "difficultyReq": 0,
                    "difficultyReplacement": ""
                }
            ]
        }
    ]
}
```

This is an excellent example of why recursive schema generation matters. The root is an object. `regions` is an array of strings. `turns` is an array of objects. Each turn contains `cardInfo`, which is another array of objects. Those objects then contain strings and numeric values.

A shallow schema system would struggle to describe this accurately. Nightly's object and array handlers are designed precisely for this kind of nested structure. The linter can then walk through the same hierarchy when validating an encounter. This demonstrates that the schema infrastructure is not merely a convenience for cards. It is a foundation for describing arbitrarily nested content models.

---

# 44. V2 content beyond cards

V2's historical expansion is one of the strongest reasons not to treat JSONLoader as merely a card serializer. The release history shows additions for starter decks, Configils, card and sigil reloading, tribes, encounters, gramophones, talking cards, masks, languages, translations, encounter overrides, emissions, custom tribes, partial card overrides, regions, power statistics, traits, items, bottled cards, Base64 textures, and additional serialized data types.

The important point is that these additions were not all introduced simultaneously. V2 grew incrementally, which means the mature stable implementation contains a large amount of accumulated behavior. Nightly therefore cannot be evaluated solely by asking whether it has a "V3 card format." Its broader purpose is to create an architecture capable of hosting many kinds of content without continuing to accumulate unrelated infrastructure inside one monolithic implementation.

---

# 45. V1 release history, version by version

The published V1 inventory is:

```text
1.0.1
1.1.0
1.1.1
1.2.0
1.2.1
1.3.3
1.3.5
1.3.6
1.3.7
1.3.8
1.3.9
1.3.10
1.3.11
1.4.0
1.5.0
1.5.1
1.5.2
1.5.3
1.6.0
1.6.1
1.7.0
1.7.1
1.7.2
```

The historical changelog does not provide an equally detailed functional description for every patch release. It is therefore important not to manufacture a feature for a version merely because the version exists. Where the changelog identifies a distinct feature or fix, that feature is described below. Where it does not, the release is identified as a maintenance release rather than assigned an invented purpose.

## 1.0.1

1.0.1 represents the early published V1 baseline. The available historical material does not provide enough evidence to construct a complete field-by-field feature list for that specific patch. It should therefore be treated as the starting point of the published V1 line rather than ascribed undocumented features. The broader V1 model establishes that the system was card-focused. Later releases demonstrate how that initial model was expanded and repaired.

## 1.1.0

1.1.0 is an early V1 release for which the available changelog evidence does not justify attributing a distinct major feature. It belongs to the period in which the loader's basic card model was being maintained and developed. It is therefore safer to describe it as an early V1 maintenance/development release. This approach avoids confusing the existence of a version with evidence of a particular feature.

## 1.1.1

1.1.1 is another early maintenance/compatibility release. The available source material does not expose a sufficiently precise feature description to justify inventing one. Its historical significance is therefore primarily that it belongs to the pre-1.2 V1 development sequence. The first clearly documented structural expansion appears with 1.2.0.

## 1.2.0

1.2.0 added the evolution, tail, and IceCube parameter structures. This is a major structural milestone because these behaviors require more than the flat card properties used by simpler card definitions. The addition of nested data objects meant that the loader had to represent relationships between a card and other cards or assets. These structures later became part of the compatibility surface that Nightly still has to understand.

## 1.2.1

1.2.1 addressed API compatibility. This is important historically because it demonstrates that JSONLoader has always had to track the underlying Inscryption API. A loader can preserve its JSON syntax while still needing changes to its conversion layer when the underlying API evolves. This precedent is useful when interpreting the later Nightly refactor.

## 1.3.3

1.3.3 is a published V1 maintenance release. The available changelog evidence does not provide a distinct feature description sufficient to characterize it more specifically. It should therefore be treated as part of the incremental stabilization of V1. The absence of a feature note is not evidence that nothing changed internally, only that the published historical record does not provide a reliable feature-level description.

## 1.3.5

1.3.5 is another published V1 maintenance release. No separate major functionality is safely attributable from the available changelog material. It belongs to the period in which the existing V1 architecture was being repaired and refined. It should not be assigned a fabricated feature simply to make the release table appear more complete.

## 1.3.6

1.3.6 is a published maintenance release. The available record does not justify a distinct feature claim for this patch. Its inclusion is nevertheless important because the user-requested research concerns the complete published version sequence rather than only major versions. This illustrates why release-history research needs to distinguish release inventory from feature inventory.

## 1.3.7

1.3.7 is another maintenance release in the V1 sequence. The available changelog evidence does not identify a sufficiently specific major feature to report. It therefore represents incremental development between the better-documented changes of the surrounding releases. This distinction is maintained throughout the report.

## 1.3.8

1.3.8 addressed texture-related problems. This matters because artwork is a significant part of JSONLoader's functionality and image fields are processed differently from ordinary strings. A texture assignment bug can therefore prevent an otherwise structurally valid card from appearing correctly. The fix is also part of the historical path toward Nightly's later centralized image-scanning architecture.

## 1.3.9

1.3.9 addressed further texture assignment behavior. The repeated attention to artwork demonstrates that image handling was already a significant source of loader complexity during V1. This becomes relevant later because Nightly separates image scanning from content parsing rather than treating image paths as ordinary card strings. The history therefore supports the architectural motivation for a reusable artwork subsystem.

## 1.3.10

1.3.10 added or repaired PNG validation. This means the loader began treating artwork files as something that could be checked rather than blindly assumed to be valid. Such validation is an early example of moving failures closer to the point where authors can understand them. It also foreshadows the broader Nightly philosophy of validating data before attempting runtime conversion.

## 1.3.11

1.3.11 fixed an issue associated with the PNG check. This is another example of the difference between adding a feature and making that feature reliable. Validation logic can itself contain bugs, so the release history records the normal maintenance process of introducing and correcting tooling. It also reinforces that image handling has long been part of JSONLoader's compatibility surface.

## 1.4.0

1.4.0 replaced Unity's `JSONUtility` approach with TinyJson. Parser choice matters because different serializers have different behavior around types, missing values, arrays, and object construction. Changing parsers can therefore affect the compatibility of existing JSON even when the visible file extension remains unchanged. This release is consequently more architecturally significant than its version number might suggest.

## 1.5.0

1.5.0 was a substantial V1 maintenance and refactoring release. It included API 1.11 compatibility, improved error checking, default-deck fallback behavior, changes involving base-game health and meta-categories, and handling around evolution and tail data. The release also involved parser and utility changes. This demonstrates that V1 had already become more than a trivial JSON-to-card converter and required a meaningful amount of compatibility logic.

## 1.5.1

1.5.1 is a maintenance release in the V1 line. The available changelog does not provide a sufficiently distinct feature description to attribute a major addition. It belongs to the stabilization sequence following the larger 1.5.0 changes. Treating it as maintenance rather than inventing a feature is the most defensible historical description.

## 1.5.2

1.5.2 is another V1 maintenance release. No independently verified major feature is attached to it here because the available changelog evidence does not justify one. This is consistent with the way patch releases should be represented in a technical history. A complete version inventory does not require every patch to have an invented narrative.

## 1.5.3

1.5.3 continues the V1 maintenance sequence. The available historical information does not identify a distinct major feature for this version. It is therefore included as a published release but not assigned unsupported behavior. This distinction keeps the release history factual rather than speculative.

## 1.6.0

1.6.0 added custom ability support. This was a significant expansion because cards could now participate in modded ability systems rather than being restricted to the existing vanilla ability set. The loader therefore had to represent additional ability information and integrate it with the underlying API. This is an early example of JSONLoader moving toward an extensible modding layer rather than merely serializing vanilla card properties.

## 1.6.1

1.6.1 fixed handling associated with empty abilities. This may appear minor, but empty collections are a common edge case in declarative formats. A loader must distinguish between "no abilities were supplied," "an empty ability list was supplied," and "the field is malformed." Fixing such behavior improves reliability for both minimal cards and generated documents.

## 1.7.0

1.7.0 included a temple-related fix, custom special abilities, custom `.jldr` behavior, `bloodCost`, utility refactoring, and cleanup of redundant evolution/tail variables. The release therefore represents another step toward a more capable V1 model. It also shows the beginnings of the tension that eventually motivates a larger rewrite: the loader is accumulating special cases, new content types, and compatibility logic within a format that began as a relatively focused card system.

## 1.7.1

1.7.1 addressed ancillary discrepancies and maintenance issues. The available record does not support assigning a separate major feature to this release. It should therefore be understood as part of the stabilization process around the final V1 line. Its significance is primarily historical because it precedes the final 1.7.2 maintenance release.

## 1.7.2

1.7.2 introduced `_example` exclusion behavior. This feature became important to the later generalized loader because mod packages frequently contain documentation or example files that should not become actual runtime content. The mechanism illustrates the need for file-level semantics beyond simply "load every supported extension." Nightly subsequently retained this concept in its broader file-discovery architecture.

---

# 46. V2 release history, version by version

The published V2 inventory is:

```text
2.0.0
2.0.1
2.1.0
2.1.1
2.2.0
2.2.1
2.2.2
2.2.3
2.2.4
2.2.5
2.3.0
2.3.1
2.4.0
2.4.1
2.4.2
2.4.3
2.4.4
2.4.5
2.5.0
2.5.1
2.5.2
2.5.3
2.5.4
2.6.0
2.7.0
```

V2 is substantially easier to describe version by version because its changelog records a sequence of clearly identifiable feature expansions. The resulting history shows why stable 2.7.0 contains such a broad feature set. It also explains why Nightly should not be assumed to have complete feature parity merely because it is the next architectural generation.

## 2.0.0

2.0.0 was the major rewrite for Inscryption API 2.0. It introduced `.jldr2` and broke backward compatibility by default, while providing a mechanism for older JLDR content to be converted or supported. This is a fundamental version boundary rather than an ordinary feature release. It demonstrates that JSONLoader has historically treated major API changes as opportunities to redesign its serialization and conversion architecture.

## 2.0.1

2.0.1 fixed problems involving JLDR-to-JLDR2 conversion and base-game card editing. The base-game editing behavior also moved toward directly modifying the existing card rather than relying on the earlier event-based approach. This distinction is important because it established the direct-edit model later represented by `fieldsToEdit`. The release therefore strengthened the semantic separation between creating new content and changing existing content.

## 2.1.0

2.1.0 added starter-deck support. This was the first major step beyond card-centric JSON because a starter deck is a collection-level object containing references to multiple cards. The loader consequently needed a new root structure and new object model. This release provides an early example of why V2 eventually required a more generalized architecture.

## 2.1.1

2.1.1 added Configils. Configils introduced behavior and configuration beyond static card definitions. The loader therefore expanded into systems where JSON could describe more than the properties of a card. This feature helped establish V2 as a general mod-content loader rather than simply a card serializer.

## 2.2.0

2.2.0 added an API for adding cards. This is important because it indicates that JSONLoader itself was developing an API-facing programming layer in addition to its file format. The distinction becomes relevant when considering Nightly compatibility: file-format compatibility and code-level API compatibility are separate concerns. A mod that calls an old API method may need changes even if its JSON files remain valid.

## 2.2.1

2.2.1 added card and sigil reloading and addressed Configil-related issues. Reloading is particularly useful during development because authors can iterate on data without restarting the entire game for every small change. It also increases the importance of predictable file discovery and state management. This is another example of the stable V2 system accumulating practical authoring features.

## 2.2.2

2.2.2 added tribe support. Tribes are shared classification objects rather than properties belonging exclusively to one card. This required the loader to create and register a new category of game content. The feature also laid groundwork for later interactions between custom tribes and cards.

## 2.2.3

2.2.3 added encounter support and introduced `GetSlot()` behavior. Encounters are substantially more nested than ordinary cards because they contain turn structures and card information. This release therefore increased the complexity of the JSON object model. It is one of the clearest historical examples of why recursive schema generation and validation become increasingly valuable as the loader grows.

## 2.2.4

2.2.4 added gramophone support. This demonstrates continued expansion into non-card content. Each new system increases the number of object types and file conventions the loader must understand. The historical accumulation of these systems is one of the reasons a generalized architecture becomes attractive.

## 2.2.5

2.2.5 was a maintenance release. The available historical material does not justify attaching a separate major feature to it. It belongs to the continuing stabilization of the growing V2 implementation. Its inclusion in the version inventory is nevertheless important for completeness.

## 2.3.0

2.3.0 added talking-card support. Talking cards introduce additional presentation and dialogue-related data beyond ordinary card properties. This further expands the kinds of objects and behaviors JSONLoader can describe. It also demonstrates how the loader's scope had moved well beyond simple static card construction.

## 2.3.1

2.3.1 was a maintenance release following the talking-card addition. No separate major feature is assigned here without stronger changelog evidence. The release belongs to the stabilization cycle of the 2.3 generation. This is another example of why feature history and release inventory should be distinguished.

## 2.4.0

2.4.0 substantially improved Configil performance and functionality. The release introduced additional variables and improved several behavior systems. Configils are especially relevant because they involve actions and runtime behavior rather than simply declarative card fields. The resulting implementation complexity reinforces the need for clearer separation between general infrastructure and content-specific logic.

## 2.4.1

2.4.1 is a maintenance and patch-notes release. The available history does not justify assigning it a major new content system. It belongs to the continuing refinement of the 2.4 generation. Its presence demonstrates the iterative nature of stable V2 development.

## 2.4.2

2.4.2 restored an important file. This is a reminder that release engineering and repository state can be just as important as code features. A missing file can break a package even when the underlying feature implementation is correct. Nightly's later packaging and build refactors therefore have practical significance beyond source-code organization.

## 2.4.3

2.4.3 actually added the file that had been intended in the previous maintenance change. This release is therefore primarily a packaging/repository correction. It should not be inflated into a new user-facing feature. Its inclusion is useful because it documents the real-world maintenance process of the project.

## 2.4.4

2.4.4 is a maintenance release without a major separately documented feature addition. It continues the stabilization of the mature V2 implementation. The absence of a major changelog entry should not be interpreted as proof that the package contained no changes at all. It simply means that the available published history does not support a more specific claim.

## 2.4.5

2.4.5 added or corrected additional Configil triggers and behavior. This continued the trend of Configil becoming a substantial part of the V2 system. The feature history demonstrates how JSONLoader's scope grew through many specialized systems rather than through one single V2 feature expansion. This accumulated complexity is relevant to understanding the eventual architectural refactor.

## 2.5.0

2.5.0 raised the API requirement to 2.18.2 and added custom masks, custom languages, translations, encounter overrides, and export functionality. These features greatly expanded the loader's interaction with game presentation and localization systems. The current stable package documentation also warns that its export system is broken and should not be used, which is an important practical limitation for authors. A mature stable release can therefore still contain individual features that should be avoided.

## 2.5.1

2.5.1 improved encounter importing, particularly when encounters referenced cards from mods. It also added better invalid-name suggestions and more detailed errors. This is significant because error diagnostics are part of the authoring experience. The loader was no longer only responsible for making content work; it was also becoming responsible for explaining why content did not work.

## 2.5.2

2.5.2 addressed emissions, custom tribe loading, partial card overrides, Configil parameter parsing, hotkeys, and `_example` handling. Partial card overrides are particularly relevant to the later discussion of `fieldsToEdit` because they emphasize selective mutation rather than wholesale replacement. The `_example` behavior also demonstrates continued attention to packaging and authoring workflows. Together these features show the growing sophistication of the V2 loader.

## 2.5.3

2.5.3 added functionality involving `abilityLearnedDialogue`, `buffCards`, `changeAppearance`, and `OnDamageDirectly`. These additions show how far the loader had moved into runtime behavior and interaction systems. At this point JSONLoader was no longer merely describing static object properties. It was increasingly acting as a declarative interface to more dynamic Inscryption behavior.

## 2.5.4

2.5.4 changed example-file behavior and included maintenance corrections. Because the available record does not justify a larger feature description, this release is best treated as a refinement of the existing ecosystem. Its significance is partly in showing that seemingly small file-loading conventions can affect compatibility and package behavior. The `_example` convention eventually became part of the generalized Nightly discovery model.

## 2.6.0

2.6.0 was one of the broadest V2 releases. It added regions, power statistics, traits, items, bottled cards, Base64 textures, support for additional serialized types such as floats, colors, Vector2 values, arrays, private serialized fields, and public properties. It also included improvements to localization, exports, configuration, and error reporting. This release demonstrates how V2 was evolving toward a generalized serialization system even before the explicit Nightly refactor.

## 2.7.0

2.7.0 is the current stable version identified by the stable package documentation. Its changelog focuses heavily on build, repository, and packaging restructuring, including a new Thunderstore build process and improved organization. This makes it less of a new content-format generation and more of a mature maintenance/release-engineering milestone. The stable line therefore represents a feature-rich V2 implementation that has reached a relatively mature organizational stage.

---

# 47. Nightly release history

The Nightly history requires more caution because the available documentation exposes a development line whose later releases do not all have equally detailed published changelog descriptions. The currently indexed package page identifies 0.1.3 as the latest version, and it continues to describe the package as a preview of future JSONLoader and CSVLoader functionality. Earlier research into the detailed Nightly changelog provides strong evidence for the early infrastructure work, particularly around 0.0.3 through 0.0.5.

The verified early sequence is therefore best described as:

```text
0.0.3
0.0.4
0.0.5
...
0.1.3 currently indexed
```

Rather than inventing detailed features for every later release, this report describes the releases for which reliable feature-level evidence is available and treats later versions as published development iterations unless the current documentation provides a precise feature list.

---

# 48. Nightly 0.0.3

0.0.3 introduced or substantially established the early Nightly infrastructure. This included JSON Schema loading/generation work, a more complete JSON linter, additional logging, image scanning, plugin-context propagation, V1 loader support, file logging, and related development infrastructure. The linter was described as substantial but not yet feature-complete, which is consistent with the development status of the branch.

This release is important because it demonstrates that Nightly's purpose was already broader than creating a new card parser. Schema and linting were being treated as first-class infrastructure. File discovery and image handling were also being moved into reusable systems. The release therefore provides strong evidence for the claim that Nightly's defining change is architectural.

---

# 49. Nightly 0.0.4

0.0.4 fixed V1 image regular expressions and added filename-only image lookup. It also added a compatibility option intended to help older JSONLoader mods and adjusted logging behavior. These changes demonstrate that compatibility was being treated as an explicit design concern rather than an accidental side effect.

The filename-only image lookup is particularly interesting because it shows the image subsystem becoming more capable independently of the V1 card model. Instead of requiring every content type to implement its own artwork search, the shared scanner can locate assets according to general rules. This is precisely the kind of responsibility separation that the Nightly architecture is designed to encourage.

---

# 50. Nightly 0.0.5

0.0.5 fixed IceCube boot-loading depth, automatic updating behavior associated with `allJLDRCardsPublic`, success logging, and a version-related loading issue. These fixes demonstrate that even early Nightly releases were dealing with the interaction between compatibility code, runtime initialization, and diagnostics. The presence of successful-load logging is particularly useful because a loader needs to communicate not only failures but also what it successfully discovered and registered.

The IceCube fix also illustrates a broader point about declarative loaders. A JSON representation may be structurally correct while the runtime initialization sequence still exposes a bug. This is another reason schema validation cannot be treated as a complete substitute for runtime testing.

---

# 51. Nightly 0.0.6 through 0.1.3

The current indexed package confirms the later Nightly releases as part of the development line and identifies 0.1.3 as the latest package version currently exposed by Thunderstore. The available documentation does not provide a sufficiently reliable feature-by-feature changelog for every one of those later releases to justify reproducing a detailed list from memory or inference. A responsible technical report should therefore distinguish "published release exists" from "specific feature has been independently verified." This is particularly important because Nightly is actively changing and internal implementations can move between releases.

The later releases should therefore be treated as newer iterations of the same architectural project unless a particular feature is documented for the exact version under examination. When targeting a specific Nightly release, the appropriate source of truth is that release's source and current Wiki rather than an older 0.0.x source snapshot. This report consequently does not pretend that the early 0.0.5 class inventory is guaranteed to be byte-for-byte identical to 0.1.3.

---

# 52. What Nightly adds

Nightly's most important additions are architectural rather than simply a larger list of card fields. The architecture introduces or reorganizes shared file discovery, schema generation, schema loading, linting, image scanning, configuration-driven origins, logging, metadata extraction, and version-specific support layers. The package documentation itself exposes separate configuration for JSON and CSV origins and describes V1 and V2 as support areas inside the new framework.

Some of these capabilities existed in earlier stable JSONLoader forms. The important difference is that Nightly attempts to make them generalized subsystems rather than capabilities tightly coupled to one content format. That means the correct statement is not "Nightly invented every one of these features." The more accurate statement is that Nightly is reorganizing these capabilities into a reusable architecture capable of supporting multiple content generations.

---

# 53. Extension Properties

The Extension Properties System is designed to allow JSONLoader to carry additional information belonging to other systems. This is important because a general-purpose content loader cannot realistically know every property that every other Inscryption mod might invent. If it attempted to hard-code every possible extension, the loader would become tightly coupled to the entire modding ecosystem.

The documented authoring model is conceptually:

```json
{
    "name": "Dragon",
    "extensionProperties": {
        "SomeOtherModProperty": "SomeValue"
    }
}
```

The property object therefore acts as an extension point. JSONLoader can preserve and expose the additional information without necessarily needing to understand its semantics itself. The receiving library or extension system can interpret the property according to its own contract.

This is an important architectural idea because it prevents the main JSON schema from becoming a universal dictionary of every mod-specific field. The core loader remains responsible for core content, while extension systems can own their additional data. The current Nightly documentation explicitly describes this as a system primarily used on cards and explains that an `extensionProperties` object can be appended to JSON or CSV.

---

# 54. Fields To Edit

`fieldsToEdit` is one of JSONLoader's most important semantic mechanisms because it establishes explicit mutation. The Nightly documentation describes the system as a way to modify an existing base-game item or other item by supplying a string array of fields to overwrite. It specifically gives `displayedName` as an example of a field that can be selected for editing.

Consider:

```json
{
    "fieldsToEdit": [
        "displayedName"
    ],
    "name": "Stoat",
    "displayedName": "Suspicious Stoat"
}
```

The important information is not merely that `displayedName` appears in the JSON. The important information is that the author explicitly placed it inside `fieldsToEdit`. That communicates intent to the loader. The author is saying that this property is part of the mutation operation while unrelated properties should not automatically be interpreted as replacements.

This is why `fieldsToEdit` should not be treated as a general duplicate-resolution mechanism. It identifies intended mutation of an existing object. If two unrelated mods both attempt to edit the same card, they have created an interaction between their modifications. The system does not automatically transform that situation into a conflict-free merge.

---

# 55. How Nightly handles duplicates

Duplicate handling needs to be divided into several different concepts. Two files can have different filenames but define the same internal identity. Two files can contain identical data but represent separate intended objects. Two mods can intentionally modify the same existing object. Two definitions can accidentally collide because they omitted a unique prefix. These are different situations even though all of them might superficially be described as "duplicates."

The safest categories are:

```text
Unique new card
    ↓
new identity

Existing card + fieldsToEdit
    ↓
intentional mutation

Two independent mods editing one object
    ↓
compatibility interaction

Two new objects with same identity
    ↓
collision
```

The documented V2 model explicitly encourages `modPrefix` as part of identity, and the Nightly documentation describes the prefix/name relationship. A new modded card should therefore use a unique internal identity rather than relying on filename uniqueness. Two files called `Dragon.jldr2` and `Dragon2.jldr2` can still collide if both produce the same underlying identity.

The important rule is that authors should **not assume undocumented last-write-wins behavior**. Unless the exact loader version documents a deterministic conflict-resolution order, relying on file discovery order or mod load order is fragile. A load-order accident is not a compatibility mechanism. Intentional modifications should use explicit identity and `fieldsToEdit`, while independent new content should use unique prefixes.

---

# 56. JSON Editor and Nightly

JSON Editor is useful because it is driven by JSON Schema rather than by Inscryption-specific knowledge. It does not inherently know what a card, sigil, encounter, or tribe is. Instead, it receives a schema describing the structure of the document and generates an authoring interface from that description.

The relationship is therefore:

```text
Nightly model
      ↓
JSON Schema
      ↓
JSON Editor
      ↓
JSON document
      ↓
Nightly
```

This makes Nightly's schema generator particularly important. Without a reliable schema, JSON Editor has no accurate description of what controls to display. The editor is therefore best understood as a client of the schema system rather than as an alternative JSONLoader implementation.

The practical workflow is:

```text
C# model
   ↓
generated schema
   ↓
JSON Editor
   ↓
author-created JSON
   ↓
Nightly validation
   ↓
runtime conversion
```

JSON Editor should not be treated as the final authority. The installed Nightly version remains the authority because the schema and implementation can change between releases. A JSON document that appears correct in an old editor configuration can still fail against a newer loader schema.

---

# 57. Practical JSON Editor workflow

A new author should first determine which loader generation they are targeting. V1 uses `.jldr`, V2 uses `.jldr2`, and the future V3 pathway is represented separately. The author should then obtain the schema corresponding to the specific content type and loader version rather than selecting an arbitrary JSON schema. Once the schema is loaded into JSON Editor, the editor can generate controls for the documented properties and nested structures. The author can fill those controls and inspect the resulting JSON.

After copying the generated JSON into the appropriate file, the author should still run it through Nightly itself. This final validation step matters because the editor and loader can be using different schema versions or configurations. It also matters because JSON Editor cannot establish that referenced runtime objects or image files actually exist. The editor is therefore an authoring assistant, while Nightly remains the runtime authority.

---

# 58. Why generated schemas are especially useful

Consider the difference between:

```json
"baseHealth": 4
```

and:

```json
"baseHealth": "4"
```

Both are valid JSON syntax, but they have different types. If the schema says `baseHealth` is an integer, the second form is structurally invalid. The same principle applies to arrays, booleans, nested objects, and other values.

For example:

```json
"traits": []
```

is structurally an array, while:

```json
"traits": "BifurcatedStrike"
```

is a string. A schema can identify that mismatch immediately. This is why generated schemas are more useful than simply having a written list of field names. They encode the actual structural contract in a machine-readable form.

---

# 59. Wiki layout

The Nightly Wiki is organized around multiple layers of documentation rather than one enormous page. The current package documentation identifies sections for general JSON/CSV API documentation, authoring, V1 support, V2 support, configuration, artwork, extension properties, fields-to-edit, maintainer documentation, logging, and reference material. The package explicitly warns that its older embedded documentation may become outdated and directs users toward the GitHub and Thunderstore Wiki systems for the most current material.

The major topic map is:

```text
Home
Installation
JSON and CSV Loader API Documentation
Artwork Form Support
Configuration
JSON Inscrybing
JSONLoaderV1 Support
JSONLoaderV2 Support
JSONLoaderV3 Support
CSVLoader Support
Extension Properties System
Fields To Edit System
Maintainer Documentation
JSON Object Tooltip Language
Logging
Tools
Vanilla Card Names
Vanilla Enums
```

The presence of separate maintainer documentation is significant. It indicates that the Wiki is not solely intended to teach mod authors how to write JSON. It also documents the architecture and conventions needed by people maintaining the loader itself.

---

# 60. Wiki topic-by-topic explanation

## Home

The Home page is the orientation point for the documentation ecosystem. It establishes what the project is and directs readers toward the appropriate areas of the Wiki. This becomes particularly important for Nightly because the package's own embedded documentation warns that it may become outdated. The Home page therefore functions as a navigation layer rather than simply a feature reference. For maintainers, it also establishes documentation conventions and contribution expectations.

## Installation

Installation explains how to place the loader and its dependencies into the Inscryption modding environment. The current Nightly documentation provides both mod-manager and manual installation paths and also contains platform-specific information for Steam Deck, Linux, and Mac. For a new author, this section is the boundary between having the game and actually having a working mod-development environment. It therefore belongs conceptually before JSON authoring rather than being treated as optional background.

## JSON and CSV Loader API Documentation

This is the umbrella section for the loader's supported formats and authoring systems. It establishes that the project is no longer only a JSON card loader. The inclusion of CSV documentation indicates that the architecture is intended to support tabular content workflows as well. It also provides the common foundation from which the V1 and V2 support pages can be understood.

## Artwork Form Support

Artwork documentation explains how asset paths and image representations are interpreted. This is important because an artwork property is not just an arbitrary string. The loader needs to resolve that string against the plugin filesystem or interpret an embedded representation. Understanding artwork support therefore helps authors diagnose a class of errors that JSON syntax validation alone cannot catch.

## Configuration

Configuration documents where JSON and CSV files are searched, where schemas are stored, and what diagnostic information is emitted. The current Nightly documentation identifies default origins of `Scripts, Plugins/Scripts, Cards, Plugins/Cards` for JSON and `Sheets, Plugins/Sheets` for CSV. It also documents verbose, additional, and summary logging options. This section is therefore central to understanding the file-loading pipeline.

## JSON Inscrybing

This is the practical authoring introduction. It explains how to prepare the filesystem, create JSON files, locate plugin paths, and begin constructing loader content. The current documentation explicitly walks authors through enabling visible file extensions and creating the appropriate JSON files. It therefore serves as the bridge between abstract API documentation and actually making a mod.

## JSONLoaderV1 Support

This section documents the legacy `.jldr` card system. It provides field tables and explanations for V1's card properties, artwork, abilities, evolution, tail, IceCube, and related structures. It is particularly useful for authors maintaining older mods or trying to understand the compatibility layer inside Nightly. The documentation also makes clear which V1 fields are limited to vanilla systems and which fields can represent modded abilities.

## JSONLoaderV2 Support

This section documents `.jldr2` and the much broader V2 content ecosystem. It covers cards, starter decks, and other V2-specific structures. Because V2 accumulated many features across many releases, this section is effectively the reference for the mature stable JSONLoader model. It is also one of the most important sources for migration because Nightly's compatibility layer is expected to understand V2 data.

## JSONLoaderV3 Support

The current Nightly documentation leaves the V3 support section empty. That absence is meaningful because it prevents the report from claiming a finished public V3 specification. The architecture contains a V3 support pathway, but the documentation does not establish a complete user-facing V3 contract. Therefore, authors should not infer a complete `.jldr3` specification merely from the existence of the section or class.

## CSVLoader Support

The current Nightly documentation similarly leaves the CSV support section incomplete. Nevertheless, the configuration system already exposes CSV loading origins, demonstrating that CSV is architecturally part of the project. This means CSV should be treated as a planned/current development subsystem rather than as a fully documented stable replacement for JSON. Exact CSV behavior should therefore be checked against the specific Nightly release and current Wiki.

## Extension Properties System

This section explains how additional properties can be carried alongside core JSONLoader content. It is especially important for interoperability with other modding libraries. The system allows external property names and values to travel through the loader without forcing the core loader to understand every extension's semantics.

## Fields To Edit System

This section documents selective mutation of existing content. It explains how an author specifies the exact fields that should be overwritten. This is central to safe overrides because it separates intentional mutation from accidental redefinition. It is also one of the key mechanisms that must be understood before attempting to make compatibility patches for other mods.

## Maintainer Documentation

Maintainer documentation concerns people working on JSONLoader itself. It covers architecture, implementation conventions, and other information that is less relevant to ordinary JSON authors. This documentation is particularly valuable for Nightly because the project is actively being refactored. A mod author can treat the public data format as the main interface, while a maintainer needs to understand how the underlying subsystems fit together.

## JSON Object Tooltip Language

This documentation concerns the structured metadata used to provide descriptions and other information about JSON properties. It is part of the bridge between source code and generated schemas. Understanding it is useful for maintainers who want generated schemas to remain readable and informative. It is also evidence that Nightly's schema system is intended to carry documentation, not merely primitive type information.

## Logging

Logging documentation explains how the loader communicates what it is doing and why something failed. This is important because a content loader operates across several stages where errors can occur. The current configuration distinguishes verbose logging, additional information, and summary information. These options allow authors to increase diagnostic detail without necessarily running maximum verbosity all the time.

## Tools

The Tools section provides supporting utilities for authors and maintainers. Tools are particularly valuable in a framework where schema generation, validation, and authoring can otherwise require repetitive manual work. The exact contents of this section can evolve as the Nightly project develops. It should therefore be treated as an auxiliary area rather than a fixed API contract.

## Vanilla Card Names

This is reference material for identifying existing game cards by their internal names. It is particularly useful when using `fieldsToEdit` because an override needs the correct target identity. It also helps authors avoid confusing displayed names with code-level names. That distinction is essential when modifying base-game objects.

## Vanilla Enums

This section provides reference information for values that correspond to vanilla game enums and enumerated systems. It is particularly useful for fields such as temples, tribes, traits, abilities, card complexity, and other values that are represented as strings in JSON but have constrained meanings. These references are valuable because a string that is syntactically valid may still be semantically invalid if it does not correspond to an accepted enum value.

---

# 61. Stable Wiki versus Nightly Wiki

The stable and Nightly Wiki systems should not be treated as interchangeable documentation sets. The stable Wiki describes the mature JSONCardLoader V2 ecosystem, including features accumulated across the 2.x release sequence. The Nightly Wiki describes the generalized JSON/CSV architecture and compatibility layers. Nightly's documentation explicitly warns that older embedded documentation can become outdated and directs users to the Wiki systems for more current information.

This distinction matters during troubleshooting. If a stable V2 example says one thing while a Nightly schema says another, the author needs to determine which loader generation they are actually running. Copying stable documentation into Nightly without checking the corresponding schema can produce subtle failures. The safest practice is to use the documentation associated with the exact loader generation and release being tested.

---

# 62. Installation structure

A practical mod authoring layout can look like:

```text
BepInEx/
└── plugins/
    └── MyMod/
        ├── MyMod.dll
        ├── Scripts/
        │   ├── Cards.jldr2
        │   └── Decks_deck.jldr2
        └── Art/
            ├── Dragon.png
            ├── Dragon_Alt.png
            └── Dragon_Emission.png
```

The exact packaging structure can vary depending on the mod manager and package format, but the conceptual requirement is that the loader's configured origin paths eventually resolve to the files. The current Nightly documentation says the default JSON origins are relative to the mod-specific folder under the `plugins` directory.

The directory structure should therefore be designed around discoverability rather than around arbitrary aesthetics. Keeping JSON under `Scripts` and artwork under an `Art` directory makes it easier to reason about paths and package contents. It also reduces the risk of accidentally placing production files in an excluded example location or outside the loader's configured search roots.

---

# 63. Setup example: a minimal card mod

A beginner can think of a JSONLoader card mod as three cooperating pieces:

```text
1. loader environment
2. JSON content
3. artwork
```

For example:

```text
MyMod/
├── MyMod.dll
├── Scripts/
│   └── Dragon.jldr2
└── Art/
    └── Dragon.png
```

A representative V2 card could look like:

```json
{
    "name": "Dragon",
    "modPrefix": "MyMod",
    "displayedName": "Dragon",
    "description": "A custom dragon.",
    "baseAttack": 3,
    "baseHealth": 4,
    "bloodCost": 2,
    "texture": "Art/Dragon.png"
}
```

This example deliberately uses only a small set of properties. The stable documentation states that the card name is required while other card fields can be optional/defaulted. The current Nightly documentation likewise identifies the core V2 card fields and their types. A beginner should therefore resist the temptation to copy a giant card object containing every possible field before understanding which properties are actually necessary.

---

# 64. Setup example: editing a base-game card

Base-game editing uses a different identity model. Instead of creating a new prefixed card, the JSON identifies the existing base-game object and specifies which properties should be overwritten. The current Nightly documentation explicitly describes `fieldsToEdit` as a mechanism for modifying a base-game or existing modded item.

A conceptual example is:

```json
{
    "fieldsToEdit": [
        "displayedName",
        "description"
    ],
    "name": "Stoat",
    "displayedName": "Suspicious Stoat",
    "description": "This stoat has seen things."
}
```

The important point is that the edit list communicates intent. The author is not defining an entirely new Stoat object. The author is identifying an existing object and asking the loader to replace two specific properties. This is fundamentally different from creating `MyMod_Stoat` as a new card.

---

# 65. Compatibility: will a mod need updating?

Compatibility depends on what the mod actually depends on. A JSON-only mod is primarily dependent on the loader's ability to interpret its file format. A C# mod that references JSONLoader classes directly is dependent on the loader's compiled assembly surface as well. Those dependencies can behave differently during a major refactor.

For a JSON-only V1/V2 mod, Nightly's explicit V1 and V2 support is strong evidence that format compatibility is a design goal. The Nightly package documentation explicitly presents those support sections as part of the new framework. That does not mean every historical file is guaranteed to work forever, but it means an automatic rewrite should not be assumed simply because Nightly is internally different.

For a C# integration, the situation is different. If a DLL references an old JSONLoader class, namespace, method signature, or assembly, the refactor can break that dependency even if the same `.jldr2` file still loads correctly. The safe assumption is therefore that data compatibility is more likely than binary compatibility during a major architectural refactor.

---

# 66. Will older mods remain compatible?

There are at least three separate compatibility questions.

```text
Format compatibility
    Can Nightly read the old JSON?

Runtime compatibility
    Can the resulting data be registered through the current API?

Binary compatibility
    Can the old DLL still call the new assembly?
```

The first question is explicitly addressed by V1/V2 support. The second depends on the current Inscryption API and the conversion implementation. The third is a completely separate matter because a compiled DLL expects particular types and method signatures.

The Nightly 0.0.4 compatibility option is evidence that preserving older JSONLoader mod behavior was an explicit development concern. It should not be interpreted as a guarantee that every old DLL or every undocumented edge case remains compatible. Compatibility layers can preserve file semantics while still being unable to preserve assumptions about unrelated assemblies, missing dependencies, load order, or game behavior.

---

# 67. How to keep a mod compatible

The strongest compatibility strategy is to use documented file formats and avoid undocumented implementation details. New content should have unique internal identities, usually achieved through a consistent `modPrefix`. Existing content should be modified through explicit `fieldsToEdit` rather than by relying on duplicate definitions. Artwork should preferably use explicit paths rather than depending on ambiguous filename searches.

Schemas should be used during development because they provide a machine-readable description of the expected document structure. C# integrations should isolate JSONLoader-specific code behind an adapter so that a loader refactor does not require changes throughout the gameplay system. Mods intended to support both stable and Nightly should be tested against both rather than assuming that a single successful run establishes compatibility with both architectures.

---

# 68. A compatibility architecture for serious mods

A serious C# mod can isolate loader-specific dependencies like this:

```text
Your mod
   |
   +--------------------+
   |                    |
Gameplay code       Loader adapter
                        |
                  JSONLoader API
                        |
                Stable / Nightly
```

The gameplay system then communicates with the adapter rather than directly depending on every loader implementation detail. If Nightly changes a class name or moves a method, the adapter can be updated without forcing the rest of the mod to change. This pattern is especially useful for projects that intend to support multiple loader generations.

The adapter can also provide a place for compatibility checks. It can determine which loader is present, choose the appropriate integration path, and normalize differences in returned data. This turns a potentially scattered compatibility problem into a localized engineering problem. It does not make binary compatibility automatic, but it makes compatibility work much easier to maintain.

---

# 69. Nightly's relationship to CSV

CSV support is part of the project's architectural scope rather than an unrelated side utility. The package is explicitly named `JSON_and_CSV_Loader_Nightly`, and its description says it is a preview of what is coming to JSONLoader and CSVLoader. The configuration system already exposes separate JSON and CSV loading origin settings.

The architecture therefore appears intended to support multiple serialized input forms feeding common loader infrastructure. JSON is naturally hierarchical and handles nested objects well, while CSV is naturally tabular and can be convenient for spreadsheet-oriented workflows. A generalized loader framework can provide shared discovery, logging, configuration, and possibly schema mechanisms while allowing the input formats to remain different. The current documentation does not establish complete CSV feature parity, however, so CSV should remain a development feature rather than being presented as a finished replacement for JSON.

---

# 70. Why Nightly has schema infrastructure

A loader containing dozens or hundreds of object types cannot realistically maintain all of its code, documentation, schema, and editor definitions independently without significant duplication. Every duplicated definition creates another opportunity for the documentation to become stale. If a C# property changes but the schema is not updated, the authoring tools can begin teaching users an incorrect format.

Nightly's approach attempts to reduce that duplication:

```text
C# definitions
     |
     +---- schema
     +---- documentation
     +---- validation
     +---- editor support
```

The source definition becomes the basis from which several other artifacts can be derived. This does not eliminate every maintenance problem, because the generated schema still needs to represent semantics accurately. It does, however, reduce the number of independent places where basic type information must be maintained.

---

# 71. Why `TooltipDisector` matters

A tooltip parser might initially seem like a minor convenience feature. Its deeper significance is that documentation can become part of the generated tooling pipeline. If a field definition contains structured metadata describing what the field does, the schema can potentially carry that description to the author. The authoring interface can then display useful information without requiring the user to constantly consult source code.

The resulting pipeline is:

```text
developer metadata
        ↓
TooltipDisector / XML_Parser
        ↓
schema metadata
        ↓
JSON Editor / documentation
```

This is important because it means the loader's schema can be both machine-readable and human-readable. A schema that says only `"type": "integer"` is useful for validation but not necessarily useful for understanding why the field exists. A schema accompanied by a description can become part of the project's documentation ecosystem.

---

# 72. The new logo

The available research does not identify a technical specification assigning compatibility or API semantics to the new logo. There is therefore no evidence that the logo itself guarantees V3 support, a particular API version, or compatibility with a particular class of mods. It should instead be interpreted as branding associated with the new development line. This is consistent with the package's explicit presentation of itself as the Nightly JSON/CSV loader and its connection to the JSONLoader 3 refactor branch.

The distinction matters because visual branding can change independently of implementation. A logo can communicate that a project is entering a new phase without defining a serialization contract. Technical compatibility should therefore always be established through version numbers, schemas, source, documentation, and release notes rather than visual identity.

---

# 73. What Nightly offers that stable does not

Nightly offers a more explicitly generalized architecture around file discovery, schema generation and loading, linting, image scanning, configuration, logging, metadata processing, and format-specific support. Some individual capabilities existed in stable JSONLoader, so the novelty lies partly in how they are organized. The Nightly documentation explicitly separates V1 and V2 support from the general API documentation and provides configuration that applies to JSON and CSV loading.

Stable V2, meanwhile, contains a large amount of mature functionality that Nightly's incomplete V3 documentation does not establish as fully reproduced. A stable V2 feature such as an encounter system can be highly mature even while Nightly has a more elegant architecture for representing future formats. The correct comparison is therefore architectural rather than a simple count of features.

---

# 74. What a new mod author should actually choose

For a released mod whose primary objective is established compatibility, stable JSONLoader remains important because it is the mature V2 implementation. For an author specifically interested in JSONLoader 3, future architecture, or helping test the new loader, Nightly is the relevant development environment. A practical strategy for a serious mod is to develop against the stable system if that is the required release target and then test the same content under Nightly.

A useful workflow is:

```text
Develop
   ↓
stable target
   ↓
test under Nightly
   ↓
identify differences
   ↓
isolate compatibility changes
   ↓
test again
```

This is especially useful when a mod contains both JSON content and C# integration. The JSON files can test format compatibility while the adapter layer can reveal binary/API compatibility problems.

---

# 75. Duplicate strategy for mod authors

The safest naming strategy for new content is:

```text
<ModPrefix>_<CardName>
```

For example:

```text
DragonMod_Dragon
DragonMod_ForestDragon
DragonMod_AncientDragon
```

The purpose is not to make the player see the prefix. The purpose is to create an internal identity that is unlikely to collide with another mod. The player-facing `displayedName` can still simply be `"Dragon"`.

This distinction becomes especially important when multiple mods contribute similarly named cards. The internal identity acts like a namespace, while the display name acts like a label. Treating those as the same thing makes collisions much more likely.

---

# 76. Why `modPrefix` is more than a naming convention

Imagine two independent mods:

```text
Mod A:
Trinity

Mod B:
Trinity
```

If both produce the same internal identity, the loader and game have a collision problem. Now consider:

```text
Mod A:
Myth_Trinity

Mod B:
Matrix_Trinity
```

The player can still see:

```text
Trinity
```

for both cards, but the underlying identities are different. This demonstrates the fundamental distinction between:

```text
internal identity
    ≠
displayed name
```

`modPrefix` is therefore a namespace mechanism as much as it is a naming convention. It lets authors create human-readable content without sacrificing collision resistance.

---

# 77. Stable V2 special filename conventions

V2 uses filename suffixes to identify certain content systems. Examples include:

```text
*_sigil.jldr2
*_talk.jldr2
*_deck.jldr2
*_tribe.jldr2
*_tribes.jldr2
*_encounter.jldr2
```

The exact accepted naming conventions should be checked against the target stable version, but the architectural point is consistent. The extension `.jldr2` establishes the V2 generation, while the filename convention can help determine which V2 subsystem should interpret the document.

This is why a simplified statement such as "the extension tells JSONLoader what the file is" is incomplete. The extension tells the loader which format generation is involved, but the content-specific suffix and root object determine which object model is appropriate. This distinction becomes increasingly important as V2 supports more than cards.

---

# 78. JSONLoader's evolution as an architectural story

The history can be summarized as:

```text
V1
|
| card-focused
| nested card data
| early API
v
V2
|
| API 2.x rewrite
| modPrefix
| more content types
| starter decks
| tribes
| encounters
| Configils
| talking cards
| regions
| items
| localization
| advanced serialization
v
Nightly
|
| generalized infrastructure
| schema system
| linter
| file abstraction
| image abstraction
| compatibility layers
| V3 architecture
| CSV architecture
v
future JSONLoader
```

V1 demonstrates the original problem: make cards easier to define through JSON. V2 demonstrates what happens when authors want the same convenience for increasingly diverse systems. Nightly addresses the resulting architectural pressure by separating common infrastructure from format-specific implementations.

This is why Nightly should not be judged solely by how many new JSON fields it adds. The deeper question is whether it makes the loader easier to extend without repeatedly duplicating the same filesystem, schema, validation, logging, and asset-handling code. That is the architectural objective behind the refactor.

---

# 79. What the report cannot claim

This report cannot truthfully claim that the currently indexed Nightly release has complete V3 feature parity with stable V2. The current package documentation itself leaves V3 and CSV support sections empty while describing Nightly as a preview. It also cannot truthfully claim that every internal method found in an early Nightly source snapshot remains identical in the current package.

It cannot truthfully claim that the maintainer officially named `Cores`, `Peripheral`, and `Subperipheral` according to one specific architectural philosophy because no explicit maintainer explanation establishing that etymology was located. It cannot claim that the new logo guarantees a particular compatibility mode because no technical documentation assigns that meaning to the branding. It also cannot claim that duplicate identities always resolve through last-write-wins behavior without a documented contract establishing such a rule.

These limitations are important rather than embarrassing. A technical report is stronger when it distinguishes documented fact from source observation and architectural interpretation. Nightly's development status makes this distinction especially necessary.

---

# 80. Complete practical workflow for a new mod author

A new author should begin by deciding which loader generation is actually required. That decision determines the file extension, schema, documentation set, and compatibility assumptions. The author should then create a clean mod directory under the appropriate plugin environment and place JSON under a configured origin such as `Scripts`. The current Nightly defaults are designed so that a mod can use these standard locations without requiring the player to edit configuration.

Next, create the smallest possible valid JSON document. Obtain the corresponding schema and validate the document before adding complexity. If desired, use JSON Editor to generate the initial structure, but still validate the resulting file against the actual loader. Add artwork after the structural JSON works, because this separates JSON/schema errors from asset-resolution errors.

Once the minimal object loads, add gameplay properties incrementally. Test references to other cards and abilities separately. Then test overrides and interactions with other mods. Finally, test the package under any other loader generation that the mod claims to support. This incremental workflow makes failures local and therefore much easier to diagnose.

---

# 81. Recommended debugging sequence

When a card or other object fails to load, the author should work through the pipeline rather than immediately assuming the Inscryption API is broken. The first question is whether the loader found the file. If it did not, no amount of JSON editing will fix the problem. The next questions concern classification, syntax, schema structure, dependencies, assets, conversion, and finally runtime behavior.

A practical sequence is:

```text
1. Did the loader find the file?
2. Did it classify the file correctly?
3. Is the JSON syntactically valid?
4. Does the schema accept it?
5. Are required fields present?
6. Are field types correct?
7. Are enum strings correct?
8. Are referenced cards/abilities valid?
9. Are images found?
10. Did object conversion succeed?
11. Did the API accept the object?
12. Does the game behave correctly?
```

This sequence mirrors the architecture. It also prevents a common debugging mistake in which a runtime failure is blamed on JSON syntax even though the JSON passed validation and the actual problem was a missing image or nonexistent ability. Each stage has its own class of failure, so each stage should be investigated separately.

---

# 82. What the logs are for

Nightly's logging configuration is designed to provide different amounts of diagnostic information. Normal logging answers the broad question of what happened. Additional information provides more context around common errors. Verbose logging exposes more internal debugging information and is therefore useful when the normal output does not reveal enough.

The current Nightly configuration exposes settings for verbose logging, additional information, and summary information. The documentation explains that verbose mode outputs debug information to the console and log file, while additional information provides more context around common errors. Summary information can include descriptions of properties during schema validation.

A practical strategy is:

```text
normal logging
      ↓
problem occurs
      ↓
additional information
      ↓
still unclear
      ↓
verbose logging
```

This avoids permanently flooding the log with development-level detail while still giving authors a clear escalation path when debugging.

---

# 83. The difference between JSONLoader and Inscryption API

A common beginner misunderstanding is that JSONLoader is the entire Inscryption modding API. It is not. The underlying API provides the runtime modding primitives, while JSONLoader provides a declarative way of describing content that is ultimately converted into those primitives.

The relationship is better represented as:

```text
Inscryption
    ↑
Inscryption API
    ↑
JSONLoader
    ↑
your JSON
```

The direction matters conceptually. JSONLoader depends on the game's modding infrastructure rather than replacing it. This is why JSONLoader releases can be tied to API versions and why a major underlying API change can require changes to conversion code even when the JSON authoring model appears similar.

---

# 84. Why V2 broke compatibility

V2 was not simply a patch to V1. It was a rewrite associated with Inscryption API 2.0 and introduced `.jldr2`. The stable documentation and historical release information identify this as a backward-compatibility break by default, accompanied by mechanisms intended to help older JLDR content transition. This is important because it establishes precedent for the idea that a major JSONLoader generation can preserve some old formats through compatibility code while still changing its underlying implementation.

That precedent helps explain Nightly. Nightly does not need to preserve the V1/V2 implementation internally in order to preserve the ability to interpret V1/V2 files. A compatibility layer can translate old data into a newer internal representation. This is one of the major reasons a refactor can be undertaken without requiring every existing JSON document to be rewritten immediately.

---

# 85. Why Nightly's V1/V2 support is important

If Nightly had simply removed the old loaders and replaced them with V3, every existing JSON mod would have been forced into an immediate migration. Instead, the architecture is closer to:

```text
new framework
    |
    +--> old V1 parser
    +--> old V2 parser
    +--> new V3 pathway
    +--> CSV pathway
```

This architecture permits gradual migration. Existing content can continue to use its established serialization generation while the shared infrastructure evolves underneath it. New content can eventually use V3 when that format is sufficiently documented and implemented.

This is also valuable for maintainers because it separates compatibility work from future-format development. A V1 bug can be handled in the V1 support layer without requiring the entire V3 system to understand V1's historical object model. The same principle applies to V2.

---

# 86. The role of compatibility mode

The explicit compatibility option documented in the early Nightly release history demonstrates that preserving older JSONLoader behavior was a deliberate concern. The current Nightly documentation also maintains V1 and V2 support sections. This provides a stronger basis for saying "Nightly is designed with compatibility in mind" than simply observing that an old file happens to load.

Compatibility mode nevertheless has limits. It can preserve file conventions and help the new framework understand older documents, but it cannot guarantee that every external dependency behaves exactly as it did under an older environment. A missing image, removed ability, incompatible game API, old binary dependency, or conflicting mod can still cause failure. Compatibility should therefore be treated as a layer in the loading pipeline rather than as a promise that an old mod will behave identically in every environment.

---

# 87. Nightly and older `.jldr` files

The conceptual path for an old V1 file is:

```text
Old .jldr
    |
    v
Nightly V1 compatibility layer
    |
    v
Nightly internal representation
    |
    v
current API
```

The important point is that the old document does not need to become the new internal representation. The compatibility layer can interpret the historical syntax and translate its meaning into the newer infrastructure. This is a common architectural strategy for maintaining compatibility during a refactor.

It also explains why V1 source structures can remain relevant even when V3 eventually becomes the primary format. The V1 implementation becomes a translator between an old public format and the new internal architecture. That role is different from making V1 the central design of the new system.

---

# 88. Nightly and older `.jldr2` files

The same conceptual model applies to V2:

```text
Old .jldr2
    |
    v
Nightly V2 support
    |
    v
Nightly infrastructure
    |
    v
Inscryption API
```

This arrangement lets Nightly reuse common systems without requiring V2 documents to be rewritten merely because the internals changed. It also makes it possible for maintainers to isolate V2-specific quirks inside the V2 support layer.

For mod authors, the practical consequence is that a V2 JSON file should be tested before being rewritten. If it already works under the target Nightly version, unnecessary migration introduces risk without providing a benefit. Migration should be driven by an actual need for V3 features or by documented compatibility requirements.

---

# 89. Why exact schema matters more than copied examples

A copied example can become stale, especially in a development branch. A schema generated or supplied for the target loader version is more directly connected to the structural contract that the validator expects. Examples remain valuable because they teach authors how the system is intended to look, but the schema provides stronger evidence about field names, types, nesting, and required properties.

This is especially important when dealing with a development branch. An example copied from an older Wiki snapshot may use a property name that has since changed. A schema generated by the exact loader build provides a much better basis for determining whether the current implementation accepts that property. The best practice is therefore:

```text
Example
    → learn the concept

Schema
    → verify the structure

Runtime loader
    → verify actual behavior
```

---

# 90. How to read a schema as a mod author

A JSON Schema generally answers several important questions. It tells you what properties exist, what types those properties have, which properties are required, what arrays contain, what nested objects contain, and sometimes what values are allowed. This means that learning basic JSON Schema terminology is a useful companion skill for JSONLoader modding.

For example:

```json
{
    "type": "integer"
}
```

means that the property is expected to be an integer.

```json
{
    "type": "string"
}
```

means it is expected to be a string.

And:

```json
{
    "type": "array",
    "items": {
        "type": "string"
    }
}
```

means the property is an array whose elements are strings.

The important conceptual leap is that a schema describes structure rather than gameplay. It can tell you that `abilities` is an array of strings, but it may not tell you whether every string names an ability that exists in the current game environment. That distinction returns us to the four levels of correctness described earlier.

---

# 91. The architecture's biggest long-term advantage

The biggest potential advantage of Nightly is the possibility of shared infrastructure. Instead of maintaining separate implementations for file discovery, schema handling, logging, validation, and image processing across every content format, the architecture can provide one reusable system for all of them.

Conceptually:

```text
one filesystem system
one schema system
one logging system
one validation system
one image system
one configuration system
```

serving:

```text
V1
V2
V3
CSV
```

This architecture reduces duplication and makes new content formats easier to add. It also means that improvements to a shared subsystem can benefit several formats simultaneously. For example, a better image resolver does not need to be separately implemented for V1, V2, and V3 if they all consume the same scanner.

---

# 92. The architecture's biggest short-term risk

The same refactoring that creates long-term architectural advantages introduces short-term instability. Classes can move, method signatures can change, helper functions can be renamed, schemas can evolve, and responsibilities can shift between namespaces. This is normal for a development branch but dangerous for code that directly depends on internal implementation details.

For JSON-only authors, this instability is partially insulated by the compatibility layers. For C# developers, it is much more visible because compiled dependencies directly reference implementation symbols. This is why a Nightly integration should minimize the number of internal classes it depends upon. The more of the implementation a mod reaches into, the more likely a refactor is to require code changes.

---

# 93. What should a mod author avoid?

Avoid relying on undocumented internal classes when a documented JSON mechanism exists. Avoid depending on accidental load order, especially as a substitute for explicit conflict resolution. Avoid using duplicate internal identities for new content. Avoid assuming that an old example document is still correct simply because it appears in a Wiki or repository.

Prefer documented JSON formats, generated or current schemas, unique prefixes, explicit asset paths, intentional `fieldsToEdit` operations, and isolated C# integration. These practices align the mod with the loader's public concepts rather than its temporary internal implementation. That is particularly important for Nightly because its internal architecture is explicitly under development.

---

# 94. Original research questions: consolidated answers

## What do the semantics of the class names mean?

The class names primarily describe responsibility. `Plugin` identifies the BepInEx entry point, `FindFiles` identifies filesystem discovery, `LoadFiles` identifies the loading coordinator, `CardObject` identifies a loader-side card representation, `LoadSchema` identifies schema consumption, `WriteSchema` identifies schema generation, `LintingTools` identifies validation, and `ScanImages` identifies artwork resolution. `JSONLoaderV1Support`, `JSONLoaderV2Support`, and `JSONLoaderV3Support` identify the format-generation boundaries. `Cores`, `Peripheral`, and `Subperipheral` appear to represent architectural organization, but their exact naming rationale is not documented sufficiently to state an official etymology.

## What does every function in a given class do?

The researched Nightly implementation provides detailed function-level information for the major infrastructure classes and V1 `CardObject`. The most significant groups are the V1 accessor and conversion functions, schema-generation handlers, schema-loading operations, recursive validation functions, filesystem operations, image scanning, XML documentation parsing, and tooltip processing. Each group has been expanded above to explain not only what the method returns or accepts but why the method exists in the architecture. Because Nightly is under active development, the exact latest method inventory should always be verified against the source version being targeted.

## How does Nightly differ from current JSONLoader?

Nightly is the next-generation architectural development line, while stable 2.7.0 is the mature V2 implementation. Nightly emphasizes shared infrastructure and compatibility layers rather than simply adding another collection of card fields. It also explicitly includes CSV architecture and a V3 support pathway. The current package describes itself as a preview of what is coming to JSONLoader and CSVLoader.

## How is the Wiki laid out?

The Wiki is divided into installation, general API documentation, authoring, artwork, configuration, V1 support, V2 support, V3/CSV development areas, extension properties, fields-to-edit, maintainer documentation, metadata language, logging, tools, and reference material. The Nightly package specifically advises that older embedded documentation can become outdated and that the Wiki systems contain the more current documentation.

## What does each Wiki topic cover?

The report provides a detailed topic-by-topic explanation above. The most important conceptual distinction is that some pages are author-facing while others are maintainer-facing. V1/V2 pages describe concrete content formats, while configuration, schema, logging, and maintainer pages describe the infrastructure surrounding those formats.

## What is the significance of the new logo?

No technical specification was found assigning compatibility or API semantics to the logo. It should therefore be treated as branding associated with the new development line rather than as a compatibility marker.

## Will I need to update my mod?

A JSON-only V1/V2 mod should not automatically be assumed to require a rewrite because Nightly explicitly maintains V1 and V2 support. A C# mod that directly references old JSONLoader assemblies is a different case because binary compatibility is not guaranteed by file-format compatibility. Such a mod should be tested and may require an adapter or updated integration.

## Will older mods remain compatible?

Old JSON formats are explicit compatibility targets. Runtime compatibility still depends on referenced cards, abilities, assets, APIs, and other dependencies. Old compiled DLLs represent a separate binary-compatibility question and should not be assumed to work merely because the corresponding JSON file loads.

## How can I ensure compatibility?

Use documented formats, unique prefixes, explicit asset paths, schema validation, intentional `fieldsToEdit` operations, and isolated C# loader integration. Test against the exact stable or Nightly version you intend to support. Avoid relying on undocumented load order, duplicate identity behavior, or temporary internal classes.

## What does Nightly entail?

Nightly is the development/preview architecture for the next generation of JSONLoader and the related JSON/CSV loader system. The current package points to `Refactor-JSONLoader-3` and describes itself as a preview of what is coming.

## What does Nightly offer that stable does not?

The most important difference is architectural generalization around file discovery, schemas, validation, image scanning, configuration, logging, metadata, and format-specific support. Some individual features already existed in stable V2, so Nightly's significance is primarily how those capabilities are organized and prepared for future formats.

## How are files loaded?

Configuration establishes search origins. File discovery searches those locations recursively, the loader classifies files, format-specific support parses them, schema validation checks structure, intermediate objects are constructed, images and other assets are resolved, conversion creates or modifies runtime representations, and the Inscryption API receives the result. The exact sequencing of individual internal calls can vary by Nightly version, so the sequence should be treated as the architectural model rather than a promise of one fixed call stack.

## How do I use JSON Editor?

Obtain the schema corresponding to the loader and content type you are targeting. Give that schema to JSON Editor, use the generated interface to create or edit the JSON, and then validate the resulting document against the actual Nightly environment. JSON Editor helps author the document, but Nightly remains the final runtime authority.

## How does Nightly handle duplicates?

New content should have unique internal identities, normally using a unique `modPrefix`. Existing content should be intentionally modified through `fieldsToEdit`. Two independent definitions that accidentally resolve to the same identity are collisions and should not be treated as a documented merge or last-write-wins mechanism.

## Did the research account for all V1 and V2 releases?

The report enumerates the published V1 and V2 version sequences and explains the documented feature significance of releases for which reliable changelog information is available. Patch releases without distinct documented features are explicitly identified as maintenance releases rather than assigned invented functionality. This is necessary for a technically responsible release history.

## Did the research cover all Nightly-added types?

It covers the major verified Nightly architectural categories, including plugin coordination, filesystem loading, schema generation and loading, linting, image handling, metadata processing, V1/V2/V3 support, and the intermediate card representation. It also distinguishes an early source-level inventory from a permanent public API list. This distinction is necessary because the current Nightly package is a development branch and its internal implementation can change.

## Does the report provide exact JSON?

It distinguishes official published structures from schema-shaped and illustrative examples. The starter-deck, tribe, and encounter structures are documented V2 structures, while card examples are explicitly labeled representative unless directly established against the target schema. This prevents an illustrative teaching example from being mistaken for a guaranteed drop-in file for every loader version.

---

# 95. Final technical assessment

JSONLoader's history is best understood as three architectural stages. V1 established a focused JSON-based card-definition system. V2 rewrote the loader around the Inscryption API 2.x generation and expanded it into a much broader content-authoring framework. Nightly is attempting to reorganize that accumulated functionality into a more reusable architecture capable of supporting multiple generations and input formats.

The core architectural direction is:

```text
filesystem discovery
        |
schema generation
        |
validation
        |
image handling
        |
logging
        |
configuration
        |
format-specific interpretation
```

The key difference is that these systems are increasingly treated as reusable infrastructure rather than as implementation details belonging to one particular JSON format. V1 and V2 then become compatibility layers within that framework, while V3 and CSV become future-oriented format pathways. This is why Nightly can be important even before its V3 feature set is complete.

The most important practical lesson is that **data compatibility and binary compatibility are not the same thing**. An existing `.jldr` or `.jldr2` file can remain usable because Nightly has dedicated support for those generations. A C# DLL compiled against an old JSONLoader assembly can still break because its dependency is on classes, methods, namespaces, and assembly contracts rather than merely on the JSON file format.

The second major lesson is that **Nightly should not be treated as a guaranteed superset of stable 2.7.0**. It is newer in architecture, but stable V2 has accumulated a substantial feature set over many releases. The current Nightly documentation does not establish that every mature V2 subsystem has been reproduced as a complete V3 implementation. The current package still presents itself as a preview, and its V3 and CSV documentation areas remain incomplete.

The third lesson is that **schemas are central to the new architecture**. A schema can describe types, required fields, arrays, nested objects, and other structural constraints. Generated schemas can then feed validators, linting tools, documentation, and external authoring interfaces such as JSON Editor. This makes schema generation one of the most important bridges between JSONLoader's internal implementation and its author-facing tooling.

The fourth lesson is that **identity management matters**. `modPrefix` is not merely decorative, and `fieldsToEdit` is not merely another optional field. Together, they help distinguish creation from modification and reduce the risk of unrelated mods accidentally targeting the same internal object. Unique identities should be treated as a fundamental compatibility practice.

The fifth lesson is that **file loading is itself an architecture**. Finding files, deciding which files should be loaded, identifying their format, validating their structure, resolving artwork, constructing intermediate objects, and registering runtime content are separate problems. Nightly's attempt to separate those responsibilities is one of the clearest indicators that JSONLoader 3 is intended to be a framework rather than merely another parser.

Finally, Nightly is significant because it represents an attempt to prevent JSONLoader from becoming an ever-growing collection of format-specific special cases. The refactor is trying to establish reusable infrastructure so that V1, V2, V3, and CSV can share file discovery, configuration, validation, schema handling, logging, documentation, and asset processing. That is the deeper meaning of JSONLoader 3: not simply a new extension, but an attempt to turn JSONLoader into a more general content-loading platform.

---

# 96. Source-quality and uncertainty statement

This report intentionally separates four evidence levels:

```text
A. Published documentation
B. Published release/changelog information
C. Source/decompiled implementation evidence
D. Architectural interpretation
```

Published documentation is treated as the primary authority for author-facing behavior. Published release notes are used to establish historical feature changes where they provide explicit evidence. Source and decompiled implementation evidence is used to explain internal behavior, but an internal method discovered in one Nightly build is not automatically treated as a permanent public API. Architectural interpretations are explicitly distinguished from maintainer-authored explanations.

This separation is particularly important for Nightly. The current package itself warns that its older embedded documentation may become outdated and directs readers to the current Wiki systems. The package is also explicitly presented as a preview of future JSONLoader and CSVLoader functionality. Therefore, a technically responsible report must be willing to say "this was observed in the examined source" rather than silently upgrading that observation into "this is the permanent JSONLoader 3 API."

---

# 97. Primary research references

**JSONLoader Releases**

[JSONLoader Releases](https://github.com/MADH95/JSONLoader/releases?utm_source=chatgpt.com)

**JSONLoader Stable Repository**

[JSONLoader Stable Repository](https://github.com/MADH95/JSONLoader?utm_source=chatgpt.com)

**JSONLoader Nightly Refactor Branch**

[JSONLoader Nightly Refactor Branch](https://github.com/MADH95/JSONLoader/tree/Refactor-JSONLoader-3?utm_source=chatgpt.com)

**Stable JSONCardLoader**

[Stable JSONCardLoader](https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/?utm_source=chatgpt.com)

**Stable JSONCardLoader Versions**

[Stable JSONCardLoader Versions](https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/versions?utm_source=chatgpt.com)

**Stable JSONCardLoader Wiki**

[Stable JSONCardLoader Wiki](https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/wiki?utm_source=chatgpt.com)

**Stable JSONLoader GitHub Wiki**

[Stable JSONLoader GitHub Wiki](https://github.com/MADH95/JSONLoader/wiki?utm_source=chatgpt.com)

**Stable Wiki Repository**

[Stable Wiki Repository](https://github.com/Chaosyr/JSONCardLoaderWiki/tree/main?utm_source=chatgpt.com)

**Nightly JSON and CSV Loader**

[Nightly JSON and CSV Loader](https://thunderstore.io/c/inscryption/p/MADH95Mods/JSON_and_CSV_Loader_Nightly/?utm_source=chatgpt.com)

**Nightly Versions**

[Nightly Versions](https://thunderstore.io/c/inscryption/p/MADH95Mods/JSON_and_CSV_Loader_Nightly/versions?utm_source=chatgpt.com)

**Nightly Wiki**

[Nightly Wiki](https://thunderstore.io/c/inscryption/p/MADH95Mods/JSON_and_CSV_Loader_Nightly/wiki?utm_source=chatgpt.com)

**Nightly Wiki Repository Snapshot**

[Nightly Wiki Repository Snapshot](https://github.com/Chaosyr/JSONCardLoaderWiki/tree/8a07abba3108bc665bd87e2f01da5773b55729d7?utm_source=chatgpt.com)

**Nightly GitHub Wiki**

[Nightly GitHub Wiki](https://github.com/Chaosyr/JSONCardLoaderWiki/wiki?utm_source=chatgpt.com)

**JSON Editor**

[JSON Editor](https://json-editor.github.io/json-editor/?utm_source=chatgpt.com)

The current Nightly package documentation confirms its role as the preview/development line for JSONLoader and CSVLoader, identifies the `Refactor-JSONLoader-3` development branch, documents the V1 and V2 support systems, describes the Fields To Edit and Extension Properties systems, and provides the current JSON/CSV configuration defaults.

---

# 98. Final practical reference card

For a mod author who wants the entire report condensed into one operational model, the architecture can be remembered as:

```text
                 YOUR MOD
                    |
          +---------+---------+
          |                   |
       JSON/CSV            Artwork
          |                   |
          +---------+---------+
                    |
                    v
              FILE LOADER
                    |
              +-----+-----+
              |           |
          discovery   classification
              |           |
              +-----+-----+
                    |
          +---------+---------+
          |         |         |
         V1        V2        V3/CSV
          |         |         |
          +---------+---------+
                    |
                SCHEMA
                    |
             +------+------+
             |             |
          validation    JSON Editor
             |
          intermediate
            object
             |
        image resolution
             |
          conversion
             |
       Inscryption API
             |
        runtime content
```

For identity:

```text
New content
    ↓
unique modPrefix + name

Existing content
    ↓
name + fieldsToEdit

External extension data
    ↓
extensionProperties

Artwork
    ↓
explicit relative path preferred

Validation
    ↓
schema + linter

Runtime
    ↓
Inscryption API
```

For compatibility:

```text
Old .jldr
    ↓
V1 compatibility

Old .jldr2
    ↓
V2 compatibility

Old DLL
    ↓
binary compatibility must be tested

New V3
    ↓
development target, not assumed complete
```

For debugging:

```text
File found?
    ↓
Correct extension?
    ↓
Correct loader generation?
    ↓
Valid JSON?
    ↓
Schema valid?
    ↓
References valid?
    ↓
Images found?
    ↓
Conversion successful?
    ↓
API registration successful?
    ↓
Gameplay correct?
```

That sequence captures the central lesson of the entire project. JSONLoader is not merely a file extension parser. It is a pipeline that turns declarative content into runtime game objects, and Nightly is an attempt to make that pipeline modular enough to support several generations of content without rebuilding the same infrastructure for each one.