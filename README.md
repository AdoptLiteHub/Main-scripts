-- Required libraries
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/memejames/elerium-v2-ui-library//main/Library", true))()
local player = game.Players.LocalPlayer
local mouse = player:GetMouse()

-- Function to find the tool called "Punch" (for Auto Punch)
local function findPunchTool()
    for _, tool in pairs(player.Backpack:GetChildren()) do
        if tool.Name == "Punch" then
            return tool
        end
    end
    return nil
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
    while bool do
        -- Loop through all players and set their humanoidrootpart's position to your hands
        for _, targetPlayer in pairs(game.Players:GetPlayers()) do
            if targetPlayer ~= player then
                local targetHRP = targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart")
                if targetHRP then
                    -- Set position to your right hand and left hand alternatively
                    local rightHand = player.Character and player.Character:FindFirstChild("RightHand")
                    local leftHand = player.Character and player.Character:FindFirstChild("LeftHand")
                    if rightHand and leftHand then
                        -- Toggle between right and left hand positions
                        targetHRP.CFrame = rightHand.CFrame
                        wait(0.5)
                        targetHRP.CFrame = leftHand.CFrame
                        wait(0.5)
                    end
                end
            end
        end
        wait(1)
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
    while bool do
        local targetPlayer = game.Players:FindFirstChild(targetPlayerName)
        if targetPlayer and targetPlayer.Character then
            local targetHRP = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
            if targetHRP then
                -- Set position to your right hand and left hand alternatively
                local rightHand = player.Character and player.Character:FindFirstChild("RightHand")
                local leftHand = player.Character and player.Character:FindFirstChild("LeftHand")
                if rightHand and leftHand then
                    -- Toggle between right and left hand positions
                    targetHRP.CFrame = rightHand.CFrame
                    wait(0.5)
                    targetHRP.CFrame = leftHand.CFrame
                    wait(0.5)
                end
            end
        end
        wait(1)
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
        local punchTool = findPunchTool()
        if punchTool then
            -- Equip and use the punch tool
            player.Character.Humanoid:EquipTool(punchTool)
            punchTool.Activated:Fire()
        end
        wait(0.1)
    end
end)
