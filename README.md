-- Configurações
local areaDeAtaque = workspace:FindFirstChild("AreaDeCombate") -- Certifique-se de que a área exista no Workspace
local danoPorAtaque = 10 -- Quantidade de dano causado por ataque
local intervaloAtaque = 2 -- Intervalo entre ataques em segundos

-- Função para atacar NPCs próximos
local function atacarNPCs(jogador)
    for _, objeto in pairs(areaDeAtaque:GetChildren()) do
        if objeto:IsA("Model") and objeto:FindFirstChild("Humanoid") and objeto:FindFirstChild("HumanoidRootPart") then
            local humanoid = objeto.Humanoid
            local npcPosicao = objeto.HumanoidRootPart.Position
            local jogadorPosicao = jogador.Character.HumanoidRootPart.Position
            local distancia = (jogadorPosicao - npcPosicao).Magnitude

            if distancia <= 20 then -- Verifica se o NPC está em um raio de 20 unidades
                humanoid:TakeDamage(danoPorAtaque)
                print("Atacando NPC: " .. objeto.Name .. " com " .. danoPorAtaque .. " de dano.")
            end
        end
    end
end

-- Ciclo de ataques automáticos
local jogador = game.Players.LocalPlayer -- Obtém o jogador local

while true do
    wait(intervaloAtaque)
    if jogador and jogador.Character and jogador.Character:FindFirstChild("HumanoidRootPart") then
        atacarNPCs(jogador)
    end
end
