
# InventoryDataSetter.as

- open \_.swf
- go to InventoryDataSetter.as\/CraftingDataSetter.as

## Frostfall Protection Data Fix

`class InventoryDataSetter` -> add:

```as
var _listProcessed;
```

in `class InventoryDataSetter` -> in `function processEntry` -> in `switch` -> in `case skyui.defines.Form.TYPE_ARMOR` -> add:

```as
if(this._listProcessed)
{
skse.SendModEvent("Frost_OnSkyUIInvListGetEntryProtectionDataOnProcess","",a_entryObject.itemIndex,0);
}
```

## Total Weight Prop

in `class InventoryDataSetter` -> in `function processEntry` -> add:

```as
a_entryObject.infoTotalWeight = !(a_itemInfo.weight > 0 && a_itemInfo.count > 0) ? null : Math.round(a_itemInfo.weight * a_itemInfo.count * 100) / 100;
```

## Total Value Prop

in `class InventoryDataSetter` -> in `function processEntry` -> add:

```as
a_entryObject.infoTotalValue = a_itemInfo.value <= 0 ? null : Math.round(a_itemInfo.value * a_itemInfo.count * 100) / 100;
```

## Base Armor Prop

- +`CraftingDataSetter`
- \\* Requires SAS\*.dll for prop to be set

in `class InventoryDataSetter` -> in `function processEntry` -> in `switch` -> in `case skyui.defines.Form.TYPE_ARMOR` -> add:

```as
a_entryObject.infoBaseArmor = _global.skse.plugins.SAS.BaseArmorRating(a_entryObject.formId);
```

## Enchantment Known Prop

- \\* Requires SAS\*.dll for prop to be set

in `class InventoryDataSetter` -> in `function processEntry` -> in `switch` -> in `case skyui.defines.Form.TYPE_ARMOR` -> add:

```as
a_entryObject.checkEnchantment = a_entryObject.SASinvobj.IsEnchantmentKnown;
```

in `class InventoryDataSetter` -> in `function processEntry` -> in `switch` -> in `case skyui.defines.Form.TYPE_WEAPON` -> add:

```as
a_entryObject.checkEnchantment = a_entryObject.SASinvobj.IsEnchantmentKnown;
```

## Enchantment Disenchantable Prop

- \\* Requires SAS\*.dll for prop to be set

in `class InventoryDataSetter` -> in `function processEntry` -> in `switch` -> in `case skyui.defines.Form.TYPE_ARMOR` -> add:

```as
a_entryObject.checkDisenchantable = _global.skse.plugins.SAS.IsDisenchantable(a_entryObject.formId,a_entryObject.isEnchanted);
```

in `class InventoryDataSetter` -> in `function processEntry` -> in `switch` -> in `case skyui.defines.Form.TYPE_WEAPON` -> add:

```as
a_entryObject.checkDisenchantable = _global.skse.plugins.SAS.IsDisenchantable(a_entryObject.formId,a_entryObject.isEnchanted);
```

## Warmth Prop

in `class InventoryDataSetter` -> in `function processEntry` -> in `switch` -> in `case skyui.defines.Form.TYPE_ARMOR` -> add:

```as
a_entryObject.infoWarmth = a_itemInfo.warmth <= 0 ? null : Math.round(a_itemInfo.warmth * 100) / 100;
```

## Base Damage Prop

- +`CraftingDataSetter`

in `class InventoryDataSetter` -> in `function processEntry` -> in `switch` -> in `case skyui.defines.Form.TYPE_WEAPON` -> add:

```as
a_entryObject.infoBaseDamage = a_entryObject.baseDamage <= 0 ? null : Math.round(a_entryObject.baseDamage * 100) / 100;
```

## Reach Prop

- +`CraftingDataSetter`

in `class InventoryDataSetter` -> in `function processEntry` -> in `switch` -> in `case skyui.defines.Form.TYPE_WEAPON` -> add:

```as
a_entryObject.infoReach = a_entryObject.reach <= 0 ? null : Math.round(a_entryObject.reach * 100) / 100;
```

## Weapon Speed Prop

- +`CraftingDataSetter`

in `class InventoryDataSetter` -> in `function processEntry` -> in `switch` -> in `case skyui.defines.Form.TYPE_WEAPON` -> add:

```as
a_entryObject.infoSpeed = a_entryObject.speed <= 0 ? null : Math.round(a_entryObject.speed * 100) / 100;
```

## Weapon Stagger Prop

- +`CraftingDataSetter`

in `class InventoryDataSetter` -> in `function processEntry` -> in `switch` -> in `case skyui.defines.Form.TYPE_WEAPON` -> add:

```as
a_entryObject.infoStagger = a_entryObject.stagger <= 0 ? null : Math.round(a_entryObject.stagger * 100) / 100;
```

## SkyUI Weapons Pack

- \\* Requires SkyUI Weapons Pack version of `icons_items_psychosteve.swf` otherwise errors

in `class InventoryDataSetter` -> in `function processWeaponType` -> add:

```as
if(a_entryObject.keywords.WeapTypeSpear != undefined)
{
   a_entryObject.subType = skyui.defines.Weapon.TYPE_SPEAR;
   a_entryObject.subTypeDisplay = skyui.util.Translator.translate("$Spear");
   return undefined;
}
if(a_entryObject.keywords.WeapTypeJavelin != undefined)
{
   a_entryObject.subType = skyui.defines.Weapon.TYPE_JAVELIN;
   a_entryObject.subTypeDisplay = skyui.util.Translator.translate("$Javelin");
   return undefined;
}
if(a_entryObject.keywords.WeapTypePike != undefined)
{
   a_entryObject.subType = skyui.defines.Weapon.TYPE_PIKE;
   a_entryObject.subTypeDisplay = skyui.util.Translator.translate("$Pike");
   return undefined;
}
if(a_entryObject.keywords.WeapTypeHalberd != undefined)
{
   a_entryObject.subType = skyui.defines.Weapon.TYPE_HALBERD;
   a_entryObject.subTypeDisplay = skyui.util.Translator.translate("$Halberd");
   return undefined;
}
if(a_entryObject.keywords.WeapTypeRapier != undefined)
{
   a_entryObject.subType = skyui.defines.Weapon.TYPE_RAPIER;
   a_entryObject.subTypeDisplay = skyui.util.Translator.translate("$Rapier");
   return undefined;
}
if(a_entryObject.keywords.WeapTypeQuarterstaff != undefined)
{
   a_entryObject.subType = skyui.defines.Weapon.TYPE_QUARTERSTAFF;
   a_entryObject.subTypeDisplay = skyui.util.Translator.translate("$Quarterstaff");
   return undefined;
}
if(a_entryObject.keywords.WeapTypeClaw != undefined)
{
   a_entryObject.subType = skyui.defines.Weapon.TYPE_CLAW;
   a_entryObject.subTypeDisplay = skyui.util.Translator.translate("$Claw");
   return undefined;
}
if(a_entryObject.keywords.WeapTypeWhip != undefined)
{
   a_entryObject.subType = skyui.defines.Weapon.TYPE_WHIP;
   a_entryObject.subTypeDisplay = skyui.util.Translator.translate("$Whip");
   return undefined;
}
if(a_entryObject.keywords.WeapTypeKatana != undefined)
{
   a_entryObject.subType = skyui.defines.Weapon.TYPE_KATANA;
   a_entryObject.subTypeDisplay = skyui.util.Translator.translate("$Katana");
   return undefined;
}
if(a_entryObject.keywords.WeapTypeScythe != undefined)
{
   a_entryObject.subType = skyui.defines.Weapon.TYPE_SCYTHE;
   a_entryObject.subTypeDisplay = skyui.util.Translator.translate("$Scythe");
   return undefined;
}
if(a_entryObject.keywords.WeapTypeGun != undefined)
{
   a_entryObject.subType = skyui.defines.Weapon.TYPE_GUN;
   a_entryObject.subTypeDisplay = skyui.util.Translator.translate("$Gun");
   return undefined;
}
```

## Slots Prop

- +`CraftingDataSetter`

in `class InventoryDataSetter` -> in `function processArmorOther` -> add:

```as
var _loc2_ = [];
var _loc3_ = 0;
var _loc4_ = skyui.defines.Armor.PARTMASK_PRECEDENCE;
while(_loc3_ < _loc4_.length)
{
   if(a_entryObject.partMask & _loc4_[_loc3_])
   {
     _loc2_.push(Math.log(_loc4_[_loc3_]) / 0.6931471805599453 + 30);
   }
   _loc3_ += 1;
}
a_entryObject.bipedSlots = a_entryObject.mainPartMask;
a_entryObject.bipedSlotsDisplay = _loc2_.join(",");
```

## Survival Mode Hunger Prop

- +`CraftingDataSetter`

- \\* Requires SAS\*.dll for prop to be set

in `class InventoryDataSetter` -> in `function processPotionType` -> in `if(...ALCHFLAG_FOOD)` -> add:

```as
a_entryObject.infoHunger = _global.skse.plugins.SAS.SMFoodHunger(a_entryObject.formId);
```

## Survival Mode Fortify Warmth Prop

- +`CraftingDataSetter`
- \\* Requires SAS\*.dll for prop to be set

in `class InventoryDataSetter` -> in `function processPotionType` -> in `if(...ALCHFLAG_FOOD)` -> add:

```as
a_entryObject.fWarmth = _global.skse.plugins.SAS.SMFoodFortifyWarmth(a_entryObject.formId);
```

## Survival Mode Restore Cold Prop

- +`CraftingDataSetter`
- \\* Requires SAS\*.dll for prop to be set

in `class InventoryDataSetter` -> in `function processPotionType` -> in `if(...ALCHFLAG_FOOD)` -> add:

```as
a_entryObject.restoreCold = _global.skse.plugins.SAS.SMFoodRestoreCold(a_entryObject.formId);
```

## SunHelm Hunger Prop

- +`CraftingDataSetter`
- \\* Requires SAS\*.dll for prop to be set

in `class InventoryDataSetter` -> in `function processPotionType` -> in `if(...ALCHFLAG_FOOD)` -> add:

```as
a_entryObject.SHHunger = _global.skse.plugins.SAS.SHHunger(a_entryObject.formId);
```

## SunHelm Thirst Prop

- +`CraftingDataSetter`
- \\* Requires SAS\*.dll for prop to be set

in `class InventoryDataSetter` -> in `function processPotionType` -> in `if(...ALCHFLAG_FOOD)` -> add:

```as
a_entryObject.SHThirst = _global.skse.plugins.SAS.SHThirst(a_entryObject.formId);
```

## SunHelm Fortify Warmth Prop

- +`CraftingDataSetter`
- \\* Requires SAS\*.dll for prop to be set

in `class InventoryDataSetter` -> in `function processPotionType` -> in `if` Food -> add:

```as
a_entryObject.SHFW = _global.skse.plugins.SAS.SHFW(a_entryObject.formId);
```

## Fix Firewood

in `class InventoryDataSetter` -> in `function processMiscType` -> in `else if` Firewood -> change:

```as
else if(a_entryObject.keywords.VendorItemFirewood != undefined)
```

to:

```as
else if(a_entryObject.keywords.VendorItemFireword != undefined)
```

## Fix Empty Soul Gem

- `CraftingDataSetter`

in `class CraftingDataSetter` -> in `function processSoulGemStatus` -> in `if` `soulSize != undefined` -> in `switch` -> in `case` `SOULGEM_NONE` -> change:

```as
a_entryObject.soulSizeDisplay = null;
```

to:

```as
a_entryObject.soulSizeDisplay = "$Empty";
```
