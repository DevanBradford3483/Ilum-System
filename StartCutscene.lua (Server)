local httpService = game:GetService("HttpService")
local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Events = ReplicatedStorage:WaitForChild("Events")
local Webhook = "https://discord.com/api/webhooks/1280139701012926541/rRLj41XER5-bYbFObTxPmUDuN0fg4CCFmoRg4hhyyHdK45eYVcuNtUB4pYtmfIFeipOn"
local ProxyService = require(script.Parent.Parent.Parent.ProxyService)
ProxyService:New("https://devansproxy3483-2d2a80f4688c.herokuapp.com/", "12d074b96ec7155bf3bec297473d25c2973f36219b6ba22e3c6d917e646e5070")

local KyberCrystalLight = game:GetService("Workspace"):WaitForChild("KyberCrystalLight")
local TopHinge = KyberCrystalLight:WaitForChild("TopHalf"):WaitForChild("TopHinge")
local BottomHinge = KyberCrystalLight:WaitForChild("BottomHalf"):WaitForChild("BottomHinge")

local StopSpinningTop = false
local StopSpinningBottom = false
local CurrentPlayer = {}

-- Start Timer Coroutine
local function StartTimer()
    local countdownDuration = 420
    local updateEvent = Events:WaitForChild("UpdateTimer")

    task.spawn(function()
        local timeLeft = countdownDuration
        while timeLeft > 0 do
            updateEvent:FireAllClients(timeLeft)
            task.wait(1)
            timeLeft = timeLeft - 1
            game:GetService("SoundService"):WaitForChild("Tick"):Play()
        end
        updateEvent:FireAllClients(0)
    end)
end

-- Helper function to handle beam enabling/disabling
local function ToggleBeams(beams, enabled)
    for _, beam in ipairs(beams) do
        if beam:IsA("Part") then
            beam.PointLight.Enabled = enabled
        end
    end
end

-- Start the Gathering process
local function StartGathering()
    warn("Started")

    ReplicatedStorage:WaitForChild("Gathering").Value = true
    Events:WaitForChild("StartMainCutscene"):FireAllClients()

    task.wait(82.5)
    
    -- Activate Big Beam and related actions
    task.spawn(function()
        task.wait(2)
        game.Workspace:WaitForChild("StartBigBeam").Part.Beam.Enabled = true
        game:GetService("SoundService"):WaitForChild("FirstBeam"):Play()

        ToggleBeams(game:GetService("Workspace"):WaitForChild("BigKyberCrystalLights"):GetChildren(), true)
        KyberCrystalLight.TopHalf["Kyber Crystal"].Material = Enum.Material.Neon
    end)

    task.wait(2)
    
    -- Enable Top and Bottom Beams and sounds
    task.spawn(function()
        task.wait(6)
        for i = 1, 8 do
            KyberCrystalLight.TopHalf["BigBeamBegin" .. i].Beam.Enabled = true
            task.wait(0.1)
            game:GetService("SoundService"):WaitForChild("BigBeam" .. i):Play()
        end
    end)

    -- Start spinning Kyber Crystals
    game:GetService("SoundService"):WaitForChild("TurningKyberCrystal"):Play()
    task.spawn(function()
        while not StopSpinningTop do
            task.wait(0.05)
            TopHinge.CFrame = TopHinge.CFrame * CFrame.fromEulerAnglesXYZ(0, math.rad(-2), 0)
        end
    end)

    task.spawn(function()
        while not StopSpinningBottom do
            task.wait(0.05)
            BottomHinge.CFrame = BottomHinge.CFrame * CFrame.fromEulerAnglesXYZ(0, math.rad(2), 0)
        end
    end)

    -- Timed stops for spinning
    task.delay(16.4, function() StopSpinningTop = true end)
    task.delay(20.23, function()
        StopSpinningBottom = true
        game:GetService("SoundService"):WaitForChild("TurningKyberCrystal"):Stop()
        -- Disable Top Beams
        for i = 1, 8 do
            KyberCrystalLight.TopHalf["BigBeamBegin" .. i].Beam.Enabled = false
        end
        task.wait(0.7)
        -- Bottom Beam starts
        KyberCrystalLight.BottomHalf.Beam2Begin.Beam.Enabled = true
        game:GetService("SoundService"):WaitForChild("FirstBeam"):Play()
        KyberCrystalLight.BottomHalf["Kyber Crystal"].Material = Enum.Material.Neon
        task.wait(0.1)
        KyberCrystalLight.BottomHalf.IceWallBeamBegin.Beam.Enabled = true
        game:GetService("SoundService"):WaitForChild("FirstBeam"):Play()
        task.wait(1)

        -- Mist & Ice Wall actions
        game:GetService("Workspace"):WaitForChild("Mist").Mist.Enabled = true
        game:GetService("SoundService"):WaitForChild("IceBreaking"):Play()
        TweenService:Create(game:GetService("Workspace").IceWall, TweenInfo.new(10, Enum.EasingStyle.Linear, Enum.EasingDirection.InOut), {CFrame = game:GetService("Workspace").IceWallMeltedPosition.CFrame}):Play()

        -- Reset and restart Timer
        task.spawn(function()
            task.wait(5)
            KyberCrystalLight.BottomHalf.IceWallBeamBegin.Beam.Enabled = false
            task.wait(2)
            game:GetService("Workspace"):WaitForChild("Mist").Mist.Enabled = false
            task.wait(5)
            game:GetService("Workspace").IceWall.CFrame = game:GetService("Workspace").IceWallFreezingPointPosition.CFrame
            task.wait(5)
            TweenService:Create(game:GetService("Workspace").IceWall, TweenInfo.new(420, Enum.EasingStyle.Linear, Enum.EasingDirection.InOut), {CFrame = game:GetService("Workspace").IceWalloriginalPosition.CFrame}):Play()
            task.spawn(StartTimer)
        end)
    end)
end

-- Player Added Event
Players.PlayerAdded:Connect(function(Player)
    table.insert(CurrentPlayer, Player.Name)

    -- Update CurrentPlayer list dynamically
    Players.PlayerRemoving:Connect(function(removedPlayer)
        for i, name in ipairs(CurrentPlayer) do
            if name == removedPlayer.Name then
                table.remove(CurrentPlayer, i)
                break
            end
        end
    end)

    Player.Chatted:Connect(function(Command)
        if Player:GetRankInGroup(34456980) >= 90 then
            if Command == "/e Start" or Command == "/e start" then
                if ReplicatedStorage:WaitForChild("Gathering").Value == false then
                    local Data = {
                        username = "Crystal Gathering - Log",
                        avatar_url = "https://i.imgur.com/DThoaQA.png",
                        embeds = {
                            {
                                color = 65415,
                                thumbnail = {
                                    url = "https://www.roblox.com/headshot-thumbnail/image?userId=" ..
                                        tostring(Player.UserId) .. "&width=420&height=420&format=png"
                                },
                                footer = {
                                    icon_url = "https://i.imgur.com/DThoaQA.png",
                                    text = "The Jedi Order",
                                },
                                fields = {
                                    {name = "", value = tostring(Player.Name) .. " has started a Crystal Gathering.", inline = false},
                                    {name = "Players In Server:", value = table.concat(CurrentPlayer, ", "), inline = false},
                                }
                            }
                        }
                    }
                    local finaldata = httpService:JSONEncode(Data)
                    ProxyService:Post(Webhook, finaldata)
                    StartGathering()
                end
            end
        end
    end)
end)
