local Players = game:GetService("Players")
local ProximityPromptService = game:GetService("ProximityPromptService")
local LocalPlayer = Players.LocalPlayer

-- trạng thái bật tắt
local AutoPick = false

-- GUI
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)

local Button = Instance.new("TextButton")
Button.Size = UDim2.new(0, 140, 0, 45)
Button.Position = UDim2.new(0, 20, 0.5, -22)
Button.Text = "Auto Lụm: OFF"
Button.BackgroundColor3 = Color3.fromRGB(180, 0, 0)
Button.TextColor3 = Color3.new(1,1,1)
Button.TextScaled = true
Button.Parent = ScreenGui

-- Toggle
Button.MouseButton1Click:Connect(function()
	AutoPick = not AutoPick
	if AutoPick then
		Button.Text = "Auto Lụm: ON"
		Button.BackgroundColor3 = Color3.fromRGB(0, 170, 0)
	else
		Button.Text = "Auto Lụm: OFF"
		Button.BackgroundColor3 = Color3.fromRGB(180, 0, 0)
	end
end)

-- Auto kích hoạt ProximityPrompt
ProximityPromptService.PromptShown:Connect(function(prompt)
	if AutoPick and prompt.ActionText == "Lụm" then
		task.wait(0.1)
		fireproximityprompt(prompt)
	end
end)
