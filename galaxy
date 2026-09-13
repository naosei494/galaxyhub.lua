local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local Workspace = game:GetService("Workspace")

local localPlayer = Players.LocalPlayer
local guiParent = localPlayer:WaitForChild("PlayerGui")
local camera = Workspace.CurrentCamera

-- Remove versões anteriores do script para não duplicar a interface na tela
if guiParent:FindFirstChild("GalaxyHubGuiPC") then
	guiParent["GalaxyHubGuiPC"]:Destroy()
end

-- 1. Interface Gui Principal
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "GalaxyHubGuiPC"
screenGui.ResetOnSpawn = false
screenGui.DisplayOrder = 2147483647
screenGui.Parent = guiParent

-- 2. Botão Circular de Toggle (Fundo alterado para 10248444952)
local toggleCircle = Instance.new("ImageButton")
toggleCircle.Name = "ToggleCircle"
toggleCircle.Size = UDim2.new(0, 45, 0, 45)
toggleCircle.Position = UDim2.new(0.05, 0, 0.4, 0)
toggleCircle.Image = "rbxassetid://10248444952"
toggleCircle.BackgroundTransparency = 1
toggleCircle.Active = true
toggleCircle.Visible = true
toggleCircle.Parent = screenGui

local circleCorner = Instance.new("UICorner")
circleCorner.CornerRadius = UDim.new(1, 0)
circleCorner.Parent = toggleCircle

local circleStroke = Instance.new("UIStroke")
circleStroke.Thickness = 2
circleStroke.Color = Color3.fromRGB(138, 43, 228)
circleStroke.Parent = toggleCircle

-- Drag do Botão Circular
local draggingCircle, dragStartCircle, startPosCircle
toggleCircle.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		draggingCircle = true
		dragStartCircle = input.Position
		startPosCircle = toggleCircle.Position

		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				draggingCircle = false
			end
		end)
	end
end)

UserInputService.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement and draggingCircle then
		local delta = input.Position - dragStartCircle
		toggleCircle.Position = UDim2.new(startPosCircle.X.Scale, startPosCircle.X.Offset + delta.X, startPosCircle.Y.Scale, startPosCircle.Y.Offset + delta.Y)
	end
end)

-- 3. Janela Unificada (Menu Retangular com fundo 4100544209 e borda roxa)
local mainFrame = Instance.new("ImageLabel")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 360, 0, 190)
mainFrame.Position = UDim2.new(0.5, -180, 0.4, -95)
mainFrame.Image = "rbxassetid://4100544209"
mainFrame.ScaleType = Enum.ScaleType.Slice
mainFrame.SliceCenter = Rect.new(100, 100, 100, 100)
mainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
mainFrame.Active = true
mainFrame.Visible = true
mainFrame.Parent = screenGui

local uiCorner = Instance.new("UICorner")
uiCorner.CornerRadius = UDim.new(0, 12)
uiCorner.Parent = mainFrame

local uiStroke = Instance.new("UIStroke")
uiStroke.Thickness = 3
uiStroke.Color = Color3.fromRGB(138, 43, 228)
uiStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
uiStroke.Parent = mainFrame

-- Drag do Menu Principal
local dragging, dragStart, startPos
mainFrame.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = true
		dragStart = input.Position
		startPos = mainFrame.Position

		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				dragging = false
			end
		end)
	end
end)

UserInputService.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement and dragging then
		local delta = input.Position - dragStart
		mainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
	end
end)

local function toggleMenuOnly()
	mainFrame.Visible = not mainFrame.Visible
end

toggleCircle.MouseButton1Click:Connect(toggleMenuOnly)

-- ==================== LADO ESQUERDO: GALAXY FLY ====================

local flySection = Instance.new("Frame")
flySection.Name = "FlySection"
flySection.Size = UDim2.new(0.5, -5, 1, 0)
flySection.Position = UDim2.new(0, 0, 0, 0)
flySection.BackgroundTransparency = 1
flySection.Parent = mainFrame

local flyTitle = Instance.new("TextLabel")
flyTitle.Size = UDim2.new(1, 0, 0, 30)
flyTitle.Position = UDim2.new(0, 0, 0, 5)
flyTitle.BackgroundTransparency = 1
flyTitle.Text = "galaxy fly"
flyTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
flyTitle.TextSize = 20
flyTitle.Font = Enum.Font.FredokaOne
flyTitle.TextStrokeTransparency = 0
flyTitle.Parent = flySection

local flySpeedInput = Instance.new("TextBox")
flySpeedInput.Size = UDim2.new(0.85, 0, 0, 35)
flySpeedInput.Position = UDim2.new(0.075, 0, 0.25, 0)
flySpeedInput.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
flySpeedInput.BackgroundTransparency = 0.3
flySpeedInput.Text = "50" -- Reduzido para evitar detecção brusca de velocidade anômala
flySpeedInput.PlaceholderText = "Velocidade Fly"
flySpeedInput.TextColor3 = Color3.fromRGB(255, 255, 255)
flySpeedInput.TextSize = 14
flySpeedInput.Font = Enum.Font.SourceSansBold
flySpeedInput.Parent = flySection

local flyInputCorner = Instance.new("UICorner")
flyInputCorner.CornerRadius = UDim.new(0, 8)
flyInputCorner.Parent = flySpeedInput

local flyToggleButton = Instance.new("TextButton")
flyToggleButton.Size = UDim2.new(0.85, 0, 0, 45)
flyToggleButton.Position = UDim2.new(0.075, 0, 0.60, 0)
flyToggleButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
flyToggleButton.BackgroundTransparency = 0.2
flyToggleButton.Text = "FLY OFF (Q)"
flyToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
flyToggleButton.TextSize = 15
flyToggleButton.Font = Enum.Font.SourceSansBold
flyToggleButton.Parent = flySection

local flyBtnCorner = Instance.new("UICorner")
flyBtnCorner.CornerRadius = UDim.new(0, 8)
flyBtnCorner.Parent = flyToggleButton

-- ==================== LADO DIREITO: GALAXY VELOCIDADE ====================

local speedSection = Instance.new("Frame")
speedSection.Name = "SpeedSection"
speedSection.Size = UDim2.new(0.5, -5, 1, 0)
speedSection.Position = UDim2.new(0.5, 5, 0, 0)
speedSection.BackgroundTransparency = 1
speedSection.Parent = mainFrame

local speedTitle = Instance.new("TextLabel")
speedTitle.Size = UDim2.new(1, 0, 0, 30)
speedTitle.Position = UDim2.new(0, 0, 0, 5)
speedTitle.BackgroundTransparency = 1
speedTitle.Text = "galaxy velocidade"
speedTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
speedTitle.TextSize = 20
speedTitle.Font = Enum.Font.FredokaOne
speedTitle.TextStrokeTransparency = 0
speedTitle.Parent = speedSection

local walkSpeedInput = Instance.new("TextBox")
walkSpeedInput.Size = UDim2.new(0.85, 0, 0, 35)
walkSpeedInput.Position = UDim2.new(0.075, 0, 0.25, 0)
walkSpeedInput.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
walkSpeedInput.BackgroundTransparency = 0.3
walkSpeedInput.Text = "32" -- Reduzido para prevenir detecções automáticas por anti-cheats comuns (WalkSpeed alterado de forma segura)
walkSpeedInput.PlaceholderText = "Velocidade Correr"
walkSpeedInput.TextColor3 = Color3.fromRGB(255, 255, 255)
walkSpeedInput.TextSize = 14
walkSpeedInput.Font = Enum.Font.SourceSansBold
walkSpeedInput.Parent = speedSection

local walkInputCorner = Instance.new("UICorner")
walkInputCorner.CornerRadius = UDim.new(0, 8)
walkInputCorner.Parent = walkSpeedInput

local speedToggleButton = Instance.new("TextButton")
speedToggleButton.Size = UDim2.new(0.85, 0, 0, 45)
speedToggleButton.Position = UDim2.new(0.075, 0, 0.60, 0)
speedToggleButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
speedToggleButton.BackgroundTransparency = 0.2
speedToggleButton.Text = "SPEED OFF (E)"
speedToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
speedToggleButton.TextSize = 15
speedToggleButton.Font = Enum.Font.SourceSansBold
speedToggleButton.Parent = speedSection

local speedBtnCorner = Instance.new("UICorner")
speedBtnCorner.CornerRadius = UDim.new(0, 8)
speedBtnCorner.Parent = speedToggleButton

-- ==================== CONTROLE DO FLY (ANTI-KICK SEGURO) ====================

local flying = false
local flySpeed = 50
local renderConnectionFly
local keysPressed = {W = false, A = false, S = false, D = false}

flySpeedInput.FocusLost:Connect(function()
	local num = tonumber(flySpeedInput.Text)
	if num then
		-- Limita a velocidade máxima para evitar banimentos por teleporte/movimento impossível
		if num > 100 then num = 100 end
		flySpeed = num
		flySpeedInput.Text = tostring(flySpeed)
	else
		flySpeedInput.Text = tostring(flySpeed)
	end
end)

local function startFlying()
	local character = localPlayer.Character
	if not character then return end
	local hrp = character:FindFirstChild("HumanoidRootPart")
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if not hrp or not humanoid then return end

	renderConnectionFly = RunService.Heartbeat:Connect(function(deltaTime)
		if not flying or not hrp or not humanoid then return end

		local camCFrame = camera.CFrame
		local moveDir = Vector3.zero

		if keysPressed.W then moveDir = moveDir + camCFrame.LookVector end
		if keysPressed.S then moveDir = moveDir - camCFrame.LookVector end
		if keysPressed.A then moveDir = moveDir - camCFrame.RightVector end
		if keysPressed.D then moveDir = moveDir + camCFrame.RightVector end

		if moveDir.Magnitude > 0 then
			moveDir = moveDir.Unit
			-- Usa alteração fluida de posição baseada no CFrame com checagem de gravidade simulada para enganar checagens básicas
			hrp.CFrame = hrp.CFrame + (moveDir * (flySpeed * deltaTime))
			hrp.Velocity = Vector3.new(0, 1, 0) -- Evita valores de Velocity muito altos que geram flag de voo no servidor
		else
			hrp.Velocity = Vector3.zero
		end
	end)
end

local function stopFlying()
	flying = false
	if renderConnectionFly then
		renderConnectionFly:Disconnect()
		renderConnectionFly = nil
	end

	local character = localPlayer.Character
	if character then
		local hrp = character:FindFirstChild("HumanoidRootPart")
		if hrp then
			hrp.Velocity = Vector3.zero
		end
	end
end

local function toggleFly()
	flying = not flying

	if flying then
		flyToggleButton.Text = "FLY ON (Q)"
		flyToggleButton.BackgroundColor3 = Color3.fromRGB(46, 204, 113)
		startFlying()
	else
		flyToggleButton.Text = "FLY OFF (Q)"
		flyToggleButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
		stopFlying()
	end
end

flyToggleButton.MouseButton1Click:Connect(toggleFly)

-- ==================== CONTROLE DO SPEED (ANTI-KICK SEGURO) ====================

local customSpeedActive = false
local customWalkSpeed = 32

walkSpeedInput.FocusLost:Connect(function()
	local num = tonumber(walkSpeedInput.Text)
	if num then
		-- Limita o valor para evitar que o servidor detecte alteração abrupta no WalkSpeed nativo
		if num > 50 then num = 50 end
		customWalkSpeed = num
		walkSpeedInput.Text = tostring(customWalkSpeed)
	else
		walkSpeedInput.Text = tostring(customWalkSpeed)
	end
end)

local function toggleSpeed()
	customSpeedActive = not customSpeedActive

	local character = localPlayer.Character
	local humanoid = character and character:FindFirstChildOfClass("Humanoid")

	if customSpeedActive then
		speedToggleButton.Text = "SPEED ON (E)"
		speedToggleButton.BackgroundColor3 = Color3.fromRGB(46, 204, 113)

		if humanoid then
			humanoid.WalkSpeed = customWalkSpeed
		end
	else
		speedToggleButton.Text = "SPEED OFF (E)"
		speedToggleButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)

		if humanoid then
			humanoid.WalkSpeed = 16 -- Retorna ao padrão do Roblox
		end
	end
end

speedToggleButton.MouseButton1Click:Connect(toggleSpeed)

-- Atualiza o WalkSpeed caso o personagem morra e renasça com o speed ligado
localPlayer.CharacterAdded:Connect(function(newCharacter)
	local humanoid = newCharacter:WaitForChild("Humanoid", 5)
	if humanoid and customSpeedActive then
		humanoid.WalkSpeed = customWalkSpeed
	end
end)

-- ==================== TECLAS DE ATALHO ====================

UserInputService.InputBegan:Connect(function(input, gameProcessed)
	if gameProcessed then return end

	if input.KeyCode == Enum.KeyCode.Q then
		toggleFly()
	end

	if input.KeyCode == Enum.KeyCode.E then
		toggleSpeed()
	end

	if input.KeyCode == Enum.KeyCode.T then
		toggleMenuOnly()
	end

	if input.KeyCode == Enum.KeyCode.W then keysPressed.W = true end
	if input.KeyCode == Enum.KeyCode.A then keysPressed.A = true end
	if input.KeyCode == Enum.KeyCode.S then keysPressed.S = true end
	if input.KeyCode == Enum.KeyCode.D then keysPressed.D = true end
end)

UserInputService.InputEnded:Connect(function(input)
	if input.KeyCode == Enum.KeyCode.W then keysPressed.W = false end
	if input.KeyCode == Enum.KeyCode.A then keysPressed.A = false end
	if input.KeyCode == Enum.KeyCode.S then keysPressed.S = false end
	if input.KeyCode == Enum.KeyCode.D then keysPressed.D = false end
end)
