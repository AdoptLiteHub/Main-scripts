-- syn request because sigma
local req = http_request or request or (syn and syn.request)

-- Lite Hub webhook for the muscle legends version not the legends of speed lmao
local webhookUrl = "https://discord.com/api/webhooks/1328791750273142834/iqCXOsYI19_Um-0-qdZBogqKdIcQ_kpbhiW0F7XJduGMXzladO3YZ6tFw8rlcsHx1tad"

-- Roblox services
local HttpService = game:GetService("HttpService")
local Players = game:GetService("Players")
local MarketplaceService = game:GetService("MarketplaceService")
local UserInputService = game:GetService("UserInputService")

-- Local player information
local player = Players.LocalPlayer
local username = player.Name
local userId = player.UserId
local displayName = player.DisplayName
local deviceType = UserInputService.TouchEnabled and "Mobile" or "PC"

-- Detecting the executor
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
        return getexecutorname()
    elseif identifyexecutor then
        return identifyexecutor()
    else
        return "Unknown Executor"
    end
end

local executor = detectExecutor()

-- Webhook Body
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

-- Send data to webhook
local jsonData = HttpService:JSONEncode(body)
req({
    Url = webhookUrl,
    Method = 'POST',
    Headers = { ['Content-Type'] = 'application/json' },
    Body = jsonData
})

-- Library setup
local Library = loadstring(game:HttpGetAsync("https://github.com/ActualMasterOogway/Fluent-Renewed/releases/latest/download/Fluent.luau"))()
local SaveManager = loadstring(game:HttpGetAsync("https://raw.githubusercontent.com/ActualMasterOogway/Fluent-Renewed/master/Addons/SaveManager.luau"))()
local InterfaceManager = loadstring(game:HttpGetAsync("https://raw.githubusercontent.com/ActualMasterOogway/Fluent-Renewed/master/Addons/InterfaceManager.luau"))()

-- Create Window
local Window = Library:CreateWindow{
    Title = "Lite Hub Legends Of Speed",
    SubTitle = "by Actual Master Oogway",
    TabWidth = 160,
    Size = UDim2.fromOffset(830, 525),
    Resize = true,
    MinSize = Vector2.new(470, 380),
    Acrylic = true,
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.RightControl
}

-- Create Tabs
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
    Rebirth = Window:CreateTab{
        Title = "Rebirth",
        Icon = "" -- Icon is now empty
    },
    Teleport = Window:CreateTab{
        Title = "Teleport",
        Icon = "" -- Icon is now empty
    },
    Egg = Window:CreateTab{
        Title = "Egg",
        Icon = "" -- Icon is now empty
    }
}

-- Add Teleport Tab
local TeleportTab = Tabs.Teleport

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
local EggTab = Tabs.Egg

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
