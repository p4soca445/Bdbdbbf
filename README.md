-- Criar o tornado
local tornado = Instance.new("Part")
tornado.Shape = Enum.PartType.Ball
tornado.Size = Vector3.new(50, 50, 50)  -- Tamanho do tornado
tornado.Position = Vector3.new(0, 50, 0)  -- Posição inicial do tornado
tornado.Anchored = true
tornado.CanCollide = false
tornado.Material = Enum.Material.SmoothPlastic
tornado.Color = Color3.fromRGB(100, 100, 255)
tornado.Parent = workspace

-- Efeitos visuais para o tornado
local tornadoEffect = Instance.new("ParticleEmitter")
tornadoEffect.Parent = tornado
tornadoEffect.Texture = "rbxassetid://1234567890"  -- ID de textura do efeito visual do tornado
tornadoEffect.Size = NumberSequence.new(10, 30)
tornadoEffect.Lifetime = NumberRange.new(3, 5)
tornadoEffect.Rate = 100
tornadoEffect.Speed = NumberRange.new(10, 20)

-- Função para puxar outros jogadores para o centro do tornado
game:GetService("RunService").Heartbeat:Connect(function()
    for _, object in ipairs(workspace:GetChildren()) do
        -- Verifica se o objeto é um modelo com um humanoide
        if object:IsA("Model") and object:FindFirstChildOfClass("Humanoid") then
            local humanoidRootPart = object:FindFirstChild("HumanoidRootPart")
            local humanoid = object:FindFirstChildOfClass("Humanoid")
            
            -- Ignora o jogador que executou o script
            if humanoidRootPart and humanoid and object.Parent ~= game.Players.LocalPlayer.Parent then
                -- Puxa os jogadores para o tornado
                local direction = tornado.Position - humanoidRootPart.Position
                local force = direction.Unit * 100  -- Intensidade da atração
                humanoidRootPart.Velocity = humanoidRootPart.Velocity + force
            end
        end
    end
end)
