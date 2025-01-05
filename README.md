-- Criando a interface principal
local player = game.Players.LocalPlayer
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = player.PlayerGui

-- Criando o botão principal movível
local mainButton = Instance.new("TextButton")
mainButton.Size = UDim2.new(0, 200, 0, 50)
mainButton.Position = UDim2.new(0.1, 0, 0.1, 0)
mainButton.Text = "Angel Hub"
mainButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
mainButton.TextColor3 = Color3.fromRGB(0, 0, 0)
mainButton.Parent = screenGui

-- Tornar o botão movível
local dragging = false
local dragStart, startPos

mainButton.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = mainButton.Position
    end
end)

mainButton.InputChanged:Connect(function(input)
    if dragging and input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        local delta = input.Position - dragStart
        mainButton.Position = UDim2.new(
            startPos.X.Scale,
            startPos.X.Offset + delta.X,
            startPos.Y.Scale,
            startPos.Y.Offset + delta.Y
        )
    end
end)

mainButton.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = false
    end
end)

-- Criando a biblioteca de scripts
mainButton.MouseButton1Click:Connect(function()
    local libraryFrame = Instance.new("Frame")
    libraryFrame.Size = UDim2.new(0, 600, 0, 450)
    libraryFrame.Position = UDim2.new(0.5, -300, 0.5, -200)
    libraryFrame.BackgroundColor3 = Color3.fromRGB(200, 200, 200)
    libraryFrame.Parent = screenGui

    -- Tornar a biblioteca movível
    local draggingLibrary = false
    local libraryDragStart, libraryStartPos

    libraryFrame.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            draggingLibrary = true
            libraryDragStart = input.Position
            libraryStartPos = libraryFrame.Position
        end
    end)

    libraryFrame.InputChanged:Connect(function(input)
        if draggingLibrary and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
            local delta = input.Position - libraryDragStart
            libraryFrame.Position = UDim2.new(
                libraryStartPos.X.Scale,
                libraryStartPos.X.Offset + delta.X,
                libraryStartPos.Y.Scale,
                libraryStartPos.Y.Offset + delta.Y
            )
        end
    end)

    libraryFrame.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            draggingLibrary = false
        end
    end)

    -- Título da biblioteca
    local title = Instance.new("TextLabel")
    title.Size = UDim2.new(1, 0, 0, 50)
    title.Text = "Biblioteca de Scripts"
    title.TextSize = 20
    title.TextColor3 = Color3.fromRGB(0, 0, 0)
    title.BackgroundColor3 = Color3.fromRGB(150, 150, 150)
    title.Parent = libraryFrame

    -- Botão de fechar
    local closeButton = Instance.new("TextButton")
    closeButton.Size = UDim2.new(0, 30, 0, 30)
    closeButton.Position = UDim2.new(1, -35, 0, 10)
    closeButton.Text = "X"
    closeButton.TextSize = 20
    closeButton.TextColor3 = Color3.fromRGB(255, 0, 0)
    closeButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    closeButton.Parent = libraryFrame

    closeButton.MouseButton1Click:Connect(function()
        libraryFrame:Destroy()
    end)

    -- Criar a lista de scripts com rolagem para a primeira biblioteca (scripts antigos)
    local scriptList1 = Instance.new("ScrollingFrame")
    scriptList1.Size = UDim2.new(0.5, -10, 1, -50)
    scriptList1.Position = UDim2.new(0, 5, 0, 50)
    scriptList1.CanvasSize = UDim2.new(0, 0, 0, 400)
    scriptList1.ScrollBarThickness = 12
    scriptList1.BackgroundColor3 = Color3.fromRGB(240, 240, 240)
    scriptList1.Parent = libraryFrame

    -- Criar a lista de scripts com rolagem para a segunda biblioteca (novos scripts)
    local scriptList2 = Instance.new("ScrollingFrame")
    scriptList2.Size = UDim2.new(0.5, -10, 1, -50)
    scriptList2.Position = UDim2.new(0.5, 5, 0, 50)
    scriptList2.CanvasSize = UDim2.new(0, 0, 0, 400)
    scriptList2.ScrollBarThickness = 12
    scriptList2.BackgroundColor3 = Color3.fromRGB(240, 240, 240)
    scriptList2.Parent = libraryFrame

    -- Títulos das bibliotecas
    local title1 = Instance.new("TextLabel")
    title1.Size = UDim2.new(1, 0, 0, 50)
    title1.Text = "Scripts Antigos"
    title1.TextSize = 18
    title1.TextColor3 = Color3.fromRGB(0, 0, 0)
    title1.BackgroundColor3 = Color3.fromRGB(200, 200, 200)
    title1.Parent = scriptList1

    local title2 = Instance.new("TextLabel")
    title2.Size = UDim2.new(1, 0, 0, 50)
    title2.Text = "Novos Scripts"
    title2.TextSize = 18
    title2.TextColor3 = Color3.fromRGB(0, 0, 0)
    title2.BackgroundColor3 = Color3.fromRGB(200, 200, 200)
    title2.Parent = scriptList2

    -- Botões da primeira biblioteca (scripts antigos)
    local infiniteYieldButton = Instance.new("TextButton")
    infiniteYieldButton.Size = UDim2.new(1, -10, 0, 50)
    infiniteYieldButton.Position = UDim2.new(0, 5, 0, 60)
    infiniteYieldButton.Text = "Infinite Yield"
    infiniteYieldButton.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    infiniteYieldButton.TextColor3 = Color3.fromRGB(0, 0, 0)
    infiniteYieldButton.Parent = scriptList1

    infiniteYieldButton.MouseButton1Click:Connect(function()
        -- Código do script Infinite Yield
        loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()
    end)

    local raelHubButton = Instance.new("TextButton")
    raelHubButton.Size = UDim2.new(1, -10, 0, 50)
    raelHubButton.Position = UDim2.new(0, 5, 0, 115)
    raelHubButton.Text = "Rael Hub"
    raelHubButton.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    raelHubButton.TextColor3 = Color3.fromRGB(0, 0, 0)
    raelHubButton.Parent = scriptList1

    raelHubButton.MouseButton1Click:Connect(function()
        -- Código do script Rael Hub
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Laelmano24/Rael-Hub/main/main.txt"))()
    end)

    local ghostHubButton = Instance.new("TextButton")
    ghostHubButton.Size = UDim2.new(1, -10, 0, 50)
    ghostHubButton.Position = UDim2.new(0, 5, 0, 170)
    ghostHubButton.Text = "Ghost Hub"
    ghostHubButton.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    ghostHubButton.TextColor3 = Color3.fromRGB(0, 0, 0)
    ghostHubButton.Parent = scriptList1

    ghostHubButton.MouseButton1Click:Connect(function()
        -- Código do script Ghost Hub
        loadstring(game:HttpGet('https://raw.githubusercontent.com/GhostPlayer352/Test4/main/GhostHub'))()
    end)

    -- Touch Speed (adicionando toques duplos na seção de Scripts Antigos)
    local touchSpeedButton = Instance.new("TextButton")
    touchSpeedButton.Size = UDim2.new(1, -10, 0, 50)
    touchSpeedButton.Position = UDim2.new(0, 5, 0, 225)
    touchSpeedButton.Text = "Touch Speed"
    touchSpeedButton.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    touchSpeedButton.TextColor3 = Color3.fromRGB(0, 0, 0)
    touchSpeedButton.Parent = scriptList1

    touchSpeedButton.MouseButton1Click:Connect(function()
        -- Código do script Touch Speed (detecção de toques duplos)
        local lastTouchTime = 0
        game:GetService("UserInputService").InputBegan:Connect(function(input, gameProcessed)
            if gameProcessed then return end
            if input.UserInputType == Enum.UserInputType.Touch then
                local currentTime = tick()
                if currentTime - lastTouchTime <= 0.5 then
                    -- Aumentar a velocidade do jogador
                    player.Character.Humanoid.WalkSpeed = 300
                end
                lastTouchTime = currentTime
            end
        end)
    end)

    -- Fê Emotes (corrigido)
    local feEmotesButton = Instance.new("TextButton")
    feEmotesButton.Size = UDim2.new(1, -10, 0, 50)
    feEmotesButton.Position = UDim2.new(0, 5, 0, 280)
    feEmotesButton.Text = "Fê Emotes"
    feEmotesButton.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    feEmotesButton.TextColor3 = Color3.fromRGB(0, 0, 0)
    feEmotesButton.Parent = scriptList1

    feEmotesButton.MouseButton1Click:Connect(function()
        -- Código do script Fê Emotes
        loadstring(game:HttpGet("https://scriptblox.com/raw/Brookhaven-RP-all-emotes-6849"))()
    end)

    -- Adicionando scripts novos (na segunda biblioteca)
    local rochipsHubButton = Instance.new("TextButton")
    rochipsHubButton.Size = UDim2.new(1, -10, 0, 50)
    rochipsHubButton.Position = UDim2.new(0, 5, 0, 60)
    rochipsHubButton.Text = "Rochips Hub"
    rochipsHubButton.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    rochipsHubButton.TextColor3 = Color3.fromRGB(0, 0, 0)
    rochipsHubButton.Parent = scriptList2

    rochipsHubButton.MouseButton1Click:Connect(function()
        -- Código do script Rochips Hub
        loadstring(game:HttpGet("https://raw.githubusercontent.com/rochips/rochips-hub/master/main.lua"))()
    end)

    local namelessAdminButton = Instance.new("TextButton")
    namelessAdminButton.Size = UDim2.new(1, -10, 0, 50)
    namelessAdminButton.Position = UDim2.new(0, 5, 0, 115)
    namelessAdminButton.Text = "Nameless Admin"
    namelessAdminButton.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    namelessAdminButton.TextColor3 = Color3.fromRGB(0, 0, 0)
    namelessAdminButton.Parent = scriptList2

    namelessAdminButton.MouseButton1Click:Connect(function()
        -- Código do script Nameless Admin
        loadstring(game:HttpGet("https://raw.githubusercontent.com/roshiie/Nameless-Admin/main/source.lua"))()
    end)

    local sanderXButton = Instance.new("TextButton")
    sanderXButton.Size = UDim2.new(1, -10, 0, 50)
    sanderXButton.Position = UDim2.new(0, 5, 0, 170)
    sanderXButton.Text = "Sander X"
    sanderXButton.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
    sanderXButton.TextColor3 = Color3.fromRGB(0, 0, 0)
    sanderXButton.Parent = scriptList2

    sanderXButton.MouseButton1Click:Connect(function()
        -- Código do script Sander X
        loadstring(game:HttpGet('https://raw.githubusercontent.com/kigredns/SanderXV4.2.2/refs/heads/main/New.lua'))()
    end)
end)
