-- Required libraries
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/memejames/elerium-v2-ui-library//main/Library", true))()
local player = game.Players.LocalPlayer
local mouse = player:GetMouse()

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
    main_color = Color3.fromRGB(41, 74, 122), -- Color
    min_size = Vector2.new(400, 450), -- Size of the gui
    can_resize = false, -- true or false
})

-- Create a tab called 'Killing'
local Killing = window:AddTab("Killing")

-- Auto Kill Toggle
Killing:AddSwitch("Auto Kill", function(bool)
    local hitboxes = {}  -- Table to store hitboxes
    while bool do
        -- Loop through all players and create an invisible hitbox near their HumanoidRootPart
        for _, targetPlayer in pairs(game.Players:GetPlayers()) do
            if targetPlayer ~= player and targetPlayer.Character then
                local targetHRP = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
                if targetHRP then
                    -- Create the invisible hitbox
                    local hitbox = createInvisibleHitbox(targetPlayer.Character)
                    table.insert(hitboxes, hitbox)  -- Store the hitbox to clean it up later
                end
            end
        end
        wait(1)
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

-- Dynamically populate dropdown with all players in the server
for _, targetPlayer in pairs(game.Players:GetPlayers()) do
    dropdown:Add(targetPlayer.Name)
end

-- Auto Kill Target Toggle
Killing:AddSwitch("Auto Kill Target", function(bool)
    local targetPlayerName = dropdown:GetSelected() -- Get selected player
    local hitboxes = {}  -- Table to store hitboxes
    while bool do
        local targetPlayer = game.Players:FindFirstChild(targetPlayerName)
        if targetPlayer and targetPlayer.Character then
            local targetHRP = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
            if targetHRP then
                -- Create the invisible hitbox for the selected player
                local hitbox = createInvisibleHitbox(targetPlayer.Character)
                table.insert(hitboxes, hitbox)  -- Store the hitbox to clean it up later
            end
        end
        wait(1)
    end

    -- Cleanup hitboxes when the toggle is turned off
    for _, hitbox in pairs(hitboxes) do
        hitbox:Destroy()
    end
end)

-- Spy Player Toggle
Killing:AddSwitch("Spy Player", function(bool)
    local targetPlayerName = dropdown:GetSelected() -- Get selected player
    while bool do
        local targetPlayer = game.Players:FindFirstChild(targetPlayerName)
        if targetPlayer and targetPlayer.Character then
            -- Set the camera to follow the selected player's character
            game.Workspace.CurrentCamera.CameraSubject = targetPlayer.Character.Humanoid
        end
        wait(0.1)
    end
end)

-- Add Punching Section
Killing:AddLabel("Punching")

-- Auto Punch Toggle
Killing:AddSwitch("Auto Punch", function(bool)
    while bool do
        equipAndUsePunch()  -- Equip and use the "Punch" tool
        wait(0.1)  -- Wait before triggering again
    end
end)
