--game:GetService("StarterGui"):SetCore("DevConsoleVisible",true)

warn("exed")

local UserInputService = game:GetService("UserInputService")

local Players = game:GetService("Players")
local Local = Players.LocalPlayer

local Camera = workspace.CurrentCamera

local script = Local.Character:WaitForChild("BaseUIS")

local Held, Tap = {}, nil
UserInputService.InputBegan:Connect(function(input)
	local start = os.clock()
	if input.UserInputType == Enum.UserInputType.Touch then
		table.insert(Held, input)
		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				local time = os.clock()-start
				if time <= 0.125 then
					Tap = input
				end
				table.remove(Held, table.find(Held, input))
			end
		end)
	end
end)

local old; old = hookmetamethod(game, "__namecall", function(self, ...)
	local args, method = {...}, getnamecallmethod()
	if method == "FireServer" and self.Name == "ParryAttempt" and Tap then
		local Hit = Tap
		--warn(unpack(args[4]))
		args[4][1] = math.floor(Hit.Position.X)
		args[4][2] = math.floor(Hit.Position.Y)
		--warn(unpack(args[4]))
		Tap = nil
	elseif method == "FireServer" and self.Name == "ParryAttempt" and not Tap then
		--warn("No Tap")
	end
	return old(self, unpack(args))
end)
