local Players = game:GetService("Players")

-- Simula que todo jogador tem qualquer Gamepass do seu jogo
Players.PlayerAdded:Connect(function(player)
    -- Cria atributos no jogador para sinalizar acesso completo
    player:SetAttribute("HasAllGamepasses", true)

    -- Se quiser usar nomes específicos de Gamepasses, adicione abaixo:
    local gamepassNames = {
        "Premium",
        "VIP",
        "Admin",
        "HorsePack",
        "VehiclePack",
        "Weapons",
        "Flying",
        "MusicPlayer"
    }

    for _, name in ipairs(gamepassNames) do
        player:SetAttribute("HasGamepass_" .. name, true)
    end
end)
# dsadas
