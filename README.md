
        local library = loadstring(game:HttpGet("https://pastebin.com/raw/Abg3RkND", true))()

local window = library:AddWindow("Nova Hub | Paid Version V2", {
    main_color = Color3.fromRGB(0, 0, 0),
    min_size = Vector2.new(700, 550),
    can_resize = false,
})

local Main = window:AddTab("Main")

Main:AddLabel("Discord Server:")

Main:AddButton("Copy Link", function()
    setclipboard("https://discord.gg/KtZtC9g6")
end)

Main:AddLabel("Local Player")

local walkSpeedValue = 16
Main:AddTextBox("WalkSpeed", function(text)
    local speed = tonumber(text)
    if speed and speed >= 1 and speed <= 500 then
        walkSpeedValue = speed
    end
end)

local setSpeed = false
Main:AddSwitch("Set Speed", function(state)
    setSpeed = state
    while setSpeed do
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = walkSpeedValue
        task.wait(0.1)
    end
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
end)

local jumpPowerValue = 50
Main:AddTextBox("JumpPower", function(text)
    local jump = tonumber(text)
    if jump then
        jumpPowerValue = jump
    end
end)

local applyJumpPower = false
Main:AddSwitch("Apply JumpPower", function(state)
    applyJumpPower = state
    local humanoid = game.Players.LocalPlayer.Character.Humanoid
    humanoid.UseJumpPower = true
    humanoid.JumpPower = applyJumpPower and jumpPowerValue or 50
end)

local sizeValue = 1
Main:AddTextBox("Size", function(text)
    local size = tonumber(text)
    if size and size >= 1 and size <= 100 then
        sizeValue = size
    end
end)

local setSize = false
Main:AddSwitch("Set Sizes", function(state)
    setSize = state
    local char = game.Players.LocalPlayer.Character
    if char then
        local humanoid = char:FindFirstChildOfClass("Humanoid")
        if humanoid then
            for _, scale in pairs({"BodyDepthScale", "BodyHeightScale", "BodyWidthScale", "HeadScale"}) do
                local scaleInstance = humanoid:FindFirstChild(scale)
                if scaleInstance then
                    scaleInstance.Value = state and sizeValue or 1
                end
            end
        end
    end
end)

local AutoFarm = window:AddTab("Auto Farm")
AutoFarm:AddLabel("Area Farming (More Coming Soon)")

local folderJungleFarming = AutoFarm:AddFolder("Jungle Farming")

local autoJungleBench = false
folderJungleFarming:AddSwitch("Auto Jungle Bench", function(State)
    autoJungleBench = State
    if State then
        task.spawn(function()
            while autoJungleBench do
                game.Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-8629.88086, 64.8842468, 1855.03467))
                game:GetService("ReplicatedStorage").rEvents.machineInteractRemote:InvokeServer("useMachine", workspace.machinesFolder["Jungle Bench"].interactSeat)
                task.wait(0.1)
            end
        end)
    end
end)

local autoJungleBarLift = false
folderJungleFarming:AddSwitch("Auto Jungle Bar Lift", function(State)
    autoJungleBarLift = State
    if State then
        task.spawn(function()
            while autoJungleBarLift do
                game.Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-8678.05566, 14.5030098, 2089.25977))
                game:GetService("ReplicatedStorage").rEvents.machineInteractRemote:InvokeServer("useMachine", workspace.machinesFolder["Jungle Bar Lift"].interactSeat)
                task.wait(0.1)
            end
        end)
    end
end)

local autoJungleSquat = false
folderJungleFarming:AddSwitch("Auto Jungle Squat", function(State)
    autoJungleSquat = State
    if State then
        task.spawn(function()
            while autoJungleSquat do
                game.Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-8374.25586, 34.5933418, 2932.44995))
                game:GetService("ReplicatedStorage").rEvents.machineInteractRemote:InvokeServer("useMachine", workspace.machinesFolder["Jungle Squat"].interactSeat)
                task.wait(0.1)
            end
        end)
    end
end)

local folderMuscleKingFarming = AutoFarm:AddFolder("Muscle King Farming")

local autoMuscleKingLift = false
folderMuscleKingFarming:AddSwitch("Auto Muscle King Lift", function(State)
    autoMuscleKingLift = State
    if State then
        task.spawn(function()
            while autoMuscleKingLift do
                game.Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-8772.97266, 24.4272194, -5638.37402))
                game:GetService("ReplicatedStorage").rEvents.machineInteractRemote:InvokeServer("useMachine", workspace.machinesFolder["Muscle King Lift"].interactSeat)
                task.wait(0.1)
            end
        end)
    end
end)

local autoMuscleKingBoulder = false
folderMuscleKingFarming:AddSwitch("Auto Muscle King Boulder", function(State)
    autoMuscleKingBoulder = State
    if State then
        task.spawn(function()
            while autoMuscleKingBoulder do
                game.Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-8986.61621, 30.0510483, -5647.14404))
                game:GetService("ReplicatedStorage").rEvents.machineInteractRemote:InvokeServer("useMachine", workspace.machinesFolder["King Boulder"].interactSeat)
                task.wait(0.1)
            end
        end)
    end
end)

local folderLegendGymFarming = AutoFarm:AddFolder("Legend Gym Farming")

local autoLegendLift = false
folderLegendGymFarming:AddSwitch("Auto Legend Lift", function(State)
    autoLegendLift = State
    if State then
        task.spawn(function()
            while autoLegendLift do
                game.Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(4551.51514, 997.727234, -4018.90186))
                game:GetService("ReplicatedStorage").rEvents.machineInteractRemote:InvokeServer("useMachine", workspace.machinesFolder["Legends Lift"].interactSeat)
                task.wait(0.1)
            end
        end)
    end
end)

local autoLegendPress = false
folderLegendGymFarming:AddSwitch("Auto Legend Press", function(State)
    autoLegendPress = State
    if State then
        task.spawn(function()
            while autoLegendPress do
                game.Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(4100.08154, 1016.20416, -3800.4187))
                game:GetService("ReplicatedStorage").rEvents.machineInteractRemote:InvokeServer("useMachine", workspace.machinesFolder["Legends Press"].interactSeat)
                task.wait(0.1)
            end
        end)
    end
end)

local Rebirth = window:AddTab("Rebirth")

local autoRebirth = false
Rebirth:AddSwitch("Auto Rebirth (Infinitely)", function(bool)
    autoRebirth = bool

    while autoRebirth do
        game:GetService("ReplicatedStorage").rEvents.rebirthRemote:InvokeServer("rebirthRequest")
        wait(0.1)
    end
end)

local rebirthTarget = 0
Rebirth:AddTextBox("Rebirth Target", function(text)
    rebirthTarget = tonumber(text) or 0
end)

local rebirthingToTarget = false
Rebirth:AddSwitch("Rebirth Until Reach Target Amount", function(bool)
    rebirthingToTarget = bool

    while rebirthingToTarget do
        local player = game.Players.LocalPlayer
        local leaderstats = player:FindFirstChild("leaderstats")
        local rebirths = leaderstats and leaderstats:FindFirstChild("Rebirths")

        if rebirths and rebirths.Value >= rebirthTarget then
            rebirthingToTarget = false
            break
        end

        game:GetService("ReplicatedStorage").rEvents.rebirthRemote:InvokeServer("rebirthRequest")
        wait(0.1)
    end
end)

local Killer = window:AddTab("Killer")

Killer:AddSwitch("Auto Good Karma", function(bool)
    autoGoodKarma = bool

    if autoGoodKarma then
        spawn(function()
            while autoGoodKarma do
                local player = game.Players.LocalPlayer
                local playerChar = player.Character
                local rightHand = playerChar and playerChar:FindFirstChild("RightHand")
                local leftHand = playerChar and playerChar:FindFirstChild("LeftHand")

                if playerChar and rightHand and leftHand then
                    for _, target in ipairs(game.Players:GetPlayers()) do
                        if target ~= player then
                            local evilKarma = target:FindFirstChild("evilKarma")
                            local goodKarma = target:FindFirstChild("goodKarma")

                            if evilKarma and goodKarma and evilKarma:IsA("IntValue") and goodKarma:IsA("IntValue") and evilKarma.Value > goodKarma.Value then
                                local targetChar = target.Character
                                local rootPart = targetChar and targetChar:FindFirstChild("HumanoidRootPart")

                                if rootPart then
                                    firetouchinterest(rightHand, rootPart, 1)
                                    firetouchinterest(leftHand, rootPart, 1)
                                    firetouchinterest(rightHand, rootPart, 0)
                                    firetouchinterest(leftHand, rootPart, 0)
                                end
                            end
                        end
                    end
                end
                task.wait(0.1)
            end
        end)
    end
end)

Killer:AddSwitch("Auto Bad Karma", function(bool)
    autoBadKarma = bool

    if autoBadKarma then
        spawn(function()
            while autoBadKarma do
                local player = game.Players.LocalPlayer
                local playerChar = player.Character
                local rightHand = playerChar and playerChar:FindFirstChild("RightHand")
                local leftHand = playerChar and playerChar:FindFirstChild("LeftHand")

                if playerChar and rightHand and leftHand then
                    for _, target in ipairs(game.Players:GetPlayers()) do
                        if target ~= player then
                            local evilKarma = target:FindFirstChild("evilKarma")
                            local goodKarma = target:FindFirstChild("goodKarma")

                            if evilKarma and goodKarma and evilKarma:IsA("IntValue") and goodKarma:IsA("IntValue") and goodKarma.Value > evilKarma.Value then
                                local targetChar = target.Character
                                local rootPart = targetChar and targetChar:FindFirstChild("HumanoidRootPart")

                                if rootPart then
                                    firetouchinterest(rightHand, rootPart, 1)
                                    firetouchinterest(leftHand, rootPart, 1)
                                    firetouchinterest(rightHand, rootPart, 0)
                                    firetouchinterest(leftHand, rootPart, 0)
                                end
                            end
                        end
                    end
                end
                task.wait(0.1)
            end
        end)
    end
end)

Killer:AddLabel("Whitelisting")

local playerWhitelist = {}

Killer:AddTextBox("Whitelist", function(text)
    local targetPlayer = game.Players:FindFirstChild(text)
    if targetPlayer then
        playerWhitelist[targetPlayer.Name] = true
    end
end)

Killer:AddTextBox("UnWhitelist", function(text)
    local targetPlayer = game.Players:FindFirstChild(text)
    if targetPlayer then
        playerWhitelist[targetPlayer.Name] = nil
    end
end)

Killer:AddLabel("Auto Killing")

local autoKill = false
Killer:AddSwitch("Auto Kill", function(bool)
    autoKill = bool

    while autoKill do
        local player = game.Players.LocalPlayer

        for _, target in ipairs(game.Players:GetPlayers()) do
            if target ~= player and not playerWhitelist[target.Name] then
                local targetChar = target.Character
                local rootPart = targetChar and targetChar:FindFirstChild("HumanoidRootPart")

                if rootPart then
                    local rightHand = player.Character and player.Character:FindFirstChild("RightHand")
                    local leftHand = player.Character and player.Character:FindFirstChild("LeftHand")
                    
                    if rightHand and leftHand then
                        firetouchinterest(rightHand, rootPart, 1)
                        firetouchinterest(leftHand, rootPart, 1)
                        firetouchinterest(rightHand, rootPart, 0)
                        firetouchinterest(leftHand, rootPart, 0)
                    end
                end
            end
        end

        wait(0.1)
    end
end)

Killer:AddLabel("Targeting")

local targetPlayerName = nil

Killer:AddTextBox("Target Name", function(text)
    targetPlayerName = text
end)

local killTarget = false
Killer:AddSwitch("Kill Target", function(bool)
    killTarget = bool

    while killTarget do
        local player = game.Players.LocalPlayer
        local target = game.Players:FindFirstChild(targetPlayerName)

        if target and target ~= player then
            local targetChar = target.Character
            local rootPart = targetChar and targetChar:FindFirstChild("HumanoidRootPart")

            if rootPart then
                local rightHand = player.Character and player.Character:FindFirstChild("RightHand")
                local leftHand = player.Character and player.Character:FindFirstChild("LeftHand")

                if rightHand and leftHand then
                    firetouchinterest(rightHand, rootPart, 1)
                    firetouchinterest(leftHand, rootPart, 1)
                    firetouchinterest(rightHand, rootPart, 0)
                    firetouchinterest(leftHand, rootPart, 0)
                end
            end
        end

        wait(0.1)
    end
end)

local spying = false
Killer:AddSwitch("Spy Player", function(bool)
    spying = bool

    if not spying then
        local player = game.Players.LocalPlayer
        local camera = workspace.CurrentCamera
        camera.CameraSubject = player.Character and player.Character:FindFirstChild("Humanoid") or player
        return
    end

    while spying do
        local player = game.Players.LocalPlayer
        local target = game.Players:FindFirstChild(targetPlayerName)

        if target and target ~= player then
            local targetChar = target.Character
            local targetHumanoid = targetChar and targetChar:FindFirstChild("Humanoid")

            if targetHumanoid then
                local camera = workspace.CurrentCamera
                camera.CameraSubject = targetHumanoid
            end
        end

        wait(0.1)
    end
end)

Killer:AddLabel("Punching Tool")

local autoEquipPunch = false
Killer:AddSwitch("Auto Equip Punch", function(state)
    autoEquipPunch = state

    while autoEquipPunch do
        local player = game.Players.LocalPlayer
        local punchTool = player.Backpack:FindFirstChild("Punch")

        if punchTool then
            punchTool.Parent = player.Character
        end

        wait(0.1)
    end
end)

local autoPunchNoAnim = false
Killer:AddSwitch("Auto Punch [No Animation]", function(state)
    autoPunchNoAnim = state

    while autoPunchNoAnim do
        local player = game.Players.LocalPlayer
        local playerName = player.Name
        local punchTool = player.Backpack:FindFirstChild("Punch") or game.Workspace:FindFirstChild(playerName):FindFirstChild("Punch")

        if punchTool then
            if punchTool.Parent ~= game.Workspace:FindFirstChild(playerName) then
                punchTool.Parent = game.Workspace:FindFirstChild(playerName)
            end

            player.muscleEvent:FireServer("punch", "rightHand")
            player.muscleEvent:FireServer("punch", "leftHand")
        else
            warn("Punch tool not found")
            autoPunchNoAnim = false
        end

        wait(0.01)
    end
end)

local Crystal = window:AddTab("Crystal")

local selectedCrystal = "Galaxy Oracle Crystal"
local autoCrystalRunning = false

local dropdown = Crystal:AddDropdown("Select Crystal", function(text)
    selectedCrystal = text
end)

local crystalNames = {
    "Blue Crystal", "Green Crystal", "Frozen Crystal", "Mythical Crystal",
    "Inferno Crystal", "Legends Crystal", "Muscle Elite Crystal",
    "Galaxy Oracle Crystal", "Sky Eclipse Crystal", "Jungle Crystal"
}

for _, name in ipairs(crystalNames) do
    dropdown:Add(name)
end

local function autoOpenCrystal()
    while autoCrystalRunning do
        game:GetService("ReplicatedStorage"):WaitForChild("rEvents"):WaitForChild("openCrystalRemote"):InvokeServer("openCrystal", selectedCrystal)
        wait(0.1)
    end
end

local switch = Crystal:AddSwitch("Auto Crystal", function(state)
    autoCrystalRunning = state

    if autoCrystalRunning then
        task.spawn(autoOpenCrystal)
    end
end)

local OpThings = window:AddTab("Op Things")

OpThings:AddSwitch("Fast Rebirth", function(bool)
    fastRebirth = bool

    if fastRebirth then
        spawn(function()
            local a = game:GetService("ReplicatedStorage")
            local b = game:GetService("Players")
            local c = b.LocalPlayer

            local d = function(e)
                local f = c.petsFolder
                for g, h in pairs(f:GetChildren()) do
                    if h:IsA("Folder") then
                        for i, j in pairs(h:GetChildren()) do
                            a.rEvents.equipPetEvent:FireServer("unequipPet", j)
                        end
                    end
                end
                task.wait(.1)
            end

            local k = function(l)
                d()
                task.wait(.01)
                for m, n in pairs(c.petsFolder.Unique:GetChildren()) do
                    if n.Name == l then
                        a.rEvents.equipPetEvent:FireServer("equipPet", n)
                    end
                end
            end

            local o = function(p)
                local q = workspace.machinesFolder:FindFirstChild(p)
                if not q then
                    for r, s in pairs(workspace:GetChildren()) do
                        if s:IsA("Folder") and s.Name:find("machines") then
                            q = s:FindFirstChild(p)
                            if q then break end
                        end
                    end
                end
                return q
            end

            local t = function()
                local u = game:GetService("VirtualInputManager")
                u:SendKeyEvent(true, "E", false, game)
                task.wait(.1)
                u:SendKeyEvent(false, "E", false, game)
            end

            while fastRebirth do
                local v = c.leaderstats.Rebirths.Value
                local w = 10000 + (5000 * v)
                if c.ultimatesFolder:FindFirstChild("Golden Rebirth") then
                    local x = c.ultimatesFolder["Golden Rebirth"].Value
                    w = math.floor(w * (1 - (x * 0.1)))
                end

                d()
                task.wait(.1)
                k("Swift Samurai")

                while c.leaderstats.Strength.Value < w do
                    for y = 1, 10 do
                        c.muscleEvent:FireServer("rep")
                    end
                    task.wait()
                end

                d()
                task.wait(.1)
                k("Tribal Overlord")

                local z = o("Jungle Bar Lift")
                if z and z:FindFirstChild("interactSeat") then
                    c.Character.HumanoidRootPart.CFrame = z.interactSeat.CFrame * CFrame.new(0, 3, 0)
                    repeat
                        task.wait(.1)
                        t()
                    until c.Character.Humanoid.Sit
                end

                local A = c.leaderstats.Rebirths.Value
                repeat
                    a.rEvents.rebirthRemote:InvokeServer("rebirthRequest")
                    task.wait(.1)
                until c.leaderstats.Rebirths.Value > A

                task.wait()
            end
        end)
    end
end)

local switch = OpThings:AddSwitch("Fast Strength", function(Value)
    getgenv().isGrinding = Value

    if not Value then return end

    for _ = 1, 30 do
        task.spawn(function()
            while getgenv().isGrinding do
                game:GetService("Players").LocalPlayer.muscleEvent:FireServer("rep")
                task.wait(0.01)
            end
        end)
    end
end)

local switchHideFrame = OpThings:AddSwitch("Hide Frame", function(bool)
    for _, frameName in ipairs({"strengthFrame", "durabilityFrame", "agilityFrame"}) do
        local frame = game:GetService("ReplicatedStorage"):FindFirstChild(frameName)
        if frame and frame:IsA("GuiObject") then
            frame.Visible = not bool
        end
    end
end)

local Statistic = window:AddTab("Statistic")

Statistic:AddLabel("Tab Inspirated By Lurnai, Credit Goes To Lurnai/MCL Havoc")

Statistic:AddLabel("Stats:")  

local labels = {  
    RebirthsGainedLabel = Statistic:AddLabel("Rebirths Gained In 1 Minute: ..."),  
    RebirthsPerMinuteLabel = Statistic:AddLabel("Rebirths Per Minute: ..."),  
    RebirthsPerHourLabel = Statistic:AddLabel("Rebirths Per Hour: ..."),  
    RebirthsPerDayLabel = Statistic:AddLabel("Rebirths Per Day: ..."),  
    RebirthsPerWeekLabel = Statistic:AddLabel("Rebirths Per Week: ...")  
}  

local player = game:GetService("Players").LocalPlayer  
local leaderstats = player:FindFirstChild("leaderstats")  
local rebirthStat = leaderstats and leaderstats:FindFirstChild("Rebirths")  

local function abbreviateNumber(num)  
    if num >= 1e9 then  
        return string.format("%.2fB", num / 1e9)  
    elseif num >= 1e6 then  
        return string.format("%.2fM", num / 1e6)  
    elseif num >= 1e3 then  
        return string.format("%.2fK", num / 1e3)  
    else  
        return tostring(num)  
    end  
end  

local lastRebirthCount = rebirthStat and rebirthStat.Value or 0  

task.spawn(function()  
    while task.wait(60) do  
        local currentRebirthCount = rebirthStat and rebirthStat.Value or 0  
        local rebirthsGained = math.max(0, currentRebirthCount - lastRebirthCount)  
        lastRebirthCount = currentRebirthCount  

        labels.RebirthsGainedLabel.Text = "Rebirths Gained In 1 Minute: " .. abbreviateNumber(rebirthsGained)  
        labels.RebirthsPerMinuteLabel.Text = "Rebirths Per Minute: " .. abbreviateNumber(rebirthsGained)  
        labels.RebirthsPerHourLabel.Text = "Rebirths Per Hour: " .. abbreviateNumber(rebirthsGained * 60)  
        labels.RebirthsPerDayLabel.Text = "Rebirths Per Day: " .. abbreviateNumber(rebirthsGained * 1440)  
        labels.RebirthsPerWeekLabel.Text = "Rebirths Per Week: " .. abbreviateNumber(rebirthsGained * 10080)  
    end  
end)

local Stats = window:AddTab("Stats")

local function abbreviateNumber(value)
    if value >= 1e15 then
        return string.format("%.1fQa", value / 1e15)
    elseif value >= 1e12 then
        return string.format("%.1fT", value / 1e12)
    elseif value >= 1e9 then
        return string.format("%.1fB", value / 1e9)
    elseif value >= 1e6 then
        return string.format("%.1fM", value / 1e6)
    elseif value >= 1e3 then
        return string.format("%.1fK", value / 1e3)
    else
        return tostring(value)
    end
end

local labels = {
    TimeSpentLabel = Stats:AddLabel("Time spent in this server: 00:00"),
    StrengthGainedLabel = Stats:AddLabel("Amount of strength gained in this server: 0"),
    DurabilityGainedLabel = Stats:AddLabel("Amount of durability gained in this server: 0"),
    AgilityGainedLabel = Stats:AddLabel("Amount of agility gained in this server: 0"),
    KillsGainedLabel = Stats:AddLabel("Amount of kills gained in this server: 0"),
    EvilKarmaGainedLabel = Stats:AddLabel("Amount of Evil Karma gained in this server: 0"),
    GoodKarmaGainedLabel = Stats:AddLabel("Amount of Good Karma gained in this server: 0")
}

local function createMyLabels()
    local player = game.Players.LocalPlayer
    if not player then return end

    local leaderstats = player:WaitForChild("leaderstats")
    if not leaderstats then return end

    local strengthStat = leaderstats:WaitForChild("Strength")
    local durabilityStat = player:WaitForChild("Durability")
    local agilityStat = player:WaitForChild("Agility")
    local killsStat = leaderstats:WaitForChild("Kills")
    local evilKarmaStat = player:WaitForChild("evilKarma")
    local goodKarmaStat = player:WaitForChild("goodKarma")

    local initialStrength = strengthStat.Value or 0
    local initialDurability = durabilityStat.Value or 0
    local initialAgility = agilityStat.Value or 0
    local initialKills = killsStat.Value or 0
    local initialEvilKarma = evilKarmaStat.Value or 0
    local initialGoodKarma = goodKarmaStat.Value or 0

    local startTime = tick()

    local function updateLabels()
        local strengthGained = strengthStat.Value - initialStrength
        local durabilityGained = durabilityStat.Value - initialDurability
        local agilityGained = agilityStat.Value - initialAgility
        local killsGained = killsStat.Value - initialKills
        local evilKarmaGained = evilKarmaStat.Value - initialEvilKarma
        local goodKarmaGained = goodKarmaStat.Value - initialGoodKarma

        labels.StrengthGainedLabel.Text = "Amount of strength gained in this server: " .. abbreviateNumber(strengthGained)
        labels.DurabilityGainedLabel.Text = "Amount of durability gained in this server: " .. abbreviateNumber(durabilityGained)
        labels.AgilityGainedLabel.Text = "Amount of agility gained in this server: " .. abbreviateNumber(agilityGained)
        labels.KillsGainedLabel.Text = "Amount of kills gained in this server: " .. abbreviateNumber(killsGained)
        labels.EvilKarmaGainedLabel.Text = "Amount of Evil Karma gained in this server: " .. abbreviateNumber(evilKarmaGained)
        labels.GoodKarmaGainedLabel.Text = "Amount of Good Karma gained in this server: " .. abbreviateNumber(goodKarmaGained)
    end

    local function updateTimeSpent()
        local timeSpent = tick() - startTime
        local minutes = math.floor(timeSpent / 60)
        local seconds = math.floor(timeSpent % 60)
        labels.TimeSpentLabel.Text = string.format("Time spent in this server: %02d:%02d", minutes, seconds)
    end

    strengthStat.Changed:Connect(updateLabels)
    durabilityStat.Changed:Connect(updateLabels)
    agilityStat.Changed:Connect(updateLabels)
    killsStat.Changed:Connect(updateLabels)
    evilKarmaStat.Changed:Connect(updateLabels)
    goodKarmaStat.Changed:Connect(updateLabels)

    game:GetService("RunService").Heartbeat:Connect(updateTimeSpent)

    updateLabels()
end

createMyLabels()

local ViewStats = window:AddTab("View Stats")

local targetPlayer = nil
local initialStats = {}

local textbox = ViewStats:AddTextBox("Target Name", function(text)
    local player = game.Players:FindFirstChild(text)
    if player then
        targetPlayer = player
        storeInitialStats()
    else
        targetPlayer = nil
        resetTargetStats()
    end
end)

local labels = {
    ViewStats = ViewStats:AddLabel("View Stats:"),
    StrengthLabel = ViewStats:AddLabel("Strength: 0"),
    DurabilityLabel = ViewStats:AddLabel("Durability: 0"),
    AgilityLabel = ViewStats:AddLabel("Agility: 0"),
    RebirthsLabel = ViewStats:AddLabel("Rebirths: 0"),
    KillsLabel = ViewStats:AddLabel("Kills: 0"),
    EvilKarmaLabel = ViewStats:AddLabel("Evil Karma: 0"),
    GoodKarmaLabel = ViewStats:AddLabel("Good Karma: 0"),
    StatsGainedLabel = ViewStats:AddLabel("Stats Gained In Server:"),
    StrengthGainedLabel = ViewStats:AddLabel("Strength: 0"),
    DurabilityGainedLabel = ViewStats:AddLabel("Durability: 0"),
    AgilityGainedLabel = ViewStats:AddLabel("Agility: 0"),
    RebirthsGainedLabel = ViewStats:AddLabel("Rebirths: 0"),
    KillsGainedLabel = ViewStats:AddLabel("Kills: 0"),
    EvilKarmaGainedLabel = ViewStats:AddLabel("Evil Karma: 0"),
    GoodKarmaGainedLabel = ViewStats:AddLabel("Good Karma: 0"),
}

local function storeInitialStats()
    if not targetPlayer then return end

    local leaderstats = targetPlayer:FindFirstChild("leaderstats")
    initialStats = {
        Strength = leaderstats and leaderstats:FindFirstChild("Strength") and leaderstats.Strength.Value or 0,
        Durability = targetPlayer:FindFirstChild("Durability") and targetPlayer.Durability.Value or 0,
        Agility = targetPlayer:FindFirstChild("Agility") and targetPlayer.Agility.Value or 0,
        Rebirths = leaderstats and leaderstats:FindFirstChild("Rebirths") and leaderstats.Rebirths.Value or 0,
        Kills = leaderstats and leaderstats:FindFirstChild("Kills") and leaderstats.Kills.Value or 0,
        EvilKarma = targetPlayer:FindFirstChild("evilKarma") and targetPlayer.evilKarma.Value or 0,
        GoodKarma = targetPlayer:FindFirstChild("goodKarma") and targetPlayer.goodKarma.Value or 0,
    }
end

local function updateTargetStats()
    if not targetPlayer then return end

    local leaderstats = targetPlayer:FindFirstChild("leaderstats")
    local goodKarma = targetPlayer:FindFirstChild("goodKarma")
    local evilKarma = targetPlayer:FindFirstChild("evilKarma")

    if leaderstats then
        labels.StrengthLabel.Text = "Strength: " .. abbreviateNumber(leaderstats:FindFirstChild("Strength") and leaderstats.Strength.Value or 0)
        labels.DurabilityLabel.Text = "Durability: " .. abbreviateNumber(targetPlayer:FindFirstChild("Durability") and targetPlayer.Durability.Value or 0)
        labels.AgilityLabel.Text = "Agility: " .. abbreviateNumber(targetPlayer:FindFirstChild("Agility") and targetPlayer.Agility.Value or 0)
        labels.RebirthsLabel.Text = "Rebirths: " .. abbreviateNumber(leaderstats:FindFirstChild("Rebirths") and leaderstats.Rebirths.Value or 0)
        labels.KillsLabel.Text = "Kills: " .. abbreviateNumber(leaderstats:FindFirstChild("Kills") and leaderstats.Kills.Value or 0)
    end

    labels.EvilKarmaLabel.Text = "Evil Karma: " .. abbreviateNumber(evilKarma and evilKarma.Value or 0)
    labels.GoodKarmaLabel.Text = "Good Karma: " .. abbreviateNumber(goodKarma and goodKarma.Value or 0)

    if initialStats then
        labels.StrengthGainedLabel.Text = "Strength: " .. abbreviateNumber((leaderstats and leaderstats:FindFirstChild("Strength") and leaderstats.Strength.Value or 0) - initialStats.Strength)
        labels.DurabilityGainedLabel.Text = "Durability: " .. abbreviateNumber((targetPlayer:FindFirstChild("Durability") and targetPlayer.Durability.Value or 0) - initialStats.Durability)
        labels.AgilityGainedLabel.Text = "Agility: " .. abbreviateNumber((targetPlayer:FindFirstChild("Agility") and targetPlayer.Agility.Value or 0) - initialStats.Agility)
        labels.RebirthsGainedLabel.Text = "Rebirths: " .. abbreviateNumber((leaderstats and leaderstats:FindFirstChild("Rebirths") and leaderstats.Rebirths.Value or 0) - initialStats.Rebirths)
        labels.KillsGainedLabel.Text = "Kills: " .. abbreviateNumber((leaderstats and leaderstats:FindFirstChild("Kills") and leaderstats.Kills.Value or 0) - initialStats.Kills)
        labels.EvilKarmaGainedLabel.Text = "Evil Karma: " .. abbreviateNumber((targetPlayer:FindFirstChild("evilKarma") and targetPlayer.evilKarma.Value or 0) - initialStats.EvilKarma)
        labels.GoodKarmaGainedLabel.Text = "Good Karma: " .. abbreviateNumber((targetPlayer:FindFirstChild("goodKarma") and targetPlayer.goodKarma.Value or 0) - initialStats.GoodKarma)
    end
end

local function resetTargetStats()
    labels.StrengthLabel.Text = "Strength: 0"
    labels.DurabilityLabel.Text = "Durability: 0"
    labels.AgilityLabel.Text = "Agility: 0"
    labels.RebirthsLabel.Text = "Rebirths: 0"
    labels.KillsLabel.Text = "Kills: 0"
    labels.EvilKarmaLabel.Text = "Evil Karma: 0"
    labels.GoodKarmaLabel.Text = "Good Karma: 0"
    labels.StrengthGainedLabel.Text = "Strength: 0"
    labels.DurabilityGainedLabel.Text = "Durability: 0"
    labels.AgilityGainedLabel.Text = "Agility: 0"
    labels.RebirthsGainedLabel.Text = "Rebirths: 0"
    labels.KillsGainedLabel.Text = "Kills: 0"
    labels.EvilKarmaGainedLabel.Text = "Evil Karma: 0"
    labels.GoodKarmaGainedLabel.Text = "Good Karma: 0"
end

task.spawn(function()
    while task.wait(0.1) do
        if targetPlayer then
            updateTargetStats()
        end
    end
end)


local Misc = window:AddTab("Misc")

local Teleport = Misc:AddFolder(Teleport)

Teleport :AddButton("Tiny Island", function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-31.8626194, 6.0588026, 2087.88672)
end)

Teleport :AddButton("Starter Island", function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(226.252472, 8.1526947, 219.366516)
end)

Teleport :AddButton("Legend Beach", function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-365.798309, 44.5082932, -501.618591)
end)

Teleport :AddButton("Frost Gym", function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-2933.47998, 29.6399612, -579.946045)
end)

Teleport :AddButton("Mythical Gym", function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(2659.50635, 21.6095238, 934.690613)
end)

Teleport :AddButton("Eternal Gym", function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-7176.19141, 45.394104, -1106.31421)
end)

Teleport :AddButton("Legend Gym", function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(4446.91699, 1004.46698, -3983.76074)
end)

Teleport :AddButton("Jungle Gym", function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-8137, 28, 2820)
end)

local folder = Misc:AddFolder("Brawl")

local godModeToggle = false
folder:AddSwitch("God Mode (Brawl)", function(State)
    godModeToggle = State
    if State then
        task.spawn(function()
            while godModeToggle do
                game:GetService("ReplicatedStorage").rEvents.brawlEvent:FireServer("joinBrawl")
                task.wait(0)
            end
        end)
    end
end)

local autoJoinToggle = false
folder:AddSwitch("Auto Join Brawl", function(State)
    autoJoinToggle = State
    if State then
        task.spawn(function()
            while autoJoinToggle do
                game:GetService("ReplicatedStorage").rEvents.brawlEvent:FireServer("joinBrawl")
                task.wait(2)
            end
        end)
    end
end)

local folder2 = Misc:AddFolder("Misc1")

folder2:AddButton("Destroy Ad Teleport", function()
    local part = workspace:FindFirstChild("RobloxForwardPortals")
    if part then
        part:Destroy()
    end
end)

folder2:AddButton("Anti Kick", function()
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

    local bb = game:GetService("VirtualUser")
    game.Players.LocalPlayer.Idled:Connect(function()
        bb:CaptureController()
        bb:ClickButton2(Vector2.new())
        ab.Text = "Roblox tried kicking you, but I won't let them!"
        wait(2)
        ab.Text = "Status: Active"
    end)
end)

folder2:AddSwitch("Unable Trade", function(State)
    if State then
        game:GetService("ReplicatedStorage").rEvents.tradingEvent:FireServer("disableTrading")
    else
        game:GetService("ReplicatedStorage").rEvents.tradingEvent:FireServer("enableTrading")
    end
end)

folder2:AddSwitch("Hide Pets", function(State)
    if State then
        game:GetService("ReplicatedStorage").rEvents.showPetsEvent:FireServer("hidePets")
    else
        game:GetService("ReplicatedStorage").rEvents.showPetsEvent:FireServer("showPets")
    end
end)

local switch = Misc:AddSwitch("Lock Position", function(Value)
    if Value then
        local currentPos = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
        getgenv().posLock = game:GetService("RunService").Heartbeat:Connect(function()
            if game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = currentPos
            end
        end)
    else
        if getgenv().posLock then
            getgenv().posLock:Disconnect()
            getgenv().posLock = nil
        end
    end
end)

local switchGamepads = Misc:AddSwitch("Free Auto Lift Gamepass", function(Value)
    local gamepassFolder = game:GetService("ReplicatedStorage"):FindFirstChild("gamepassIds")
    local player = game:GetService("Players").LocalPlayer

    if not gamepassFolder or not player then return end

    if Value then
        for _, gamepass in pairs(gamepassFolder:GetChildren()) do
            if not player.ownedGamepasses:FindFirstChild(gamepass.Name) then
                local value = Instance.new("IntValue")
                value.Name = gamepass.Name
                value.Value = gamepass.Value
                value.Parent = player.ownedGamepasses
            end
        end
    else
        for _, gamepass in pairs(player.ownedGamepasses:GetChildren()) do
            gamepass:Destroy()
        end
    end
end)

local Credit = window:AddTab("Credit")

Credit:AddLabel("Script Made By Encrypted")
Credit:AddLabel("Nova Hub Paid Version , 1.7K Robux")
Credit:AddLabel("|")
Credit:AddLabel("Close Friends:")
Credit:AddLabel("D3Ath, Slayerson, CwmoKai, X3NO, MLR Taken, Havoc, Lucky, Aabis, Blackyy")
