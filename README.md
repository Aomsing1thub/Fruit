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

function Tw(v,CF)
    local Distance = (CF.Position - v.HumanoidRootPart.Position).Magnitude -- จุดที่จะไป Position Only
    local Speed = 16
    tweenService, tweenInfo = game:GetService("TweenService"), TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear)
    tween = tweenService:Create(v.HumanoidRootPart, tweenInfo, {CFrame = CF})
    tween:Play()
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
        Name = "Anubis the Bone Keeper (Level 800)"
        if find(Name) and findHealth(Name) then
            step = 13
        else
            step = 12
        end
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
        CFrame_Wait = CFrame.new(-369.2081604003906, 216.5130157470703, 387.48699951171875)
    elseif step == 2 then
        Boss = true
        Name_Mon = "Bandit Leader (Level 15)"
        CFrame_Wait = CFrame.new(-371.2571716308594, 247.01300048828125, 496.6766052246094)
    elseif step == 3 then
        Boss = false
        Name_Mon = "Clown Pirate (Level 30)"
        CFrame_Wait = CFrame.new(-315.8768005371094, 219.99827575683594, -1497.806884765625)
    elseif step == 4 then
        Boss = true
        Name_Mon = "Clown Leader (Level 60)"
        CFrame_Wait = CFrame.new(-321.23004150390625, 238.9982452392578, -1587.2579345703125)
    elseif step == 5 then
        Boss = false
        Name_Mon = "Caveman (Level 75)"
        CFrame_Wait = CFrame.new(215.53306579589844, 221.99879455566406, 2216.151123046875)
    elseif step == 6 then
        Boss = false
        Name_Mon = "Monkey (Level 90)"
        CFrame_Wait = CFrame.new(591.8125610351562, 267.9991455078125, 2251.00634765625)
    elseif step == 7 then
        Boss = true
        Name_Mon = "Gorilla (Level 120)"
        CFrame_Wait = CFrame.new(243.0989532470703, 334.9992980957031, 2430.525390625)
    elseif step == 8 then
        Boss = false
        Name_Mon = "Snow Bandit (Level 200)"
        CFrame_Wait = CFrame.new(-2355.30517578125, 252.4988250732422, 2219.086669921875)
    elseif step == 9 then
        Boss = false
        Name_Mon = "Small Yeti (Level 275)"
        CFrame_Wait = CFrame.new(-2398.7294921875, 553.5922241210938, 2610.006591796875)
    elseif step == 10 then
        Boss = false
        Name_Mon = "Yeti (Level 350)"
        CFrame_Wait = CFrame.new(-2786.235595703125, 552.5003662109375, 3006.614990234375)
    elseif step == 11 then
        Boss = false
        Name_Mon = "Sand Bandit (Level 450)"
        CFrame_Wait = CFrame.new(-2153.0302734375, 457.39990234375, -3759.306884765625)
    elseif step == 12 then
        Boss = false
        Name_Mon = "Pharaoh Guard (Level 600)"
        CFrame_Wait = CFrame.new(-2937.670654296875, 602.24951171875, -4605.40673828125)
    elseif step == 13 then
        Boss = false
        Name_Mon = "Anubis the Bone Keeper (Level 800)"
        CFrame_Wait = CFrame.new(-2968.497802734375, 628.7483520507812, -4785.97216796875)
    elseif step == 14 then
        Boss = false
        Name_Mon = "Sky Bandit (Level 1000)"
        CFrame_Wait = CFrame.new(2824.896728515625, 1837.2039794921875, -5212.48974609375)
    elseif step == 15 then
        Boss = false
        Name_Mon = "High-Level Sky Bandit (Level 1100)"
        CFrame_Wait = CFrame.new(3277.7236328125, 1886.7039794921875, -5286.43017578125)
    elseif step == 16 then
        Boss = false
        Name_Mon = "Sky Leader (Level 1200)"
        CFrame_Wait = CFrame.new(3083.838134765625, 1825.2039794921875, -5521.16064453125)
    end
end

Section:NewToggle("Auto", "ToggleInfo", function(state)
Auto_Farm = state
Wait = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,50,0)
    if not Auto_Farm then
        repeat wait()
        if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ") then
            game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ"):Destroy()
        end
        until not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ")
    end
end)

-- spawn(function()
-- while wait() do
-- if Auto_Farm then
-- pcall(function()
--     for i,v in pairs(game:GetService("Workspace").Mobs:GetChildren()) do -- GetDescendants
--         if v.Name == Name_Mon then
--             if v.Head:FindFirstChild("Handle") then
--                 v.Head:FindFirstChild("Handle"):Destroy()
--             end
--         end
--     end
-- end)
-- end
-- end
-- end)

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
                        Wait = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,50,0)
                        stop = false
                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0,15,0)
                        spawn(function()
                        Tw(v,CFrame_Wait)
                        end)
                        wait(.3)
                    end
                end
            end
            if stop then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Wait
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
    if not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ") then
        local Noclip = Instance.new("BodyVelocity")
        Noclip.Name = "GGEZ"
        Noclip.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
        Noclip.MaxForce = Vector3.new(100000,100000,100000)
        Noclip.Velocity = Vector3.new(0,0,0)
    end
end)
end
end
end)

spawn(function()
while wait() do
if Auto_Farm then
pcall(function()
    for i,v in pairs (game.Players.LocalPlayer.Backpack:GetChildren()) do
        if v:IsA "Tool" then
            if v.Name == "Night Katana" then
                hit_sword("Night Katana")
            elseif v.Name == "Nameless Katana" and 
                not game.Players.LocalPlayer.Character:FindFirstChild("Night Katana") and
                not game.Players.LocalPlayer.Character:FindFirstChild("Nameless Katana") then
                hit_sword("Nameless Katana")
            elseif v.Name == "Shinsen" and
                not game.Players.LocalPlayer.Character:FindFirstChild("Night Katana") and
                not game.Players.LocalPlayer.Character:FindFirstChild("Shinsen") and
                not game.Players.LocalPlayer.Character:FindFirstChild("Nameless Katana") then
                hit_sword("Shinsen") 
            elseif v.Name == "Combat" and
                not game.Players.LocalPlayer.Character:FindFirstChild("Night Katana") and
                not game.Players.LocalPlayer.Character:FindFirstChild("Combat") and
                not game.Players.LocalPlayer.Character:FindFirstChild("Shinsen") and
                not game.Players.LocalPlayer.Character:FindFirstChild("Nameless Katana") then
                hit_combat("Combat")
            else
                for x,y in pairs (game.Players.LocalPlayer.Character:GetChildren()) do
                    if y:IsA "Tool" then
                        if y.Name == "Night katana" then
                            hit_sword("Night katana")
                        elseif y.Name == "Nameless Katana" and
                            not game.Players.LocalPlayer.Backpack:FindFirstChild("Night Katana") and
                            not game.Players.LocalPlayer.Backpack:FindFirstChild("Nameless Katana") then
                            hit_sword("Nameless Katana")
                        elseif y.Name == "Shinsen" and 
                            not game.Players.LocalPlayer.Backpack:FindFirstChild("Night Katana") and
                            not game.Players.LocalPlayer.Backpack:FindFirstChild("Shinsen") and
                            not game.Players.LocalPlayer.Backpack:FindFirstChild("Nameless Katana") then
                            hit_sword("Shinsen") 
                        elseif y.Name == "Combat" and
                            not game.Players.LocalPlayer.Backpack:FindFirstChild("Night Katana") and
                            not game.Players.LocalPlayer.Backpack:FindFirstChild("Combat") and
                            not game.Players.LocalPlayer.Backpack:FindFirstChild("Shinsen") and
                            not game.Players.LocalPlayer.Backpack:FindFirstChild("Nameless Katana") then
                            hit_combat("Combat")
                        end
                    end
                end
            end
        end
    end
end)
end
end
end)

Section:NewKeybind("KeybindText", "KeybindInfo", Enum.KeyCode.Z, function()
	print("You just clicked the bind")
end)

Section:NewButton("Random Fruit 900K", "Check", function() -- Buttton
game:GetService("ReplicatedStorage").Remotes.FruitRoll:FireServer("3","Beli")
end)

Section:NewButton("Random Fruit 250K", "Check", function() -- Buttton
game:GetService("ReplicatedStorage").Remotes.FruitRoll:FireServer("2","Beli")
end)

Section:NewKeybind("KeybindText", "KeybindInfo", Enum.KeyCode.RightControl, function() -- Key OPEN/CLOSE
	Library:ToggleUI()
end)
