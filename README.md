_G.Settings = {
    Auto_Farm = false,
    Auto_Bounty = false,
    Auto_Kill = false,
    Spectate = false,
    Auto_Kill = false,
    Health = 50,
    Auto_Random_Fruit = false,
    Auto_Store_Fruit = false,
    Aimbot = false
}

local a = "Duck HUB"
local b = game.Players.LocalPlayer.Name..".lua"
function saveSettings()
    local c = game:GetService("HttpService")
    local d = c:JSONEncode(_G.Settings)
    if writefile then
        if isfolder(a) then
            writefile(a .. "\\" .. b, d)
        else
            makefolder(a)
            writefile(a .. "\\" .. b, d)
        end
    end
end

function loadSettings()
    local c = game:GetService("HttpService")
    if isfile(a .. "\\" .. b) then
        _G.Settings = c:JSONDecode(readfile(a .. "\\" .. b))
    end
end

loadSettings()
Name_GUI = "Duck HUB"
local Ui = game:GetService("CoreGui"):FindFirstChild(Name_GUI)
if Ui then
    Ui:Destroy()
end
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/naypramx/Ui__Project/Script/XeNonUi", true))()
local CenterHubNo1 = library:CreateWindow("[UPDATE 1] Fruit Warriors By. Duck Hub Version 0.1 🙂",Enum.KeyCode.RightControl)

local GC = getconnections or get_signal_cons
if GC then
	for i,v in pairs(GC(game.Players.LocalPlayer.Idled)) do
		if v["Disable"] then
			v["Disable"](v)
		elseif v["Disconnect"] then
			v["Disconnect"](v)
		end
	end
else
	Players.LocalPlayer.Idled:Connect(function()
		local VirtualUser = game:GetService("VirtualUser")
		VirtualUser:CaptureController()
		VirtualUser:ClickButton2(Vector2.new())
	end)
end

function Delete(v,Name)
    if v.Head:FindFirstChild(Name) then
        v.Head:FindFirstChild(Name):Destroy()
    end
end

function Tw(v,CF)
    -- local Distance = (CF.Position - v.Head.Handle.Position).Magnitude -- จุดที่จะไป Position Only
    -- local Speed = 16
    -- tweenService, tweenInfo = game:GetService("TweenService"), TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear)
    -- tween = tweenService:Create(v.Head.Handle, tweenInfo, {CFrame = CF})
    -- tween:Play()
    v.HumanoidRootPart.CFrame = CF
    v.Head.Handle.CFrame = CF
end

function GodMode()
    spawn(function()
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
    end)
end

function leaderstats()
    Defense = tonumber(string.match(game:GetService("Players").LocalPlayer.PlayerGui.Stats.Main.Frame.StatsContainer.Defense.Text,"%d+"))
    Strength = tonumber(string.match(game:GetService("Players").LocalPlayer.PlayerGui.Stats.Main.Frame.StatsContainer.Strength.Text,"%d+"))
    Stamina = tonumber(string.match(game:GetService("Players").LocalPlayer.PlayerGui.Stats.Main.Frame.StatsContainer.Stamina.Text,"%d+"))
    Fruit = tonumber(string.match(game:GetService("Players").LocalPlayer.PlayerGui.Stats.Main.Frame.StatsContainer.Fruit.Text,"%d+"))
    Haki = tonumber(string.match(game:GetService("Players").LocalPlayer.PlayerGui.Stats.Main.Frame.StatsContainer.Haki.Text,"%d+"))
    Level = tonumber(string.match(game:GetService("Players").LocalPlayer.PlayerGui.Stats.Main.Frame.StatsContainer.AverageLevel.Text,"%d+"))
    gg1 = string.gsub(game:GetService("Players").LocalPlayer.PlayerGui.PC.OnScreen.Beli.Text,",","")
    gg2 = string.gsub(gg1,"B$ | ","")
    Money = tonumber(gg2)
    gg3 = string.gsub(game:GetService("Players").LocalPlayer.PlayerGui.PC.OnScreen.Token.Text,",","")
    gg4 = string.gsub(gg3,"T$ | ","")
    Token = tonumber(gg4)
end

function hit(Weapon)
    spawn(function()
        if game.Players.LocalPlayer.Backpack:FindFirstChild(Weapon) then
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

function hit_player(Weapon)
    spawn(function()
        game:GetService("ReplicatedStorage").Remotes.Mouse1Combat:FireServer(Weapon)
        for i,v in pairs (game.Players:GetChildren()) do
            if v ~= game.Players.LocalPlayer and v.Character.Humanoid.Health > 0 then
                game:GetService("ReplicatedStorage").Remotes.M1sDamage:FireServer(Weapon,v.Character)
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

function findback(Name)
    if game.Players.LocalPlayer.Backpack:FindFirstChild(Name) then
        return true
    end
end

function findchar(Name)
    if game.Players.LocalPlayer.Character:FindFirstChild(Name) then
        return true
    end
end

function Use()
    spawn(function()
        if _G.step == 4 then
            if findback("Black Leg") and not findchar("Black Leg") then
                if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") then
                   game.Players.LocalPlayer.Character.Humanoid:EquipTool(game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg"))
                end
            elseif findback("Combat") and not findchar("Combat") and not findchar("Black Leg") then
                if game.Players.LocalPlayer.Backpack:FindFirstChild("Combat") then
                   game.Players.LocalPlayer.Character.Humanoid:EquipTool(game.Players.LocalPlayer.Backpack:FindFirstChild("Combat"))
                end
            end
        else
            if findback("Night Katana") and not findchar("Night Katana") then
                hit("Night Katana")
            elseif findback("Nameless Katana") and not findchar("Nameless Katana") then
                hit("Nameless Katana")
            elseif findback("Shinsen") and not findchar("Shinsen") then
                hit("Shinsen")
            elseif findback("Katana") and not findchar("Katana") then
                hit("Katana")
            elseif findback("Black Leg") and
                -- not findchar("Combat") and
                -- not findchar("Shinsen") and
                -- not findchar("Nameless Katana") and
                -- not findchar("Night Katana") and
                -- not findchar("Katana") and
                not findchar("Black Leg") then
                hit("Black Leg")
                elseif findback("Combat") and
                -- not findchar("Black Leg") and
                -- not findchar("Shinsen") and
                -- not findchar("Nameless Katana") and
                -- not findchar("Night Katana") and
                -- not findchar("Katana") and
                not findchar("Combat") then
                hit("Combat")
            end
        end
        wait(.2)
    end)
    
    if _G.Settings.Auto_Bounty or _G.Settings.Auto_Kill then
        if findchar("Night Katana") then
            hit_player("Night Katana")
        elseif findchar("Nameless Katana") then
            hit_player("Nameless Katana")
        elseif findchar("Shinsen") then
            hit_player("Shinsen")
        elseif findchar("Katana") then
            hit_player("Katana")
        elseif findchar("Black Leg") then
            hit_player("Black Leg")
        elseif findchar("Combat") then
            hit_player("Combat")
        end
    end
end

_G.farm = true

function Check()
    Level = tonumber(string.match(game.Players.LocalPlayer.PlayerGui.Stats.Main.Frame.StatsContainer.AverageLevel.Text,"%d+"))
    if Level >= 0 and Level < 15 and _G.farm then
        _G.step = 1
    elseif Level >= 15 and Level < 30 and _G.farm then
        Name = "Bandit Leader (Level 15)"
        if find(Name) and findHealth(Name) and _G.farm then
            _G.step = 2
        else
            _G.step = 1
        end
    elseif Level >= 30 and Level < 60 and _G.farm then
        _G.step = 3
    elseif Level >= 60 and Level < 75 and _G.farm then
        Name = "Clown Leader (Level 60)"
        if find(Name) and findHealth(Name) and _G.farm then
            _G.step = 4
        else
            _G.step = 3
        end
    elseif Level >= 75 and Level < 90 and _G.farm then
        _G.step = 5
    elseif Level >= 90 and Level < 120 and _G.farm then
        _G.step = 6
    elseif Level >= 120 and Level < 200 and _G.farm then
        Name = "Gorilla (Level 120)"
        if find(Name) and findHealth(Name) and _G.farm then
            _G.step = 7
        else
            _G.step = 6
        end
    elseif Level >= 200 and Level < 275 and _G.farm then
        _G.step = 8
    elseif Level >= 275 and Level < 450 and _G.farm then
        _G.step = 9
    elseif Level >= 350 and Level < 450 and _G.farm then
        _G.step = 10
    elseif Level >= 450 and Level < 600 and _G.farm then
        _G.step = 11
    elseif Level >= 600 and Level < 800 and _G.farm then
        _G.step = 12
    elseif Level >= 800 and Level < 1000 and _G.farm then
        Name = "Anubis the Bone Keeper (Level 800)"
        if find(Name) and findHealth(Name) and _G.farm then
            _G.step = 13
        else
            _G.step = 12
        end
    elseif Level >= 1000 and Level < 1100 and _G.farm then
        _G.step = 14
    elseif Level >= 1100 and Level < 1200 and _G.farm then
        _G.step = 15
    elseif Level >= 1200 and _G.farm then
        Name = "Sky Leader (Level 1200)"
        if find(Name) and findHealth(Name) then
            _G.step = 16
        else
            _G.step = 15
        end
    end
    
    if _G.step == 1 then
        Name_Mon = "Bandit (Level 1)"
        CFrame_Wait = CFrame.new(-369.2081604003906, 216.5130157470703, 387.48699951171875)
    elseif _G.step == 2 then
        Name_Mon = "Bandit Leader (Level 15)"
        CFrame_Wait = CFrame.new(-371.2571716308594, 247.01300048828125, 496.6766052246094)
    elseif _G.step == 3 then
        Name_Mon = "Clown Pirate (Level 30)"
        CFrame_Wait = CFrame.new(-315.8768005371094, 219.99827575683594, -1497.806884765625)
    elseif _G.step == 4 then
        Name_Mon = "Clown Leader (Level 60)"
        CFrame_Wait = CFrame.new(-321.23004150390625, 238.9982452392578, -1587.2579345703125)
    elseif _G.step == 5 then
        Name_Mon = "Caveman (Level 75)"
        CFrame_Wait = CFrame.new(215.53306579589844, 221.99879455566406, 2216.151123046875)
    elseif _G.step == 6 then
        Name_Mon = "Monkey (Level 90)"
        CFrame_Wait = CFrame.new(591.8125610351562, 267.9991455078125, 2251.00634765625)
    elseif _G.step == 7 then
        Name_Mon = "Gorilla (Level 120)"
        CFrame_Wait = CFrame.new(243.0989532470703, 334.9992980957031, 2430.525390625)
    elseif _G.step == 8 then
        Name_Mon = "Snow Bandit (Level 200)"
        CFrame_Wait = CFrame.new(-2355.30517578125, 252.4988250732422, 2219.086669921875)
    elseif _G.step == 9 then
        Name_Mon = "Small Yeti (Level 275)"
        CFrame_Wait = CFrame.new(-2398.7294921875, 553.5922241210938, 2610.006591796875)
    elseif _G.step == 10 then
        Name_Mon = "Yeti (Level 350)"
        CFrame_Wait = CFrame.new(-2786.235595703125, 552.5003662109375, 3006.614990234375)
    elseif _G.step == 11 then
        Name_Mon = "Sand Bandit (Level 450)"
        CFrame_Wait = CFrame.new(-2153.0302734375, 457.39990234375, -3759.306884765625)
    elseif _G.step == 12 then
        Name_Mon = "Pharaoh Guard (Level 600)"
        CFrame_Wait = CFrame.new(-2937.670654296875, 602.24951171875, -4605.40673828125)
    elseif _G.step == 13 then
        Name_Mon = "Anubis the Bone Keeper (Level 800)"
        CFrame_Wait = CFrame.new(-2968.497802734375, 628.7483520507812, -4785.97216796875)
    elseif _G.step == 14 then
        Name_Mon = "Sky Bandit (Level 1000)"
        CFrame_Wait = CFrame.new(2824.896728515625, 1837.2039794921875, -5212.48974609375)
    elseif _G.step == 15 then
        Name_Mon = "High-Level Sky Bandit (Level 1100)"
        CFrame_Wait = CFrame.new(3273.7890625, 1887.7042236328125, -5280.36328125)
    elseif _G.step == 16 then
        Name_Mon = "Sky Leader (Level 1200)"
        CFrame_Wait = CFrame.new(3083.838134765625, 1825.2039794921875, -5521.16064453125)
    end
end

function Change(String)
    Display = {}
    Name = {}
    
    for i,v in pairs(game:GetService("Players"):GetChildren()) do
       table.insert(Display,v.DisplayName)
       table.insert(Name,v.Name)
    end
    
    for i,v in pairs (Display) do
        if String == v then
            return Name[i]
        end
    end
end

function GetPlayer(String)
    local Found = {}
    local strl = String:lower()
       for i,v in pairs(game.Players:GetPlayers()) do
            if v ~= game.Players.LocalPlayer then
                if v.Name:lower():sub(1, #String) == String:lower() then
                    table.insert(Found,v.Name)
                elseif v.DisplayName:lower():sub(1, #String) == String:lower() then
                    table.insert(Found,v.DisplayName)
                end
            end
       end    
    return Found[1] 
end

local Tab = CenterHubNo1:CreateTab("Auto Farm")
local Sector1 = Tab:CreateSector("Auto Farm","left")

Sector1:AddToggle("Auto Farm",_G.Settings.Auto_Farm,function(t)
    _G.Settings.Auto_Farm = t
    saveSettings()
    spawn(function()
        if not _G.Settings.Auto_Farm then
            repeat wait()
            if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ") then
                game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ"):Destroy()
            end
            until not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ")
        end
    end)
end)

spawn(function()
while wait() do
if _G.Settings.Auto_Farm then
pcall(function()
    leaderstats()
    
    if not findchar("Night Katana") and not findback("Night Katana") then
        game:GetService("ReplicatedStorage").Remotes.ItemsEquip:FireServer("Night Katana","Equip")
        wait(.5)
        if not findchar("Night Katana") and not findback("Night Katana") then
            game:GetService("ReplicatedStorage").Remotes.ItemsEquip:FireServer("Nameless Katana","Equip")
            wait(.5)
            if not findchar("Nameless Katana") and not findback("Nameless Katana") then
                leaderstats()
                if Money >= 1600000 then
                    game:GetService("ReplicatedStorage").Remotes.ItemBuy:FireServer("NamelessKatana")
                else
                    if not findchar("Shinsen Katana") and not findback("Shinsen Katana") then
                        game:GetService("ReplicatedStorage").Remotes.ItemsEquip:FireServer("Shinsen","Equip")
                        wait(.5)
                        if not findchar("Shinsen") and not findback("Shinsen") then
                            leaderstats()
                            if Money >= 1200000 then
                                game:GetService("ReplicatedStorage").Remotes.ItemBuy:FireServer("Shinsen")
                            else
                                if not findchar("Katana") and not findback("Katana") then
                                    game:GetService("ReplicatedStorage").Remotes.ItemsEquip:FireServer("Katana","Equip")
                                    wait(.5)
                                    if not findchar("Katana") and not findback("Katana") then
                                        leaderstats()
                                        if Money >= 5000 then
                                            game:GetService("ReplicatedStorage").Remotes.ItemBuy:FireServer("Katana")
                                        end
                                    end
                                end 
                            end
                        end
                    end
                end
            end
        end
    end
    if not findchar("Black Leg") and not findback("Black Leg") then
        if Strength >= 50 and Stamina >= 50 and Money >= 50000 then
            game:GetService("ReplicatedStorage").Remotes.FightingStyleLearn:FireServer("Black Leg")
        end
    end
end)
end
end
end)

function get_fruit()
    for i,v in pairs (game.Players.LocalPlayer.Backpack:GetChildren()) do
        if v:FindFirstChild("Main") and not v:FindFirstChild("LocalBlackLegHandler") and not v:FindFirstChild("Handle") then
            if not game.Players.LocalPlayer.Character:FindFirstChild(v.Name) then
               game.Players.LocalPlayer.Character.Humanoid:EquipTool(game.Players.LocalPlayer.Backpack:FindFirstChild(v.Name))
            end
        end
    end
end

function findHealthper(v,per)
    Max = (v.Humanoid.MaxHealth * per) / 100
    return Max
end

spawn(function()
while wait() do
if _G.Settings.Auto_Farm then
pcall(function()
    GodMode()
    Check()
    
    if tostring(game.Players.LocalPlayer.PlayerGui.Quests.Main.Position) == "{0, 0}, {0, 0}" and string.find(game.Players.LocalPlayer.PlayerGui.Quests.Main.Handler.QuestObject.Text,"(Level "..string.match(Name_Mon,"%d+")..")") then
        spawn(function()
            stop = true
            for i,v in pairs(game:GetService("Workspace").Mobs:GetChildren()) do -- GetDescendants
                if v.Name == Name_Mon then
                    if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") then
                        if v.Humanoid:FindFirstChild("Animator") then
                            v.Humanoid:FindFirstChild("Animator"):Destroy()
                        end
                        if v:FindFirstChild("Humanoid").Health > 0 then
                            if _G.Settings.Auto_Farm_Mastery then
                                if v:FindFirstChild("Humanoid").Health < findHealthper(v,10) then
                                    get_fruit()
                                    stop = false
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0,15,0)
                                    hit_skill(v)
                                else
                                    Use()
                                    Wait =  game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,150,0)
                                    stop = false
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0,15,0)
                                end
                            else
                                Use()
                                wait(.2)
                                Wait =  game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,150,0)
                                stop = false
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0,15,0)
                                wait(.2)
                                if v:FindFirstChild("Humanoid").Health < findHealthper(v,70) and v:FindFirstChild("Humanoid").Health > findHealthper(v,20) then
                                hit_skill(v)
                                end
                            end
                        end
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
while task.wait() do
if _G.Settings.Auto_Farm then
pcall(function()
    for i,v in pairs(game:GetService("Workspace").Mobs:GetChildren()) do -- GetDescendants
        if v.Name == Name_Mon then
            if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid").Health > 0 then
                if v.HumanoidRootPart:FindFirstChild("Hit1") then
                    v.HumanoidRootPart:FindFirstChild("Hit1"):Destroy()
                elseif v.HumanoidRootPart:FindFirstChild("Hit2") then
                    v.HumanoidRootPart:FindFirstChild("Hit2"):Destroy()
                elseif v.HumanoidRootPart:FindFirstChild("Hit3") then
                    v.HumanoidRootPart:FindFirstChild("Hit3"):Destroy()
                elseif v.HumanoidRootPart:FindFirstChild("Hit4") then
                    v.HumanoidRootPart:FindFirstChild("Hit4"):Destroy()
                end
            end
        end
    end
end)
end
end
end)

spawn(function()
while task.wait() do
if _G.Settings.Auto_Farm or _G.Settings.Auto_Bounty then
pcall(function()
    if not game.Players.LocalPlayer.Character["Left Arm"]:FindFirstChild("HakiPart") then
        game:GetService("VirtualInputManager"):SendKeyEvent(true,106,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
        game:GetService("VirtualInputManager"):SendKeyEvent(false,106,false,game.Players.LocalPlayer.Character.HumanoidRootPart)
        wait(.5)
        if not game.Players.LocalPlayer.Character["Left Arm"]:FindFirstChild("HakiPart") then
            leaderstats()
            if Defense >= 100 and Strength >= 100 and Money >= 100000 then
                game:GetService("ReplicatedStorage").Remotes.LearnAbilities:FireServer("ArmamentHaki")
            end
        end
    end
end)
end
end
end)

spawn(function()
while wait() do
if _G.Settings.Auto_Bounty or _G.Settings.Auto_Farm or _G.Settings.Auto_Kill then
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
if _G.Settings.Auto_Farm then
pcall(function()
    for i,v in pairs(game:GetService("Workspace").Mobs:GetChildren()) do -- GetDescendants
        if v.Name == Name_Mon then
            if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid").Health > 0 then
                if (v.HumanoidRootPart.Position - CFrame_Wait.Position).Magnitude <= 50 then
                    Tw(v,CFrame_Wait)
                    if not v.HumanoidRootPart:FindFirstChild("GGEZ") then
                        local Noclip = Instance.new("BodyVelocity")
                        Noclip.Name = "GGEZ"
                        Noclip.Parent = v.HumanoidRootPart
                        Noclip.MaxForce = Vector3.new(100000,100000,100000)
                        Noclip.Velocity = Vector3.new(0,0,0)
                    end
                end
            end
        end
    end
end)
end
end
end)

Sector1:AddToggle("Auto Farm Mastery",_G.Settings.Auto_Farm_Mastery,function(t)
    _G.Settings.Auto_Farm_Mastery = t
    saveSettings()
    spawn(function()
        if not _G.Settings.Auto_Farm_Mastery then
            repeat wait()
            if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ") then
                game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ"):Destroy()
            end
            until not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ")
        end
    end)
end)

function VFX(Name_Skill,Target)
local args = {
    [1] = Name_Skill,
    [2] = {
        ["Status"] = "Charge",
        ["MouseTarget"] = Target,
        ["MousePos"] = Target.Position
    }
}

game:GetService("ReplicatedStorage").Remotes.VFX:FireServer(unpack(args))
local args = {
    [1] = Name_Skill,
    [2] = {
        ["Status"] = "Release",
        ["MouseTarget"] = Target,
        ["MousePos"] = Target.Position
    }
}

game:GetService("ReplicatedStorage").Remotes.VFX:FireServer(unpack(args))
end

function hit_skill(Target)
    w = {}
    
    for i,v in pairs (game.Players.LocalPlayer.Character:GetChildren()) do
        if v:IsA "Tool" then
            for i,x in pairs (v.Main:GetChildren()) do
                table.insert(w,x)
            end
        end
    end
    
    for i,Mon in pairs (w) do
        VFX(Mon.Name,Target.HumanoidRootPart)
    end
end

Sector1:AddToggle("Auto Farm Bounty",_G.Settings.Auto_Bounty,function(t)
    _G.Settings.Auto_Bounty = t
    saveSettings()
    spawn(function()
        if not _G.Settings.Auto_Bounty then
            repeat wait()
            if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ") then
                game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ"):Destroy()
            end
            until not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ")
        end
    end)
end)

num = 2

spawn(function()
while wait() do
if _G.Settings.Auto_Bounty then
pcall(function()
    for i,v in pairs (game.Players:GetChildren()) do
        if i == num then
            gg = v.Character.Humanoid.Health
            wait(2)
            gg1 = v.Character.Humanoid.Health
            if gg <= gg1 then
                num = num + 1
            else
                hit_skill(v.Character)
            end
        end
    end
    if num >= Max then
        num = 2
    end
end)
end
end
end)

spawn(function()
while wait() do
if _G.Settings.Auto_Bounty then
pcall(function()
    GodMode()
    Use()
    Max = #game.Players:GetChildren()
    for i,v in pairs (game.Players:GetChildren()) do
        if i == num then
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.Character.HumanoidRootPart.CFrame * CFrame.new(0,10,0)
            if v.Character.Humanoid.Health <= 0 then
                num = num + 1
            end
        end
    end
end)
end
end
end)

Sector1:AddToggle("SAFE MODE",_G.Settings.Safe_Mode,function(t)
    _G.Settings.Safe_Mode = t
    saveSettings()
    spawn(function()
        if not _G.Settings.Safe_Mode then
            repeat wait()
            if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ") then
                game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ"):Destroy()
            end
            until not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ")
        end
    end)
end)

Sector1:AddSlider("Select % Health",30,_G.Settings.Health,100,1,function(x)
    _G.Settings.Health = x
    saveSettings()
end)

spawn(function()
while wait() do
if _G.Settings.Safe_Mode then
pcall(function()
    MaxHealth = game.Players.LocalPlayer.Character.Humanoid.MaxHealth
    Health = game.Players.LocalPlayer.Character.Humanoid.Health
    Result = (MaxHealth * _G.Settings.Health) / 100
    if Health < Result then
        if not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ") then
            local Noclip = Instance.new("BodyVelocity")
            Noclip.Name = "GGEZ"
            Noclip.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
            Noclip.MaxForce = Vector3.new(100000,100000,100000)
            Noclip.Velocity = Vector3.new(0,0,0)
        end
        x = math.random(-1000,1000)
        z = math.random(-1000,1000)
        me = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(x,me.Y,z)
    end
end)
end
end
end)

local Sector1 = Tab:CreateSector("Auto Kill","right")

Sector1:AddTextbox("Name Player ",false,function(t)
    Select = GetPlayer(t)
end)

Sector1:AddToggle("Auto Kill",_G.Settings.Auto_Kill,function(t)
    _G.Settings.Auto_Kill = t
    saveSettings()
    spawn(function()
        if not _G.Settings.Auto_Kill then
            repeat wait()
            if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ") then
                game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ"):Destroy()
            end
            until not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ")
        end
    end)
end)

spawn(function()
while wait() do
if _G.Settings.Auto_Kill then
pcall(function()
    Use()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Change(Select)].Character.HumanoidRootPart.CFrame * CFrame.new(0,10,0)
end)
end
end
end)

Sector1:AddToggle("Spectate",_G.Settings.Spectate,function(t)
    _G.Settings.Spectate = t
    saveSettings()
    spawn(function()
        if not _G.Settings.Spectate then
            workspace.CurrentCamera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
        end
    end)
end)

spawn(function()
while wait() do
if _G.Settings.Spectate then
pcall(function()
workspace.CurrentCamera.CameraSubject = game.Players[Change(Select)].Character.Humanoid
end)
end
end
end)

Sector1:AddToggle("Aimbot",_G.Settings.Aimbot,function(t)
    _G.Settings.Aimbot = t
    saveSettings()
    spawn(function()
        if not _G.Settings.Aimbot then
            
        end
    end)
end)

local old
old = hookmetamethod(game,"__namecall",function(self,...)
    local args = {...}
    if getnamecallmethod() == "FireServer" and tostring(self) == "VFX" then
        if typeof(args[2]) == "table" and args[2]["MousePos"] then
            if typeof(args[2]["MousePos"]) == "Vector3" and _G.Settings.Aimbot then
                args[2]["MousePos"] = _G.MobTarget.Position
                args[2]["MouseTarget"] = _G.MobTarget
                 return old(self,unpack(args))
            end
        end
    end
    return old(self,...)
end)

spawn(function()
while wait() do
if _G.Settings.Aimbot then
pcall(function()
    _G.MobTarget = game.Players[Select].Character.HumanoidRootPart
end)
end
end
end)

Sector1:AddButton("Teleport",function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Change(Select)].Character.HumanoidRootPart.CFram
end)

local Sector1 = Tab:CreateSector("Auto Buy","left")
Stage = "Stage 3 900K B$"
Sector1:AddDropdown("Select Stage",{"Stage 1 25K B$","Stage 2 250K B$","Stage 3 900K B$"},"Stage 3 900K B$",false,function(t)
    Stage = t
end)

Sector1:AddToggle("Auto Random Fruit ",_G.Settings.Auto_Random_Fruit,function(t)
    _G.Settings.Auto_Random_Fruit = t
    saveSettings()
end)

spawn(function()
while wait() do
if _G.Settings.Auto_Random_Fruit then
pcall(function()
    gg = string.gsub(game:GetService("Players").LocalPlayer.PlayerGui.PC.OnScreen.Beli.Text,",","")
    gg1 = string.gsub(gg,"B$ | ","")
    Money = tonumber(gg1)
    if Stage == "Stage 3 900K B$" then
        if Money >= 10000000 and Money > 9100000 then
            game:GetService("ReplicatedStorage").Remotes.FruitRoll:FireServer("3","Beli")
            repeat wait(1)
            until Money > 9100000
        end
    elseif Stage == "Stage 2 250K B$" then
        if Money >= 10000000 and Money > 10000000 - 250000 then
            game:GetService("ReplicatedStorage").Remotes.FruitRoll:FireServer("2","Beli")
            repeat wait(1)
            until Money > 10000000 - 250000
        end
    elseif Stage == "Stage 1 25K B$" then
        if Money >= 10000000 and Money > 10000000 - 25000 then
            game:GetService("ReplicatedStorage").Remotes.FruitRoll:FireServer("1","Beli")
            repeat wait(1)
            until Money > 10000000 - 25000
        end
    end
end)
end
end
end)

Sector1:AddToggle("Auto Store Fruit ",_G.Settings.Auto_Store_Fruit,function(t)
    _G.Settings.Auto_Store_Fruit = t
    saveSettings()
end)

spawn(function()
while wait() do
if _G.Settings.Auto_Store_Fruit then
pcall(function()
    for i,v in pairs (game.Players.LocalPlayer.Backpack:GetChildren()) do
        if string.find(v.Name,"Fruit") then
            game:GetService("ReplicatedStorage").Remotes.FruitHandler:FireServer(v.Name,"Store")
        end
    end
end)
end
end
end)

Sector1:AddButton("Stage 3 900K B$",function()
    game:GetService("ReplicatedStorage").Remotes.FruitRoll:FireServer("3","Beli")
end)

Sector1:AddButton("Stage 2 250K B$",function()
    game:GetService("ReplicatedStorage").Remotes.FruitRoll:FireServer("2","Beli")
end)

Sector1:AddButton("Stage 1 25K B$",function()
    game:GetService("ReplicatedStorage").Remotes.FruitRoll:FireServer("1","Beli")
end)

local Tab = CenterHubNo1:CreateTab("Teleport")
local Sector1 = Tab:CreateSector("Place","left")

Places = {}

for i,v in pairs (game:GetService("Workspace").Map:GetChildren()) do
    if v:IsA "Folder" then
        table.insert(Places,v.Name)
    end
end

Sector1:AddDropdown("Select Place",Places,"Rookie Town",false,function(t)
    Place = t
    if Place == "Rookie Town" then
        GoTo = CFrame.new(-368.315673828125, 217.0130615234375, 283.4286193847656)
    elseif Place == "Snow Island" then
        GoTo = CFrame.new(-2206.1171875, 243.498779296875, 2337.36474609375)
    elseif Place == "Orange Town" then
        GoTo = CFrame.new(-320.22393798828125, 220.4982452392578, -1414.3162841796875)
    elseif Place == "Jungle" then
        GoTo = CFrame.new(491.2817687988281, 267.9991455078125, 2324.74853515625)
    elseif Place == "Arena  Island" then
        GoTo = CFrame.new(1577.7603759765625, 206.12889099121094, 1056.0426025390625)
    elseif Place == "East Hill" then
        GoTo = CFrame.new(597.1534423828125, 632.1998291015625, -596.9248046875)
    elseif Place == "North Hill" then
        GoTo = CFrame.new(-2022.1378173828125, 632.1998291015625, -463.5531005859375)
    elseif Place == "South Hill" then
        GoTo = CFrame.new(-1100.102783203125, 392.9499206542969, 1189.421142578125)
    elseif Place == "Island In The Sky" then
        GoTo = CFrame.new(2984.09130859375, 1900.71044921875, -5373.017578125)
    elseif Place == "Fallen Island" then
        GoTo = CFrame.new(2514.302490234375, 218.40245056152344, -3094.522216796875)
    elseif Place == "Sky Dungeon" then
        GoTo = CFrame.new(2287.54248046875, 6413.6943359375, -5288.02685546875)
    elseif Place == "Desert Island" then
        GoTo = CFrame.new(-2855.125244140625, 580.549072265625, -4407.7568359375)
    end
end)

Sector1:AddButton("Teleport",function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = GoTo
end)
