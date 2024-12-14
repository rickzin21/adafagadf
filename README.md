--Abaixo estará nossa Lib da Ui

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()

local function getNearestPlayer()
    local nearestPlayer = nil
    local shortestDistance = math.huge

    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            local distance = (player.Character.HumanoidRootPart.Position - LocalPlayer.Character.HumanoidRootPart.Position).magnitude
            if distance < shortestDistance then
                nearestPlayer = player
                shortestDistance = distance
            end
        end
    end

    return nearestPlayer
end

RunService.RenderStepped:Connect(function()
    local targetPlayer = getNearestPlayer()
    if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
        local targetPosition = targetPlayer.Character.HumanoidRootPart.Position
        local screenPoint = workspace.CurrentCamera:WorldToScreenPoint(targetPosition)
        Mouse.X = screenPoint.X
        Mouse.Y = screenPoint.Y
    end
end)
