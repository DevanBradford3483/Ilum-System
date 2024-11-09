local ProximityPrompt = script.Parent

local KyberCrystalColors = {
	{"Cyan", chance = 25},
	{"Blue", chance = 25},
	{"Green", chance = 20},
	{"Orange", chance = 15},
	{"Yellow", chance = 10},
	{"Pink", chance = 2.5},
	{"Purple", chance = 2.5}
}

ProximityPrompt.Triggered:Connect(function(Player)
	if game:GetService("ReplicatedStorage"):WaitForChild("Gathering").Value == true then
		local totalWeight = 0
		for _, colorData in pairs(KyberCrystalColors) do
			totalWeight = totalWeight + colorData.chance
		end

		local randomNumber = math.random() * totalWeight
		local cumulativeWeight = 0
		local selectedColor = nil

		for _, colorData in pairs(KyberCrystalColors) do
			cumulativeWeight = cumulativeWeight + colorData.chance
			if randomNumber <= cumulativeWeight then
				selectedColor = colorData[1]
				break
			end
		end

		if selectedColor then
			Player:WaitForChild("FoundKyberCrystalColor").Value = selectedColor
		end


		Player:WaitForChild("KyberCrystalCount").Value = Player:WaitForChild("KyberCrystalCount").Value + 1
		script.Parent.Enabled = false
		task.wait(0.7)
		script.Parent.Parent:Destroy()
		game:GetService("ReplicatedStorage"):WaitForChild("Events"):WaitForChild("KyberCrystlPickedUp"):FireClient(Player)
	end
end)
