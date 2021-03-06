[SIZE="4"]A Theater Items API For Insurgency(2014)[/SIZE]
This API provides the function of querying the class name of gears and weapon upgrades of player equipment, and also provides the function of giving weapon the weapon upgrade.

[SIZE="4"]Command[/SIZE]
[PHP]"sm_update_theater_items" // Force update the theater items name record list
"listweapons" // List all weapons in the currently loaded theater
"listupgrades" // List all weapon upgrades in the currently loaded theater
"listexplosives" // List all explosives in the currently loaded theater
"listplayergear" // List all player gear in the currently loaded theater[/PHP]

[SIZE="4"]Installation Guide[/SIZE]
[CODE]Put TheaterItemsAPI.smx into "sourcemod\plugins\"
Put TheaterItemsAPI.inc into "sourcemod\scripting\include\"
Add "#include <TheaterItemsAPI>" at the top of your plugin code and check the TheaterItemsAPI.inc file when you use it[/CODE]

[SIZE="4"]Main API[/SIZE]
 [SPOILER][PHP]/**
 * Get theater item's index by weapon upgrade Name
 * 
 * @param cWeaponUpgradeName  Weapon upgrade name in theater.
 * @return                    Weapon upgrade theater item's index if found, -1 otherwise.
 */
int GetTheaterItemIdByWeaponUpgradeName(char[] cWeaponUpgradeName)

 /**
 * Get theater item's index by Player gear Name
 * 
 * @param cPlayerGearName     Player gear name in theater.
 * @return                    Player gear theater item's index if found, -1 otherwise.
 */
int GetTheaterItemIdByPlayerGearName(char[] cPlayerGearName)

 /**
 * Get weapon upgrade name by theater weapon upgrade item's index
 * 
 * @param iItemIndex        Theater weapon upgrade item's index
 * @param cItemName         Buffer to store the item's name.
 * @param len               Maximum length of string buffer
 * @return                  True on success, false otherwise.
 */
bool GetWeaponUpgradeItemName(int iItemIndex, char[] cItemName, int len)

 /**
 * Get player gear name by theater player gear item's index
 * 
 * @param iItemIndex        Theater player gear item's index
 * @param cItemName         Buffer to store the item's name.
 * @param len               Maximum length of string buffer
 * @return                  True on success, false otherwise.
 */
bool GetPlayerGearItemName(int iItemIndex, char[] cItemName, int len)

 /**
 * Check if client has gear by gear name. (this "has" only mean player actually equipped and wearing it, but not necessarily equipped it in the inventory.)
 * 
 * @param client              Client index
 * @param cGearName           Gear name for check
 * @return                    Whether client has the gear
 */
bool IsClientHasGear(int client, char[] cGearName)

 /**
 * Check if client equipped gear by gear name. (this "equipped" only mean equipped in the inventory, but it's not necessarily actually equipped. player may not be wearing it)
 * 
 * @param client              Client index
 * @param cGearName           Gear name for check
 * @return                    Whether client Equipped the gear
 */
bool IsClientEquippedGear(int client, char[] cGearName)

 /**
 * Check if weapon has upgrade by upgrade name
 * 
 * @param iWeaponID           Weapon index
 * @param cUpgradeName        Weapon Upgrade name for check
 * @return                    Whether weapon has the upgrade
 */
bool IsWeaponHasUpgrade(int iWeaponID, char[] cUpgradeName)

 /**
 * Give weapon a upgrade by upgrade name
 * 
 * @param iWeaponID           Weapon index
 * @param iUpgradeSlotType    Weapon upgrade slot type
 * @param cUpgradeName        Weapon Upgrade name in theater
 * @return                    True on success, false otherwise.
 */
bool GiveUpgradeToWeaponByName(int iWeaponID, WEAPON_UPGRADE_SLOT iUpgradeSlotType, char[] cUpgradeName)

 /**
 * Give weapon a upgrade by upgrade theater item's index
 * 
 * @param iWeaponID           Weapon index
 * @param iUpgradeSlotType    Weapon upgrade slot type
 * @param iUpgradeID          Weapon Upgrade theater item's index
 * @return                    True on success, false otherwise.
 */
bool GiveUpgradeToWeaponByTheaterId(int iWeaponID, WEAPON_UPGRADE_SLOT iUpgradeSlotType, int iUpgradeID)[/PHP][/SPOILER]
[SIZE="4"]Example Code[/SIZE]
[SPOILER][PHP]#include <TheaterItemsAPI>

...

void CheckClientGear(int client)
{
    if (IsClientHasGear(client, "nightvision"))
    {
        // Do something about client wearing a night vision
        // ...
    }
    return;
}

void GiveClientANewWeaponWithSomeUpgrades(int client)
{
    int iWeaponID = GivePlayerItem(client, "weapon_mk18");
    if (iWeaponID > MaxClients && IsValidEntity(iWeaponID))
    {
        GiveUpgradeToWeaponByName(iWeaponID, WEAPON_UPGRADE_OPTICS, "optic_eotech");
        GiveUpgradeToWeaponByName(iWeaponID, WEAPON_UPGRADE_SIDERAIL, "siderail_flashlight_rail");
    }
    return;
}

void GiveClientsWeaponAnOpticalSight(int client)
{
    int iWeaponID = GetEntPropEnt(client, Prop_Data, "m_hActiveWeapon");
    GiveUpgradeToWeaponByName(iWeaponID, WEAPON_UPGRADE_OPTICS, "optic_eotech");
    return;
}[/PHP][/SPOILER]

中文INS服务器使用此插件请注明和鸣谢作者。

[SIZE="4"]Link[/SIZE]
[LIST]
[*][SIZE="4"][URL="https://github.com/gandor233/INS_TheaterItemsAPI"]Github[/URL][/SIZE]
[/LIST]