local httpService = game:GetService("HttpService")
local TweenService = game:GetService("TweenService")
local ProximityPrompt = script.Parent.ProximityPrompt.ProximityPrompt
local KyberCrystalStation = script.Parent
local LightsaberModel = script.Parent.LightsaberModel
local Webhook = "https://discord.com/api/webhooks/1280139701012926541/rRLj41XER5-bYbFObTxPmUDuN0fg4CCFmoRg4hhyyHdK45eYVcuNtUB4pYtmfIFeipOn"
local ProxyService = require(game:GetService("ServerScriptService"):WaitForChild("ProxyService"))

local ProximityPromptDebounce = false

spawn(function()
	while true do
		task.wait()
		TweenService:Create(LightsaberModel.MainPart, TweenInfo.new(3.7, Enum.EasingStyle.Linear, Enum.EasingDirection.InOut), {CFrame = KyberCrystalStation.MainPartUpper.CFrame}):Play()
		task.wait(3.7)
		TweenService:Create(LightsaberModel.MainPart, TweenInfo.new(3.7, Enum.EasingStyle.Linear, Enum.EasingDirection.InOut), {CFrame = KyberCrystalStation.MainPartLower.CFrame}):Play()
		task.wait(3.7)
	end
end)

ProximityPrompt.Triggered:Connect(function(Player)
	warn("success")
	if ProximityPromptDebounce == false and Player:WaitForChild("KyberCrystalCount").Value > 0 then
		ProximityPromptDebounce = true
		spawn(function()
			local function IgniteSaber()
				spawn(function()
					local kyberColor = Player:WaitForChild("FoundKyberCrystalColor").Value
					local saberColor = {
						Cyan = { Color3.new(0, 0.701961, 1), ColorSequence.new(Color3.fromRGB(0, 179, 255)), "Light Blue Kyber Crystal", "https://media.discordapp.net/attachments/1280114235715620958/1284140274884280381/LightsaberCrystal-SWE.webp", 0x00B3FF },
						Blue = { Color3.new(0, 0.0666667, 1), ColorSequence.new(Color3.fromRGB(0, 17, 255)), "Blue Kyber Crystal", "https://media.discordapp.net/attachments/1280114235715620958/1284140086220554321/dfdzqtz-62f03e73-d955-42bc-8f35-31843d0aa670.png", 0x0011FF },
						Green = { Color3.new(0.152941, 0.580392, 0.145098), ColorSequence.new(Color3.fromRGB(39, 148, 37)), "Green Kyber Crystal", "https://media.discordapp.net/attachments/1280114235715620958/1284140127249109042/8b1db129a61fb67f791dec4a12cddc73.png", 0x279425 },
						Orange = { Color3.new(0.623529, 0.435294, 0), ColorSequence.new(Color3.fromRGB(159, 111, 0)), "Orange Kyber Crystal", "https://media.discordapp.net/attachments/1280114235715620958/1284140205237862491/493b6e5e0b4e1595ca371251415ca931.png", 0x9F6F00 },
						Yellow = { Color3.new(0.819608, 0.819608, 0), ColorSequence.new(Color3.fromRGB(209, 209, 0)), "Yellow Kyber Crystal", "https://media.discordapp.net/attachments/1280114235715620958/1284140169275900067/Yellow_Lightsaber_Crystal.webp", 0xD1D100 },
						Pink = { Color3.new(0.870588, 0.0784314, 0.858824), ColorSequence.new(Color3.fromRGB(222, 20, 219)), "Pink Kyber Crystal", "https://media.discordapp.net/attachments/1280114235715620958/1284140413279666237/Pink_Lightsaber_Crystal.png", 0xDE14DB },
						Purple = { Color3.new(0.427451, 0.0313725, 0.596078), ColorSequence.new(Color3.fromRGB(109, 8, 152)), "Purple Kyber Crystal", "https://media.discordapp.net/attachments/1280114235715620958/1284140245134344254/eb4818dbb45c0ddfe6d575e72161d22b.png", 0x6D0898 }
					}

					local data = saberColor[kyberColor]
					if data then
						LightsaberModel.BottomBlade.Glow.Color = data[1]
						LightsaberModel.BottomBlade.Outer.Color = data[2]

						local discordData = {
							username = "Crystal Gathering - Log",
							avatar_url = "https://i.imgur.com/DThoaQA.png",
							embeds = {
								{
									color = data[5],  -- Embed color matching saber color
									thumbnail = { url = data[4] },  -- The specific image for the Kyber Crystal
									fields = { { name = "", value = tostring(Player.Name) .. " has found a " .. kyberColor .. " Kyber Crystal.", inline = false } }
								}
							}
						}

						-- Send data to webhook
						ProxyService:Post(Webhook, httpService:JSONEncode(discordData))

						local crystalStorage = Player:WaitForChild("KyberCrystals")
						local crystal = crystalStorage:WaitForChild(data[3])
						if not crystal.Value then
							crystal.Value = true
						end
					end
				end)

				LightsaberModel.BottomBlade.Glow.Enabled = true
				LightsaberModel.BottomBlade.Inner.Enabled = true
				LightsaberModel.BottomBlade.Outer.Enabled = true
				LightsaberModel.MainPart.IgniteVersion1:Play()
				task.wait(0.4)
				LightsaberModel.MainPart.HummingVersion1:Play()
				task.wait(5)
				LightsaberModel.BottomBlade.Glow.Enabled = false
				LightsaberModel.BottomBlade.Inner.Enabled = false
				LightsaberModel.BottomBlade.Outer.Enabled = false
				LightsaberModel.MainPart.HummingVersion1:Stop()
				LightsaberModel.MainPart.DisIgniteVersion1:Play()
			end

			IgniteSaber()
			task.wait(5)
			ProximityPromptDebounce = false
		end)
	end
end)
