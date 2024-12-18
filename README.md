-- Script para criar uma habilidade especial no Blox Fruits

-- Variáveis iniciais
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local cooldown = false  -- Para garantir que a habilidade não será usada em cooldown

-- Função que executa a habilidade especial
function habilidadeEspecial()
    if cooldown then
        print("Habilidade em cooldown!")
        return
    end

    -- Ativar habilidade: por exemplo, criar uma explosão de luz
    local explosion = Instance.new("Part")  -- Cria uma nova parte no jogo
    explosion.Size = Vector3.new(10, 10, 10)  -- Tamanho da explosão
    explosion.Shape = Enum.PartType.Ball  -- Forma esférica
    explosion.Position = character.HumanoidRootPart.Position + Vector3.new(0, 5, 0)  -- Posiciona acima do personagem
    explosion.Anchored = true  -- A explosão não vai cair
    explosion.Material = Enum.Material.Neon  -- Material de neon para efeito visual
    explosion.Color = Color3.fromRGB(255, 0, 0)  -- Cor vermelha (explosão)
    explosion.Parent = workspace  -- Coloca a explosão no mundo

    -- Adiciona uma animação visual para a habilidade (efeito de luz)
    local light = Instance.new("PointLight", explosion)
    light.Color = Color3.fromRGB(255, 255, 255)  -- Luz branca
    light.Range = 20  -- Alcance da luz
    light.Brightness = 5  -- Brilho da luz

    -- Coloca um cooldown de 5 segundos para a habilidade
    cooldown = true
    wait(5)  -- Espera 5 segundos
    cooldown = false  -- Libera o uso da habilidade novamente

    -- Destroi a explosão depois de 1 segundo
    wait(1)
    explosion:Destroy()
end

-- Detectar quando a tecla "Q" for pressionada para usar a habilidade
game:GetService("UserInputService").InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end  -- Ignora se o input já foi processado por outra função
    if input.KeyCode == Enum.KeyCode.Q then  -- Verifica se a tecla pressionada foi "Q"
        habilidadeEspecial()  -- Chama a função da habilidade especial
    end
end)
