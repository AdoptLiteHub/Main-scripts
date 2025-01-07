-- Required libraries
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/memejames/elerium-v2-ui-library//main/Library", true))()
local player = game.Players.LocalPlayer
local mouse = player:GetMouse()

-- Function to create an invisible hitbox for a player's HumanoidRootPart
local function createInvisibleHitbox(targetCharacter)
    local hitbox = Instance.new("Part")
    hitbox.Size = Vector3.new(2, 2, 2)  -- Size of the hitbox (adjust as needed)
    hitbox.Position = targetCharacter.HumanoidRootPart.Position  -- Position near the HumanoidRootPart
    hitbox.Anchored = true
    hitbox.CanCollide = false
    hitbox.Transparency = 1  -- Make the hitbox invisible
    hitbox.Parent = game.Workspace
    return hitbox
end

-- Function to find the tool called "Punch" (for Auto Punch)
local function findPunchTool()
    -- Check for the "Punch" tool in the player's backpack
    for _, tool in pairs(player.Backpack:GetChildren()) do
        if tool.Name == "Punch" then
            return tool
        end
    end
    return nil
end

-- Function to equip the "Punch" tool and use it
local function equipAndUsePunch()
    local punchTool = findPunchTool()
    if punchTool then
        -- Equip the "Punch" tool
        player.Character.Humanoid:EquipTool(punchTool)
        
        -- Simulate the use of the tool (punching)
        -- The "Activated" event is triggered when the tool is used.
        punchTool.Activated:Fire()
    end
end

-- Create the UI window
local window = library:AddWindow("Lite Hub test", {
    main_color = Color3.fromRGB(41, 74, 122),  -- Color
    min_size = Vector2.new(400, 450),  -- Size of the GUI
    can_resize = false,  -- true or false
})

-- Create a tab called 'Killing'
local Killing = window:AddTab("Killing")

-- Auto Kill Toggle (for all players)
Killing:AddSwitch("Auto Kill", function(bool)
    local hitboxes = {}  -- Table to store hitboxes
    local rightHand = player.Character:WaitForChild("RightHand")
    local leftHand = player.Character:WaitForChild("LeftHand")
    
    while bool do
        -- Loop through all players and create an invisible hitbox near their HumanoidRootPart
        for _, targetPlayer in pairs(game.Players:GetPlayers()) do
            if targetPlayer ~= player and targetPlayer.Character then
                local targetHRP = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
                if targetHRP then
                    -- Create the invisible hitbox for each player
                    local hitbox = createInvisibleHitbox(targetPlayer.Character)
                    table.insert(hitboxes, hitbox)  -- Store the hitbox to clean it up later

                    -- Move the invisible hitbox to the player's right and left hands
                    hitbox.Position = rightHand.Position + (rightHand.CFrame.LookVector * 3)  -- Offset from right hand
                    wait(0.1)  -- Adjust speed if necessary
                    hitbox.Position = leftHand.Position + (leftHand.CFrame.LookVector * 3)  -- Offset from left hand
                    wait(0.1)  -- Adjust speed if necessary
                end
            end
        end
        wait(1)  -- Update every second
    end

    -- Cleanup hitboxes when the toggle is turned off
    for _, hitbox in pairs(hitboxes) do
        hitbox:Destroy()
    end
end)

-- Add a Label
Killing:AddLabel("Target")

-- Create Dropdown for selecting player
local dropdown = Killing:AddDropdown("Select Player", function(text)
    -- No print statements anymore, just the dropdown to select a player
end)

-- Function to populate the dropdown with all players in the server
local function updateDropdown()
    -- Clear existing options in the dropdown
    dropdown:Clear()

    -- Dynamically populate dropdown with all players in the server
    for _, targetPlayer in pairs(game.Players:GetPlayers()) do
        dropdown:Add(targetPlayer.Name)
    end
end

-- Update dropdown on script load
updateDropdown()

-- Listen for players joining or leaving and update the dropdown
game.Players.PlayerAdded:Connect(function()
    updateDropdown()
end)

game.Players.PlayerRemoving:Connect(function()
    updateDropdown()
end)

-- Auto Kill Target Toggle (for the selected player)
Killing:AddSwitch("Auto Kill Target", function(bool)
    local targetPlayerName = dropdown:GetSelected()  -- Get selected player
    local hitboxes = {}  -- Table to store hitboxes
    local rightHand = player.Character:WaitForChild("RightHand")
    local leftHand = player.Character:WaitForChild("LeftHand")
    
    while bool do
        local targetPlayer = game.Players:FindFirstChild(targetPlayerName)
        if targetPlayer and targetPlayer.Character then
            local targetHRP = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
            if targetHRP then
                -- Create the invisible hitbox for the selected player
                local hitbox = createInvisibleHitbox(targetPlayer.Character)
                table.insert(hitboxes, hitbox)  -- Store the hitbox to clean it up later

                -- Move the invisible hitbox to the player's right and left hands
                while bool do
                    -- Teleport the hitbox to the right hand
                    hitbox.Position = rightHand.Position + (rightHand.CFrame.LookVector * 3)  -- Offset from right hand
                    wait(0.1)  -- Adjust speed if necessary
                    
                    -- Teleport the hitbox to the left hand
                    hitbox.Position = leftHand.Position + (leftHand.CFrame.LookVector * 3)  -- Offset from left hand
                    wait(0.1)  -- Adjust speed if necessary
                end
            end
        end
        wait(1)  -- Update every second
    end

    -- Cleanup hitboxes when the toggle is turned off
    for _, hitbox in pairs(hitboxes) do
        hitbox:Destroy()
    end
end)

-- Add Punching Section (for example)
Killing:AddLabel("Punching")

-- Auto Punch Toggle (Equip and use the Punch tool infinitely)
Killing:AddSwitch("Auto Punch", function(bool)
    while bool do
        equipAndUsePunch()  -- Equip and use the "Punch" tool
        wait(0.1)  -- Wait before triggering again (this controls how fast it punches)
    end
end)
