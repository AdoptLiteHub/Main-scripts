--Head Of Script
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/AhmadV99/Main/refs/heads/main/Library/V5.lua"))()

--Script Window
local Window = V5.CreateWindow({
    Name = "Complete Window", 
    Visible = false
})

--Minimize Whole Gui Button
local MinimizeButton = V5.CreateButton({
    Parent = Window,
    Image = "rbxassetid://YOUR_IMAGE_ID",  
    Size = UDim2.new(0, 30, 0, 30),
    Callback = function()
        Window.Visible = false
    end
})

--tab creation 
local Tab = V5.CreateTab({
    Parent = Window,
    Name = "My Tab", 
    Content = function()

    --Label
        local SectionLabel = V5.CreateLabel({
            Parent = Tab,
            Text = "Section 1: Introduction",
            Size = UDim2.new(0, 300, 0, 30),
            TextSize = 18,
            TextBold = true
        })
        
--Paragraph
        local Paragraph = V5.CreateLabel({
            Parent = Tab,
            Text = "This is the first section where you can explain your topic or introduce the content.",
            Size = UDim2.new(0, 300, 0, 100),
            TextSize = 14,
            TextWrapped = true
        })

--Button
        local Button = V5.CreateButton({
            Parent = Tab,
            Text = "Click Me",
            Size = UDim2.new(0, 200, 0, 40),
            Callback = function()
                print("Button clicked!")
            end
        })

--Toggle
        local Toggle = V5.CreateToggle({
            Parent = Tab,
            Text = "Enable Feature",
            Size = UDim2.new(0, 200, 0, 40),
            Callback = function(state)
                print("Toggle state: " .. tostring(state))
            end
        })

--Slider
        local Slider = V5.CreateSlider({
            Parent = Tab,
            Text = "Adjust Value",
            Min = 0,
            Max = 100,
            Size = UDim2.new(0, 200, 0, 40),
            Callback = function(value)
                print("Slider value: " .. value)
            end
        })

--Dropdown
        local Dropdown = V5.CreateDropdown({
            Parent = Tab,
            Text = "Select Option",
            Options = {"Option 1", "Option 2", "Option 3"},
            Size = UDim2.new(0, 200, 0, 40),
            Callback = function(selectedOption)
                print("Dropdown selected: " .. selectedOption)
            end
        })
    end
})
