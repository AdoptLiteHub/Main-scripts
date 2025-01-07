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

Killing:AddSwitch("Auto Kill", function(bool)
	 -- toggle_god_mode(bool)
end)

Killing:AddLabel("Target")


local dropdown = Killing:AddDropdown("Select Player", function(text)
	if text == "Mars" then  -- Code
		print("o")
	elseif text == "Earth" then
	print("k")
	elseif text == "Iridocyclitis" then
	print("Weeeee")
	end
end)
local mars = dropdown:Add("Mars")  -- Options 
local earth = dropdown:Add("Earth")
local not_a_planet = dropdown:Add("Iridocyclitis")

Killing:AddSwitch("Auto Kill Target", function(bool)
	 -- toggle_god_mode(bool)
end

Killing:AddSwitch("Spy Player", function(bool)
	 -- toggle_god_mode(bool)
end)

Killing:AddLabel("Punching")

Killing:AddSwitch("Auto Punch", function(bool)
	 -- toggle_god_mode(bool)
end)
