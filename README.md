local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local UserInputService = game:GetService("UserInputService")

-- Criar a interface
local screenGui = script.Parent

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 250, 0, 300)
frame.Position = UDim2.new(0.5, -125, 0.5, -150)
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
frame.BorderSizePixel = 0
frame.Visible = false
frame.Parent = screenGui

local uiList = Instance.new("UIListLayout")
uiList.Padding = UDim.new(0, 10)
uiList.FillDirection = Enum.FillDirection.Vertical
uiList.HorizontalAlignment = Enum.HorizontalAlignment.Center
uiList.VerticalAlignment = Enum.VerticalAlignment.Top
uiList.Parent = frame

-- Função para criar botões
local function createButton(text, callback)
	local button = Instance.new("TextButton")
	button.Size = UDim2.new(0, 200, 0, 40)
	button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
	button.TextColor3 = Color3.new(1, 1, 1)
	button.Font = Enum.Font.GothamBold
	button.TextSize = 18
	button.Text = text
	button.Parent = frame

	button.MouseButton1Click:Connect(callback)
end

-- Cheats
createButton("Velocidade +", function()
	local humanoid = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.WalkSpeed = 100
	end
end)

createButton("Pulo +", function()
	local humanoid = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.JumpPower = 150
	end
end)

createButton("Voar (pressione espaço)", function()
	local humanoid = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.PlatformStand = true
		local bodyVelocity = Instance.new("BodyVelocity", player.Character.HumanoidRootPart)
		bodyVelocity.Velocity = Vector3.new(0, 50, 0)
		bodyVelocity.MaxForce = Vector3.new(0, math.huge, 0)

		wait(2)
		bodyVelocity:Destroy()
		humanoid.PlatformStand = false
	end
end)

createButton("Vida Infinita", function()
	local humanoid = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.Health = math.huge
	end
end)

-- Tecla para abrir/fechar menu
UserInputService.InputBegan:Connect(function(input, gameProcessed)
	if gameProcessed then return end
	if input.KeyCode == Enum.KeyCode.P then
		frame.Visible = not frame.Visible
	end
end)
