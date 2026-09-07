-- =========================================================================
--  PHANTOM HUB | VERSÃO CAOS TOTAL (MAIS FUNÇÕES FE)
-- =========================================================================

local LocalPlayer = game.Players.LocalPlayer
local RunService = game:GetService("RunService")

-- 1. Criação da Tela de Login/Verificação
local IntroGui = Instance.new("ScreenGui")
IntroGui.Name = "Phantom_Auth_Screen"
IntroGui.Parent = game.CoreGui

local BaseFrame = Instance.new("Frame")
BaseFrame.Size = UDim2.new(0, 350, 0, 220)
BaseFrame.Position = UDim2.new(0.4, 0, 0.35, 0)
BaseFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 20)
BaseFrame.Active = true
BaseFrame.Draggable = true
BaseFrame.Parent = IntroGui

local Corner = Instance.new("UICorner")
Corner.CornerRadius = UDim.new(0, 8)
Corner.Parent = BaseFrame

-- Título Principal
local TitleLabel = Instance.new("TextLabel")
TitleLabel.Size = UDim2.new(1, 0, 0, 40)
TitleLabel.Text = "PHANTOM HUB — LOGIN"
TitleLabel.TextColor3 = Color3.fromRGB(0, 170, 255)
TitleLabel.Font = Enum.Font.SourceSansBold
TitleLabel.TextSize = 16
TitleLabel.BackgroundTransparency = 1
TitleLabel.Parent = BaseFrame

-- Campo para Digitar a Chave (TextBox)
local KeyInput = Instance.new("TextBox")
KeyInput.Size = UDim2.new(1, -40, 0, 40)
KeyInput.Position = UDim2.new(0, 20, 0, 60)
KeyInput.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
KeyInput.Text = ""
KeyInput.PlaceholderText = "Digite a chave de acesso..."
KeyInput.TextColor3 = Color3.fromRGB(255, 255, 255)
KeyInput.PlaceholderColor3 = Color3.fromRGB(120, 120, 130)
KeyInput.Font = Enum.Font.SourceSans
KeyInput.TextSize = 15
KeyInput.Parent = BaseFrame

local InputCorner = Corner:Clone()
InputCorner.CornerRadius = UDim.new(0, 5)
InputCorner.Parent = KeyInput

-- Botão de Entrar
local CheckButton = Instance.new("TextButton")
CheckButton.Size = UDim2.new(1, -40, 0, 40)
CheckButton.Position = UDim2.new(0, 20, 0, 115)
CheckButton.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
CheckButton.Text = "Verificar Chave"
CheckButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CheckButton.Font = Enum.Font.SourceSansBold
CheckButton.TextSize = 15
CheckButton.Parent = BaseFrame

local BtnCorner = Corner:Clone()
BtnCorner.CornerRadius = UDim.new(0, 5)
BtnCorner.Parent = CheckButton

-- Texto de Status/Aviso
local StatusLabel = Instance.new("TextLabel")
StatusLabel.Size = UDim2.new(1, 0, 0, 30)
StatusLabel.Position = UDim2.new(0, 0, 0, 175)
StatusLabel.Text = "Chave padrão: CHAOS123"
StatusLabel.TextColor3 = Color3.fromRGB(150, 150, 150)
StatusLabel.Font = Enum.Font.SourceSansItalic
StatusLabel.TextSize = 13
StatusLabel.BackgroundTransparency = 1
StatusLabel.Parent = BaseFrame

-- =========================================================================
--  PAINEL PRINCIPAL COM TODAS AS FUNÇÕES (ABRE APÓS LOGIN)
-- =========================================================================
local function AbrirPainelPrincipal()
    local ScreenGui = Instance.new("ScreenGui")
    ScreenGui.Parent = game.CoreGui
    ScreenGui.Name = "PhantomClient_Base"

    local MainFrame = Instance.new("Frame")
    MainFrame.Parent = ScreenGui
    MainFrame.BackgroundColor3 = Color3.fromRGB(18, 18, 24)
    MainFrame.Position = UDim2.new(0.3, 0, 0.2, 0)
    MainFrame.Size = UDim2.new(0, 530, 0, 420) -- Painel maior para caber tudo
    MainFrame.Active = true
    MainFrame.Draggable = true
    
    local MainCorner = Corner:Clone()
    MainCorner.Parent = MainFrame

    -- Barra de Título do Painel Interno
    local TitleBar = Instance.new("Frame")
    TitleBar.Parent = MainFrame
    TitleBar.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
    TitleBar.Size = UDim2.new(1, 0, 0, 40)
    
    local BarCorner = Corner:Clone()
    BarCorner.Parent = TitleBar

    local Title = Instance.new("TextLabel")
    Title.Parent = TitleBar
    Title.Size = UDim2.new(1, -40, 1, 0)
    Title.Position = UDim2.new(0, 15, 0, 0)
    Title.Text = "PHANTOM HUB PRO v4.0 | BROOKHAVEN EDITION"
    Title.TextColor3 = Color3.fromRGB(0, 170, 255)
    Title.Font = Enum.Font.SourceSansBold
    Title.TextSize = 16
    Title.TextXAlignment = Enum.TextXAlignment.Left

    local Container = Instance.new("ScrollingFrame") -- Mudado para rolar se tiver muitas funções
    Container.Parent = MainFrame
    Container.BackgroundColor3 = Color3.fromRGB(18, 18, 24)
    Container.Position = UDim2.new(0, 0, 0, 40)
    Container.Size = UDim2.new(1, 0, 1, -40)
    Container.CanvasSize = UDim2.new(0, 0, 0, 480)
    Container.ScrollBarThickness = 6

    -- Função para criar os botões internos de forma organizada
    local function CriarBotao(texto, posY, callback)
        local Botao = Instance.new("TextButton")
        Botao.Parent = Container
        Botao.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
        Botao.Position = UDim2.new(0, 15, 0, posY)
        Botao.Size = UDim2.new(1, -36, 0, 38)
        Botao.Text = texto
        Botao.TextColor3 = Color3.fromRGB(245, 245, 245)
        Botao.Font = Enum.Font.SourceSansSemibold
        Botao.TextSize = 14
        
        local BtnInCorner = Corner:Clone()
        BtnInCorner.CornerRadius = UDim.new(0, 5)
        BtnInCorner.Parent = Botao

        Botao.MouseButton1Click:Connect(callback)
    end

    -- =========================================================================
    -- LISTA COMPLETA DE FUNÇÕES INJETADAS
    -- =========================================================================

    -- 1. Velocidade Avançada por Loop
    CriarBotao("⚡ Injetar Super Velocidade Constante (Speed 120)", 15, function()
        task.spawn(function()
            while task.wait(0.1) do
                if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
                    LocalPlayer.Character.Humanoid.WalkSpeed = 120
                end
            end
        end)
    end)

    -- 2. Teletransporte CFrame para o Cofre
    CriarBotao("🏡 Teleportar Dentro do Cofre do Banco (Posição Exata)", 65, function()
        if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
            LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-24.2, 11.8, 11.5)
        end
    end)

    -- 3. Injeção do Fly Script Estável
    CriarBotao("🕊️ Injetar Script de Voo Livre (Pressione E para Ativar)", 115, function()
        loadstring(game:HttpGet("https://githubusercontent.com"))()
    end)

    -- 4. Função Noclip (Atravessar qualquer parede do mapa)
    local noclipAtivo = false
    CriarBotao("🧱 Ativar / Desativar Atravessar Paredes (Noclip)", 165, function()
        noclipAtivo = not noclipAtivo
        if noclipAtivo then
            task.spawn(function()
                while noclipAtivo do
                    RunService.Stepped:Wait()
                    if LocalPlayer.Character then
                        for _, v in pairs(LocalPlayer.Character:GetDescendants()) do
                            if v:IsA("BasePart") then
                                v.CanCollide = false
                            end
                        end
                    end
                end
            end)
        end
    end)

    -- 5. Script Fling (Gira o corpo ultra rápido para empurrar os outros longe)
    CriarBotao("🌪️ Injetar Script Fling (Empurrar Outros Jogadores)", 215, function()
        loadstring(game:HttpGet("https://githubusercontent.com"))()
    end)

    -- 6. Injetar Script de Animações e Tamanho do Avatar Gigante
    CriarBotao("🧍 Injetar Menu de Tamanho de Avatar (Giga Gui)", 265, function()
        loadstring(game:HttpGet("https://githubusercontent.com"))()
    end)

    -- 7. Visão Noturna Geral do Mapa
    CriarBotao("👁️ Remover Escuridão da Noite (FullBright)", 315, function()
        game:GetService("Lighting").Ambient = Color3.fromRGB(255, 255, 255)
        game:GetService("Lighting").Brightness = 3
    end)

    -- 8. Respawn/Reset Rápido (Caso trave em algum lugar)
    CriarBotao("🔄 Resetar Personagem Rapidamente", 365, function()
        if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
            LocalPlayer.Character.Humanoid.Health = 0
        end
    end)

    -- Botão Fechar (Canto Superior Direito)
    local BotaoFechar = Instance.new("TextButton")
    BotaoFechar.Parent = TitleBar
    BotaoFechar.BackgroundColor3 = Color3.fromRGB(220, 60, 60)
    BotaoFechar.Position = UDim2.new(1, -30, 0, 8)
    BotaoFechar.Size = UDim2.new(0, 22, 0, 22)
    BotaoFechar.Text = "×"
    BotaoFechar.TextColor3 = Color3.fromRGB(255, 255, 255)
    BotaoFechar.TextSize = 18
    BotaoFechar.Font = Enum.Font.SourceSansBold
    
    local CloseCorner = Corner:Clone()
    CloseCorner.CornerRadius = UDim.new(0, 4)
    CloseCorner.Parent = BotaoFechar
    BotaoFechar.MouseButton1Click:Connect(function() ScreenGui:Destroy() end)
end

-- =========================================================================
--  EXECUÇÃO E VALIDAÇÃO DA CHAVE LOCAL
-- =========================================================================
CheckButton.MouseButton1Click:Connect(function()
    local chaveDigitada = KeyInput.Text
    local ChaveCorreta = "CHAOS123"

    StatusLabel.Text = "Injetando pacotes e funções..."
    StatusLabel.TextColor3 = Color3.fromRGB(0, 170, 255)
    task.wait(0.8)

    if chaveDigitada == ChaveCorreta then
        StatusLabel.Text = "Acesso Permitido! Carregando..."
        StatusLabel.TextColor3 = Color3.fromRGB(50, 220, 50)
        task.wait(0.5)
        IntroGui:Destroy()
        AbrirPainelPrincipal()
    else
        StatusLabel.Text = "Chave Errada! Digite CHAOS123 para testar."
        StatusLabel.TextColor3 = Color3.fromRGB(220, 50, 50)
    end
end)
