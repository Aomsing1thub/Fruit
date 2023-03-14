local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("TITLE", "Synapse")
local Tab = Window:NewTab("Main")
local Section = Tab:NewSection("Section Name")

function Check()
    Level = tonumber(string.match(game.Players.LocalPlayer.PlayerGui.Stats.Main.Frame.StatsContainer.AverageLevel.Text,"%d+"))
    if Level >= 0 and Level < 15 then
        Name_Mon = "Bandit (Level 1)"
        CFrame_Wait = CFrame.new(-350.4381103515625, 351.5129089355469, 325.9688720703125)
    elseif Level >= 15 and Level < 30 then
        Name_Mon = "Bandit Leader (Level 15)"
        CFrame_Wait = CFrame.new(-369.7712097167969, 282.6755065917969, 554.2888793945312)
    elseif Level >= 30 and Level < 60 then
        Name_Mon = "Clown Pirate (Level 30)"
        CFrame_Wait = CFrame.new(-293.0843200683594, 250.24668884277344, -1447.1566162109375)
    elseif Level >= 60 and Level < 75 then
        Name_Mon = "Clown Leader (Level 60)"
        CFrame_Wait = CFrame.new(-368.898193359375, 229.9982452392578, -1552.44384765625)
    elseif Level >= 75 and Level < 90 then
        Name_Mon = "Caveman (Level 75)"
        CFrame_Wait = CFrame.new(255.96511840820312, 206.99850463867188, 2118.405029296875)
    elseif Level >= 90 and Level < 200 then
        Name_Mon = "Monkey (Level 90)"
        CFrame_Wait = CFrame.new(574.6945190429688, 365.9721374511719, 2391.791015625)
    -- elseif Level >= 120 and Level < 200 then
        -- Name_Mon = "Gorilla (Level 120)"
        -- CFrame_Wait = CFrame.new(150.89414978027344, 358.5003662109375, 2518.702392578125)
    elseif Level >= 200 and Level < 275 then
        Name_Mon = "Snow Bandit (Level 200)"
        CFrame_Wait = CFrame.new(-2320.17236328125, 283.4620361328125, 2290.921630859375)
    elseif Level >= 275 and Level < 450 then
        Name_Mon = "Small Yeti (Level 275)"
        CFrame_Wait = CFrame.new(-2316.49169921875, 613.6150512695312, 2639.348388671875)
    -- elseif Level >= 350 and Level < 450 then
    --     Name_Mon = "Yeti (Level 350)"
    --     CFrame_Wait = CFrame.new(-2716.358154296875, 598.7385864257812, 3070.25537109375)
    elseif Level >= 450 and Level < 600 then
        Name_Mon = "Sand Bandit (Level 450)"
        CFrame_Wait = CFrame.new(-2237.26220703125, 589.4641723632812, -3608.683837890625)
    elseif Level >= 600 and Level < 800 then
        Name_Mon = "Pharaoh Guard (Level 600)"
        CFrame_Wait = CFrame.new(-2943.594482421875, 745.7305908203125, -4513.64990234375)
    elseif Level >= 800 and Level < 1000 then
        Name_Mon = "Anubis the Bone Keeper (Level 800)"
        CFrame_Wait = CFrame.new(-2928.767333984375, 710.3206787109375, -4834.81396484375)
    elseif Level >= 1000 and Level < 1100 then
        Name_Mon = "Sky Bandit (Level 1000)"
        CFrame_Wait = CFrame.new(2891.716064453125, 1889.7041015625, -5228.427734375)
    elseif Level >= 1100 and Level < 1200 then
        Name_Mon = "High-Level Sky Bandit (Level 1100)"
        CFrame_Wait = CFrame.new(3335.843017578125, 1994.8367919921875, -5381.94091796875)
    elseif Level >= 1200 then
        Name_Mon = "Sky Leader (Level 1200)"
        CFrame_Wait = CFrame.new(2989.11962890625, 1929.1815185546875, -5449.62841796875)
    end
end

Section:NewToggle("Auto", "ToggleInfo", function(state)
Auto_Farm = state
    if not Auto_Farm then
        repeat wait()
        if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ") then
            game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ"):Destroy()
        end
        until not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ")
    end
end)

spawn(function()
while wait() do
if Auto_Farm then
pcall(function()
    Check()
    
    if tostring(game.Players.LocalPlayer.PlayerGui.Quests.Main.Position) == "{0, 0}, {0, 0}" and string.find(game.Players.LocalPlayer.PlayerGui.Quests.Main.Handler.QuestObject.Text,"(Level "..string.match(Name_Mon,"%d+")..")") then
        spawn(function()
            stop = true
            for i,v in pairs(game:GetService("Workspace").Mobs:GetChildren()) do -- GetDescendants
                if v.Name == Name_Mon then
                    if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid").Health > 0 then
                        if i >= 1 then
                            stop = false
                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0,10,0)
                            wait(.3)
                        end
                    end
                end
            end
            if stop then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame_Wait
            end
        end)
        
        spawn(function()
            game:GetService("ReplicatedStorage").Remotes.Mouse1Combat:FireServer("Combat")

            for i,v in pairs(game:GetService("Workspace").Mobs:GetChildren()) do -- GetDescendants
                if v.Name == Name_Mon then
                    game:GetService("ReplicatedStorage").Remotes.M1sDamage:FireServer("Combat",v)
                end
            end
        end)
        spawn(function()
            game:GetService("ReplicatedStorage").Remotes.Mouse1Combat:FireServer("Katana",1)

            for i,v in pairs(game:GetService("Workspace").Mobs:GetChildren()) do -- GetDescendants
                if v.Name == Name_Mon then
                    game:GetService("ReplicatedStorage").Remotes.M1sDamage:FireServer("Katana",v)
                end
            end
        end)
        spawn(function()
            if not game.Players.LocalPlayer.Character:FindFirstChild("Combat") then
                game.Players.LocalPlayer.Character.Humanoid:EquipTool(game.Players.LocalPlayer.Backpack:FindFirstChild("Combat"))
            end
            if not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ") then
                local Noclip = Instance.new("BodyVelocity")
                Noclip.Name = "GGEZ"
                Noclip.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
                Noclip.MaxForce = Vector3.new(100000,100000,100000)
                Noclip.Velocity = Vector3.new(0,0,0)
            end
        end)
    else
        game:GetService("ReplicatedStorage").Remotes.QuestRemote:FireServer("GetQuest",Name_Mon)
        repeat wait()
        until tostring(game.Players.LocalPlayer.PlayerGui.Quests.Main.Position) == "{0, 0}, {0, 0}"
    end
end)
end
end
end)

Section:NewKeybind("KeybindText", "KeybindInfo", Enum.KeyCode.RightControl, function() -- Key OPEN/CLOSE
	Library:ToggleUI()
end)
