
local TextChatService = game:GetService("TextChatService") 

local Players = game:GetService("Players") 

local Fluxus = gethui():FindFirstChild("FluxusAndroidUI")

getgenv().Cache = Cache

if Fluxus and not Cache then
	Cache = true
	
	game:GetService("StarterGui"):SetCore("SendNotification",{
		Title = "Hf/Sf",
		Text = "Hf to hide\nSf to show",
		Duration = 7.5,
	})
	
	local TCS, PLC
	TextChatService.OnIncomingMessage = function(message: TextChatMessage)
		if TCS then return end
		local properties = Instance.new("TextChatMessageProperties")
		PLC:Disconnect()
		if message.Text:lower() == "hf" then
			Fluxus.Enabled = false
			return
		elseif message.Text:lower() == "sf" then
			Fluxus.Enabled = true
			return
		end
		return properties 
	end

	PLC = Players.LocalPlayer.Chatted:Connect(function(message)
		TCS = true
		if message:lower() == "hf" then
			Fluxus.Enabled = false
			return
		elseif message:lower() == "sf" then
			Fluxus.Enabled = true
			return
		end
	end)
end
