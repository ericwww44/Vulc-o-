if identifyexecutor and identifyexecutor():lower() == "delta" then
    local function getDragon()
        for _, obj in pairs(workspace:GetDescendants()) do
            if obj:IsA("Tool") and obj.Name:lower():find("dragon") then
                return obj
            end
        end
        return nil
    end

    local function tpTo(position)
        local char = game.Players.LocalPlayer.Character
        if char and char:FindFirstChild("HumanoidRootPart") then
            char:MoveTo(position)
            repeat task.wait() until (char.HumanoidRootPart.Position - position).Magnitude < 5
        end
    end

    local function storeFruit()
        local args = {
            [1] = "StoreFruit",
            [2] = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool")
        }
        game:GetService("ReplicatedStorage").Remotes.Fruit:FireServer(unpack(args))
    end

    local dragon = getDragon()

    if dragon then
        local path = {
            Vector3.new(-120, 20, 340), -- Ilha 1
            Vector3.new(-80, 28, 370),  -- Ilha 2
            Vector3.new(-40, 35, 400),  -- Ilha 3
            dragon.Handle.Position      -- Bloco de fogo com Dragon
        }

        for _, pos in ipairs(path) do
            tpTo(pos)
            task.wait(0.5)
        end

        task.wait(0.5)
        firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart, dragon.Handle, 0)
        task.wait(0.5)
        storeFruit()

        -- Trocar de servidor (opcional)
        -- loadstring(game:HttpGet("https://pastebin.com/raw/1gtVMUz3"))() -- exemplo
    else
        warn("❌ Dragon não encontrada.")
    end
else
    warn("Este script funciona apenas no executor Delta.")
end# Vulc-o-
