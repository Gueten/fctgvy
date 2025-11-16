--// GUI + FARM CANDY CORN + AUTO EQUIP SLOT 3 + AUTO E
-- coloque este LocalScript dentro de StarterGui

local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local player = Players.LocalPlayer

local teleportPos = Vector3.new(-7550.52294921875, 26.863250732421875, -818.1243286132812)

--// Criar GUI
local ScreenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
ScreenGui.ResetOnSpawn = false

local Frame = Instance.new("Frame", ScreenGui)
Frame.Size = UDim2.new(0, 160, 0, 60)
Frame.Position = UDim2.new(0.05, 0, 0.4, 0)
Frame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
Frame.BorderSizePixel = 0
Instance.new("UICorner", Frame).CornerRadius = UDim.new(0, 8)

local Button = Instance.new("TextButton", Frame)
Button.Size = UDim2.new(1, -10, 1, -10)
Button.Position = UDim2.new(0, 5, 0, 5)
Button.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
Button.TextColor3 = Color3.new(1,1,1)
Button.Font = Enum.Font.GothamBold
Button.TextSize = 16
Button.Text = "🍬 Farm Candy: OFF"
Instance.new("UICorner", Button).CornerRadius = UDim.new(0, 6)

--// Ativo?
local ativo = false

--// Função teleporte
local function teleportar()
	local char = player.Character or player.CharacterAdded:Wait()
	local root = char:WaitForChild("HumanoidRootPart")
	root.CFrame = CFrame.new(teleportPos)
end

--// Thread Auto E + Equip slot 3
task.spawn(function()
	while true do
		if ativo then
			-- Garantir slot 3 equipado
			UserInputService.InputBegan:Fire({
				KeyCode = Enum.KeyCode.Three
			})

			-- Pressionar E
			UserInputService.InputBegan:Fire({
				KeyCode = Enum.KeyCode.E
			})

			wait(0.5)
		else
			wait(0.2)
		end
	end
end)

--// Ativar / Desativar
Button.MouseButton1Click:Connect(function()
	ativo = not ativo

	if ativo then
		Button.Text = "🍬 Farm Candy: ON"
		Button.BackgroundColor3 = Color3.fromRGB(0, 170, 0)

		teleportar()
	else
		Button.Text = "🍬 Farm Candy: OFF"
		Button.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
	end
end)
