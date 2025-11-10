-- LocalScript: TPAllMenu.lua
-- Autor: 7n / Lipe
-- Coloque em StarterPlayer > StarterPlayerScripts

local Players = game:GetService("Players")
local Lighting = game:GetService("Lighting")
local Workspace = game:GetService("Workspace")
local StarterGui = game:GetService("StarterGui")
local LocalPlayer = Players.LocalPlayer
local playerGui = LocalPlayer:WaitForChild("PlayerGui")

-- Função de notificação
local function notify(title, text, duration)
	pcall(function()
		StarterGui:SetCore("SendNotification", {
			Title = title or "Aviso";
			Text = text or "";
			Duration = duration or 3;
		})
	end)
end

-- Criar ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "TPAllGui"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

-- Botão principal (abrir/fechar menu)
local openButton = Instance.new("TextButton")
openButton.Name = "TPAllButton"
openButton.Size = UDim2.new(0, 140, 0, 40)
openButton.Position = UDim2.new(0, 20, 0, 100)
openButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
openButton.BorderSizePixel = 0
openButton.Text = "TP/All"
openButton.TextColor3 = Color3.fromRGB(255, 255, 255)
openButton.Font = Enum.Font.SourceSansBold
openButton.TextSize = 22
openButton.Parent = screenGui

-- Menu principal
local menu = Instance.new("Frame")
menu.Name = "TPAllMenu"
menu.Size = UDim2.new(0, 260, 0, 230)
menu.Position = UDim2.new(0, 20, 0, 150)
menu.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
menu.BorderSizePixel = 0
menu.Visible = false
menu.Active = true
menu.Draggable = true
menu.Parent = screenGui

-- Função para criar botões
local function makeButton(yPos, text)
	local button = Instance.new("TextButton")
	button.Size = UDim2.new(1, -20, 0, 40)
	button.Position = UDim2.new(0, 10, 0, yPos)
	button.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
	button.BorderSizePixel = 1
	button.BorderColor3 = Color3.fromRGB(40, 40, 40)
	button.Text = text
	button.TextColor3 = Color3.fromRGB(255, 255, 255)
	button.Font = Enum.Font.SourceSansBold
	button.TextSize = 18
	button.Parent = menu
	return button
end

-- Criar botões
local salvarBtn = makeButton(10, "Salvar Posicao")
local tpBtn = makeButton(60, "Teleportar")
local antiLagBtn = makeButton(110, "Ativar Anti Lag")

-- Texto de crédito
local creditLabel = Instance.new("TextLabel")
creditLabel.Size = UDim2.new(1, -20, 0, 60)
creditLabel.Position = UDim2.new(0, 10, 0, 160)
creditLabel.BackgroundTransparency = 1
creditLabel.Text = "Agradeca ao 7n por estar passando gratis"
creditLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
creditLabel.Font = Enum.Font.SourceSansBold
creditLabel.TextWrapped = true
creditLabel.TextSize = 16
creditLabel.Parent = menu

-- Variável de posição salva
local savedPosition = nil

-- Ação: Salvar posição
salvarBtn.MouseButton1Click:Connect(function()
	if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
		savedPosition = LocalPlayer.Character.HumanoidRootPart.Position
		notify("Lipe Script", "Posicao salva com sucesso!", 3)
	else
		notify("Erro", "Personagem nao encontrado!", 3)
	end
end)

-- Ação: Teleportar
tpBtn.MouseButton1Click:Connect(function()
	if not savedPosition then
		notify("Erro", "Nenhuma posicao salva ainda!", 3)
		return
	end

	local hrp = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
	if hrp then
		hrp.CFrame = CFrame.new(savedPosition)
		notify("Lipe Script", "Teleportado com sucesso!", 3)
	else
		notify("Erro", "Nao foi possivel teleportar!", 3)
	end
end)

-- Ação: Anti Lag
antiLagBtn.MouseButton1Click:Connect(function()
	notify("Lipe Script", "Ativando Anti Lag...", 2)
	
	-- Remover efeitos visuais
	for _, obj in pairs(Lighting:GetChildren()) do
		if obj:IsA("BloomEffect") or obj:IsA("BlurEffect") or obj:IsA("ColorCorrectionEffect") or obj:IsA("SunRaysEffect") or obj:IsA("DepthOfFieldEffect") or obj:IsA("Atmosphere") then
			obj:Destroy()
		end
	end

	-- Otimizar o jogo removendo partes desnecessárias
	for _, obj in pairs(Workspace:GetDescendants()) do
		if obj:IsA("ParticleEmitter") or obj:IsA("Trail") or obj:IsA("Smoke") or obj:IsA("Fire") or obj:IsA("Sparkles") then
			obj.Enabled = false
		end
	end

	-- Desativar sombras
	Lighting.GlobalShadows = false
	Lighting.FogEnd = 100000
	settings().Rendering.QualityLevel = Enum.QualityLevel.Level01

	notify("Lipe Script", "Anti Lag ativado e jogo otimizado!", 3)
end)

-- Abrir / Fechar menu
openButton.MouseButton1Click:Connect(function()
	menu.Visible = not menu.Visible
end)
