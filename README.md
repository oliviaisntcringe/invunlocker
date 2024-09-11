# invunlocker
Inventory Unlocker
It's nothing new but it's following functions (SDK):

Code:
> Function ShooterGame.ContentLibrary.ApplySkin @ game+0x2c7a550
 
> // other stuff
> ShooterGame.ShooterCharacter.GetInventory
> ShooterGame.AresInventory.GetCurrentEquippable***
And for clearing the weapon components on the gun (before apply):
Code:
>Function ShooterGame.ContentLibrary.ClearWeaponComponents // @ game+0x2c7a720
So we need multiple shit to apply the skin on your equippable.

Code:
>struct AActor* Parent // Your equippable
>struct UEquippableSkinDataAsset* EquippableSkinAsset // Your Skin Asset
>struct UEquippableSkinChromaDataAsset* EquippableChromaAsset // Your Chroma (The colors)
>int32_t SkinLevel // Skin Level 
>struct UEquippableCharmDataAsset* EquippableCharmAsset, // Buddie
>int32_t CharmLevel // Buddielevel
You can set the skin over your arsenal, it's pretty easy but you have to unlock your aresnal first - But i will not explain it here. This post is only for the skin changer in general.

You can find all skin assets over find_object - Here a example: (Skins: https://valorant-api.com/v1/weapons/skins)

Asset Path: ShooterGame/Content/Equippables/Guns/HvyMachineGuns/HMG/Alien/HMG_Alien_PrimaryAsset
Chroma (Lvl2): ShooterGame/Content/Equippables/Guns/HvyMachineGuns/HMG/Alien/Levels/HMG_Alien_Lv2_PrimaryAsset

FindObject Asset Path:
Code:
>Default__HMG_Alien_PrimaryAsset_C
>FindObject Chroma:
Code:
>Default__HMG_Alien_Lv2_PrimaryAsset_C
Example Code:
Code:
>uobject* skin_data_asset = (uobject*)uobject::static_find_object(nullptr, reinterpret_cast<uobject*>(-1), L"Default__HMG_Alien_PrimaryAsset_C", false);
>uobject* chroma_data_asset = (uobject*)uobject::static_find_object(nullptr, reinterpret_cast<uobject*>(-1), L"Default__HMG_Alien_Lv2_PrimaryAsset_C", false);
 
>if(skin_data_asset && chroma_data_asset) {
>	content_library::clear_weapon_components(equippable);
>	content_library::apply_skin(equippable, skin_data_asset, chroma_data_asset, 2, nullptr, -1);	
>}

That's it -> This example will give you the Alien Skin...

It is important that you set your skin within a game thread, otherwise your game will crash.

[B]Before you set the skin you need to bypass the small protection by riot.
