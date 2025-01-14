local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- Reference to the existing skin system
-- Make sure to adjust this for the actual inventory system in Counter Blox
local skinDatabase = {
    "Dragon Lore",
    "Asiimov",
    "Hyper Beast",
    "Medusa",
    -- Add all available skins here
}

local function grantAllSkins(player)
    -- Verify that the player is an admin
    if player:IsInGroup(YOUR_ADMIN_GROUP_ID) then -- Replace YOUR_ADMIN_GROUP_ID with the ID of the admin group
        -- Player's inventory system (adjust according to Counter Blox's system)
        local inventory = player:FindFirstChild("Inventory")
        
        if not inventory then
            warn("Player " .. player.Name .. " does not have an Inventory object.")
            return
        end

        -- Add all skins to the player's inventory
        for _, skinName in ipairs(skinDatabase) do
            if not inventory:FindFirstChild(skinName) then
                local newSkin = Instance.new("StringValue")
                newSkin.Name = skinName
                newSkin.Parent = inventory
            end
        end

        print("All skins granted to " .. player.Name)
    else
        warn("Player " .. player.Name .. " is not an admin and cannot receive all skins.")
    end
end

-- Command to grant skins (adjust for your command system)
game.Players.PlayerAdded:Connect(function(player)
    player.Chatted:Connect(function(msg)
        if msg == "!grantAllSkins" then
            grantAllSkins(player)
        end
    end)
end)
