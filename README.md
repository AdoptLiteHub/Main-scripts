-- Required libraries
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/memejames/elerium-v2-ui-library//main/Library", true))()
local player = game.Players.LocalPlayer

-- Create the UI window
local window = library:AddWindow("Lite Hub test", {
	main_color = Color3.fromRGB(41, 74, 122), -- Color
	min_size = Vector2.new(400, 450), -- Size of the gui
	can_resize = false, -- true or false
})

-- Create a tab called 'Killing'
window:AddTab("Killing") 

-- Variable to hold the current target
local currentTarget = nil
local AutoKillToggle = nil
local KillTargetToggle = nil

-- Create a label for Punching
KillingTab:CreateLabel("Punching")

-- Auto Kill Toggle
AutoKillToggle = KillingTab:CreateToggle({
    Name = "Auto Kill",
    Callback = function(state)
        if state then
            -- Start auto killing (create invisible hitboxes for each player, except yourself)
            while AutoKillToggle:GetState() do
                for _, targetPlayer in pairs(game.Players:GetPlayers()) do
                    if targetPlayer ~= player then
                        -- Create a hitbox at the target player's HumanoidRootPart
                        local humanoidRootPart = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
                        if humanoidRootPart then
                            local hitbox = Instance.new("Part")
                            hitbox.Size = Vector3.new(2, 2, 2)
                            hitbox.Position = humanoidRootPart.Position
                            hitbox.Anchored = true
                            hitbox.CanCollide = false
                            hitbox.Transparency = 1 -- Invisible hitbox
                            hitbox.Parent = game.Workspace

                            -- Attach the hitbox to the player's right and left hand
                            local rightHand = player.Character:FindFirstChild("RightHand")
                            local leftHand = player.Character:FindFirstChild("LeftHand")
                            if rightHand and leftHand then
                                hitbox.CFrame = CFrame.new(rightHand.Position) -- Position at right hand
                                wait(0.1) -- Adjust for desired speed
                                hitbox.CFrame = CFrame.new(leftHand.Position) -- Position at left hand
                                wait(0.1)
                            end

                            -- Cleanup after using the hitbox
                            hitbox:Destroy()
                        end
                    end
                end
                wait(0.1) -- Adjust for desired speed
            end
        end
    end
})

-- Create a label and dropdown for players
KillingTab:CreateLabel("Target")
local PlayerDropdown = KillingTab:CreateDropdown({
    Name = "Player Dropdown",
    Options = {},
    Callback = function(selectedPlayerName)
        -- Handle dropdown selection for target player
        local targetPlayer = game.Players:FindFirstChild(selectedPlayerName)
        if targetPlayer then
            -- Update the selected target
            currentTarget = targetPlayer
        end
    end
})

-- Update dropdown options to list all players in the server
game.Players.PlayerAdded:Connect(function(newPlayer)
    PlayerDropdown:AddOption(newPlayer.Name)
end)

game.Players.PlayerRemoving:Connect(function(removedPlayer)
    PlayerDropdown:RemoveOption(removedPlayer.Name)
end)

-- Create 'Kill Target' Toggle
KillTargetToggle = KillingTab:CreateToggle({
    Name = "Kill Target",
    Callback = function(state)
        if state then
            -- Start killing the selected target
            while KillTargetToggle:GetState() and currentTarget do
                local humanoidRootPart = currentTarget.Character:FindFirstChild("HumanoidRootPart")
                if humanoidRootPart then
                    -- Create a hitbox at the selected target's HumanoidRootPart
                    local hitbox = Instance.new("Part")
                    hitbox.Size = Vector3.new(2, 2, 2)
                    hitbox.Position = humanoidRootPart.Position
                    hitbox.Anchored = true
                    hitbox.CanCollide = false
                    hitbox.Transparency = 1 -- Invisible hitbox
                    hitbox.Parent = game.Workspace

                    -- Attach the hitbox to the player's right and left hand
                    local rightHand = player.Character:FindFirstChild("RightHand")
                    local leftHand = player.Character:FindFirstChild("LeftHand")
                    if rightHand and leftHand then
                        hitbox.CFrame = CFrame.new(rightHand.Position) -- Position at right hand
                        wait(0.1) -- Adjust for desired speed
                        hitbox.CFrame = CFrame.new(leftHand.Position) -- Position at left hand
                        wait(0.1)
                    end

                    -- Cleanup after using the hitbox
                    hitbox:Destroy()
                end
                wait(0.1) -- Adjust for desired speed
            end
        end
    end
})

-- Create 'Spy' Toggle
KillingTab:CreateToggle({
    Name = "Spy",
    Callback = function(state)
        if state then
            -- Go into the POV of the selected player
            if currentTarget then
                game:GetService("Players").LocalPlayer.CameraMode = Enum.CameraMode.Locked
                -- You can set the camera's CFrame to match the target's CFrame
                local humanoidRootPart = currentTarget.Character:WaitForChild("HumanoidRootPart")
                game.Workspace.CurrentCamera.CFrame = CFrame.new(humanoidRootPart.Position + Vector3.new(0, 5, 0)) -- Adjust the offset as needed
            end
        else
            -- Exit Spy Mode (camera back to first-person view)
            game:GetService("Players").LocalPlayer.CameraMode = Enum.CameraMode.Default
        end
    end
})

-- Auto Punch Toggle
KillingTab:CreateToggle({
    Name = "Auto Punch",
    Callback = function(state)
        if state then
            -- Keep equipping and using the 'Punch' tool infinitely
            while true do
                local punchTool = player.Backpack:FindFirstChild("Punch")
                if punchTool then
                    -- Equip the 'Punch' tool
                    punchTool.Parent = player.Character

                    -- Use the punch tool infinitely
                    local humanoid = player.Character:FindFirstChild("Humanoid")
                    if humanoid then
                        humanoid:EquipTool(punchTool)
                        humanoid:UseTool(punchTool)
                    end
                end
                wait(0.1) -- Adjust for desired speed
            end
        end
    end
})

-- Keep the dropdown updated with the list of players
PlayerDropdown:SetOptions(function()
    local players = {}
    for _, p in ipairs(game.Players:GetPlayers()) do
        table.insert(players, p.Name)
    end
    return players
end)

