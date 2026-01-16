-- SERVICES
local Players = game:GetService("Players")
local CollectionService = game:GetService("CollectionService")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

-- GUI
local button = script.Parent:WaitForChild("AutoFarmButton")

-- SETTINGS
local AUTO_FARM = false
local ATTACK_DISTANCE = 3
local TELE_OFFSET = CFrame.new(0, 0, -2)

-- AUTO ATTACK (bạn sửa chỗ này theo game)
local function attackNPC(npc)
    for _,v in pairs(npc:GetDescendants()) do
        if v:IsA("Humanoid") then
            v.Health = 0 -- ⚠️ Nếu game có anti-cheat thì cần remote
        end
    end
end

-- TÌM NPC GẦN NHẤT
local function getNearestNPC()
    local nearestNPC = nil
    local shortestDistance = math.huge

    for _,npc in pairs(CollectionService:GetTagged("NPC")) do
        if npc:FindFirstChild("HumanoidRootPart")
        and npc:FindFirstChild("Humanoid")
        and npc.Humanoid.Health > 0 then

            local distance = (humanoidRootPart.Position - npc.HumanoidRootPart.Position).Magnitude
            if distance < shortestDistance then
                shortestDistance = distance
                nearestNPC = npc
            end
        end
    end

    return nearestNPC
end

-- AUTO FARM LOOP
task.spawn(function()
    while task.wait(0.1) do
        if AUTO_FARM then
            local npc = getNearestNPC()
            if npc then
                humanoidRootPart.CFrame =
                    npc.HumanoidRootPart.CFrame * TELE_OFFSET

                task.wait(0.2)
                attackNPC(npc)
            end
        end
    end
end)

-- BUTTON TOGGLE
button.MouseButton1Click:Connect(function()
    AUTO_FARM = not AUTO_FARM
    button.Text = AUTO_FARM and "AUTO FARM : ON" or "AUTO FARM : OFF"
end)		Button.BackgroundColor3 = Color3.fromRGB(0, 170, 0)
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
