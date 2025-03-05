-- Criação do GUI
local screenGui = Instance.new("ScreenGui")
local button = Instance.new("TextButton")

-- Configurando o ScreenGui
screenGui.Name = "RemoveFallDamageGui"
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Configurando o botão
button.Name = "RemoveFallDamageButton"
button.Parent = screenGui
button.BackgroundColor3 = Color3.new(0.5, 0.5, 0.5)
button.Size = UDim2.new(0, 200, 0, 50)
button.Position = UDim2.new(0.5, -100, 0.5, -25)
button.Text = "Remover Dano de Queda"

-- Função para desativar o dano de queda
local function removeFallDamage()
    local player = game.Players.LocalPlayer
    player.CharacterAdded:Connect(function(character)
        character:WaitForChild("Humanoid").StateChanged:Connect(function(_, newState)
            if newState == Enum.HumanoidStateType.Freefall then
                character.Humanoid:ChangeState(Enum.HumanoidStateType.Physics)
            end
        end)
    end)
end

-- Conectando o botão à função
button.MouseButton1Click:Connect(removeFallDamage)

