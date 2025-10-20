# rrty4-- Auto Farm + Bring Mobs para Black Grimoire: Odyssey
local player = game.Players.LocalPlayer
local mobsFolder = workspace:WaitForChild("Mobs")

-- Função para trazer mobs até o jogador
function bringMobs()
    for _, mob in pairs(mobsFolder:GetChildren()) do
        if mob:FindFirstChild("HumanoidRootPart") then
            mob.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame + Vector3.new(0, 5, 0)
        end
    end
end

-- Função de ataque automático
function autoAttack()
    while true do
        for _, mob in pairs(mobsFolder:GetChildren()) do
            if mob:FindFirstChild("Humanoid") and mob.Humanoid.Health > 0 then
                game:GetService("ReplicatedStorage").AttackEvent:FireServer(mob)
            end
        end
        wait(0.5)
    end
end

-- Loop principal
spawn(function()
    while true do
        bringMobs()
        wait(2)
    end
end)

spawn(autoAttack)
