-- Criando a ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Criando o botão
local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 200, 0, 50)
button.Position = UDim2.new(0.5, -100, 0.1, 0)
button.Text = "Desativar Dano de Queda"
button.Parent = screenGui

-- Variável de controle
danoDeQuedaAtivo = true

-- Função para ativar/desativar o dano de queda
button.MouseButton1Click:Connect(function()
    local humanoid = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
    if humanoid then
        if danoDeQuedaAtivo then
            humanoid:SetStateEnabled(Enum.HumanoidStateType.Freefall, false)
            humanoid:SetStateEnabled(Enum.HumanoidStateType.FallingDown, false)
            button.Text = "Ativar Dano de Queda"
        else
            humanoid:SetStateEnabled(Enum.HumanoidStateType.Freefall, true)
            humanoid:SetStateEnabled(Enum.HumanoidStateType.FallingDown, true)
            button.Text = "Desativar Dano de Queda"
        end
        danoDeQuedaAtivo = not danoDeQuedaAtivo
    end
end)
