local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("TITLE", "Synapse")
local Tab = Window:NewTab("Main")
local Section = Tab:NewSection("Section Name")

farm = true
function Delete(v,Name)
    if v.Head:FindFirstChild(Name) then
        v.Head:FindFirstChild(Name):Destroy()
    end
end

function GodMode()
    for i,v in pairs (game:GetService("Workspace").Players:GetChildren()) do
        if v.Name == game.Players.LocalPlayer.Name then
            Delete(v,"Mesh")
            Delete(v,"MobGUI")
            Delete(v,"face")
            if v:FindFirstChild("Pants") then
                v.Pants:Destroy()
            end
            if v:FindFirstChild("Shirt") then
                v.Shirt:Destroy()
            end
            for i,v in pairs (game:GetService("Workspace").Players[game.Players.LocalPlayer.Name].Race:GetChildren()) do
                v:Destroy()
            end
            for i,v in pairs (game:GetService("Workspace").Players[game.Players.LocalPlayer.Name]:GetChildren()) do
                if v:IsA "Accessory" then
                    v:Destroy()
                end
            end
        end
    end
end

function hit_sword(Weapon)
    spawn(function()
        if not game.Players.LocalPlayer.Character:FindFirstChild(Weapon) then
            game.Players.LocalPlayer.Character.Humanoid:EquipTool(game.Players.LocalPlayer.Backpack:FindFirstChild(Weapon))
        end
        game:GetService("ReplicatedStorage").Remotes.Mouse1Combat:FireServer(Weapon)
        for i,v in pairs(game:GetService("Workspace").Mobs:GetChildren()) do -- GetDescendants
            if v.Name == Name_Mon then
                game:GetService("ReplicatedStorage").Remotes.M1sDamage:FireServer(Weapon,v)
            end
        end
    end)
end

function hit_combat(Combat)
    spawn(function()
        if not game.Players.LocalPlayer.Character:FindFirstChild(Combat) then
            game.Players.LocalPlayer.Character.Humanoid:EquipTool(game.Players.LocalPlayer.Backpack:FindFirstChild(Combat))
        end
        game:GetService("ReplicatedStorage").Remotes.Mouse1Combat:FireServer(Combat)
        for i,v in pairs(game:GetService("Workspace").Mobs:GetChildren()) do -- GetDescendants
            if v.Name == Name_Mon then
                game:GetService("ReplicatedStorage").Remotes.M1sDamage:FireServer(Combat,v)
            end
        end
    end)
end

function find(NameMon)
    if Workspace.Mobs:FindFirstChild(NameMon) then
        return true
    end
end

function findHealth(NameMon)
    if Workspace.Mobs:FindFirstChild(NameMon):FindFirstChild("Humanoid").Health > 0 then
        return true
    end
end

function Check()
    Level = tonumber(string.match(game.Players.LocalPlayer.PlayerGui.Stats.Main.Frame.StatsContainer.AverageLevel.Text,"%d+"))
    if Level >= 0 and Level < 15 and farm then
        step = 1
    elseif Level >= 15 and Level < 30 and farm then
        Name = "Bandit Leader (Level 15)"
        if find(Name) and findHealth(Name) and farm then
            step = 2
        else
            step = 1
        end
    elseif Level >= 30 and Level < 60 and farm then
        step = 3
    elseif Level >= 60 and Level < 75 and farm then
        Name = "Clown Leader (Level 60)"
        if find(Name) and findHealth(Name) and farm then
            step = 4
        else
            step = 3
        end
    elseif Level >= 75 and Level < 90 and farm then
        step = 5
    elseif Level >= 90 and Level < 120 and farm then
        step = 6
    elseif Level >= 120 and Level < 200 and farm then
        Name = "Gorilla (Level 120)"
        if find(Name) and findHealth(Name) and farm then
            step = 7
        else
            step = 6
        end
    elseif Level >= 200 and Level < 275 and farm then
        step = 8
    elseif Level >= 275 and Level < 450 and farm then
        step = 9
    elseif Level >= 350 and Level < 450 and farm then
        step = 10
    elseif Level >= 450 and Level < 600 and farm then
        step = 11
    elseif Level >= 600 and Level < 800 and farm then
        step = 12
    elseif Level >= 800 and Level < 1000 and farm then
        step = 13
    elseif Level >= 1000 and Level < 1100 and farm then
        step = 14
    elseif Level >= 1100 and Level < 1200 and farm then
        step = 15
    elseif Level >= 1200 and farm then
        Name = "Sky Leader (Level 1200)"
        if find(Name) and findHealth(Name) then
            step = 16
        else
            step = 15
        end
    end
    
    if step == 1 then
        Boss = false
        Name_Mon = "Bandit (Level 1)"
        CFrame_Wait = CFrame.new(-350.4381103515625, 351.5129089355469, 325.9688720703125)
    elseif step == 2 then
        Boss = true
        Name_Mon = "Bandit Leader (Level 15)"
        CFrame_Wait = CFrame.new(-369.7712097167969, 282.6755065917969, 554.2888793945312)
    elseif step == 3 then
        Boss = false
        Name_Mon = "Clown Pirate (Level 30)"
        CFrame_Wait = CFrame.new(-293.0843200683594, 250.24668884277344, -1447.1566162109375)
    elseif step == 4 then
        Boss = true
        Name_Mon = "Clown Leader (Level 60)"
        CFrame_Wait = CFrame.new(-368.898193359375, 229.9982452392578, -1552.44384765625)
    elseif step == 5 then
        Boss = false
        Name_Mon = "Caveman (Level 75)"
        CFrame_Wait = CFrame.new(255.96511840820312, 206.99850463867188, 2118.405029296875)
    elseif step == 6 then
        Boss = false
        Name_Mon = "Monkey (Level 90)"
        CFrame_Wait = CFrame.new(574.6945190429688, 365.9721374511719, 2391.791015625)
    elseif step == 7 then
        Boss = true
        Name_Mon = "Gorilla (Level 120)"
        CFrame_Wait = CFrame.new(150.89414978027344, 358.5003662109375, 2518.702392578125)
    elseif step == 8 then
        Boss = false
        Name_Mon = "Snow Bandit (Level 200)"
        CFrame_Wait = CFrame.new(-2320.17236328125, 283.4620361328125, 2290.921630859375)
    elseif step == 9 then
        Boss = false
        Name_Mon = "Small Yeti (Level 275)"
        CFrame_Wait = CFrame.new(-2316.49169921875, 613.6150512695312, 2639.348388671875)
    elseif step == 10 then
        Boss = false
        Name_Mon = "Yeti (Level 350)"
        CFrame_Wait = CFrame.new(-2716.358154296875, 598.7385864257812, 3070.25537109375)
    elseif step == 11 then
        Boss = false
        Name_Mon = "Sand Bandit (Level 450)"
        CFrame_Wait = CFrame.new(-2237.26220703125, 589.4641723632812, -3608.683837890625)
    elseif step == 12 then
        Boss = false
        Name_Mon = "Pharaoh Guard (Level 600)"
        CFrame_Wait = CFrame.new(-2943.594482421875, 745.7305908203125, -4513.64990234375)
    elseif step == 13 then
        Boss = false
        Name_Mon = "Anubis the Bone Keeper (Level 800)"
        CFrame_Wait = CFrame.new(-2928.767333984375, 710.3206787109375, -4834.81396484375)
    elseif step == 14 then
        Boss = false
        Name_Mon = "Sky Bandit (Level 1000)"
        CFrame_Wait = CFrame.new(2891.716064453125, 1889.7041015625, -5228.427734375)
    elseif step == 15 then
        Boss = false
        Name_Mon = "High-Level Sky Bandit (Level 1100)"
        CFrame_Wait = CFrame.new(3335.843017578125, 1994.8367919921875, -5381.94091796875)
    elseif step == 16 then
        Boss = false
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
    GodMode()
    Check()
    
    if tostring(game.Players.LocalPlayer.PlayerGui.Quests.Main.Position) == "{0, 0}, {0, 0}" and string.find(game.Players.LocalPlayer.PlayerGui.Quests.Main.Handler.QuestObject.Text,"(Level "..string.match(Name_Mon,"%d+")..")") then
        spawn(function()
            stop = true
            for i,v in pairs(game:GetService("Workspace").Mobs:GetChildren()) do -- GetDescendants
                if v.Name == Name_Mon then
                    if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid").Health > 0 then
                        stop = false
                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0,15,0)
                        wait(.3)
                    end
                end
            end
            if stop then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame_Wait
            end
        end)
        spawn(function()
            if not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ") then
                local Noclip = Instance.new("BodyVelocity")
                Noclip.Name = "GGEZ"
                Noclip.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
                Noclip.MaxForce = Vector3.new(100000,100000,100000)
                Noclip.Velocity = Vector3.new(0,0,0)
            end
        end)
    else
        game:GetService("ReplicatedStorage").Remotes.QuestRemote:FireServer("AbandonQuest")
        game:GetService("ReplicatedStorage").Remotes.QuestRemote:FireServer("GetQuest",Name_Mon)
        repeat wait()
        until tostring(game.Players.LocalPlayer.PlayerGui.Quests.Main.Position) == "{0, 0}, {0, 0}" and string.find(game.Players.LocalPlayer.PlayerGui.Quests.Main.Handler.QuestObject.Text,"(Level "..string.match(Name_Mon,"%d+")..")")
    end
end)
end
end
end)

spawn(function()
while wait() do
if Auto_Farm then
pcall(function()
    hit_combat("Combat")
    wait(.1)
    hit_sword("Katana")
    hit_sword("Shinsen")
    hit_sword("Nameless Katana")
end)
end
end
end)
Section:NewKeybind("KeybindText", "KeybindInfo", Enum.KeyCode.Z, function()
	print("You just clicked the bind")
end)

Section:NewButton("Random Fruit", "Check", function() -- Buttton
-- game:GetService("ReplicatedStorage").Remotes.FruitRoll:FireServer("3","Beli")
step = 16
farm = false
end)

Section:NewButton("Random Fruit", "Check", function() -- Buttton
-- game:GetService("ReplicatedStorage").Remotes.FruitRoll:FireServer("3","Beli")
step = 7
farm = true
end)

Section:NewKeybind("KeybindText", "KeybindInfo", Enum.KeyCode.RightControl, function() -- Key OPEN/CLOSE
	Library:ToggleUI()
end)
