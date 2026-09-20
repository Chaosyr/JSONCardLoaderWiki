```xml
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>JSON Loader v3</name>
    </assembly>
    <members>
        <member name="T:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil">
            <summary>
            This class represents the Configil Data Type.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.name">
            <summary>
            The In-Code name of the Sigil.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.GUID">
            <summary>
            The In-Code GUID/ModPrefix of the Sigil.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.displayName">
            <summary>
            The In-Game name of the Sigil.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.description">
            <summary>
            The Description of the Sigil shown in the Rulebook.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.metaCategories">
            <summary>
            The Meta Categories which Apply to this Sigil.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.texture">
            <summary>
            The Path to your sigils Icon, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '49x49' image. This is your sigils Icon within 3D acts.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.pixelTexture">
            <summary>
            The Path to your sigils Act 2 Icon, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '49x49' image. This is your sigils Icon within 2D acts.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.powerLevel">
            <summary>
            The Sigils Power Level.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.abilityLearnedDialouge">
            <summary>
            The Dialogue in which will appear when the Sigil is learned for the first time.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.priority">
            <summary>
            How high in priority this sigils activation is.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.opponentUsable">
            <summary>
            Whether this sigil should be usable by the Opponent.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.canStack">
            <summary>
            Whether this sigil should be able to be stacked.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.isSpecialAbility">
            <summary>
            Whether this sigil is actually a Special Ability.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.isPowerStat">
            <summary>
            Whether this Special Ability is actually a Power Stat as well.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.appliesToAttack">
            <summary>
            Whether this Power Stat applies to Attack.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.appliesToHealth">
            <summary>
            Whether this Power Stat applies to Health.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.ConfigilsV1Support.Schemas.Sigil.configilSchema">
            <summary>
            The Underarching Schema for a Configil.
            </summary>
        </member>
        <member name="T:JSONLoader3.Cores.ConfigilsV1Support.Schemas.UnderarchingConfigilSchema">
            <summary>
            The Underarching Configils Schema for Sigils and Items.
            </summary>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject">
            <summary>
            An Object representing an <see cref="T:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card"/>.
            </summary>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.fieldsToEdit">
            <summary>
            A List of fields to Overwrite in the case the Card's Name belongs to the base game.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.name">
            <summary>
            The cards In-Code name.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.displayedName">
            <summary>
            The cards In-Game name.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.description">
            <summary>
            The Description of the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.metaCategories">
            <summary>
            A List of all Meta Categories the card has.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.cardComplexity">
            <summary>
            The Complexity of the Card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.temple">
            <summary>
            The Card's Temple.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.baseAttack">
            <summary>
            An Int determining the cards BaseAttack.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.baseHealth">
            <summary>
            An Int determining the cards BaseHealth.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.hideAttackAndHealth">
            <summary>
            A Boolean determining whether the Attack and Health are hidden or not.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.bloodCost">
            <summary>
            An Int representing the Blood Cost of the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.bonesCost">
            <summary>
            An Int representing the Bone Cost of the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.energyCost">
            <summary>
            An Int representing the Energy Cost of the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.gemColors">
            <summary>
            A List representing all the Gem Colors applied to the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.specialStatIcon">
            <summary>
            A string representing what Stat Icon to apply to the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.tribes">
            <summary>
            A List of all Tribes that the card has.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.traits">
            <summary>
            A List of all Traits that the card has.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.specialAbilities">
            <summary>
            A List of all Special Abilities that the card has.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.abilities">
            <summary>
            A List of all Abilities that the card has.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.customAbilities">
            <summary>
            A List of the Modded Abilities that the card has.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.customSpecialAbilities">
            <summary>
            A List of the Modded Special Abilities that the card has.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.evolution">
            <summary>
            The Evolve Ability Related Parameters.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.defaultEvolutionName">
            <summary>
            The Default Evolution Name for the Card if it has no Evolve Ability Related Parameters.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.tail">
            <summary>
            The LooseTail Ability Related Parameters.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.iceCube">
            <summary>
            The IceCube Ability related Parameters.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.flipPortraitForStrafe">
            <summary>
            A boolean determining whether the Portrait should Flip on Strafe.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.onePerDeck">
            <summary>
            A boolean determining if only one version of the card is allowed in the deck or not.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.appearanceBehaviour">
            <summary>
            A List of AppearanceBehaviours to apply to the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.texture">
            <summary>
            The Card's Portrait.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.altTexture">
            <summary>
            The Alternate Version of the Card's Portrait.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.emissionTexture">
            <summary>
            The Emission Version of the Card's Portrait.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.titleGraphic">
            <summary>
            The Title Graphic of the Card, this appears overlayed on the card's name.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.pixelTexture">
            <summary>
            The Act 2 Version of the Card's Portrait.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.decals">
            <summary>
            A list of all Decal paths to be on the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.file">
            <summary>
            The Internal full path to the File the card came from.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.pluginName">
            <summary>
            The Internal full path to the Plugin the card came from.
            </summary>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.#ctor(System.Collections.Generic.List{System.String},System.String,System.String,System.String,System.Collections.Generic.List{System.String},System.String,System.String,System.Int32,System.Int32,System.Boolean,System.Int32,System.Int32,System.Int32,System.Collections.Generic.List{System.String},System.String,System.Collections.Generic.List{System.String},System.Collections.Generic.List{System.String},System.Collections.Generic.List{System.String},System.Collections.Generic.List{System.String},System.Collections.Generic.List{JSONLoader3.Cores.JSONLoaderV1Support.Objects.AbilityData},System.Collections.Generic.List{JSONLoader3.Cores.JSONLoaderV1Support.Objects.SpecialAbilityData},JSONLoader3.Cores.JSONLoaderV1Support.Objects.EvolveData,System.String,JSONLoader3.Cores.JSONLoaderV1Support.Objects.TailData,JSONLoader3.Cores.JSONLoaderV1Support.Objects.IceCubeData,System.Boolean,System.Boolean,System.Collections.Generic.List{System.String},System.String,System.String,System.String,System.String,System.String,System.Collections.Generic.List{System.String},System.String,System.String)">
            <summary>
            The Constructor for making Card Objects.
            </summary>
            <param name="fieldsToEdit"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.fieldsToEdit"/></param>
            <param name="name"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.name"/></param>
            <param name="displayedName"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.displayedName"/></param>
            <param name="description"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.description"/></param>
            <param name="metaCategories"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.metaCategories"/></param>
            <param name="cardComplexity"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.cardComplexity"/></param>
            <param name="temple"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.temple"/></param>
            <param name="baseAttack"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.baseAttack"/></param>
            <param name="baseHealth"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.baseHealth"/></param>
            <param name="hideAttackAndHealth"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.hideAttackAndHealth"/></param>
            <param name="bloodCost"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.bloodCost"/></param>
            <param name="bonesCost"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.bonesCost"/></param>
            <param name="energyCost"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.energyCost"/></param>
            <param name="gemColors"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.gemColors"/></param>
            <param name="specialStatIcon"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.specialStatIcon"/></param>
            <param name="tribes"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.tribes"/></param>
            <param name="traits"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.traits"/></param>
            <param name="specialAbilities"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.specialAbilities"/></param>
            <param name="abilities"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.abilities"/></param>
            <param name="customAbilities"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.customAbilities"/></param>
            <param name="customSpecialAbilities"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.customSpecialAbilities"/></param>
            <param name="evolution"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.evolution"/></param>
            <param name="defaultEvolutionName"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.defaultEvolutionName"/></param>
            <param name="tail"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.tail"/></param>
            <param name="iceCube"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.iceCube"/></param>
            <param name="flipPortraitForStrafe"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.flipPortraitForStrafe"/></param>
            <param name="onePerDeck"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.onePerDeck"/></param>
            <param name="appearanceBehaviour"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.appearanceBehaviour"/></param>
            <param name="texture"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.texture"/></param>
            <param name="altTexture"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.altTexture"/></param>
            <param name="emissionTexture"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.emissionTexture"/></param>
            <param name="titleGraphic"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.titleGraphic"/></param>
            <param name="pixelTexture"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.pixelTexture"/></param>
            <param name="decals"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.decals"/></param>
            <param name="file"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.file"/></param>
            <param name="pluginName"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.pluginName"/></param>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV1Support.Objects.CardObject.ConvertCardObjectToCardInfo">
            <summary>
            Converts the given CardObject into a CardInfo and adds it automatically via the API.
            </summary>
            <returns>A CardInfo representing the card passed in.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV1Support.Objects.AbilityData">
            <summary>
            An Object Representing Modded Abilities
            </summary>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.AbilityData.name">
            <summary>
            The Name of the Ability.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.AbilityData.GUID">
            <summary>
            The GUID of the Ability.
            </summary>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV1Support.Objects.AbilityData.#ctor(System.String,System.String)">
            <summary>
            A Constructor for Modded Abilities.
            </summary>
            <param name="name"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.AbilityData.name"/></param>
            <param name="GUID"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.AbilityData.GUID"/></param>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV1Support.Objects.AbilityData.GetAbility">
            <summary>
            A function that fetches the Modded Ability.
            </summary>
            <returns>An Ability associated wih the Modded Ability</returns>
            <remarks>This code is derived from code made by LilySylvie.</remarks>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV1Support.Objects.SpecialAbilityData">
            <summary>
            An Object Representing Modded Special Abilities
            </summary>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.SpecialAbilityData.name">
            <summary>
            The Name of the Special Ability.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.SpecialAbilityData.GUID">
            <summary>
            The GUID Of the Special Ability.
            </summary>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV1Support.Objects.SpecialAbilityData.#ctor(System.String,System.String)">
            <summary>
            A Constructor for Modded Special Abilities.
            </summary>
            <param name="name"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.SpecialAbilityData.name"/></param>
            <param name="GUID"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.SpecialAbilityData.GUID"/></param>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV1Support.Objects.SpecialAbilityData.GetSpecialAbility">
            <summary>
            A function that fetches the Modded Special Ability.
            </summary>
            <returns>A SpecialTriggeredAbility associated wih the Modded Special Ability</returns>
            <remarks>This code is derived from code made by LilySylvie.</remarks>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV1Support.Objects.EvolveData">
            <summary>
            An Object representing the Evolution Parameters.
            </summary>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.EvolveData.name">
            <summary>
            The Name of the Card this card will Evolve into.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.EvolveData.turnsToEvolve">
            <summary>
            The Amount of Turns this card needs in order to evolve.
            </summary>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV1Support.Objects.EvolveData.#ctor(System.String,System.Int32)">
            <summary>
            A Constructor for the Evolution Parameters.
            </summary>
            <param name="name"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.EvolveData.name"/></param>
            <param name="turnsToEvolve"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.EvolveData.turnsToEvolve"/></param>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV1Support.Objects.TailData">
            <summary>
            An Object representing the Tail Parameters.
            </summary>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.TailData.name">
            <summary>
            The Name of the Card that will become the Tail.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.TailData.tailLostPortrait">
            <summary>
            The Portrait the card gains after losing its tail.
            </summary>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV1Support.Objects.TailData.#ctor(System.String,System.String)">
            <summary>
            A Constructor for the Tail Parameters.
            </summary>
            <param name="name"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.TailData.name"/></param>
            <param name="tailLostPortrait"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.TailData.tailLostPortrait"/></param>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV1Support.Objects.IceCubeData">
            <summary>
            An Object representing the IceCube Parameters.
            </summary>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.IceCubeData.creatureWithin">
            <summary>
            The Card this will become on death.
            </summary>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV1Support.Objects.IceCubeData.#ctor(System.String)">
            <summary>
            A constructor for the IceCue Parameters.
            </summary>
            <param name="creatureWithin"><see cref="P:JSONLoader3.Cores.JSONLoaderV1Support.Objects.IceCubeData.creatureWithin"/></param>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card">
            <summary>
            The main data Object for JSONLoader V1's Card system.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.fieldsToEdit">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string array for the fields you wish to edit. The fields must be the exact names as in the right hand side of this table" |
            
             New Description from JSONLoader v3.0.0: Any items applied within this field will be used for overwriting the In-Game card associated with the field 'name'.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.name">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string for the name the game will use to identify the card - should contain no spaces. When editing, this field must match the card's name (See Card Names.txt for a list of ingame card names)" |
            
             New Description from JSONLoader v3.0.0: The In-Code name for the card, please append on a Prefix unique to your mod if you are NOT editing a base game card. For example; "JSONFanMod5_Gorilla".
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.displayedName">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string for the name displayed on the card" |
            
             New Description from JSONLoader v3.0.0: The In-Game name for the card, it can be anything as long as this font can display it; https://font.download/font/heavyweight
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.description">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string for the description Leshy gives when you find the card" |
            
             New Description from JSONLoader v3.0.0: The In-Game flavor for the card, this will show when receiving the card for the first time, if you want to prevent it being seen from saving use; https://thunderstore.io/c/inscryption/p/creator/Fuck_Dialouge_Saving/
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.metaCategories">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string array of meta catagories the card has (See Enums.txt for a list of catagories)" |
            
             New Description from JSONLoader v3.0.0: These Meta-Categories control how your card will show up within the game, see the following page for what each of them do; https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/wiki/5396-vanilla-enums
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.cardComplexity">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string for the complexity of the card (See Enums.txt for a list of levels of complexity)" |
            
             New Description from JSONLoader v3.0.0: This controls WHEN your card can show up in the game, see the following page for what each of them do; https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/wiki/5396-vanilla-enums
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.temple">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string for which Scrybe created the card" |
            
             New Description from JSONLoader v3.0.0: This controls which temple in Act 2 the card is apart of, as well as meant to determine which Act outside Act 2 the card shows up in, whether mods follow the convention is up to question, but that's what these do. So, Nature is Act 1 and the Nature Temple, Tech is Act 3 and the Technology Temple, Undead is the Grimora Portion of the Finale and the Undead Temple, Wizard is the Magnificus Portion of the Finale and the Magicks Temple.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.baseAttack">
             <summary>
             Original Description from JSONLoader v1.7.2: "An integer value for the attack of a card" |
            
             New Description from JSONLoader v3.0.0: This value determines the attack value of the card, it cannot be negative.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.baseHealth">
             <summary>
             Original Description from JSONLoader v1.7.2: "An integer value for the health of a card" |
            
             New Description from JSONLoader v3.0.0: This value determines the health value of the card, it cannot be negative or 1.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.hideAttackAndHealth">
             <summary>
             Original Description from JSONLoader v1.7.2: "A boolean value to toggle if the cards attack and health are visible" |
            
             New Description from JSONLoader v3.0.0: This boolean value determines whether the Attack and Health of the card should be hidden or not.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.bloodCost">
             <summary>
             Original Description from JSONLoader v1.7.2: "An integer value for the blood cost of a card" |
            
             New Description from JSONLoader v3.0.0: This value determines the amount of Blood this card will cost.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.bonesCost">
             <summary>
             Original Description from JSONLoader v1.7.2: "An integer value for the bones cost of a card" |
            
             New Description from JSONLoader v3.0.0: This value determines the amount of Bones this card will cost.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.energyCost">
             <summary>
             Original Description from JSONLoader v1.7.2: "An integer value for the energy cost of a card" |
            
             New Description from JSONLoader v3.0.0: This value determines the amount of Energy this card will cost.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.gemColors">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string array for the gems cost of a card (See Enums.txt for a list of gems)" |
            
             New Description from JSONLoader v3.0.0: The following 3 values are accepted here: Green for the Green Gem, Orange for the Orange Gem, and Blue for the Blue Gem. Each of these correlates to the Gem Cost of a card. This version of JSONLoader does not support multiple of the same color of gem.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.specialStatIcon">
             <summary>
             Original Description from JSONLoader v1.7.2: "An string for which special stat icon the card has (See Enums.txt for a list of icons)" |
            
             New Description from JSONLoader v3.0.0: This determines which Stat Icon to show on the card, this must be used alongside the associated Special Ability.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.tribes">
             <summary>
             Original Description from JSONLoader v1.7.2: "An string array for the tribes the card belongs to (See Enums.txt for a list of tribes)" |
            
             New Description from JSONLoader v3.0.0: This List determines what Tribes are applied to the card, this works with Base Game tribes only. Use a newer version of JSONLoader for Modded Tribes. You can find the full list here; https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/wiki/5396-vanilla-enums
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.traits">
             <summary>
             Original Description from JSONLoader v1.7.2: "An string array for the traits a card has (See Enums.txt for a list of traits)" |
            
             New Description from JSONLoader v3.0.0: This List determines what Traits are applied to this card, this works with Base Game traits only. Use a newer version of JSONLoader for Modded Traits. You can find the full list here; https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/wiki/5396-vanilla-enums
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.specialAbilities">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string array for the special abilities a card has (See Enums.txt for a list of special abilities)" |
            
             New Description from JSONLoader v3.0.0: This List determines what Special Abilities are applied to this card, this works specifically with Base Game Special Abilities. For Modded Special Abilities utilize the 'customSpecialAbilities' field. You can find the full list here; https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/wiki/5396-vanilla-enums
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.abilities">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string array for the sigils a card has. (See Enums.txt for a list of sigil abilities)." |
            
             New Description from JSONLoader v3.0.0: This List determines what Abilities are applied to this card, this works specifically with Base Game Abilities. For Modded Abilities utilize the 'customAbilities' field. You can find the full list here; https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/wiki/5396-vanilla-enums
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.customAbilities">
             <summary>
             Original Description from JSONLoader v1.7.2: "An array of objects for the custom ability name and mod GUID (It's children are in the table below this one)" |
            
             New Description from JSONLoader v3.0.0: This List determines the Modded Abilities that will be applied to this card. You may find this to be a useful resource; https://github.com/Chaosyr/SaxbyModEnums/wiki
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.customSpecialAbilities">
             <summary>
             Original Description from JSONLoader v1.7.2: "An array of objects for the custom special ability name and mod GUID (It's children are in the table below this one)" |
            
             New Description from JSONLoader v3.0.0: This List determines the Modded Special Abilities that will be applied to this card. You may find this to be a useful resource; https://github.com/Chaosyr/SaxbyModEnums/wiki
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.evolution">
             <summary>
             Original Description from JSONLoader v1.7.2: "A json object for the evolveParams of the card. (It's children are in the table below this one)" |
            
             New Description from JSONLoader v3.0.0: This Object determines the Evolution related Parameters for this card, such as what it will turn into, and how long it will take to turn into it.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.defaultEvolutionName">
             <summary>
             Original Description from JSONLoader v1.7.2: "The name the card will have when it evolves (when it doesn't have evolve_ fields set)" |
            
             New Description from JSONLoader v3.0.0: This determines what the Default Evolution Name will be, note it will appear in the format of; '[defaultEvolutionName] [displayedName]', just replace the variables with your JSON's values.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.tail">
             <summary>
             Original Description from JSONLoader v1.7.2: "A json object for the tailParams of the card. (It's children are in the table below this one)" |
            
             New Description from JSONLoader v3.0.0: This Object determines the LooseTail related Parameters for this card, such as this cards Texture after losing its tail, or the Card the Tail Will Be.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.iceCube">
             <summary>
             Original Description from JSONLoader v1.7.2: "A json object for the iceCubeParams of the card. (It's children are in the table below this one)" |
            
             New Description from JSONLoader v3.0.0: This Object determines the IceCube related Parameters for this card, namely what card it will be turned into, if left empty the default is an Opossum.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.flipPortraitForStrafe">
             <summary>
             Original Description from JSONLoader v1.7.2: "A boolean to determine if the cards portrait should flip when it uses one of the strafe sigils" |
            
             New Description from JSONLoader v3.0.0: A bool determining whether this cards portrait will flip when the card moves. (like the sigil icon does)
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.onePerDeck">
             <summary>
             Original Description from JSONLoader v1.7.2: "A boolean value that toggles if there can be only one of the card per deck" |
            
             New Description from JSONLoader v3.0.0: A bool determining if there can only be one copy of this card within the Player's deck.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.appearanceBehaviour">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string array for the behaviours the cards appearance should have (See enums.txt for a list of appearance behaviours)" |
            
             New Description from JSONLoader v3.0.0: This List determines the Appearance Behaviors in which will be applied to this card. Use a newer version of JSONLoader for Modded Appearance Behaviors. You can find the full list here; https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/wiki/5396-vanilla-enums
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.texture">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string for the name of the card's image (must be .png). If it is in a subfolder within Artwork the subfolder should preceed the file name seperated by a '/' (or your system equivelent)" |
            
             New Description from JSONLoader v3.0.0: The Path to your cards Portrait, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '114x94' image.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.altTexture">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string for the name of the card's alternate image (must be .png)" |
            
             New Description from JSONLoader v3.0.0: The Path to your cards Alternative Portrait, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '114x94' image. This applies in the case you have a Goat's Eye or possibly some other cases.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.emissionTexture">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string for the name of the card's emission image (must be .png)" |
            
             New Description from JSONLoader v3.0.0: The Path to your cards Emissive Portrait, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '114x94' image. This applies in the case you've transferred a sigil at the Sacrificial Stones onto this card.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.titleGraphic">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string for the name of the card's title image (must be .png)" |
            
             New Description from JSONLoader v3.0.0: The Path to your cards Title Graphic, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '113x28' image. This applies specifically over your card name as a way of obscuring it like the Tentacle Cards are.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.pixelTexture">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string for the name of the card's act2 image (must be .png)" |
            
             New Description from JSONLoader v3.0.0: The Path to your cards Pixel Portrait, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '41x28' image. This applies specifically in Act 2, its just that act's version of the card portrait.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card.decals">
             <summary>
             Original Description from JSONLoader v1.7.2: "A string array for the texture names of a card decals (must be .png)" |
            
             New Description from JSONLoader v3.0.0: This is a list of all the Decal Images in which will be stacked onto your card, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '125x190' image.
             </summary>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.AbilityData">
            <summary>
            An Object for the Custom Ability related Data for JSONLoader V1's Card system.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.AbilityData.name">
             <summary>
             Original Description from JSONLoader v1.7.2: "The name of the ability. This may be seperate form the name that appears in the book, check the mod description or ask in the discord for specifics" |
            
             New Description from JSONLoader v3.0.0: This is the In-Code name of the Ability.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.AbilityData.GUID">
             <summary>
             Original Description from JSONLoader v1.7.2: "The GUID the mod maker made for their mod. This may be found in the mod description. It is usually in the layout of 'MakerName.inscryption.ModName'" |
            
             New Description from JSONLoader v3.0.0: This is the Ability Libraries GUID, it's a similar concept to your card's prefix.
             </summary>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.SpecialAbilityData">
            <summary>
            An Object for the Custom Special Ability related Data for JSONLoader V1's Card system.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.SpecialAbilityData.name">
             <summary>
             Original Description from JSONLoader v1.7.2: "The name of the special ability. This may be seperate form the name that appears in the book, check the mod description or ask in the discord for specifics" |
            
             New Description from JSONLoader v3.0.0: This is the In-Code name of the Special Ability.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.SpecialAbilityData.GUID">
             <summary>
             Original Description from JSONLoader v1.7.2: "The GUID the mod maker made to identify their mod. This may be found in the mod description. It is usually in the layout of 'MakerName.inscryption.ModName'" |
            
             New Description from JSONLoader v3.0.0: This is the Special Ability Libraries GUID, it's a similar concept to your card's prefix.
             </summary>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.EvolveData">
            <summary>
            An Object for the Evolve related Data for JSONLoader V1's Card system.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.EvolveData.name">
             <summary>
             Original Description from JSONLoader v1.7.2: "The name of the card this card evolves into (See Card Names.txt for a list of ingame card names)" |
            
             New Description from JSONLoader v3.0.0: This represents the In-Code name of the card this card is meant to evolve into. 
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.EvolveData.turnsToEvolve">
             <summary>
             Original Description from JSONLoader v1.7.2: "The number of turns til the card evolves (The game supports sigil art for up to 3 turns)" |
            
             New Description from JSONLoader v3.0.0: This value represents the amount of turns it takes for this card to evolve. This version's Turn Count must be between 1-3 for more use a newer version of JSONLoader.
             </summary>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.TailData">
            <summary>
            An Object for the Tail related Data for JSONLoader V1's Card system.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.TailData.name">
             <summary>
             Original Description from JSONLoader v1.7.2: "The name of the tail card this will produce (See Card Names.txt for a list of ingame card names)" |
            
             New Description from JSONLoader v3.0.0: This represents the In-Code name of the card this card will leave in its old lane if Loose Tail triggers.
             </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.TailData.tailLostPortrait">
             <summary>
             Original Description from JSONLoader v1.7.2: "The portrait the card should have once it's tail is lost" |
            
             New Description from JSONLoader v3.0.0: The Path to your cards Tail Lost Portrait, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '114x94' image. This applies specifically when this card is struck and lost its tail.
             </summary>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.IceCubeData">
            <summary>
            An Object for the IceCube related Data for JSONLoader V1's Card system.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.IceCubeData.creatureWithin">
             <summary>
             Original Description from JSONLoader v1.7.2: "The name of the creature the card should turn into when it perishes (See Card Names.txt for a list of ingame card names)" |
            
             New Description from JSONLoader v3.0.0: This represents the In-Code name of the card this card will leave behind in its place when it is to die.
             </summary>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV1Support.Utilities.CardUtils">
            <summary>
            A class for <see cref="T:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card"/> related Utilities.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Utilities.CardUtils.CardsToLoad">
            <summary>
            A list of all the <see cref="T:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card"/> Files in which we need to load.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV1Support.Utilities.CardUtils.allJLDRCards">
            <summary>
            An internal facing List of all JLDR <see cref="T:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card"/>s passed to the API.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV1Support.Utilities.CardUtils.allJLDRCardsPublic">
            <summary>
            A public facing read-only collection of all JLDR <see cref="T:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card"/>s passed to the API.
            </summary>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV1Support.Utilities.CardUtils.HandleCards">
            <summary>
            A function to handle the loading of <see cref="T:JSONLoader3.Cores.JSONLoaderV1Support.Schemas.Card"/>'s.
            </summary>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV1Support.Utilities.CardUtils.Parse(System.Collections.Generic.List{System.ValueTuple{System.Int32,System.String,System.String}},System.String,System.String)">
            <summary>
            This function handles the Parsing of a Card into the Game.
            </summary>
            <param name="JSONCard">A List (of a int resembling JSON depth, a string resembling the field Name, a string resembling the string Value) representing the Card.</param>
            <param name="file">The full Path to the File.</param>
            <param name="pluginName">The full Path to the Plugin.</param>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject">
            <summary>
            An Object representing an <see cref="T:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card"/>.
            </summary>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.fieldsToEdit">
            <summary>
            A List of fields to Overwrite in the case the Card's Name belongs to the base game.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.name">
            <summary>
            The cards In-Code name.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.modPrefix">
            <summary>
            The cards In-Code ModPrefix (this is to help you extract the raw name, as name automatically has the prefix attached.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.displayedName">
            <summary>
            The cards In-Game name.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.description">
            <summary>
            The Description of the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.metaCategories">
            <summary>
            A List of all Meta Categories the card has.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.cardComplexity">
            <summary>
            The Complexity of the Card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.temple">
            <summary>
            The Card's Temple.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.baseAttack">
            <summary>
            An Int determining the cards BaseAttack.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.baseHealth">
            <summary>
            An Int determining the cards BaseHealth.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.hideAttackAndHealth">
            <summary>
            A Boolean determining whether the Attack and Health are hidden or not.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.bloodCost">
            <summary>
            An Int representing the Blood Cost of the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.bonesCost">
            <summary>
            An Int representing the Bones Cost of the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.energyCost">
            <summary>
            An Int representing the Energy Cost of the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.gemsCost">
            <summary>
            A List representing all the Gem Colors applied to the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.specialStatIcon">
            <summary>
            A string representing what Stat Icon to apply to the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.tribes">
            <summary>
            A List of all Tribes that the card has.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.traits">
            <summary>
            A List of all Traits that the card has.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.abilities">
            <summary>
            A List of all Abilities that the card has.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.specialAbilities">
            <summary>
            A List of all Special Abilities that the card has.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.evolveIntoName">
            <summary>
            The Name of the Card this card will Evolve into.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.evolveTurns">
            <summary>
            The Amount of Turns this card needs in order to evolve.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.defaultEvolutionName">
            <summary>
            The Default Evolution Name for the Card if it has no Evolve Ability Related Parameters.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.tailName">
            <summary>
            The Name of the Card that will become the Tail.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.tailLostPortrait">
            <summary>
            The Portrait the card gains after losing its tail.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.iceCubeName">
            <summary>
            The Card this will become on death.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.flipPortraitForStrafe">
            <summary>
            A boolean determining whether the Portrait should Flip on Strafe.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.onePerDeck">
            <summary>
            A boolean determining if only one version of the card is allowed in the deck or not.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.appearanceBehaviour">
            <summary>
            A List of AppearanceBehaviours to apply to the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.texture">
            <summary>
            The Card's Portrait.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.emissionTexture">
            <summary>
            The Emission Version of the Card's Portrait.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.altTexture">
            <summary>
            The Alternate Version of the Card's Portrait.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.altEmissionTexture">
            <summary>
            The Alternate Emission Version of the Card's Portrait.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.pixelTexture">
            <summary>
            The Act 2 Version of the Card's Portrait.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.titleGraphic">
            <summary>
            The Title Graphic of the Card, this appears overlayed on the card's name.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.decals">
            <summary>
            A list of all Decal paths to be on the card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.extensionProperties">
            <summary>
            A Dictionary of Extension Properties applied upon this card.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.file">
            <summary>
            The Internal full path to the File the card came from.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.pluginName">
            <summary>
            The Internal full path to the Plugin the card came from.
            </summary>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.#ctor(System.Collections.Generic.List{System.String},System.String,System.String,System.String,System.String,System.Collections.Generic.List{System.String},System.Int32,System.Int32,System.Boolean,System.Int32,System.Int32,System.Int32,System.Collections.Generic.List{System.String},System.String,System.Collections.Generic.List{System.String},System.Collections.Generic.List{System.String},System.Collections.Generic.List{System.String},System.Collections.Generic.List{System.String},System.String,System.Int32,System.String,System.String,System.String,System.String,System.Boolean,System.Boolean,System.Collections.Generic.List{System.String},System.String,System.String,System.String,System.String,System.String,System.String,System.Collections.Generic.List{System.String},System.Collections.Generic.Dictionary{System.String,System.String},System.String,System.String)">
            <summary>
            The Constructor for making Card Objects.
            </summary>
            <param name="fieldsToEdit"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.fieldsToEdit"/></param>
            <param name="name"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.name"/></param>
            <param name="modPrefix"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.modPrefix"/></param>
            <param name="displayedName"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.displayedName"/></param>
            <param name="description"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.description"/></param>
            <param name="metaCategories"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.metaCategories"/></param>
            <param name="baseAttack"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.baseAttack"/></param>
            <param name="baseHealth"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.baseHealth"/></param>
            <param name="hideAttackAndHealth"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.hideAttackAndHealth"/></param>
            <param name="bloodCost"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.bloodCost"/></param>
            <param name="bonesCost"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.bonesCost"/></param>
            <param name="energyCost"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.energyCost"/></param>
            <param name="gemsCost"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.gemsCost"/></param>
            <param name="specialStatIcon"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.specialStatIcon"/></param>
            <param name="tribes"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.tribes"/></param>
            <param name="traits"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.traits"/></param>
            <param name="abilities"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.abilities"/></param>
            <param name="specialAbilities"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.specialAbilities"/></param>
            <param name="evolveIntoName"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.evolveIntoName"/></param>
            <param name="evolveTurns"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.evolveTurns"/></param>
            <param name="defaultEvolutionName"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.defaultEvolutionName"/></param>
            <param name="tailName"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.tailName"/></param>
            <param name="tailLostPortrait"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.tailLostPortrait"/></param>
            <param name="iceCubeName"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.iceCubeName"/></param>
            <param name="flipPortraitForStrafe"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.flipPortraitForStrafe"/></param>
            <param name="onePerDeck"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.onePerDeck"/></param>
            <param name="appearanceBehaviour"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.appearanceBehaviour"/></param>
            <param name="texture"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.texture"/></param>
            <param name="emissionTexture"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.emissionTexture"/></param>
            <param name="altTexture"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.altTexture"/></param>
            <param name="altEmissionTexture"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.altEmissionTexture"/></param>
            <param name="pixelTexture"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.pixelTexture"/></param>
            <param name="titleGraphic"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.titleGraphic"/></param>
            <param name="decals"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.decals"/></param>
            <param name="extensionProperties"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.extensionProperties"/></param>
            <param name="file"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.file"/></param>
            <param name="pluginName"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.pluginName"/></param>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.ConvertCardObjectToCardInfo">
            <summary>
            Converts the given CardObject into a CardInfo and adds it automatically via the API.
            </summary>
            <returns>A CardInfo representing the card passed in.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV2Support.Objects.CardObject.GetEnumValue``1(System.String)">
            <summary>
            Gets the Enum Value compared to the Type Param.
            </summary>
            <param name="value">The Value we want an Enum From.</param>
            <typeparam name="T">The Type to check it against.</typeparam>
            <returns>The Parsed Enum Value.</returns>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckObject">
            <summary>
            An Object resembling the StarterDeck List.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckObject.decks">
            <summary>
            The List of Decks in the DeckObject.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckObject.file">
            <summary>
            The JSON File.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckObject.pluginName">
            <summary>
            The Plugin In Which the Starter Deck originates.
            </summary>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckObject.#ctor(System.Collections.Generic.List{JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject},System.String,System.String)">
            <summary>
            Creates the Deck Object.
            </summary>
            <param name="decks"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckObject.decks"/></param>
            <param name="file"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckObject.file"/></param>
            <param name="pluginName"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckObject.pluginName"/></param>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckObject.ConvertDeckObjectToStarterDeckInfo">
            <summary>
            Converts the Deck Object to a List of <see cref="T:DiskCardGame.StarterDeckInfo"/>
            </summary>
            <returns>A List of <see cref="T:DiskCardGame.StarterDeckInfo"/></returns>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject">
            <summary>
            An Object resembling the Individual Starter Deck.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.fieldsToEdit">
            <summary>
            The Fields In Which Will be overwrote for the deck with the associated name.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.name">
            <summary>
            The Starter Decks Name.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.modPrefix">
            <summary>
            The Starter Decks Mod Prefix.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.title">
            <summary>
            The Starter Decks title.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.cards">
            <summary>
            The Starter Decks Cards.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.iconTexture">
            <summary>
            The Starter Decks IconTexture.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.unlockLevel">
            <summary>
            The Starter Decks UnlockLevel.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.file">
            <summary>
            The JSON File.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.pluginName">
            <summary>
            The Plugin In Which the Starter Deck originates.
            </summary>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.#ctor(System.Collections.Generic.List{System.String},System.String,System.String,System.String,System.Collections.Generic.List{System.String},System.String,System.Int32,System.String,System.String)">
            <summary>
            Creates A DeckDataObject.
            </summary>
            <param name="fieldsToEdit"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.fieldsToEdit"/></param>
            <param name="name"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.name"/></param>
            <param name="modPrefix"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.modPrefix"/></param>
            <param name="title"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.title"/></param>
            <param name="cards"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.cards"/></param>
            <param name="iconTexture"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.iconTexture"/></param>
            <param name="unlockLevel"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.unlockLevel"/></param>
            <param name="file"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.file"/></param>
            <param name="pluginName"><see cref="P:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.pluginName"/></param>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV2Support.Objects.DeckDataObject.ConvertDeckDataObjectToStarterDeckInfo">
            <summary>
            Converts the DeckDataObject into a <see cref="T:DiskCardGame.StarterDeckInfo"/>.
            </summary>
            <returns>A <see cref="T:DiskCardGame.StarterDeckInfo"/>.</returns>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card">
            <summary>
            The main data Object for JSONLoader V2's Card system.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.fieldsToEdit">
            <summary>
            Any items applied within this field will be used for overwriting the In-Game card associated with the field 'name'.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.name">
            <summary>
            The In-Code name for the card, when referencing this card, it is the piece that comes after the 'modPrefix' field.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.modPrefix">
            <summary>
            The In-Code identifier for the card, when referencing this card, it is the piece that comes before the 'name' field.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.displayedName">
            <summary>
            The In-Game name for the card, it can be anything as long as this font can display it; https://font.download/font/heavyweight
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.description">
            <summary>
            The In-Game flavor for the card, this will show when receiving the card for the first time, if you want to prevent it being seen from saving use; https://thunderstore.io/c/inscryption/p/creator/Fuck_Dialouge_Saving/
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.metaCategories">
            <summary>
            These Meta-Categories control how your card will show up within the game, see the following page for what each of them do; https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/wiki/5396-vanilla-enums
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.cardComplexity">
            <summary>
            This controls WHEN your card can show up in the game, see the following page for what each of them do; https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/wiki/5396-vanilla-enums
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.temple">
            <summary>
            This controls which temple in Act 2 the card is apart of, as well as meant to determine which Act outside Act 2 the card shows up in, whether mods follow the convention is up to question, but that's what these do. So, Nature is Act 1 and the Nature Temple, Tech is Act 3 and the Technology Temple, Undead is the Grimora Portion of the Finale and the Undead Temple, Wizard is the Magnificus Portion of the Finale and the Magicks Temple.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.baseAttack">
            <summary>
            This value determines the attack value of the card, it cannot be negative.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.baseHealth">
            <summary>
            This value determines the health value of the card, it cannot be negative or 0.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.hideAttackAndHealth">
            <summary>
            This boolean value determines whether the Attack and Health of the card should be hidden or not.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.bloodCost">
            <summary>
            This value determines the amount of Blood this card will cost.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.bonesCost">
            <summary>
            This value determines the amount of Bones this card will cost.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.energyCost">
            <summary>
            This value determines the amount of Energy this card will cost.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.gemsCost">
            <summary>
            The following 3 values are accepted here: Green for the Green Gem, Orange for the Orange Gem, and Blue for the Blue Gem. Each of these correlates to the Gem Cost of a card. This version of JSONLoader does not support multiple of the same color of gem.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.specialStatIcon">
            <summary>
            This determines which Stat Icon to show on the card, this must be used alongside the associated Special Ability.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.tribes">
            <summary>
            This List determines what Tribes are applied to the card. You can find the full list here; https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/wiki/5396-vanilla-enums
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.traits">
            <summary>
            This List determines what Traits are applied to this card. You can find the full list here; https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/wiki/5396-vanilla-enums
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.abilities">
            <summary>
            This List determines what Abilities are applied to this card. You can find the full list here; https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/wiki/5396-vanilla-enums
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.specialAbilities">
            <summary>
            This List determines what Special Abilities are applied to this card. You can find the full list here; https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/wiki/5396-vanilla-enums
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.evolveIntoName">
            <summary>
            This represents the In-Code name of the card this card is meant to evolve into. It should match the following: [Mod Prefix]_[Name].
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.evolveTurns">
            <summary>
            This value represents the amount of turns it takes for this card to evolve. This version's Turn Count must be greater than 1.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.defaultEvolutionName">
            <summary>
            This determines what the Default Evolution Name will be, note it will appear in the format of; '[defaultEvolutionName] [displayedName]', just replace the variables with your JSON's values.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.tailName">
            <summary>
            This represents the In-Code name of the card this card will leave in its old lane if Loose Tail triggers. It should match the following: [Mod Prefix]_[Name].
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.tailLostPortrait">
            <summary>
            The Path to your cards Tail Lost Portrait, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '114x94' image. This applies specifically when this card is struck and lost its tail.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.iceCubeName">
            <summary>
            This represents the In-Code name of the card this card will leave behind in its place when it is to die. It should match the following: [Mod Prefix]_[Name].
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.flipPortraitForStrafe">
            <summary>
            A bool determining whether this cards portrait will flip when the card moves. (like the sigil icon does)
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.onePerDeck">
            <summary>
            A bool determining if there can only be one copy of this card within the Player's deck.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.appearanceBehaviour">
            <summary>
            This List determines the Appearance Behaviors in which will be applied to this card. Use a newer version of JSONLoader for Modded Appearance Behaviors. You can find the full list here; https://thunderstore.io/c/inscryption/p/MADH95Mods/JSONCardLoader/wiki/5396-vanilla-enums
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.texture">
            <summary>
            The Path to your cards Portrait, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '114x94' image.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.emissionTexture">
            <summary>
            The Path to your cards Emissive Portrait, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '114x94' image. This applies in the case you've transferred a sigil at the Sacrificial Stones onto this card.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.altTexture">
            <summary>
            The Path to your cards Alternative Portrait, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '114x94' image. This applies in the case you have a Goat's Eye or possibly some other cases.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.altEmissionTexture">
            <summary>
            The Path to your cards Alternative Portrait, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '114x94' image. This applies in the case you have a Goat's Eye or possibly some other cases and, you've transferred a sigil at the Sacrificial Stones onto this card.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.pixelTexture">
            <summary>
            The Path to your cards Pixel Portrait, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '41x28' image. This applies specifically in Act 2, its just that act's version of the card portrait.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.titleGraphic">
            <summary>
            The Path to your cards Title Graphic, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '113x28' image. This applies specifically over your card name as a way of obscuring it like the Tentacle Cards are.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.decals">
            <summary>
            This is a list of all the Decal Images in which will be stacked onto your card, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '125x190' image.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card.extensionProperties">
            <summary>
            This is a list of all Extended Properties to this Card. You'll need to supply your own Field:Value pairs according to the mods specifications. If using the Editor, hit edit by the property to edit this Object.
            </summary>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Deck">
            <summary>
            The main data Object for JSONLoader V2's Card system.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Deck.decks">
            <summary>
            A List of all Decks this Object holds.
            </summary>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.DeckData">
            <summary>
            The data Object for each Individual Deck.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.DeckData.fieldsToEdit">
            <summary>
            Any items applied within this field will be used for overwriting the In-Game deck associated with the field 'name'.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.DeckData.name">
            <summary>
            The In-Code name for the Starter Deck, when referencing this Starter Deck, it is the piece that comes after the 'modPrefix' field.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.DeckData.modPrefix">
            <summary>
            The In-Code identifier for the Starter Deck, when referencing this Starter Deck, it is the piece that comes before the 'name' field.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.DeckData.title">
            <summary>
            The Display Title for the Starter Deck, this is the name that will appear in game.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.DeckData.cards">
            <summary>
            The Full List of Cards within the Starter Deck.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.DeckData.iconTexture">
            <summary>
            The Path to your Starter Decks Icon, this is localized to your Plugins Folder. It's your job to keep it organized, do it as you would these 'JLDR' files. This must be a PNG File and must be a '35x44' image.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.DeckData.unlockLevel">
            <summary>
            The Unlock Level of the Deck, this is used to determine what challenge level in which this Starter Deck will be unlocked.
            </summary>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV2Support.Utilities.CardUtils">
            <summary>
            A class for <see cref="T:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card"/> related Utilities.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Utilities.CardUtils.CardsToLoad">
            <summary>
            A list of all the <see cref="T:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card"/> Files in which we need to load.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Utilities.CardUtils.allJLDR2Cards">
            <summary>
            An internal facing List of all JLDR2 <see cref="T:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card"/>s passed to the API.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Utilities.CardUtils.allJLDR2CardsPublic">
            <summary>
            A public facing read-only collection of all JLDR2 <see cref="T:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card"/>s passed to the API.
            </summary>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV2Support.Utilities.CardUtils.HandleCards">
            <summary>
            A function to handle the loading of <see cref="T:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card"/>'s.
            </summary>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV2Support.Utilities.CardUtils.Parse(System.Collections.Generic.List{System.ValueTuple{System.Int32,System.String,System.String}},System.String,System.String)">
            <summary>
            This function handles the Parsing of a Card into the Game.
            </summary>
            <param name="JSONCard">A List (of a int resembling JSON depth, a string resembling the field Name, a string resembling the string Value) representing the Card.</param>
            <param name="file">The full Path to the File.</param>
            <param name="pluginName">The full Path to the Plugin.</param>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="T:JSONLoader3.Cores.JSONLoaderV2Support.Utilities.DeckUtils">
            <summary>
            A class for <see cref="T:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Deck"/> related Utilities.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Utilities.DeckUtils.StarterDecksToLoad">
            <summary>
            A list of all the <see cref="T:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Deck"/> Files in which we need to load.
            </summary>
        </member>
        <member name="F:JSONLoader3.Cores.JSONLoaderV2Support.Utilities.DeckUtils.allJLDR2Decks">
            <summary>
            An internal facing List of all JLDR2 <see cref="T:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Deck"/>s passed to the API.
            </summary>
        </member>
        <member name="P:JSONLoader3.Cores.JSONLoaderV2Support.Utilities.DeckUtils.allJLDR2DecksPublic">
            <summary>
            A public facing read-only collection of all JLDR2 <see cref="T:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Deck"/>s passed to the API.
            </summary>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV2Support.Utilities.DeckUtils.HandleDecks">
            <summary>
            A function to handle the loading of <see cref="T:JSONLoader3.Cores.JSONLoaderV2Support.Schemas.Card"/>'s.
            </summary>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Cores.JSONLoaderV2Support.Utilities.DeckUtils.Parse(System.Collections.Generic.List{System.ValueTuple{System.Int32,System.String,System.String}},System.String,System.String)">
            <summary>
            This function handles the Parsing of a Starter Deck into the Game.
            </summary>
            <param name="JSONStarterDeck">A List (of a int resembling JSON depth, a string resembling the field Name, a string resembling the string Value) representing the Starter Deck.</param>
            <param name="file">The full Path to the File.</param>
            <param name="pluginName">The full Path to the Plugin.</param>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="T:JSONLoader3.JSONLoader3">
            <summary>
            This class is the Origin Point of the JSONLoader3 and CSVLoader API's.
            </summary>
        </member>
        <member name="F:JSONLoader3.JSONLoader3.PluginGuid">
            <summary>
            This is the PluginGuid for the API, it will be hardcoded to this, if anything changes it will be addressed in the Changelog so you can fix any C# Dependencies you have upon it.
            </summary>
        </member>
        <member name="F:JSONLoader3.JSONLoader3.PluginName">
            <summary>
            This is the PluginName for the API, note it may change over time.
            </summary>
        </member>
        <member name="F:JSONLoader3.JSONLoader3.PluginVersion">
            <summary>
            This resembles the Version of the API, when this is updated make sure to update the value.
            </summary>
        </member>
        <member name="F:JSONLoader3.JSONLoader3.Error">
            <summary>
            This color is associated with the Error Logging Level.
            </summary>
        </member>
        <member name="F:JSONLoader3.JSONLoader3.Warning">
            <summary>
            This color is associated with the Warning Logging Level.
            </summary>
        </member>
        <member name="F:JSONLoader3.JSONLoader3.Information">
            <summary>
            This color is associated with the Information Logging Level.
            </summary>
        </member>
        <member name="F:JSONLoader3.JSONLoader3.Verbose">
            <summary>
            This color is associated with the Verbose Logging Level.
            </summary>
        </member>
        <member name="F:JSONLoader3.JSONLoader3.Debug">
            <summary>
            This color is associated with the Debug Logging Level.
            </summary>
        </member>
        <member name="F:JSONLoader3.JSONLoader3.ExtendedInformation">
            <summary>
            This color is associated with the ExtendedInformation Logging Level.
            </summary>
        </member>
        <member name="F:JSONLoader3.JSONLoader3.SummaryInformation">
            <summary>
            This color is associated with the SummaryInformation Logging Level.
            </summary>
        </member>
        <member name="M:JSONLoader3.JSONLoader3.Awake">
            <summary>
            Sets up some of the API including making our Startup Phase.
            </summary>
        </member>
        <member name="M:JSONLoader3.JSONLoader3.JSONLoaderStartupPhase">
            <summary>
            This serves as the Starting Point for the entire API, whatever is put here will be done first and foremost in startup.
            </summary>
        </member>
        <member name="M:JSONLoader3.JSONLoader3.FormatLogger(System.String,System.String,System.String)">
            <summary>
            This is a nifty function which will help automate and keep tidy our Logging System across our API. Below defines all of the levels, and what Message and Source reference.
            </summary>
            <param name="level">The following are all of the levels in which apply to our Logger.
                <list type="table">
                    <listheader>
                        <term>Level</term>
                        <description>What It Is Meant For</description>
                    </listheader>
                    <item>
                        <term>Error</term>
                        <description>This is meant for any Errors in which this API may spit out.</description>
                    </item>
                    <item>
                        <term>Warning</term>
                        <description>This is meant for any Warnings in which this API may spit out (something that isn't quite right, but may still work).</description>
                    </item>
                    <item>
                        <term>Information (Info)</term>
                        <description>This is meant for any General Details in which this API may spit out.</description>
                    </item>
                    <item>
                        <term>AdditionalInformation (AdditionalInfo)</term>
                        <description>This is meant for any Additional Details in which this API may spit out.</description>
                    </item>
                    <item>
                        <term>Debug</term>
                        <description>This is meant for any Details in which this API usually would keep BTS but may spit out.</description>
                    </item>
                    <item>
                        <term>Summary</term>
                        <description>This is used Exclusively by the Linter to Output Schema Property Descriptions.</description>
                    </item>
                    <item>
                        <term>Verbose</term>
                        <description>This is meant for showing exactly what a card is being defined with in Live Logging.</description>
                    </item>
                </list>
            </param>
            <param name="message">This is the message in which is to be spit out.</param>
            <param name="source">This is where the message came from, so we can indentify the stemming point of the error.</param>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="T:JSONLoader3.Peripheral.FILE_Loader.FindFiles">
            <summary>
            This class handles the finding of files for the JSONLoaders and CSVLoader.
            </summary>
        </member>
        <member name="F:JSONLoader3.Peripheral.FILE_Loader.FindFiles.assembly">
            <summary>
            The Path to the Executing Assembly.
            </summary>
        </member>
        <member name="F:JSONLoader3.Peripheral.FILE_Loader.FindFiles.DLLPath">
            <summary>
            The Path to the JSONLoader DLL.
            </summary>
        </member>
        <member name="M:JSONLoader3.Peripheral.FILE_Loader.FindFiles.FindFilesToLoad">
            <summary>
            A function which will find Files in which need to be loaded from the configured Paths.
            </summary>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.FILE_Loader.FindFiles.HandleJSONFile(System.String,System.String)">
            <summary>
            A function used to handle Files for JSONLoader.
            </summary>
            <param name="JSONFile">The exact path to a JSONLoader file.</param>
            <param name="plugin">The Full Path to the Plugin.</param>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.FILE_Loader.FindFiles.HandleCSVFile(System.String,System.String)">
            <summary>
            A function used to handle Files for CSVLoader.
            </summary>
            <param name="CSVFile">The exact path to a CSVLoader path.</param>
            <param name="plugin">The Full Path to the Plugin.</param>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.FILE_Loader.FindFiles.FindElementInPath(System.String,System.String)">
            <summary>
            A function to find a given element within the Path passed in.
            </summary>
            <param name="fullPath">The entire Path.</param>
            <param name="toFind">The folder in that path your trying to get a path to.</param>
            <returns>The Full Path up to the folder you were after, if not found we return a 'null' value.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="T:JSONLoader3.Peripheral.FILE_Loader.LoadFiles">
            <summary>
            This class handles the Loading of Files into their Respective Lists.
            </summary>
        </member>
        <member name="F:JSONLoader3.Peripheral.FILE_Loader.LoadFiles.JLDRFiles">
            <summary>
            A list of ALL JLDR Files.
            </summary>
        </member>
        <member name="F:JSONLoader3.Peripheral.FILE_Loader.LoadFiles.JLDR2Files">
            <summary>
            A list of ALL JLDR2 Files.
            </summary>
        </member>
        <member name="F:JSONLoader3.Peripheral.FILE_Loader.LoadFiles.JLDR3Files">
            <summary>
            A list of all JLDR3 Files.
            </summary>
        </member>
        <member name="F:JSONLoader3.Peripheral.FILE_Loader.LoadFiles.CSVFiles">
            <summary>
            A list of all CSV Files.
            </summary>
        </member>
        <member name="M:JSONLoader3.Peripheral.FILE_Loader.LoadFiles.LoadFoundFiles">
            <summary>
            A function to Load All Found Files.
            </summary>
        </member>
        <member name="T:JSONLoader3.Peripheral.ImageHandling.ScanImages">
            <summary>
            A class to handle the scanning of Images into the Game.
            </summary>
        </member>
        <member name="M:JSONLoader3.Peripheral.ImageHandling.ScanImages.ParseImage(System.String,System.String)">
            <summary>
            A function that handles and determines how to Parse the Image.
            </summary>
            <param name="plugin">The full path to the Plugin.</param>
            <param name="imagePath">Either the Relative Image Path or Base64 of the Image.</param>
            <returns>A Sprite of the Image.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.ImageHandling.ScanImages.GetTextureFromString(System.String)">
            <summary>
            Gets a Texture2D from the Base64 Image.
            </summary>
            <param name="path">The Base64 Path of the Image.</param>
            <returns>A Texture2D from the Base64.</returns>
        </member>
        <member name="M:JSONLoader3.Peripheral.ImageHandling.ScanImages.GetTextureFromBase64(System.String)">
            <summary>
            Converts the Base64 into a Sprite.
            </summary>
            <param name="texture">The Base64's Texture2D.</param>
            <returns>A Sprite of the Base64 Texture.</returns>
        </member>
        <member name="M:JSONLoader3.Peripheral.ImageHandling.ScanImages.GetTextureFromPluginAndPath(System.String,System.String)">
            <summary>
            Gets the Texture from a Plugin with a Path.
            </summary>
            <param name="plugin">The Full Path to the Plugin.</param>
            <param name="filePath">The Relative Path to the File.</param>
            <returns>A Sprite from the Plugin and Path.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.ImageHandling.ScanImages.GetSpriteFromFileName(System.String,System.String)">
            <summary>
            Gets the Image when all you have is the FileName and PluginPath.
            </summary>
            <param name="fileName">The Name of the File.</param>
            <param name="pluginPath">The Plugin in which is originating the request for the file.</param>
            <returns>A Sprite if Successful it will have the image requested, if it failed it will be an empty image.</returns>
        </member>
        <member name="M:JSONLoader3.Peripheral.ImageHandling.ScanImages.LoadCustomPNG(System.String,System.String)">
            <summary>
            This essentially is LoadCustomTexture but from a PNG File.
            </summary>
            <param name="fileName">The name of the file.</param>
            <param name="imagePath">The path to the file.</param>
            <returns>A Texture2D of the inputted Image</returns>
            <remarks>This code is provided by the amazing dark dragoon on nexus mods and discord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.ImageHandling.ScanImages.LoadCustomTexture(System.String,System.String)">
            <summary>
            This is a simple function that converts a file into a Texture2D
            </summary>
            <param name="fileName">The name of the file.</param>
            <param name="imagePath">The path to the file.</param>
            <returns>A Texture2D of the inputted Image</returns>
            <remarks>This code is provided by the amazing dark dragoon on nexus mods and discord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.ImageHandling.ScanImages.GetCustomImage(System.String,System.String)">
            <summary>
            This gets a sprite from the passed in file, specifically a PNG.
            </summary>
            <param name="fileName">The name of the file.</param>
            <param name="imagePath">The path to the file.</param>
            <returns>A Sprite of the inputted Image</returns>
            <remarks>This code is provided by the amazing dark dragoon on nexus mods and discord.</remarks>
        </member>
        <member name="T:JSONLoader3.Peripheral.JSON_LINT.LintingTools">
            <summary>
            This class handles JSON Linting.
            </summary>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.LintAgainstSchema``1(System.String,System.Collections.Generic.List{System.String},System.String)">
            <summary>
            A function intended to lint a JSON File against a JSON Schema.
            </summary>
            <param name="file">The Full Path to the JSON File.</param>
            <param name="JSONSchema">A List of String Resembling the full Schema.</param>
            <param name="LoaderName">The Loaders Identifier, this is used in the Schema and File Name.</param>
            <typeparam name="Class">The Class in which the Schema is being made for.</typeparam>
            <returns>A Tuple (of a List (of a int resembling JSON depth, a string resembling the field Name, a string resembling the string Value), and a bool saying whether it was valid or not).</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.GetTraversalPath(System.Collections.Generic.List{System.ValueTuple{System.Int32,System.String,System.String}},System.ValueTuple{System.Int32,System.String,System.String},System.Int32)">
            <summary>
            A function to get a Path for Traversal in <see cref="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.GetJSONSchemaProperty(System.String,System.Collections.Generic.List{System.String})"/>.
            </summary>
            <param name="JSONSchemaProperties">The List (of a int resembling JSON depth, a string resembling the field Name, a string resembling the string Value) resembling the JSON Schema.</param>
            <param name="JSON">List (of a int resembling JSON depth, a string resembling the field Name, a string resembling the string Value) resembling the JSON.</param>
            <param name="spelunkingDepth">The Multiplier to the Schema Level.</param>
            <returns>A string resembling a Schema Based Traversal Path</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.DisectedJSON(System.Collections.Generic.List{System.String})">
            <summary>
            A function which dissects the JSON into the format expected by several functions.
            </summary>
            <param name="JSONFile">The List of String representing the JSON File.</param>
            <returns>List (of a int resembling JSON depth, a string resembling the field Name, a string resembling the string Value)</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.LoadInJSONItem(System.String)">
            <summary>
            Loads a JSON File into a List of String representing the JSON File.
            </summary>
            <param name="file">The full path to the JSON File.</param>
            <returns>A List of String representing the JSON File.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.GetJSONSchemaProperty(System.String,System.Collections.Generic.List{System.String})">
            <summary>
            Gets a JSON Schema Property List from a Traversal List and the JSON Schema.
            </summary>
            <param name="propertyPath">The Traversal Path from <see cref="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.GetTraversalPath(System.Collections.Generic.List{System.ValueTuple{System.Int32,System.String,System.String}},System.ValueTuple{System.Int32,System.String,System.String},System.Int32)"/>.</param>
            <param name="JSONSchema">A List of String representing the JSON Schema.</param>
            <returns>A List of String representing all of the JSON Lines relevant to the given Property.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.GetRequiredFromSchema(System.Collections.Generic.List{System.String})">
            <summary>
            A function that gets all of the Required Properties from the passed in JSON Schema.
            </summary>
            <param name="JSONSchema">A List of String representing the JSON Schema.</param>
            <returns>A List of String representing all of the Required Properties for the Object.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.GetAllOf(System.Collections.Generic.List{System.String})">
            <summary>
            A function that gets all of the AllOf Properties from the passed in JSON Schema.
            </summary>
            <param name="JSONSchema">A List of String representing the JSON Schema.</param>
            <returns>A List of a List of String representing all of the OneOf Properties contained within each AllOf.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.AllowExtraFieldsCheck(System.Collections.Generic.List{System.String})">
            <summary>
            A Boolean for whether or not Extra Fields are Allowed for the Object by the Schema.
            </summary>
            <param name="JSONSchema">A List of String representing the JSON Schema.</param>
            <returns>A true if allowed, and a false if disallowed</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.GetAdditionalPropertiesSchema(System.Collections.Generic.List{System.String})">
            <summary>
            Gets the AdditionalProperties in a Schema Variant.
            </summary>
            <param name="JSONSchema">A List of String representing the JSON Schema.</param>
            <returns>A true if allowed, and a false if disallowed</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.DigThroughArrayFindRelevant(System.String)">
            <summary>
            Digs Through an Array, Finds all of the Arrays Contents, and Sends it back.
            </summary>
            <param name="jsonArray">A string representing the JSON Array.</param>
            <returns>A List of String representing the JSON Arrays Contents. An empty string is returned if the Array has no Items.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.DigThroughSchemaFindRelevant(System.String,System.Collections.Generic.List{System.String})">
            <summary>
            A function that Digs through the JSON Schema and finds all Lines Relevant to a specific Property.
            </summary>
            <param name="propertyToFind">The Property in which you want to find in the Schema Sample passed in.</param>
            <param name="JSONSchema">A List Of String resembling the Schema Segment to Dig Through.</param>
            <returns>A List of String of all the Content related to the Property your after.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.GetObjectProperties(System.String)">
            <summary>
            This is a helper unused in this class directly, but useful if you need to GetProperties related to an Object in your Items Utilities.
            </summary>
            <param name="jsonObject">A String representing the JSON Object.</param>
            <returns>List (of a int resembling JSON depth, a string resembling the field Name, a string resembling the string Value)</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.GetObjectProperties(System.String,System.String,System.String)">
            <summary>
            This is a helper unused in this class directly, but useful if you need to GetProperties related to an Object in your Items Utilities.
            </summary>
            <param name="jsonObject">A String representing the JSON Object.</param>
            <param name="propertyToFind">The Property in which you want to find in the Schema Sample passed in.</param>
            <param name="file">The full path to the JSON File.</param>
            <returns>List (of a int resembling JSON depth, a string resembling the field Name, a string resembling the string Value)</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.GetArrayItems(System.String,System.String,System.String)">
            <summary>
            See <see cref="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.DigThroughArrayFindRelevant(System.String)"/> for more details.
            </summary>
            <param name="jsonArray">A String representing the JSON Array.</param>
            <param name="propertyName">The Name of the Property.</param>
            <param name="file">The full path to the file.</param>
            <returns>A List of String based on the results of <see cref="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.DigThroughArrayFindRelevant(System.String)"/>.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.GetAnyOfSchemas(System.Collections.Generic.List{System.String})">
            <summary>
            Gets The Schemas under the AnyOf Type.
            </summary>
            <param name="JSONSchema">A List Of String resembling the Schema Segment to Dig Through.</param>
            <returns>A List of Schemas associated with the AnyOf Type.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.GetArrayItems(System.String)">
            <summary>
            See <see cref="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.DigThroughArrayFindRelevant(System.String)"/> for more details.
            </summary>
            <param name="jsonArray">A String representing the JSON Array.</param>
            <returns>A List of String based on the results of <see cref="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.DigThroughArrayFindRelevant(System.String)"/>.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.ValidatePropertyAgainstSchema(System.String,System.String,System.Collections.Generic.List{System.String},System.String,System.String,System.Boolean)">
            <summary>
            This is the JSON Validator's core, it handles ensuring the JSON Itself is valid.
            </summary>
            <param name="jsonPropertyName">The Property we are Validating.</param>
            <param name="jsonPropertyValue">The Property Value we are Validating.</param>
            <param name="PropertySchema">The List of String representing the Schema.</param>
            <param name="file">The Full Path to the JSON File.</param>
            <param name="schemaFile">The Full Path to the JSON Schema File.</param>
            <param name="validateAnyOf">Determines whether errors should log or not.</param>
            <returns>A true if valid, a false if invalid.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.ValidateAnyOf(System.String,System.String,System.Collections.Generic.List{System.String},System.String,System.String,System.Boolean)">
            <summary>
            This is the JSON Validator's AnyOf Handler, it handles ensuring the String Property is Valid.
            </summary>
            <param name="jsonPropertyName">The Property we are Validating.</param>
            <param name="jsonPropertyValue">The Property Value we are Validating.</param>
            <param name="PropertySchema">The List of String representing the Schema.</param>
            <param name="file">The Full Path to the JSON File.</param>
            <param name="schemaFile">The Full Path to the JSON Schema File.</param>
            <param name="validateAnyOf">Determines whether errors should log or not.</param>
            <returns>A true if valid, a false if invalid.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.ValidateString(System.String,System.String,System.Collections.Generic.List{System.String},System.String,System.String,System.Boolean)">
            <summary>
            This is the JSON Validator's String Handler, it handles ensuring the String Property is Valid.
            </summary>
            <param name="jsonPropertyName">The Property we are Validating.</param>
            <param name="jsonPropertyValue">The Property Value we are Validating.</param>
            <param name="PropertySchema">The List of String representing the Schema.</param>
            <param name="file">The Full Path to the JSON File.</param>
            <param name="schemaFile">The Full Path to the JSON Schema File.</param>
            <param name="validateAnyOf">Determines whether errors should log or not.</param>
            <returns>A true if valid, a false if invalid.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.ValidateInteger(System.String,System.String,System.Collections.Generic.List{System.String},System.String,System.String,System.Boolean)">
            <summary>
            This is the JSON Validator's Integer Handler, it handles ensuring the String Property is Valid.
            </summary>
            <param name="jsonPropertyName">The Property we are Validating.</param>
            <param name="jsonPropertyValue">The Property Value we are Validating.</param>
            <param name="PropertySchema">The List of String representing the Schema.</param>
            <param name="file">The Full Path to the JSON File.</param>
            <param name="schemaFile">The Full Path to the JSON Schema File.</param>
            <param name="validateAnyOf">Determines whether errors should log or not.</param>
            <returns>A true if valid, a false if invalid.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.ValidateBoolean(System.String,System.String,System.Collections.Generic.List{System.String},System.String,System.String,System.Boolean)">
            <summary>
            This is the JSON Validator's Boolean Handler, it handles ensuring the String Property is Valid.
            </summary>
            <param name="jsonPropertyName">The Property we are Validating.</param>
            <param name="jsonPropertyValue">The Property Value we are Validating.</param>
            <param name="PropertySchema">The List of String representing the Schema.</param>
            <param name="file">The Full Path to the JSON File.</param>
            <param name="schemaFile">The Full Path to the JSON Schema File.</param>
            <param name="validateAnyOf">Determines whether errors should log or not.</param>
            <returns>A true if valid, a false if invalid.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.ValidateObject(System.String,System.String,System.Collections.Generic.List{System.String},System.String,System.String,System.Boolean)">
            <summary>
            This is the JSON Validator's Object Handler, it handles ensuring the String Property is Valid.
            </summary>
            <param name="jsonPropertyName">The Property we are Validating.</param>
            <param name="jsonPropertyValue">The Property Value we are Validating.</param>
            <param name="PropertySchema">The List of String representing the Schema.</param>
            <param name="file">The Full Path to the JSON File.</param>
            <param name="schemaFile">The Full Path to the JSON Schema File.</param>
            <param name="validateAnyOf">Determines whether errors should log or not.</param>
            <returns>A true if valid, a false if invalid.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_LINT.LintingTools.ValidateArray(System.String,System.String,System.Collections.Generic.List{System.String},System.String,System.String,System.Boolean)">
            <summary>
            This is the JSON Validator's Array Handler, it handles ensuring the String Property is Valid.
            </summary>
            <param name="jsonPropertyName">The Property we are Validating.</param>
            <param name="jsonPropertyValue">The Property Value we are Validating.</param>
            <param name="PropertySchema">The List of String representing the Schema.</param>
            <param name="file">The Full Path to the JSON File.</param>
            <param name="schemaFile">The Full Path to the JSON Schema File.</param>
            <param name="validateAnyOf">Determines whether errors should log or not.</param>
            <returns>A true if valid, a false if invalid.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="T:JSONLoader3.Peripheral.JSON_SCHEMA.LoadSchema">
            <summary>
            This class will handle the loading of a Schema File.
            </summary>
        </member>
        <member name="F:JSONLoader3.Peripheral.JSON_SCHEMA.LoadSchema.SchemaFolder">
            <summary>
            This resembles the Schema Folder Location.
            </summary>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.LoadSchema.FindAndLoadSchema``1(System.String)">
            <summary>
            This function Loads the Given Item into a List of String resembling its Schema.
            </summary>
            <param name="LoaderName">The Loaders Identifier, this is used in the Schema and File Name.</param>
            <typeparam name="Class">The Class in which the Schema is being made for.</typeparam>
            <returns>A List of String resembling the entire JSON Schema Line by Line.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.LoadSchema.GetFullSchemaPath``1(System.String)">
            <summary>
            This gets the full Schema Path for the Given Item.
            </summary>
            <param name="LoaderName">The Loaders Identifier, this is used in the Schema and File Name.</param>
            <typeparam name="Class">The Class in which the Schema is being made for.</typeparam>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="T:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema">
            <summary>
            This class handles the Writing of JSON Schemas.
            </summary>
        </member>
        <member name="F:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.SchemaFolder">
            <summary>
            This resembles the Schema Folder Location.
            </summary>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.CreateSchemaDirectors(System.String)">
            <summary>
            A simple function to handle the creation of the Schema Directory
            </summary>
            <param name="LoaderName">The Loaders Identifier, this is used in the Schema and File Name.</param>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.CreateAndOpenSchema``1(System.String)">
            <summary>
            A function to create and open the Schema.
            </summary>
            <param name="LoaderName">The Loaders Identifier, this is used in the Schema and File Name.</param>
            <typeparam name="Class">The Class in which the Schema is being made for.</typeparam>
            <returns>An opened <see cref="T:System.IO.StreamWriter"/>.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.CloseWriterAndFile(System.IO.StreamWriter)">
            <summary>
            This function closes the passed in StreamWriter.
            </summary>
            <param name="Writer">The StreamWriter associated with <see cref="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.CreateAndOpenSchema``1(System.String)"/></param>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.GetToolTips(System.Collections.Generic.List{System.Reflection.FieldInfo})">
            <summary>
            Extracts all the Tooltips and puts them in a tuple List.
            </summary>
            <param name="fields">All of the fieldInfo's relevant for the Tooltip List.</param>
            <returns>A List of (a Tuple of (a Field Info, and a List of String resembling the tooltips)).</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.GetRequired(System.Collections.Generic.List{System.ValueTuple{System.Reflection.FieldInfo,System.Collections.Generic.List{System.String}}})">
            <summary>
            Gets all the Required fields from a passed in Field to Tooltip List.
            </summary>
            <param name="fieldTooltipList">The full Field to Tooltip List from <see cref="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.GetToolTips(System.Collections.Generic.List{System.Reflection.FieldInfo})"/>.</param>
            <returns>A list of the required Fields.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.GetAllOfRequired(System.Collections.Generic.List{System.ValueTuple{System.Reflection.FieldInfo,System.Collections.Generic.List{System.String}}})">
            <summary>
            A function in which gets AllOf variant of Required Fields from a passed in Field to Tooltip List.
            </summary>
            <param name="fieldTooltipList">The full Field to Tooltip List from <see cref="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.GetToolTips(System.Collections.Generic.List{System.Reflection.FieldInfo})"/>.</param>
            <returns>A list of the required AllOf Variant Fields.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.GetWritable(System.Collections.Generic.List{System.ValueTuple{System.Reflection.FieldInfo,System.Collections.Generic.List{System.String}}})">
            <summary>
            Gets all the Writable fields from a passed in Field to Tooltip List.
            </summary>
            <param name="fieldTooltipList">The full Field to Tooltip List from <see cref="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.GetToolTips(System.Collections.Generic.List{System.Reflection.FieldInfo})"/>.</param>
            <returns>All of the Writable fields in the format in which it came in.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.GetWritableExtended(System.Collections.Generic.List{System.ValueTuple{System.Reflection.FieldInfo,System.Collections.Generic.List{System.String}}})">
            <summary>
            Gets all the Writable fields from a passed in Field to Tooltip List, recursively expanding fields marked with EXTENDS.
            </summary>
            <param name="fieldTooltipList">The full Field to Tooltip List from <see cref="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.GetToolTips(System.Collections.Generic.List{System.Reflection.FieldInfo})"/>.</param>
            <returns>All of the Writable fields, with EXTENDS fields recursively expanded.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.IsExtends(System.Collections.Generic.List{System.String})">
            <summary>
            Determines whether a field extends the current Schema Level.
            </summary>
            <param name="tooltips">The list of tooltips associated with the field.</param>
            <returns>True if the field contains the EXTENDS tooltip.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.HandleAllOf(System.Collections.Generic.List{System.Collections.Generic.List{System.String}},System.Int32)">
            <summary>
            Handles writing an AllOf segment of the Schema
            </summary>
            <param name="allOf">The List of a List of String representing the AllOf Condition.</param>
            <param name="Indentation">The amount of additional Indentation.</param>
            <returns>A Multi-Lined string representing the Handled AllOf</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.HandleAnyOf(System.String,System.Int32)">
            <summary>
            This function handles the Schema Writing logic for AnyOf[] fields within JSON Schema.
            </summary>
            <param name="anyOf">The String Value associated with the AnyOf Tooltip.</param>
            <param name="Indentation">The amount of excess indentation needed.</param>
            <returns>A Multi-Line String representing the Handled AnyOf Array.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.HandleString(System.Collections.Generic.List{System.ValueTuple{System.Reflection.FieldInfo,System.Collections.Generic.List{System.String}}},System.Reflection.FieldInfo,System.Collections.Generic.List{System.String},System.Int32,System.Type)">
            <summary>
            This function handles String related JSON Schema Components.
            </summary>
            <param name="writableFields">A list of all the writable fields, we namely use it here for comma assurance.</param>
            <param name="field">The specific field of the property in which needs to be Handled.</param>
            <param name="tooltips">The list of tooltips associated with that field.</param>
            <param name="Indentation">The amount of excess indentation needed.</param>
            <param name="Class">The class in which this property belongs.</param>
            <returns>A Multi-Line String representing the Handled String Property.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.HandleInt(System.Collections.Generic.List{System.ValueTuple{System.Reflection.FieldInfo,System.Collections.Generic.List{System.String}}},System.Reflection.FieldInfo,System.Collections.Generic.List{System.String},System.Int32,System.Type)">
            <summary>
            This function handles Int related JSON Schema Components.
            </summary>
            <param name="writableFields">A list of all the writable fields, we namely use it here for comma assurance.</param>
            <param name="field">The specific field of the property in which needs to be Handled.</param>
            <param name="tooltips">The list of tooltips associated with that field.</param>
            <param name="Indentation">The amount of excess indentation needed.</param>
            <param name="Class">The class in which this property belongs.</param>
            <returns>A Multi-Line String representing the Handled Int Property.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.HandleBoolean(System.Collections.Generic.List{System.ValueTuple{System.Reflection.FieldInfo,System.Collections.Generic.List{System.String}}},System.Reflection.FieldInfo,System.Collections.Generic.List{System.String},System.Int32,System.Type)">
            <summary>
            This function handles Boolean related JSON Schema Components.
            </summary>
            <param name="writableFields">A list of all the writable fields, we namely use it here for comma assurance.</param>
            <param name="field">The specific field of the property in which needs to be Handled.</param>
            <param name="tooltips">The list of tooltips associated with that field.</param>
            <param name="Indentation">The amount of excess indentation needed.</param>
            <param name="Class">The class in which this property belongs.</param>
            <returns>A Multi-Line String representing the Handled Boolean Property.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.HandleStringArray(System.Collections.Generic.List{System.ValueTuple{System.Reflection.FieldInfo,System.Collections.Generic.List{System.String}}},System.Reflection.FieldInfo,System.Collections.Generic.List{System.String},System.Int32,System.Type)">
            <summary>
            This function handles String Array related JSON Schema Components.
            </summary>
            <param name="writableFields">A list of all the writable fields, we namely use it here for comma assurance.</param>
            <param name="field">The specific field of the property in which needs to be Handled.</param>
            <param name="tooltips">The list of tooltips associated with that field.</param>
            <param name="Indentation">The amount of excess indentation needed.</param>
            <param name="Class">The class in which this property belongs.</param>
            <returns>A Multi-Line String representing the Handled String Array Property.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.HandleObjectArray(System.Collections.Generic.List{System.ValueTuple{System.Reflection.FieldInfo,System.Collections.Generic.List{System.String}}},System.Reflection.FieldInfo,System.Collections.Generic.List{System.String},System.Int32,System.Type)">
            <summary>
            This function handles Object Array related JSON Schema Components.
            </summary>
            <param name="writableFields">A list of all the writable fields, we namely use it here for comma assurance.</param>
            <param name="field">The specific field of the property in which needs to be Handled.</param>
            <param name="tooltips">The list of tooltips associated with that field.</param>
            <param name="Indentation">The amount of excess indentation needed.</param>
            <param name="Class">The class in which this property belongs.</param>
            <returns>A Multi-Line String representing the Handled Object Array Property.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.HandleObject(System.Collections.Generic.List{System.ValueTuple{System.Reflection.FieldInfo,System.Collections.Generic.List{System.String}}},System.Reflection.FieldInfo,System.Collections.Generic.List{System.String},System.Int32,System.Type)">
            <summary>
            This function handles Object related JSON Schema Components.
            </summary>
            <param name="writableFields">A list of all the writable fields, we namely use it here for comma assurance.</param>
            <param name="field">The specific field of the property in which needs to be Handled.</param>
            <param name="tooltips">The list of tooltips associated with that field.</param>
            <param name="Indentation">The amount of excess indentation needed.</param>
            <param name="Class">The class in which this property belongs.</param>
            <returns>A Multi-Line String representing the Handled Object Property.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.WriteJSONSchema``1(System.String)">
            <summary>
            The Non-Recursive JSON Schema Writer
            </summary>
            <param name="LoaderName">The Loaders Identifier, this is used in the Schema and File Name.</param>
            <typeparam name="Class">The Class in which the Schema is being made for.</typeparam>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.JSON_SCHEMA.WriteSchema.RecursiveWrite(System.Type,System.Int32)">
            <summary>
            The Recursive JSON Schema Writer
            </summary>
            <param name="Class">The Class in which the Object Schema Extension is being made for.</param>
            <param name="Indentation">The amount of excess indentation needed.</param>
            <returns>A Multi-Line String resembling the Object.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="T:JSONLoader3.Peripheral.Tooltip_Parser.TooltipDisector">
             <summary>
             This class handles Tooltip Dissection for our JSON Objects.
            
             This supports the following terms:
             * REQUIRED - Mark this field as a Required field in the Schema.
             * EXCLUDED - Mark this field as something to not include in the Schema.
             * EXTENDS - Mark this field as extending the current Schema Level.
             * ALTERNATIVES - Mark this field as having Alternatives.
            
             VARIABLES!!!
            
             All Variables will work as follows: VariableName(Definition), kinda like a KeyPairValue.
            
             The following is a list of all Variables:
             * MinimumLength - Int - Used in String and String Array - Mandates a Minimum Length.
             * Pattern - Raw Regex - Used in String and String Array - Mandates a Pattern the Value must follow.
             * Items - Boolean - Used in String Array and Object Array - Marks the fact the Array has items as true.
             * ItemType - Type - Used in String Array and Object Array - Used to define the type of Array in which the items belong. (e.g. string or object)
             * Enums - A List of Predefined Values - Used in String and String Array - This provides a Pre-Defined list of items users may use for defining the value.
             * UniqueItems - Boolean - Used in String Array and Object Array - This mandates uniqueness among the values.
             * Default - Value - Used in String, Int, and Boolean - This provides a default for Schema Validators.
             * Minimum - Int - Used in Int - This mandates a Minimum Number.
             * Maximum - Int - Used in Int - This mandates a Maximum Number.
             * AdditionalProperties - Boolean - Used in Object and Object Array - Determines whether additional properties are valid.
             * AnyOf - WOAH SEE THE SECTION BY THE SAME NAME - Used in String Array - Defines whether other variations are okay for this array.
             * AlternativeNames - String Array - Used by any Property - Indicates Alternative Names for a Given Property.
            
             If you inevitably need more as of present you'll need to code handling into the Schema and Linter.
            
             MULTI-VAR!!!!
            
             To use more than one variable all you need to do is add a '|' between each Variable, this acts as a Delimiter.
            
             An example of such would be: [Tooltip("REQUIRED | MinimumLength(1) | Pattern(^[a-zA-Z\\d_]+$)")]
            
             Notice the '\\' in the Regex? That's because C# needs it to be escaped in quotes, but don't worry we properly escape it for JSON in <see cref="M:JSONLoader3.Peripheral.XML_Parser.ReadDocumentationFile.EscapeJSON(System.String)"/>
            
             AnyOf Variable
            
             To use this we need to define some special syntaxes, it kinda has its own language within the language.
            
             First things first, any valid AnyOf Items should be surrounded in '[]' and than after that split by the ';' delimitor.
            
             Next up to define the properties we have our own set of vars, with their own definitions:
            
             * Title - The Title of the Validator Set for the Array.
             * Description - The Description of the Validator Set for the Array.
             * Type - The Type in which the Validator is used to Validate.
             * Enums - A list of options which are valid under that validator.
            
             To define it would be for example "AnyOf([Title: Base Game Meta Category, Description: A Meta Category from the Base Game, Type: string, Enums: ChoiceNode > TraderOffer > Part3Random > Rare > GBCPack > GBCPlayable > AscensionUnlock];[Title: Modded Meta Category, Description: Format is {Mod GUID}.{Meta Category Name}, Type: string])"
            
             Each variable is delimited by ',' within the AnyOf Validator Set, and the ':' acts as delimiter between field and value. Lastly within Enums because we delimit our fields with ',' the delimiter is '>'.
             </summary>
             <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
             <example>Hey, please go to the Original Class to view this properly.</example>
        </member>
        <member name="M:JSONLoader3.Peripheral.Tooltip_Parser.TooltipDisector.GetTooltipProperties(System.Reflection.FieldInfo)">
            <summary>
            This function returns A list of all tooltip properties on the Field.
            </summary>
            <param name="field">The Field to fetch the Tooltips off of.</param>
            <returns>A List of String. It returns an Empty List if there are no Tooltips.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="T:JSONLoader3.Peripheral.XML_Parser.ReadDocumentationFile">
            <summary>
            This class handles the reading of the XML Documentation.
            </summary>
        </member>
        <member name="F:JSONLoader3.Peripheral.XML_Parser.ReadDocumentationFile.assembly">
            <summary>
            The Path to the Executing Assembly.
            </summary>
        </member>
        <member name="F:JSONLoader3.Peripheral.XML_Parser.ReadDocumentationFile.DLLPath">
            <summary>
            The Path to the JSONLoader DLL.
            </summary>
        </member>
        <member name="F:JSONLoader3.Peripheral.XML_Parser.ReadDocumentationFile.DLLName">
            <summary>
            The Path to the JSONLoader DLL.
            </summary>
        </member>
        <member name="F:JSONLoader3.Peripheral.XML_Parser.ReadDocumentationFile.DocFileXML">
            <summary>
            The Full Contents of the XML Documentation File.
            </summary>
        </member>
        <member name="M:JSONLoader3.Peripheral.XML_Parser.ReadDocumentationFile.FetchDocFile">
            <summary>
            A function in which reads and stores the Documentation File.
            </summary>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.XML_Parser.ReadDocumentationFile.FetchItemSummary(System.ValueTuple{System.String,System.String,System.String})">
            <summary>
            This function fetches the full ItemSummary for a passed in Item.
            </summary>
            <param name="tup">A tuple from <see cref="M:JSONLoader3.Peripheral.XML_Parser.ReadDocumentationFile.GetInfo(System.String,System.Type)"/> or the Generic Version.</param>
            <returns>The Full Item Summary in non-JSON Form.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.XML_Parser.ReadDocumentationFile.GetJSONSummary(System.ValueTuple{System.String,System.String,System.String})">
            <summary>
            Gets the JSON Formatted variant of the XML Summary.
            </summary>
            <param name="tup">A tuple from <see cref="M:JSONLoader3.Peripheral.XML_Parser.ReadDocumentationFile.GetInfo(System.String,System.Type)"/> or the Generic Version.</param>
            <returns>A single-line, trimmed String of the XML Summary.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.XML_Parser.ReadDocumentationFile.GetInfo``1(System.String)">
            <summary>
            This function gets all the info you need regarding the passed in Item. This is the Generic Version.
            </summary>
            <param name="ItemName">The String Name of the Item specifically: <see cref="T:System.Reflection.FieldInfo"/> specifically the Name field.</param>
            <typeparam name="Class">The Class in which the Item comes from.</typeparam>
            <returns>A tuple persisting of the Namespace, ClassName and the ItemName you passed in.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.XML_Parser.ReadDocumentationFile.GetInfo(System.String,System.Type)">
            <summary>
            This function gets all the info you need regarding the passed in Item. This is the version where you have the actual Type.
            </summary>
            <param name="ItemName">The String Name of the Item specifically: <see cref="T:System.Reflection.FieldInfo"/> specifically the Name field.</param>
            <param name="Class">The Class in which the Item comes from.</param>
            <returns>A tuple persisting of the Namespace, ClassName and the ItemName you passed in.</returns>
            <remarks>This code is provided by Creator/Chaosyr/SaxbyMod/The Stoat Lord.</remarks>
        </member>
        <member name="M:JSONLoader3.Peripheral.XML_Parser.ReadDocumentationFile.EscapeJSON(System.String)">
            <summary>
            A small function that handles Escaping for JSON's.
            </summary>
            <param name="value">The value in which needs Escape Handling.</param>
            <returns>An escaped version of the value passed in, if something wasn't escaped properly have a dev update this function.</returns>
        </member>
        <member name="T:JSONLoader3.Subperipheral.JSONLoaderConfiguration.DefineConfiguration">
            <summary>
            This class handles the defining of Configuration relevant to the JSONLoaders and CSVLoaders.
            </summary>
        </member>
        <member name="F:JSONLoader3.Subperipheral.JSONLoaderConfiguration.DefineConfiguration.JSONLoadingPaths">
            <summary>
            This config determines the paths for JSON Based Loading in JSONLoader3+.
            </summary>
        </member>
        <member name="F:JSONLoader3.Subperipheral.JSONLoaderConfiguration.DefineConfiguration.CSVLoadingPaths">
            <summary>
            This config determines the paths for CSV Based Loading in CSVLoader.
            </summary>
        </member>
        <member name="F:JSONLoader3.Subperipheral.JSONLoaderConfiguration.DefineConfiguration.SchemaSavePath">
            <summary>
            This config determines where JSON Schemas will be saved to on boot.
            </summary>
        </member>
        <member name="F:JSONLoader3.Subperipheral.JSONLoaderConfiguration.DefineConfiguration.ShowDebugLogging">
            <summary>
            This config determines whether DebugLogging is enabled by the user or not.
            </summary>
        </member>
        <member name="F:JSONLoader3.Subperipheral.JSONLoaderConfiguration.DefineConfiguration.ShowVerboseLogging">
            <summary>
            This config determines whether VerboseLogging is enabled by the user or not.
            </summary>
        </member>
        <member name="F:JSONLoader3.Subperipheral.JSONLoaderConfiguration.DefineConfiguration.ShowAdditionalInformation">
            <summary>
            This config determines whether AdditionalInformation is enabled by the user or not.
            </summary>
        </member>
        <member name="F:JSONLoader3.Subperipheral.JSONLoaderConfiguration.DefineConfiguration.ShowSummary">
            <summary>
            This config determines whether Linting Summary Information is enabled by the user or not.
            </summary>
        </member>
        <member name="F:JSONLoader3.Subperipheral.JSONLoaderConfiguration.DefineConfiguration.HideValidationAnyOfErrors">
            <summary>
            This config determines whether Linting Will output errors for Validation Path under Any Of's is enabled by the user or not.
            </summary>
        </member>
        <member name="F:JSONLoader3.Subperipheral.JSONLoaderConfiguration.DefineConfiguration.toggleRecursiveOnPlugin">
            <summary>
            Toggles Global Recursiveness from the Plugin Level.
            </summary>
        </member>
        <member name="F:JSONLoader3.Subperipheral.JSONLoaderConfiguration.DefineConfiguration.configFile">
            <summary>
            The ConfigFile Variable referenced throughout this class.
            </summary>
        </member>
        <member name="M:JSONLoader3.Subperipheral.JSONLoaderConfiguration.DefineConfiguration.DefineConfigs(BepInEx.Configuration.ConfigFile)">
            <summary>
            This function defines all of our Configurations into the Config associated with the API.
            </summary>
            <param name="config">(Arbitrary but represents this mods ConfigFile.)</param>
        </member>
        <member name="T:JSONLoader3.Subperipheral.JSONLoaderStartupPhase.AddJSONLoaderStartupPhase">
            <summary>
            This class handles inserting our Startup Phase into the PlayerLoopSystem.
            </summary>
        </member>
        <member name="F:JSONLoader3.Subperipheral.JSONLoaderStartupPhase.AddJSONLoaderStartupPhase.hasPhaseExecuted">
            <summary>
            A check determining if our Phase has ran already.
            </summary>
        </member>
        <member name="P:JSONLoader3.Subperipheral.JSONLoaderStartupPhase.AddJSONLoaderStartupPhase.OnStartupPhaseExecuted">
            <summary>
            An action that ensures X Method is actually called by our Phase.
            </summary>
        </member>
        <member name="M:JSONLoader3.Subperipheral.JSONLoaderStartupPhase.AddJSONLoaderStartupPhase.Install">
            <summary>
            Installs our Phase into the PlayerLoopSystem.
            </summary>
        </member>
        <member name="M:JSONLoader3.Subperipheral.JSONLoaderStartupPhase.AddJSONLoaderStartupPhase.ExecuteStartupPhase">
            <summary>
            Executes our Loading Phase.
            </summary>
        </member>
        <member name="M:JSONLoader3.Subperipheral.JSONLoaderStartupPhase.AddJSONLoaderStartupPhase.InsertAfter(UnityEngine.LowLevel.PlayerLoopSystem@,System.Type,UnityEngine.LowLevel.PlayerLoopSystem)">
            <summary>
            A bool determining whether we inserted after the System successfully
            </summary>
            <param name="root">The root PlayerLoopSystem.</param>
            <param name="targetType">The Type we're trying to Insert After.</param>
            <param name="newSystem">The Phase we want to Insert.</param>
            <returns>True if we inserted successfully, false otherwise.</returns>
        </member>
    </members>
</doc>
```