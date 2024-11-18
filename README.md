-- Referências
local player = game.Players.LocalPlayer
local button = script.Parent:WaitForChild("AutoClickButton")  -- Referência ao botão
local clickDetectorObject = game.Workspace:WaitForChild("BotaoClicker")  -- Nome do objeto de clique
local intervaloDeClique = 1  -- Intervalo entre os cliques automáticos (em segundos)
local cliqueAtivo = false  -- Se os cliques automáticos estão ativados

-- Função para ativar/desativar cliques automáticos
local function alternarCliqueAutomatico()
    cliqueAtivo = not cliqueAtivo  -- Alterna entre ativado/desativado
    
    if cliqueAtivo then
        -- Mudar texto do botão
        button.Text = "Desativar Clique Automático"
        -- Começar o loop de cliques automáticos
        while cliqueAtivo do
            wait(intervaloDeClique)
            
            -- Verifica se o objeto de clique ainda existe
            if clickDetectorObject and clickDetectorObject:FindFirstChild("ClickDetector") then
                -- Simula um clique no objeto
                clickDetectorObject.ClickDetector:FireClickDetector(player)
            end
        end
    else
        -- Mudar texto do botão
        button.Text = "Ativar Clique Automático"
    end
end

-- Conectar o evento de clique no botão
button.MouseButton1Click:Connect(alternarCliqueAutomatico)

-- Referências
local player = game.Players.LocalPlayer
local button = script.Parent:WaitForChild("AutoRespawnButton")  -- Referência ao botão
local autoRespawnAtivo = false  -- Se o renascimento automático está ativado

-- Função para alternar o renascimento automático
local function alternarRenascimentoAutomatico()
    autoRespawnAtivo = not autoRespawnAtivo  -- Alterna entre ativado/desativado
    
    if autoRespawnAtivo then
        -- Muda o texto do botão para indicar que o renascimento automático está ativado
        button.Text = "Desativar Renascimento Automático"
        
        -- Ativa o renascimento automático
        player.CharacterAdded:Connect(function(character)
            -- Conecta ao evento de morte do personagem
            character:WaitForChild("Humanoid").Died:Connect(function()
                -- Quando o jogador morre, aguarda um tempo e renasce
                wait(3)  -- Espera 3 segundos antes de renascer
                player:LoadCharacter()  -- Renasce o jogador
            end)
        end)
        
    else
        -- Muda o texto do botão para indicar que o renascimento automático está desativado
        button.Text = "Ativar Renascimento Automático"
    end
end

-- Conectar o evento de clique no botão
button.MouseButton1Click:Connect(alternarRenascimentoAutomatico)
