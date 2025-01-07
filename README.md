local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/AhmadV99/Main/main/Library/V3.lua"))()

local Window = Library:MakeWindow({
    Title = "Lite Hub testing " .. Version,
    SaveFolder = ""
})

Window:AddMinimizeButton({
    Button = {Image = "rbxassetid://86093303748141"},
    Corner = {CornerRadius = UDim.new(0, 5)}
})

local Home = Window:MakeTab({"Home", "scan-face"})

local function Toggle(Tab, Name, Desc, Default)
    local Ver = Tab:AddToggle({
        Name = Name, Description = Desc or "", Default = Default,
        Callback = function(Value)
            SpeedHubX[Name] = Value
        end
    })
    return Ver
end

local function Dropdown(Tab, Name, Desc, Options, Default)
    local Ver = Tab:AddDropdown({
        Name = Name, Description = Desc or "", Options = Options, Default = Default,
        Callback = function(Value)
            SpeedHubX[Name] = Value
        end
    })
    return Ver
end

local function Slider(Tab, Name, Min, Max, Default)
    local Ver = Tab:AddSlider({
        Name = Name, Min = Min, Max = Max, Default = Default,
        Callback = function(Value)
            SpeedHubX[Name] = Value
        end
    })
    return Ver
end

Home:AddSection({"Local Player"})
Slider(Home, "Set WalkSpeed", 0, 100000, 1000)
Slider(Home, "Set JumpPower", 0, 100000, 1000)
Toggle(Home, "Enable WalkSpeed", "This Can Set Walk Speed!", false)
Toggle(Home, "Enable JumpPower", "This Can Set JumpPower!", false)
Toggle(Home, "No Clip", "", false)
Toggle(Home, "Infinite Jump Ping", "", false)

local Kill = Window:MakeTab({"Kill", "rbxassetid://16279627995"})

local autoKillToggle = Toggle(Kill, "Auto Kill", "", false)

Kill:AddSection({"Target Player"})
local playerList = {}  -- This will hold player names
for _, player in pairs(game.Players:GetPlayers()) do
    table.insert(playerList, player.Name)
end

local selectedPlayerDropdown = Dropdown(Kill, "Select Player", "", playerList, "")

local killPlayerToggle = Toggle(Kill, "Kill Player", "", false)
local spyToggle = Toggle(Kill, "Spy", "", false)

Kill:AddSection({"Punching"})
local autoPunchToggle = Toggle(Kill, "Auto Punch", "", false)
local autoPunchNoAnimToggle = Toggle(Kill, "Auto Punch (No Animation)", "", false)

-- Function to set the hitboxes of another player's HumanoidRootPart to your right and left hands
local function setHitboxes(targetPlayer)
    local character = targetPlayer.Character
    if character then
        local hrp = character:FindFirstChild("HumanoidRootPart")
        if hrp then
            -- Get the right and left hands of the local player
            local rightHand = game.Players.LocalPlayer.Character:FindFirstChild("RightHand")
            local leftHand = game.Players.LocalPlayer.Character:FindFirstChild("LeftHand")
            
            if rightHand and leftHand then
                -- Create invisible hitboxes
                local function createInvisibleHitbox(position)
                    local hitbox = Instance.new("Part")
                    hitbox.Name = "Hitbox"
                    hitbox.Size = Vector3.new(2, 2, 2)  -- Set desired hitbox size
                    hitbox.Transparency = 1  -- Make the hitbox invisible
                    hitbox.CanCollide = true  -- Enable collision
                    hitbox.Anchored = true  -- Anchor it to the world
                    hitbox.Position = position  -- Position at the target location
                    hitbox.Parent = game.Workspace  -- Parent to the workspace (not the character)
                    return hitbox
                end

                -- Create and position the right and left hand hitboxes
                local rightHandHitbox = createInvisibleHitbox(rightHand.Position)
                local leftHandHitbox = createInvisibleHitbox(leftHand.Position)
                
                -- Optionally, you could attach the hitboxes to the HumanoidRootPart if needed, but this works well for positioning them
                rightHandHitbox.CFrame = rightHand.CFrame
                leftHandHitbox.CFrame = leftHand.CFrame
            end
        end
    end
end

-- Function to equip and use the "Punch" tool infinitely
local function equipPunchTool()
    local character = game.Players.LocalPlayer.Character
    if not character then return end
    
    local punchTool = character:FindFirstChild("Punch")
    if punchTool then
        -- Equip and use the Punch tool infinitely
        while true do
            if not punchTool.Parent then
                -- Reequip if the tool is not in the player's hand
                local backpack = game.Players.LocalPlayer.Backpack
                punchTool.Parent = backpack
            end
            -- Use the Punch tool (simulate punching)
            game:GetService("ReplicatedStorage").PunchEvent:FireServer()  -- Adjust the event name if necessary
            wait(0.1)
        end
    end
end

-- Auto Kill feature: Equip and use Punch tool without animation, set hitboxes to the right and left hands of all other players
autoKillToggle.Callback = function(Value)
    if Value then
        equipPunchTool()
        -- Set hitboxes to the right and left hands of all other players
        for _, player in pairs(game.Players:GetPlayers()) do
            if player ~= game.Players.LocalPlayer then
                setHitboxes(player)
            end
        end
    end
end

-- Kill Target feature: Set the hitboxes to right and left hands of the selected player
killPlayerToggle.Callback = function(Value)
    if Value then
        local selectedPlayerName = selectedPlayerDropdown.Value
        local targetPlayer = game.Players:FindFirstChild(selectedPlayerName)
        if targetPlayer then
            equipPunchTool()
            -- Set the hitbox of the selected player's HumanoidRootPart
            setHitboxes(targetPlayer)
        end
    end
end

-- Spy feature: Move the camera to the selected player's viewpoint
spyToggle.Callback = function(Value)
    if Value then
        local selectedPlayerName = selectedPlayerDropdown.Value
        local targetPlayer = game.Players:FindFirstChild(selectedPlayerName)
        if targetPlayer then
            -- Change the camera to the selected player's camera
            local character = targetPlayer.Character
            if character and character:FindFirstChild("HumanoidRootPart") then
                game.Workspace.CurrentCamera.CameraSubject = character.Humanoid
                game.Workspace.CurrentCamera.CameraType = Enum.CameraType.Attach
            end
        end
    end
end

-- Auto Punch feature: Equip and use Punch tool with animation
autoPunchToggle.Callback = function(Value)
    if Value then
        equipPunchTool()  -- This function should be modified to include animation if required
    end
end

-- Auto Punch No Animation feature: Equip and use the "Auto Punch" tool without animation
autoPunchNoAnimToggle.Callback = function(Value)
    if Value then
        equipPunchTool()  -- This should be the version that does not include animation
    end
end

game.Players.PlayerAdded:Connect(function(player)
    -- Update the player list dropdown when a new player joins
    table.insert(playerList, player.Name)
    selectedPlayerDropdown:SetOptions(playerList)
end)

game.Players.PlayerRemoving:Connect(function(player)
    -- Update the player list dropdown when a player leaves
    for i, name in ipairs(playerList) do
        if name == player.Name then
            table.remove(playerList, i)
            break
        end
    end
    selectedPlayerDropdown:SetOptions(playerList)
end)
