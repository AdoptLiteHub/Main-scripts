local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/AhmadV99/Main/main/Library/V3.lua"))()

local Window = Library:MakeWindow({
    Title = "Lite Hub testing " .. Version,
    SaveFolder = ""
});Window:AddMinimizeButton({
    Button = {Image = "rbxassetid://86093303748141"},
    Corner = {CornerRadius = UDim.new(0, 5)}
})

local Home = Window:MakeTab({"Home", "scan-face"})

local function Toggle(Tab, Name, Desc, Default)
  local Ver = Tab:AddToggle({
    Name = Name,Description = Desc or "",Default = Default,
    Callback = function(Value)
      SpeedHubX[Name] = Value
    end})
    return Ver
end
local function Dropdown(Tab, Name, Desc, Option, Default)
  local Ver = Tab:AddDropdown({
    Name = Name,Description = Desc or "",Options = Option,Default = Default,
    Callback = function(Value)
      SpeedHubX[Name] = Value
    end})
    return Ver
end
local function Silder(Tab, Name, Min, Max, Default)
  local Ver = Tab:AddSlider({
    Name = Name,Min = Min,Max = Max,Default = Default,
    Callback = function(Value)
      SpeedHubX[Name] = Value
    end})
    return Ver
end

Home:AddSection({"Local Player"})
Silder(Home, "Set WalkSpeed", 0, 100000, 1000)
Silder(Home, "Set JumpPower", 0, 100000, 1000)
Toggle(Home, "Enable WalkSpeed", "This Can Set Walk Speed!", false)
Toggle(Home, "Enable JumpPower", "This Can Set JumpPower!", false)
Toggle(Home, "No Clip", "", false)
Toggle(Home, "Infinits Jump Ping", "", false)

