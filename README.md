-- Script Test 
local ESP = {}
ESP.TeamCheck = true

-- Função para desenhar caixas - substituir pela função gráfica do seu jogo
function ESP:DrawBox(player, color)
    -- Exemplo: printa to console (substituir com desenho real na tela)
    print("Desenhando caixa para "..player.name.." na cor RGB("..color.r..","..color.g..","..color.b..")")
end

-- Checa se player é inimigo
function ESP:IsEnemy(player, localPlayer)
    if not self.TeamCheck then return true end
    return player.team ~= localPlayer.team
end

-- Atualiza ESP com lista de players
function ESP:Update(localPlayer, players)
    for _, player in ipairs(players) do
        if player ~= localPlayer then
            if self:IsEnemy(player, localPlayer) then
                self:DrawBox(player, {r=255,g=0,b=0}) -- vermelho para inimigos
            else
                self:DrawBox(player, {r=0,g=255,b=0}) -- verde para aliados
            end
        end
    end
end

-- Alterna o team check
function ESP:ToggleTeamCheck()
    self.TeamCheck = not self.TeamCheck
    print("Team check "..(self.TeamCheck and "ativado" or "desativado"))
end

-- Exemplo de uso:
local localPlayer = {name = "JogadorLocal", team = "Azul"}
local players = {
    {name = "Inimigo1", team = "Vermelho"},
    {name = "Aliado1", team = "Azul"},
}

ESP:Update(localPlayer, players)  -- Inicial: desenha com team check ativado
ESP:ToggleTeamCheck()             -- Desativa a checagem de time
ESP:Update(localPlayer, players)  -- Atualiza novamente com team check desativado
