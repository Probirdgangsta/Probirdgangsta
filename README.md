--made by Probird
-- init
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/GreenDeno/Venyx-UI-Library/main/source.lua"))()
local bird = library.new("Bird Hub")

-- themes
local themes = {
Background = Color3.fromRGB(24, 24, 24),
Glow = Color3.fromRGB(0, 0, 0),
Accent = Color3.fromRGB(10, 10, 10),
LightContrast = Color3.fromRGB(20, 20, 20),
DarkContrast = Color3.fromRGB(14, 14, 14),  
TextColor = Color3.fromRGB(255, 255, 255)
}

-- first page
local page = bird:addPage("Client", 5012544693)
local section1 = page:addSection("Section 1")
local section2 = page:addSection("Section 2")

section1:addToggle("Toggle", nil, function(value)
print("Toggled", value)
end)
section1:addButton("Destroy all Doors", function()
game.workspace.Doors:Destroy()
end)
section1:addButton("Get all guns", function()
local args = {
    [1] = workspace.Prison_ITEMS.giver:FindFirstChild("Remington 870").ITEMPICKUP
}

workspace.Remote.ItemHandler:InvokeServer(unpack(args))

local args = {
    [1] = workspace.Prison_ITEMS.giver:FindFirstChild("M9").ITEMPICKUP
}

workspace.Remote.ItemHandler:InvokeServer(unpack(args))

local args = {
    [1] = workspace.Prison_ITEMS.giver:FindFirstChild("AK-47").ITEMPICKUP
}

workspace.Remote.ItemHandler:InvokeServer(unpack(args))

end)
section1:addTextbox("Notification", "Default", function(value, focusLost)
print("Input", value)

if focusLost then
bird:Notify("Title", value)
end
end)

section2:addKeybind("Toggle Keybind", Enum.KeyCode.One, function()
print("Activated Keybind")
bird:toggle()
end, function()
print("Changed Keybind")
end)
section2:addSlider("Walkspeed", 0, 16, 300, function(value)
game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
end)
section2:addSlider("JumpPower", 0, 0, 300, function(value)
game.Players.LocalPlayer.Character.Humanoid.JumpPower = value
end)
section2:addDropdown("Teams", {"Inmate", "World", "Hello World", "Word", 1, 2, 3}, function(text)

end)

-- second page
local theme = bird:addPage("Theme", 5012544693)
local colors = theme:addSection("Colors")

for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
colors:addColorPicker(theme, color, function(color3)
    bird:setTheme(theme, color3)
end)
end

-- load
bird:SelectPage(bird.pages[1], true)
