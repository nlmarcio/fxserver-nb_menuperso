# fxserver-nb_menuperso
Menu personnel pour ESX<br>
Un menu simple qui regroupe l'inventaire, les factures, le téléphone, les emotes et gestion lite des voitures<br>
Il permet aussi une compatibilité manette accru. Pour ouvrir le menu personnel faite F5 ou X+Fleche du haut a la manette<br>
Pour ouvrir l'inventaire depuis le clavier : Maj+G<br>
Pour ouvrir le téléphone depuis le clavier : Maj+U<br>
Pour ouvrir les factures depuis le clavier : Maj+Y<br>

# NECESSAIRE
https://github.com/indilo53/fivem-es_extended<br>
https://github.com/FXServer-ESX/fxserver-esx_phone<br>
https://github.com/FXServer-ESX/fxserver-esx_billing<br>

# INSTALLATION
Copier le dossier "nb_menuperso" dans resources<br>
Ajouter "start nb_menuperso" dans votre serveur.cfg<br>
<br>
Modifier le esx_phone/client/main.lua pour commenter les lignes suivante :<br>
```lua
    else

      if IsControlPressed(0, Keys['F1']) and (GetGameTimer() - GUI.Time) > 150 then

        if not ESX.UI.Menu.IsOpen('phone', GetCurrentResourceName(), 'main') then
        	ESX.UI.Menu.CloseAll()
        	ESX.UI.Menu.Open('phone', GetCurrentResourceName(), 'main')
        end

        GUI.Time = GetGameTimer()

      end
```
et ajouter ces lignes en fin de script :<br>
```lua
---------------------------------------------------------------------------------------------------------
--NB : gestion des menu
---------------------------------------------------------------------------------------------------------

RegisterNetEvent('nb:openMenuTelephone')
AddEventHandler('nb:openMenuTelephone', function()
	ESX.UI.Menu.Open('phone', GetCurrentResourceName(), 'main')
end)

RegisterNetEvent('nb:closeMenuTelephone')
AddEventHandler('nb:closeMenuTelephone', function()
	TriggerEvent('nb:closeAllMenu')
end)
```
Modifier le es_extended/client/main.lua pour commenter les lignes suivante :<br>
```lua
-- Menu interactions
Citizen.CreateThread(function()
	while true do

  	Wait(0)

  	if IsControlPressed(0, Keys["F2"]) and not ESX.UI.Menu.IsOpen('default', 'es_extended', 'inventory') and (GetGameTimer() - GUI.Time) > 150 then
  		ESX.ShowInventory()
	  	GUI.Time  = GetGameTimer()
    end

  end
end)
```
et ajouter ces lignes en fin de script :<br>
```lua
---------------------------------------------------------------------------------------------------------
--NB : gestion des menu
---------------------------------------------------------------------------------------------------------

RegisterNetEvent('nb:openMenuInventaire')
AddEventHandler('nb:openMenuInventaire', function()
	ESX.ShowInventory()
end)

RegisterNetEvent('nb:closeMenuInventaire')
AddEventHandler('nb:closeMenuInventaire', function()
	if ESX.UI.Menu.IsOpen('default', GetCurrentResourceName(), 'inventory') then
		ESX.UI.Menu.Close('default', GetCurrentResourceName(), 'inventory')
		
	elseif ESX.UI.Menu.IsOpen('default', GetCurrentResourceName(), 'inventory_item') then
		ESX.UI.Menu.Close('default', GetCurrentResourceName(), 'inventory_item')
		
	elseif ESX.UI.Menu.IsOpen('default', GetCurrentResourceName(), 'inventory_item_count_give') then
		ESX.UI.Menu.Close('default', GetCurrentResourceName(), 'inventory_item_count_give')
		
	elseif ESX.UI.Menu.IsOpen('default', GetCurrentResourceName(), 'inventory_item_count_remove') then
		ESX.UI.Menu.Close('default', GetCurrentResourceName(), 'inventory_item_count_remove')
	end
end)
```
Modifier le esx_billing/client/main.lua pour commenter les lignes suivante :<br>
```lua
--Key controls
Citizen.CreateThread(function()
	while true do

  	Wait(0)

  	if IsControlPressed(0, Keys["F7"]) and not ESX.UI.Menu.IsOpen('default', GetCurrentResourceName(), 'billing') and (GetGameTimer() - GUI.Time) > 150 then
  		ShowBillsMenu()
	  	GUI.Time  = GetGameTimer()
    end

  end
end)
```
et ajouter ces lignes en fin de script :<br>
```lua
---------------------------------------------------------------------------------------------------------
--NB : gestion des menu
---------------------------------------------------------------------------------------------------------

RegisterNetEvent('nb:openMenuFactures')
AddEventHandler('nb:openMenuFactures', function()
  	ShowBillsMenu()
end)

RegisterNetEvent('nb:closeMenuFactures')
AddEventHandler('nb:closeMenuFactures', function()
	TriggerEvent('nb:closeAllMenu')
end)
```
# Attention : Ce script est optimisable et peut etre mis a jour a tout moment.
