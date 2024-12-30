# More Crafting Object Properties

SWF files that need support: `constructibleobjectmenu.swf`, `craftingmenu.swf`.

Open the swf file you're adding support to in JPEXS FFdec.

Find and select the `CraftingDataSetter` tag. In the Resources View, it should be under `scripts/__Packages/<default package>/CraftingDataSetter`.

In the `ActionScript source` panel, you will find the ActionScript code for the `CraftingDataSetter` class. This is where we will add our new properties.

## Armor Stats

In the `process Entry` function, in the switch case for `TYPE_ARMOR`, add the following code if it does not already exist:

```as
            a_entryObject.checkEnchantment = a_entryObject.SASinvobj.IsEnchantmentKnown;
            a_entryObject.checkDisenchantable = _global.skse.plugins.SAS.IsDisenchantable(a_entryObject.formId,a_entryObject.isEnchanted);
```

## Weapon Stats

In the `process Entry` function, in the switch case for `TYPE_WEAPON`, add the following code if it does not already exist:

```as
            a_entryObject.infoBaseDamage = a_entryObject.baseDamage <= 0 ? null : Math.round(a_entryObject.baseDamage * 100) / 100;
            a_entryObject.infoReach = a_entryObject.reach <= 0 ? null : Math.round(a_entryObject.reach * 100) / 100;
            a_entryObject.infoSpeed = a_entryObject.speed <= 0 ? null : Math.round(a_entryObject.speed * 100) / 100;
            a_entryObject.infoStagger = a_entryObject.stagger <= 0 ? null : Math.round(a_entryObject.stagger * 100) / 100;
```

## Armor Slots

In the `processArmorOther` function, add the following code if it does not already exist:

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

## Food Stats

In the `processPotionType` function, in the if case for `ALCHFLAG_FOOD`, add the following code if it does not already exist:

```as
         a_entryObject.infoHunger = _global.skse.plugins.SAS.SMFoodHunger(a_entryObject.formId);
         a_entryObject.fWarmth = _global.skse.plugins.SAS.SMFoodFortifyWarmth(a_entryObject.formId);
         a_entryObject.restoreCold = _global.skse.plugins.SAS.SMFoodRestoreCold(a_entryObject.formId);
         a_entryObject.SHHunger = _global.skse.plugins.SAS.SHHunger(a_entryObject.formId);
         a_entryObject.SHThirst = _global.skse.plugins.SAS.SHThirst(a_entryObject.formId);
         a_entryObject.SHFW = _global.skse.plugins.SAS.SHFW(a_entryObject.formId);
```
