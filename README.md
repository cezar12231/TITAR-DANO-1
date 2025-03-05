-- Configuração inicial
local players = game:GetService("Players")
local localPlayer = players.LocalPlayer

-- Função para criar linhas coloridas
local function createESPLine(target)
    local line = Drawing.new("Line")
    line.Color = Color3.new(math.random(), math.random(), math.random()) -- Linhas coloridas aleatórias
    line.Thickness = 2
    line.Transparency = 1

    -- Atualizando a linha
    game:GetService("RunService").RenderStepped:Connect(function()
        if target and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
            local targetPos = target.Character.HumanoidRootPart.Position
            local camera = workspace.CurrentCamera
            local screenPos, onScreen = camera:WorldToViewportPoint(targetPos)

            if onScreen then
                line.From = Vector2.new(camera.ViewportSize.X / 2, camera.ViewportSize.Y) -- Posição inicial (base da tela)
                line.To = Vector2.new(screenPos.X, screenPos.Y) -- Posição do jogador na tela
                line.Visible = true
            else
                line.Visible = false
            end
        else
            line.Visible = false
        end
    end)
end

-- Adicionando ESP para outros jogadores
for _, player in pairs(players:GetPlayers()) do
    if player ~= localPlayer then
        createESPLine(player)
    end
end

-- Atualizando o ESP quando novos jogadores entram
players.PlayerAdded:Connect(function(newPlayer)
    createESPLine(newPlayer)
end)
