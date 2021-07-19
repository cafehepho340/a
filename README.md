
local gui1 = Instance.new("ScreenGui")
local main = Instance.new("Frame")
local title = Instance.new("TextLabel")
local script1 = Instance.new("TextButton")
local UIGradient = Instance.new("UIGradient")
local script2 = Instance.new("TextButton")
local close = Instance.new("TextButton")

--Properties:

gui1.Name = "gui1"
gui1.Parent = game.CoreGui
gui1.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

main.Name = "main"
main.Parent = gui1
main.BackgroundColor3 = Color3.fromRGB(30, 255, 30)
main.Position = UDim2.new(0.218641132, 0, 0.453543305, 0)
main.Size = UDim2.new(0, 380, 0, 188)
main.Active = true
main.Draggable = true

title.Name = "title"
title.Parent = main
title.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
title.BackgroundTransparency = 1.000
title.Position = UDim2.new(0, 0, -0.00100221031, 0)
title.Size = UDim2.new(0, 379, 0, 54)
title.Font = Enum.Font.Michroma
title.Text = "ANIME FIGHTER -# cafehepho340"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.TextSize = 18.000

script1.Name = "script1"
script1.Parent = main
script1.BackgroundColor3 = Color3.fromRGB(163, 208, 212)
script1.Position = UDim2.new(0.025087487, 0, 0.502757967, 0)
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

script2.Name = "script2"
script2.Parent = main
script2.BackgroundColor3 = Color3.fromRGB(163, 208, 212)
script2.Position = UDim2.new(0.541191876, 0, 0.502757967, 0)
script2.Size = UDim2.new(0, 168, 0, 42)
script2.Font = Enum.Font.RobotoMono
script2.Text = "ANIME FIGHTER 2"
script2.TextColor3 = Color3.fromRGB(0, 0, 0)
script2.TextSize = 14.000
script2.TextStrokeTransparency = 0.780
script2.MouseButton1Down:connect(function()
	local library = loadstring(game:HttpGet(('https://raw.githubusercontent.com/Maxgat5/UiLib/main/lua')))()
	local w = library:CreateWindow("Anime Fighters Simulator")
	local b = w:CreateFolder("AutoFarm")
	local e = w:CreateFolder("Mix")
	local u = w:CreateFolder("Credits")
	SelectedEnemy = "Frieza1"
	Enemies = {}
	for i,v in pairs(game:GetService("Workspace").Worlds:GetDescendants()) do
		if v.Name == "Enemies" and v.ClassName == "Folder" then
			for i,v1 in pairs(v:GetChildren()) do
				if not table.find(Enemies,v1.Name) then
					table.insert(Enemies,v1.Name)
				end
			end
		end
	end

	function ClosestPart()
		local dist = math.huge
		local target = nil
		for i,v in pairs(game:GetService("Workspace").Worlds:GetDescendants()) do
			if v.ClassName == "Humanoid" then
				if v.Parent.Name == SelectedEnemy then
					if v.Parent:FindFirstChild("HumanoidRootPart") then
						local magnitude = (v.Parent.HumanoidRootPart.Position - game:GetService("Players").LocalPlayer.Character.Head.Position).magnitude
						if magnitude < dist then
							dist = magnitude
							target = v.Parent.HumanoidRootPart
						end
					end
				end
			end
		end
		return target
	end

	b:Toggle("AutoKillEnemies",function(bool)
		shared.toggle = bool
		AutoKillEnemies = bool
	end)

	b:Dropdown("Select Mob",Enemies,true,function(mob)
		SelectedEnemy = mob
	end)

	b:Toggle("AutoClickDamage",function(bool)
		shared.toggle = bool
		AutoClickDamage = bool
	end)

	b:Toggle("AutoCollectCoins",function(bool)
		shared.toggle = bool
		AutoCollectCoins = bool
	end)

	e:Toggle("AntiAfk",function(bool)
		shared.toggle = bool
		AntiAfk = bool
	end)

	--Credits
	u:Button("maxgat5#8395",function()
		setclipboard("maxgat5#8395")
	end)

	u:Button("Discord Server",function()
		setclipboard("https://discord.gg/K4txdRSVfq")
	end)

	game:GetService('RunService').Stepped:connect(function()
		spawn(function()
			if AutoClickDamage == true then
				game:GetService("ReplicatedStorage").Remote.ClickerDamage:FireServer()
			end
		end)
	end)

	while wait() do
		spawn(function()
			if AutoCollectCoins == true then
				for i,v in pairs(game:GetService("Workspace").Effects:GetDescendants()) do
					if v.Name == "Base" then
						v.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame + Vector3.new(0,0,0)
					end
				end
			end
		end)

		spawn(function()
			if AutoKillEnemies == true then
				for i,v in pairs(workspace.Pets:GetDescendants()) do
					if v.Name == "Owner" then
						if v.Value == game.Players.LocalPlayer then
							if v.Parent.Attacking.Value == nil then
								game:GetService("Players").LocalPlayer.CameraMaxZoomDistance = 0
								local tweenInfo = TweenInfo.new(
									0
								)
								local t = game.TweenService:Create(game.Players.LocalPlayer.Character.PrimaryPart, tweenInfo, {CFrame = CFrame.new(
									ClosestPart().CFrame.Position + Vector3.new(0,0,0)
									)})
								game.Players.LocalPlayer.Character.PrimaryPart.Anchored = true 
								t:Play()
								wait(0)
								mouse1press() wait() mouse1release()
							else
								game.Players.LocalPlayer.Character.PrimaryPart.Anchored = false
								game:GetService("Players").LocalPlayer.CameraMaxZoomDistance = 128
							end
						end
					end
				end
			else
				game:GetService("Players").LocalPlayer.CameraMaxZoomDistance = 128
			end
		end)

		spawn(function()
			if AntiAfk == true then
				local bb=game:service'VirtualUser'
				bb:CaptureController()
				bb:ClickButton2(Vector2.new())
			end
		end)
	end
end)


close.Name = "close"
close.Parent = main
close.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
close.BackgroundTransparency = 1.000
close.Position = UDim2.new(0.899999976, 0, 0.00531914877, 0)
close.Size = UDim2.new(0, 38, 0, 32)
close.Font = Enum.Font.TitilliumWeb
close.Text = "X"
close.TextColor3 = Color3.fromRGB(255, 255, 255)
close.TextSize = 41.000

-- Scripts:

local function ILYDFR_fake_script() -- close.LocalScript 
	local script = Instance.new('LocalScript', close)

	local Frame = script.Parent.Parent
	
	script.Parent.MouseButton1Click:Connect(function()
		Frame.Visible = false
	end)
end
coroutine.wrap(ILYDFR_fake_script)()
