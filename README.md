-- Configurações
local usarClick = true -- true = com click (M1), false = só skills

-- Função para verificar se tem ataque M1
function frutaTemM1()
    local humanoid = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
    if not humanoid then return false end
    local tool = humanoid:FindFirstChildOfClass("Tool")
    if not tool then return false end
    return tool:FindFirstChild("RemoteFunction") ~= nil or tool:FindFirstChild("RemoteEvent") ~= nil
end

-- Função de ataque com clique (M1)
function usarM1()
    local tool = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool")
    if tool then
        pcall(function()
            tool:Activate()
        end)
    end
end

-- Função para usar habilidades da fruta
function usarSkills()
    local vim = game:GetService("VirtualInputManager")
    for _, key in ipairs({"Z", "X", "C", "V", "F"}) do
        vim:SendKeyEvent(true, key, false, game)
        wait(0.2)
        vim:SendKeyEvent(false, key, false, game)
        wait(1.2)
    end
end

-- Loop de farm
spawn(function()
    while task.wait(0.5) do
        pcall(function()
            if frutaTemM1() and usarClick then
                usarM1()
            else
                usarSkills()
            end
        end)
    end
end)
