-- Sang Jet Jet Hub

local player = game.Players.LocalPlayer
local VirtualUser = game:GetService("VirtualUser")
local RunService = game:GetService("RunService")
local UIS = game:GetService("UserInputService")

local treo = false

-- GUI
local gui = Instance.new("ScreenGui")
gui.Parent = game.CoreGui
gui.Name = "SangJetJet"

local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0,180,0,90)
frame.Position = UDim2.new(0.5,-90,0.8,0)
frame.BackgroundColor3 = Color3.fromRGB(0,0,0)
frame.BorderSizePixel = 0

local corner = Instance.new("UICorner", frame)
corner.CornerRadius = UDim.new(0,20)

-- TITLE
local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1,0,0.3,0)
title.BackgroundTransparency = 1
title.Text = "Sang Jet Jet"
title.TextColor3 = Color3.fromRGB(255,255,255)
title.Font = Enum.Font.GothamBold
title.TextScaled = true

-- FPS
local fpsLabel = Instance.new("TextLabel", frame)
fpsLabel.Size = UDim2.new(1,0,0.25,0)
fpsLabel.Position = UDim2.new(0,0,0.3,0)
fpsLabel.BackgroundTransparency = 1
fpsLabel.Text = "FPS: ..."
fpsLabel.TextColor3 = Color3.fromRGB(0,255,0)
fpsLabel.Font = Enum.Font.Gotham
fpsLabel.TextScaled = true

-- BUTTON
local button = Instance.new("TextButton", frame)
button.Size = UDim2.new(1,-20,0.35,0)
button.Position = UDim2.new(0,10,0.6,0)
button.BackgroundColor3 = Color3.fromRGB(25,25,25)
button.Text = "Treo: OFF"
button.TextColor3 = Color3.new(1,1,1)
button.Font = Enum.Font.GothamBold
button.TextScaled = true
button.BorderSizePixel = 0

local corner2 = Instance.new("UICorner", button)
corner2.CornerRadius = UDim.new(1,0)

-- Toggle
button.MouseButton1Click:Connect(function()
	treo = not treo
	
	if treo then
		button.Text = "Treo: ON"
	else
		button.Text = "Treo: OFF"
	end
end)

-- Anti AFK
player.Idled:Connect(function()
	if treo then
		VirtualUser:Button2Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
		task.wait(1)
		VirtualUser:Button2Up(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
	end
end)

-- FPS Counter
local last = tick()
local frames = 0

RunService.RenderStepped:Connect(function()
	frames += 1
	if tick() - last >= 1 then
		fpsLabel.Text = "FPS: "..frames
		frames = 0
		last = tick()
	end
end)

-- DRAG MENU
local dragging
local dragInput
local dragStart
local startPos

local function update(input)
	local delta = input.Position - dragStart
	frame.Position = UDim2.new(
		startPos.X.Scale,
		startPos.X.Offset + delta.X,
		startPos.Y.Scale,
		startPos.Y.Offset + delta.Y
	)
end

frame.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
		dragging = true
		dragStart = input.Position
		startPos = frame.Position
		
		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				dragging = false
			end
		end)
	end
end)

frame.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
		dragInput = input
	end
end)

UIS.InputChanged:Connect(function(input)
	if input == dragInput and dragging then
		update(input)
	end
end)
