local ScreenGui = Instance.new("ScreenGui")
local main = Instance.new("Frame")
local title = Instance.new("TextLabel")
local script1 = Instance.new("TextButton")
local UIGradient = Instance.new("UIGradient")

--Properties:

ScreenGui.Parent = game.CoreGui
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

main.Name = "main"
main.Parent = ScreenGui
main.BackgroundColor3 = Color3.fromRGB(30, 255, 30)
main.Position = UDim2.new(0.218641117, 0, 0.453543305, 0)
main.Size = UDim2.new(0, 351, 0, 187)
main.Active = true
main.Draggable = true

title.Name = "title"
title.Parent = main
title.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
title.BackgroundTransparency = 1.000
title.Position = UDim2.new(-0.000732099172, 0, -0.00100216083, 0)
title.Size = UDim2.new(0, 351, 0, 33)
title.Font = Enum.Font.Ubuntu
title.Text = "GUI Menu "
title.TextColor3 = Color3.fromRGB(0, 0, 0)
title.TextSize = 14.000

script1.Name = "script1"
script1.Parent = main
script1.BackgroundColor3 = Color3.fromRGB(163, 208, 212)
script1.Position = UDim2.new(0.258030951, 0, 0.385110915, 0)
script1.Size = UDim2.new(0, 168, 0, 42)
script1.Font = Enum.Font.RobotoMono
script1.Text = "ANIME FIGHTER 1"
script1.TextColor3 = Color3.fromRGB(0, 0, 0)
script1.TextSize = 14.000
script1.TextStrokeTransparency = 0.780
script1.MouseButton1Down:connect(function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/JRL-lav/Scripts/main/anime%20fighter"))()
end)

UIGradient.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(89, 12, 255)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 255, 255))}
UIGradient.Parent = main
