-- Required libraries
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/memejames/elerium-v2-ui-library//main/Library", true))()
local player = game.Players.LocalPlayer

-- Create the UI window
local Window = library:CreateWindow("Lite Hub") 

-- Create a tab called 'Killing'
local KillingTab = Window:CreateTab("Killing")

-- Auto Kill Toggle
local AutoKillToggle = KillingTab:CreateToggle({
    Name = "Auto Kill",
    Callback = function(state)
        if state then
            -- Start auto killing (punching without animation)
            while AutoKillToggle:GetState() do
                -- Equip the 'Punch' tool
                local punchTool = player.Backpack:FindFirstChild("Punch")
                if punchTool then
                    punchTool.Parent = player.Character
                    player.Character:FindFirstChild("RightHand").CFrame = player.Character:FindFirstChild("RightHand").CFrame
                    player.Character:FindFirstChild("LeftHand").CFrame = player.Character:FindFirstChild("LeftHand").CFrame
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
local KillTargetToggle = KillingTab:CreateToggle({
    Name = "Kill Target",
    Callback = function(state)
        if state then
            -- Start killing the selected target
            while KillTargetToggle:GetState() and currentTarget do
                -- Equip the 'Punch' tool again
                local punchTool = player.Backpack:FindFirstChild("Punch")
                if punchTool then
                    punchTool.Parent = player.Character
                    player.Character:FindFirstChild("RightHand").CFrame = currentTarget.Character.HumanoidRootPart.CFrame
                    player.Character:FindFirstChild("LeftHand").CFrame = currentTarget.Character.HumanoidRootPart.CFrame
                end
                wait(0.1) -- Adjust for desired speed
            end
        end
    end
})

-- Create a 'Spy' Toggle
local SpyToggle = KillingTab:CreateToggle({
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

-- Keep the dropdown updated with the list of players
PlayerDropdown:SetOptions(function()
    local players = {}
    for _, p in ipairs(game.Players:GetPlayers()) do
        table.insert(players, p.Name)
    end
    return players
end)

-- The above code should work under the assumption that the "Punch" tool exists
-- and players' characters are appropriately structured with the humanoidrootpart.
