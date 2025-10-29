-- =====================================
-- Metódo Filipin - LocalScript OTIMIZADO
-- Coloque em: StarterPlayer > StarterPlayerScripts
-- =====================================

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Variável para o RemoteEvent (será conectado depois)
local teleportRemote = nil

-- Criar ScreenGui IMEDIATAMENTE
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "MetodoFilipinGui"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

-- =====================================
-- BOTÃO METÓDO (APARECE IMEDIATAMENTE)
-- =====================================
local metodoButton = Instance.new("TextButton")
metodoButton.Name = "MetodoButton"
metodoButton.Size = UDim2.new(0, 130, 0, 45)
metodoButton.Position = UDim2.new(0, 20, 0, 20)
metodoButton.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
metodoButton.Text = "Metódo"
metodoButton.TextSize = 18
metodoButton.TextColor3 = Color3.fromRGB(255, 255, 255)
metodoButton.Font = Enum.Font.GothamBold
metodoButton.BorderSizePixel = 0
metodoButton.ZIndex = 999
metodoButton.Parent = screenGui

local buttonCorner = Instance.new("UICorner")
buttonCorner.CornerRadius = UDim.new(0, 10)
buttonCorner.Parent = metodoButton

-- =====================================
-- FRAME GIGANTE
-- =====================================
local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 900, 0, 500)
mainFrame.Position = UDim2.new(0.5, -450, 0.5, -250)
mainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
mainFrame.BorderSizePixel = 3
mainFrame.BorderColor3 = Color3.fromRGB(0, 255, 255)
mainFrame.Visible = false
mainFrame.Parent = screenGui

local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 15)
mainCorner.Parent = mainFrame

-- =====================================
-- BOTÃO X (FECHAR)
-- =====================================
local closeButton = Instance.new("TextButton")
closeButton.Name = "CloseButton"
closeButton.Size = UDim2.new(0, 35, 0, 35)
closeButton.Position = UDim2.new(1, -45, 0, 10)
closeButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
closeButton.Text = "X"
closeButton.TextSize = 20
closeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
closeButton.Font = Enum.Font.GothamBold
closeButton.BorderSizePixel = 0
closeButton.Parent = mainFrame

local closeCorner = Instance.new("UICorner")
closeCorner.CornerRadius = UDim.new(0, 8)
closeCorner.Parent = closeButton

-- =====================================
-- TÍTULO
-- =====================================
local title = Instance.new("TextLabel")
title.Name = "Title"
title.Size = UDim2.new(1, 0, 0, 80)
title.Position = UDim2.new(0, 0, 0, 20)
title.BackgroundTransparency = 1
title.Text = "Metódo Filipin"
title.TextSize = 48
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.Font = Enum.Font.GothamBold
title.Parent = mainFrame

-- =====================================
-- CAMPO DE INPUT
-- =====================================
local inputBox = Instance.new("TextBox")
inputBox.Name = "InputBox"
inputBox.Size = UDim2.new(0, 680, 0, 50)
inputBox.Position = UDim2.new(0.5, -340, 0, 120)
inputBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
inputBox.PlaceholderText = "Cole o link do servidor aqui..."
inputBox.Text = ""
inputBox.TextSize = 16
inputBox.TextColor3 = Color3.fromRGB(255, 255, 255)
inputBox.Font = Enum.Font.Gotham
inputBox.ClearTextOnFocus = false
inputBox.Parent = mainFrame

local inputCorner = Instance.new("UICorner")
inputCorner.CornerRadius = UDim.new(0, 8)
inputCorner.Parent = inputBox

-- =====================================
-- BOTÕES: ENVIAR E CANCELAR
-- =====================================
local buttonContainer = Instance.new("Frame")
buttonContainer.Name = "ButtonContainer"
buttonContainer.Size = UDim2.new(0, 680, 0, 40)
buttonContainer.Position = UDim2.new(0.5, -340, 0, 185)
buttonContainer.BackgroundTransparency = 1
buttonContainer.Parent = mainFrame

local enviarButton = Instance.new("TextButton")
enviarButton.Name = "EnviarButton"
enviarButton.Size = UDim2.new(0.48, 0, 1, 0)
enviarButton.Position = UDim2.new(0, 0, 0, 0)
enviarButton.BackgroundColor3 = Color3.fromRGB(0, 200, 100)
enviarButton.Text = "Enviar"
enviarButton.TextSize = 16
enviarButton.TextColor3 = Color3.fromRGB(255, 255, 255)
enviarButton.Font = Enum.Font.GothamBold
enviarButton.BorderSizePixel = 0
enviarButton.Parent = buttonContainer

local enviarCorner = Instance.new("UICorner")
enviarCorner.CornerRadius = UDim.new(0, 10)
enviarCorner.Parent = enviarButton

local cancelarButton = Instance.new("TextButton")
cancelarButton.Name = "CancelarButton"
cancelarButton.Size = UDim2.new(0.48, 0, 1, 0)
cancelarButton.Position = UDim2.new(0.52, 0, 0, 0)
cancelarButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
cancelarButton.Text = "Cancelar"
cancelarButton.TextSize = 16
cancelarButton.TextColor3 = Color3.fromRGB(255, 255, 255)
cancelarButton.Font = Enum.Font.GothamBold
cancelarButton.BorderSizePixel = 0
cancelarButton.Parent = buttonContainer

local cancelarCorner = Instance.new("UICorner")
cancelarCorner.CornerRadius = UDim.new(0, 10)
cancelarCorner.Parent = cancelarButton

-- =====================================
-- ÁREA DE MENSAGENS
-- =====================================
local messageFrame = Instance.new("Frame")
messageFrame.Name = "MessageFrame"
messageFrame.Size = UDim2.new(0, 680, 0, 235)
messageFrame.Position = UDim2.new(0.5, -340, 0, 240)
messageFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
messageFrame.BorderSizePixel = 2
messageFrame.BorderColor3 = Color3.fromRGB(70, 70, 70)
messageFrame.Parent = mainFrame

local messageCorner = Instance.new("UICorner")
messageCorner.CornerRadius = UDim.new(0, 8)
messageCorner.Parent = messageFrame

local messageScroll = Instance.new("ScrollingFrame")
messageScroll.Name = "MessageScroll"
messageScroll.Size = UDim2.new(1, -10, 1, -70)
messageScroll.Position = UDim2.new(0, 5, 0, 5)
messageScroll.BackgroundTransparency = 1
messageScroll.BorderSizePixel = 0
messageScroll.ScrollBarThickness = 6
messageScroll.CanvasSize = UDim2.new(0, 0, 0, 0)
messageScroll.Parent = messageFrame

local messageList = Instance.new("UIListLayout")
messageList.Parent = messageScroll
messageList.SortOrder = Enum.SortOrder.LayoutOrder
messageList.Padding = UDim.new(0, 5)

local progressBar = Instance.new("Frame")
progressBar.Name = "ProgressBar"
progressBar.Size = UDim2.new(0.95, 0, 0, 25)
progressBar.Position = UDim2.new(0.025, 0, 1, -35)
progressBar.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
progressBar.Visible = false
progressBar.Parent = messageFrame

local progressCorner = Instance.new("UICorner")
progressCorner.CornerRadius = UDim.new(0, 12)
progressCorner.Parent = progressBar

local progressFill = Instance.new("Frame")
progressFill.Name = "ProgressFill"
progressFill.Size = UDim2.new(0, 0, 1, 0)
progressFill.BackgroundColor3 = Color3.fromRGB(0, 255, 255)
progressFill.BorderSizePixel = 0
progressFill.Parent = progressBar

local progressFillCorner = Instance.new("UICorner")
progressFillCorner.CornerRadius = UDim.new(0, 12)
progressFillCorner.Parent = progressFill

-- =====================================
-- VARIÁVEIS
-- =====================================
local isProcessing = false
local processConnection = nil
local playersFound = 0

-- =====================================
-- FUNÇÕES
-- =====================================

local function isValidRobloxLink(link)
	return string.match(link, "^https://www%.roblox%.com/share%?code=[a-f0-9]+&type=Server$") ~= nil
end

local function addMessage(text, color)
	local msg = Instance.new("TextLabel")
	msg.Size = UDim2.new(1, -10, 0, 25)
	msg.BackgroundTransparency = 1
	msg.Text = text
	msg.TextSize = 14
	msg.TextColor3 = color
	msg.Font = Enum.Font.Gotham
	msg.TextXAlignment = Enum.TextXAlignment.Left
	msg.Parent = messageScroll
	messageScroll.CanvasSize = UDim2.new(0, 0, 0, messageList.AbsoluteContentSize.Y)
end

local function clearMessages()
	for _, child in ipairs(messageScroll:GetChildren()) do
		if child:IsA("TextLabel") then
			child:Destroy()
		end
	end
	messageScroll.CanvasSize = UDim2.new(0, 0, 0, 0)
end

local function resetInterface()
	inputBox.Text = ""
	inputBox.TextEditable = true
	clearMessages()
	progressBar.Visible = false
	progressFill.Size = UDim2.new(0, 0, 1, 0)
	enviarButton.Visible = true
	cancelarButton.Visible = true
	isProcessing = false
	playersFound = 0
	if processConnection then
		processConnection:Disconnect()
		processConnection = nil
	end
end

local function closeAllFrames()
	mainFrame.Visible = false
	resetInterface()
end

local function processLink()
	local link = inputBox.Text
	
	if not isValidRobloxLink(link) then
		clearMessages()
		addMessage("Coloque um link válido!", Color3.fromRGB(255, 50, 50))
		progressBar.Visible = false
		return
	end
	
	isProcessing = true
	clearMessages()
	addMessage("Processando 0%", Color3.fromRGB(0, 255, 255))
	progressBar.Visible = true
	progressFill.Size = UDim2.new(0, 0, 1, 0)
	inputBox.TextEditable = false
	playersFound = 0
	
	-- Tentar enviar ao servidor
	if teleportRemote then
		pcall(function()
			teleportRemote:FireServer("StartSearch", link)
		end)
	else
		addMessage("⚠️ ServerScript não detectado!", Color3.fromRGB(255, 150, 0))
	end
	
	local duration = 30
	local startTime = tick()
	
	processConnection = game:GetService("RunService").Heartbeat:Connect(function()
		if not isProcessing then return end
		
		local elapsed = tick() - startTime
		local progress = math.min(elapsed / duration, 1)
		local percentage = math.floor(progress * 100)
		
		progressFill.Size = UDim2.new(progress, 0, 1, 0)
		
		local firstMsg = messageScroll:FindFirstChildOfClass("TextLabel")
		if firstMsg and percentage < 100 then
			firstMsg.Text = "Processando " .. percentage .. "%"
		elseif percentage >= 100 then
			if firstMsg then
				firstMsg.Text = "Concluído ✔️"
				firstMsg.TextColor3 = Color3.fromRGB(0, 255, 100)
			end
			isProcessing = false
			processConnection:Disconnect()
			
			wait(2)
			closeAllFrames()
		end
	end)
end

local function cancelProcess()
	if inputBox.Text ~= "" then
		resetInterface()
		if teleportRemote then
			pcall(function()
				teleportRemote:FireServer("CancelSearch")
			end)
		end
	end
end

-- =====================================
-- EVENTOS
-- =====================================

metodoButton.MouseButton1Click:Connect(function()
	mainFrame.Visible = true
end)

closeButton.MouseButton1Click:Connect(function()
	closeAllFrames()
	if teleportRemote then
		pcall(function()
			teleportRemote:FireServer("CancelSearch")
		end)
	end
end)

enviarButton.MouseButton1Click:Connect(function()
	processLink()
end)

cancelarButton.MouseButton1Click:Connect(function()
	cancelProcess()
end)

-- =====================================
-- CONECTAR AO REMOTEVENT (EM BACKGROUND)
-- =====================================
task.spawn(function()
	-- Tentar encontrar o RemoteEvent por até 30 segundos
	for i = 1, 30 do
		teleportRemote = ReplicatedStorage:FindFirstChild("MetodoFilipinRemote")
		if teleportRemote then
			print("✅ Conectado ao ServerScript!")
			
			-- Conectar eventos
			teleportRemote.OnClientEvent:Connect(function(action, data)
				if action == "PlayerFound" then
					playersFound = playersFound + 1
					addMessage("Script achou o jogador: " .. data, Color3.fromRGB(0, 255, 100))
				elseif action == "Error" then
					addMessage(data, Color3.fromRGB(255, 50, 50))
				end
			end)
			
			break
		end
		wait(1)
	end
	
	if not teleportRemote then
		warn("⚠️ ServerScript não encontrado! Interface funcionará mas teleporte não.")
	end
end)

print("✅ Método Filipin - Interface carregada!")

-- =====================================
-- Metódo Filipin - ServerScript
-- Coloque em: ServerScriptService
-- =====================================

local Players = game:GetService("Players")
local TeleportService = game:GetService("TeleportService")
local MessagingService = game:GetService("MessagingService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local PLACE_ID = 109983668079237  -- ID do jogo "Steal a Brainrot"
local MESSAGE_TOPIC = "MetodoFilipinTeleport"

-- Criar RemoteEvent
local teleportRemote = Instance.new("RemoteEvent")
teleportRemote.Name = "MetodoFilipinRemote"
teleportRemote.Parent = ReplicatedStorage

-- Tabela para controlar buscas ativas
local activeSearches = {}

-- =====================================
-- FUNÇÕES
-- =====================================

-- Extrair código do link
local function extractServerCode(link)
	local code = string.match(link, "code=([a-f0-9]+)")
	return code
end

-- Verificar se jogador está online no jogo
local function isPlayerOnlineInGame(playerName)
	for _, player in ipairs(Players:GetPlayers()) do
		if player.Name == playerName then
			return true
		end
	end
	return false
end

-- Processar mensagem de teleporte
local function onTeleportMessage(message)
	local data = message.Data
	
	if data.Action == "SearchPlayers" then
		-- Outro servidor está procurando jogadores
		local requesterId = data.RequesterId
		local serverCode = data.ServerCode
		local searchId = data.SearchId
		
		-- Não responder se for o próprio servidor que enviou
		if requesterId == game.JobId then
			return
		end
		
		-- Verificar se há jogadores online neste servidor
		local onlinePlayers = Players:GetPlayers()
		
		if #onlinePlayers > 0 then
			-- Enviar resposta com até 2 jogadores
			local playersToSend = {}
			for i = 1, math.min(2, #onlinePlayers) do
				table.insert(playersToSend, {
					Name = onlinePlayers[i].Name,
					UserId = onlinePlayers[i].UserId
				})
			end
			
			-- Enviar resposta
			pcall(function()
				MessagingService:PublishAsync(MESSAGE_TOPIC, {
					Action = "PlayersFound",
					SearchId = searchId,
					RequesterId = requesterId,
					Players = playersToSend,
					ServerCode = serverCode
				})
			end)
		end
		
	elseif data.Action == "PlayersFound" then
		-- Recebeu resposta com jogadores encontrados
		local searchId = data.SearchId
		local requesterId = data.RequesterId
		
		-- Verificar se esta busca pertence a este servidor
		if requesterId ~= game.JobId then
			return
		end
		
		local searchData = activeSearches[searchId]
		if not searchData then
			return
		end
		
		-- Adicionar jogadores encontrados
		for _, playerData in ipairs(data.Players) do
			if searchData.PlayersFound < 2 then
				table.insert(searchData.FoundPlayers, playerData)
				searchData.PlayersFound = searchData.PlayersFound + 1
				
				-- Notificar cliente
				if searchData.Requester and searchData.Requester.Parent then
					teleportRemote:FireClient(searchData.Requester, "PlayerFound", playerData.Name)
				end
				
				-- Se encontrou 2, parar busca
				if searchData.PlayersFound >= 2 then
					searchData.Completed = true
					break
				end
			end
		end
		
	elseif data.Action == "TeleportPlayers" then
		-- Ordem para teleportar jogadores
		local playersToTeleport = data.Players
		local serverCode = data.ServerCode
		
		-- Teleportar cada jogador
		for _, playerData in ipairs(playersToTeleport) do
			local player = Players:FindFirstChild(playerData.Name)
			if player then
				-- Teleportar usando o código do servidor
				pcall(function()
					local options = Instance.new("TeleportOptions")
					options.ServerInstanceId = serverCode
					TeleportService:TeleportAsync(PLACE_ID, {player}, options)
				end)
			end
		end
	end
end

-- Iniciar busca por jogadores
local function startPlayerSearch(requester, serverLink)
	local serverCode = extractServerCode(serverLink)
	
	if not serverCode then
		teleportRemote:FireClient(requester, "Error", "Código do servidor inválido!")
		return
	end
	
	-- Criar ID único para esta busca
	local searchId = game.JobId .. "_" .. tick()
	
	-- Registrar busca
	activeSearches[searchId] = {
		Requester = requester,
		ServerCode = serverCode,
		PlayersFound = 0,
		FoundPlayers = {},
		Completed = false,
		StartTime = tick()
	}
	
	-- Enviar mensagem para todos os servidores
	pcall(function()
		MessagingService:PublishAsync(MESSAGE_TOPIC, {
			Action = "SearchPlayers",
			RequesterId = game.JobId,
			ServerCode = serverCode,
			SearchId = searchId
		})
	end)
	
	-- Aguardar até encontrar 2 jogadores ou timeout (30 segundos)
	task.spawn(function()
		local maxWaitTime = 30
		local startTime = tick()
		
		while tick() - startTime < maxWaitTime do
			local searchData = activeSearches[searchId]
			
			if not searchData then
				break
			end
			
			if searchData.Completed or searchData.PlayersFound >= 2 then
				-- Encontrou os jogadores, aguardar processamento chegar em 100%
				wait(maxWaitTime - (tick() - startTime))
				
				-- Enviar ordem de teleporte
				if #searchData.FoundPlayers > 0 then
					pcall(function()
						MessagingService:PublishAsync(MESSAGE_TOPIC, {
							Action = "TeleportPlayers",
							Players = searchData.FoundPlayers,
							ServerCode = serverCode
						})
					end)
				end
				
				break
			end
			
			wait(1)
		end
		
		-- Limpar busca
		activeSearches[searchId] = nil
	end)
end

-- Cancelar busca
local function cancelSearch(requester)
	-- Remover todas as buscas deste jogador
	for searchId, searchData in pairs(activeSearches) do
		if searchData.Requester == requester then
			activeSearches[searchId] = nil
		end
	end
end

-- =====================================
-- EVENTOS
-- =====================================

-- Escutar mensagens de outros servidores
pcall(function()
	MessagingService:SubscribeAsync(MESSAGE_TOPIC, onTeleportMessage)
end)

-- Escutar requisições dos clientes
teleportRemote.OnServerEvent:Connect(function(player, action, data)
	if action == "StartSearch" then
		startPlayerSearch(player, data)
	elseif action == "CancelSearch" then
		cancelSearch(player)
	end
end)

print("✅ Método Filipin - ServerScript carregado!")
