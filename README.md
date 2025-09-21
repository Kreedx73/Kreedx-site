-- Painel KreedxMD - Roxo, emoji 🐢, otimização real, arrastável, remove árvores

local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "KreedxMD_PAINEL"

-- Main frame (grande, gradiente roxo, arrastável)
local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0,540,0,420)
frame.Position = UDim2.new(0.5,-270,0.5,-210)
frame.BackgroundColor3 = Color3.fromRGB(50,20,80)
frame.BackgroundTransparency = 0.15
frame.Active = true
frame.Draggable = true
frame.ZIndex = 10

-- Roxo gradiente top-bottom
local grad = Instance.new("UIGradient", frame)
grad.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(110, 60, 170)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(30, 10, 40))
}
grad.Rotation = 90

-- TopBar
local topBar = Instance.new("Frame", frame)
topBar.Size = UDim2.new(1,0,0,62)
topBar.Position = UDim2.new(0,0,0,0)
topBar.BackgroundColor3 = Color3.fromRGB(32,16,48)
topBar.BackgroundTransparency = 0.22
topBar.ZIndex = 11

-- Título
local title = Instance.new("TextLabel", topBar)
title.Text = "KreedxMD"
title.Font = Enum.Font.GothamSemibold
title.TextColor3 = Color3.fromRGB(230,200,255)
title.BackgroundTransparency = 1
title.Size = UDim2.new(1,0,1,0)
title.TextSize = 36
title.ZIndex = 12

-- Botões X e -
local xBtn = Instance.new("TextButton", topBar)
xBtn.Text = "X"
xBtn.Font = Enum.Font.GothamBold
xBtn.TextColor3 = Color3.new(1,0.2,0.5)
xBtn.BackgroundColor3 = Color3.fromRGB(60,20,60)
xBtn.Size = UDim2.new(0,38,0,38)
xBtn.Position = UDim2.new(1, -54, 0, 12)
xBtn.TextSize = 26
xBtn.ZIndex = 13
xBtn.AutoButtonColor = false

local minusBtn = Instance.new("TextButton", topBar)
minusBtn.Text = "-"
minusBtn.Font = Enum.Font.GothamBold
minusBtn.TextColor3 = Color3.fromRGB(230,200,255)
minusBtn.BackgroundColor3 = Color3.fromRGB(60,20,60)
minusBtn.Size = UDim2.new(0,38,0,38)
minusBtn.Position = UDim2.new(1, -104, 0, 12)
minusBtn.TextSize = 26
minusBtn.ZIndex = 13
minusBtn.AutoButtonColor = false

-- Hover efeito botões
xBtn.MouseEnter:Connect(function() xBtn.BackgroundColor3 = Color3.fromRGB(120,40,90) end)
xBtn.MouseLeave:Connect(function() xBtn.BackgroundColor3 = Color3.fromRGB(60,20,60) end)
minusBtn.MouseEnter:Connect(function() minusBtn.BackgroundColor3 = Color3.fromRGB(120,40,90) end)
minusBtn.MouseLeave:Connect(function() minusBtn.BackgroundColor3 = Color3.fromRGB(60,20,60) end)

-- Área de categorias (colunas, fácil expansão)
local categorias = {
    {nome="Otimização", btnText="Otimização: OFF"}
    -- Adicione mais categorias aqui!
}

local catFrame = Instance.new("Frame", frame)
catFrame.Size = UDim2.new(0.31,0,1,-72)
catFrame.Position = UDim2.new(0,20,0,70)
catFrame.BackgroundColor3 = Color3.fromRGB(35,12,55)
catFrame.BackgroundTransparency = 0.45
catFrame.ZIndex = 12

local catGrad = Instance.new("UIGradient", catFrame)
catGrad.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(70, 20, 120)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(40, 20, 50))
}
catGrad.Rotation = 90

local catTitle = Instance.new("TextLabel", catFrame)
catTitle.Text = "Categorias"
catTitle.Font = Enum.Font.GothamBold
catTitle.TextColor3 = Color3.fromRGB(200,180,255)
catTitle.BackgroundTransparency = 1
catTitle.Size = UDim2.new(1,0,0,36)
catTitle.Position = UDim2.new(0,0,0,0)
catTitle.TextSize = 20
catTitle.ZIndex = 13

local catBtns = {}
local function renderCategorias()
    for _,btn in pairs(catBtns) do btn:Destroy() end
    catBtns = {}
    local y = 42
    for i,cat in ipairs(categorias) do
        local btn = Instance.new("TextButton", catFrame)
        btn.Text = cat.nome
        btn.Font = Enum.Font.Gotham
        btn.TextColor3 = Color3.fromRGB(220,200,255)
        btn.BackgroundColor3 = Color3.fromRGB(60,20,80)
        btn.BackgroundTransparency = 0.06
        btn.Size = UDim2.new(0.9,0,0,34)
        btn.Position = UDim2.new(0.05,0,0,y)
        btn.TextSize = 18
        btn.ZIndex = 14
        btn.AutoButtonColor = false
        btn.MouseEnter:Connect(function() btn.BackgroundColor3 = Color3.fromRGB(120,40,160) end)
        btn.MouseLeave:Connect(function() btn.BackgroundColor3 = Color3.fromRGB(60,20,80) end)
        table.insert(catBtns,btn)
        y = y+38
    end
end
renderCategorias()

-- Área de comando/ação da categoria (pode expandir para cada categoria)
local cmdFrame = Instance.new("Frame", frame)
cmdFrame.Size = UDim2.new(0.61,0,1,-72)
cmdFrame.Position = UDim2.new(0.35,0,0,70)
cmdFrame.BackgroundColor3 = Color3.fromRGB(20,8,20)
cmdFrame.BackgroundTransparency = 0.55
cmdFrame.ZIndex = 12

local otimBtn = Instance.new("TextButton", cmdFrame)
otimBtn.Text = "Otimização: OFF"
otimBtn.Font = Enum.Font.GothamBold
otimBtn.TextColor3 = Color3.fromRGB(240,220,255)
otimBtn.BackgroundColor3 = Color3.fromRGB(80,40,120)
otimBtn.Position = UDim2.new(0.5,-120,0.05,30)
otimBtn.Size = UDim2.new(0,240,0,54)
otimBtn.TextSize = 22
otimBtn.ZIndex = 13
otimBtn.AutoButtonColor = false
otimBtn.MouseEnter:Connect(function() otimBtn.BackgroundColor3 = Color3.fromRGB(140,60,180) end)
otimBtn.MouseLeave:Connect(function() otimBtn.BackgroundColor3 = Color3.fromRGB(80,40,120) end)

local status = Instance.new("TextLabel", frame)
status.Position = UDim2.new(0,0,1,-32)
status.Size = UDim2.new(1,0,0,32)
status.Font = Enum.Font.Gotham
status.TextSize = 17
status.TextColor3 = Color3.fromRGB(220,180,255)
status.BackgroundTransparency = 1
status.ZIndex = 12
status.Text = "Pronto!"

-- Emoji Turtle minimizado
local turtleBtn = Instance.new("TextButton", gui)
turtleBtn.Text = "🐢"
turtleBtn.Font = Enum.Font.GothamBold
turtleBtn.TextSize = 48
turtleBtn.Size = UDim2.new(0,60,0,60)
turtleBtn.BackgroundColor3 = Color3.fromRGB(80,40,120)
turtleBtn.Position = UDim2.new(0,40,0,80)
turtleBtn.Visible = false
turtleBtn.ZIndex = 100
turtleBtn.Active = true
turtleBtn.Draggable = true

-- Otimização REAL + REMOVER ÁRVORES
local otimizado = false
local removedObjects = {}
local removedTrees = {}

local function otimizarJogo()
    local lighting = game:GetService("Lighting")
    local terrain = workspace:FindFirstChildOfClass("Terrain")
    lighting.GlobalShadows = false
    lighting.FogEnd = 100000
    lighting.Brightness = 1
    lighting.OutdoorAmbient = Color3.new(1,1,1)
    lighting.Ambient = Color3.new(1,1,1)
    for _,v in pairs(lighting:GetChildren()) do
        if v:IsA("PostEffect") then v:Destroy() end
    end
    for _,obj in pairs(workspace:GetDescendants()) do
        if obj:IsA("Decal") or obj:IsA("Texture") then
            if not removedObjects[obj] then
                removedObjects[obj] = obj.Transparency
                obj.Transparency = 1
            end
        end
        if obj:IsA("ParticleEmitter") or obj:IsA("Trail") or obj:IsA("Smoke") or obj:IsA("Fire") or obj:IsA("Explosion") then
            if not removedObjects[obj] then
                removedObjects[obj] = obj.Enabled
                obj.Enabled = false
            end
        end
    end
    if terrain then
        terrain.WaterWaveSize = 0
        terrain.WaterWaveSpeed = 0
        terrain.WaterReflectance = 0
        terrain.WaterTransparency = 1
    end
    -- Remover todas as árvores do mapa
    for _,obj in pairs(workspace:GetDescendants()) do
        if obj:IsA("Model") and obj.Parent ~= nil then
            local nameLower = string.lower(obj.Name)
            if nameLower:find("arvore") or nameLower:find("tree") then
                if not removedTrees[obj] then
                    removedTrees[obj] = obj.Parent
                    obj.Parent = nil -- Remove do mapa
                end
            end
        end
    end
    status.Text = "Otimização máxima ativada! Árvores removidas!"
end

local function restaurarJogo()
    for obj,val in pairs(removedObjects) do
        if obj:IsA("Decal") or obj:IsA("Texture") then
            obj.Transparency = val
        elseif obj:IsA("ParticleEmitter") or obj:IsA("Trail") or obj:IsA("Smoke") or obj:IsA("Fire") or obj:IsA("Explosion") then
            obj.Enabled = val
        end
    end
    removedObjects = {}
    -- Restaurar árvores (se possível)
    for obj,parent in pairs(removedTrees) do
        if obj.Parent == nil then
            obj.Parent = parent
        end
    end
    removedTrees = {}
    local lighting = game:GetService("Lighting")
    lighting.GlobalShadows = true
    lighting.FogEnd = 500
    lighting.Brightness = 2
    lighting.OutdoorAmbient = Color3.new(0.5,0.5,0.5)
    lighting.Ambient = Color3.new(0.5,0.5,0.5)
    status.Text = "Otimização desativada. Árvores restauradas!"
end

otimBtn.MouseButton1Click:Connect(function()
    otimizado = not otimizado
    if otimizado then
        otimBtn.Text = "Otimização: ON"
        otimBtn.BackgroundColor3 = Color3.fromRGB(60,120,80)
        otimizarJogo()
    else
        otimBtn.Text = "Otimização: OFF"
        otimBtn.BackgroundColor3 = Color3.fromRGB(80,40,120)
        restaurarJogo()
    end
end)

-- Minimizar para emoji 🐢
minusBtn.MouseButton1Click:Connect(function()
    frame.Visible = false
    turtleBtn.Visible = true
end)
turtleBtn.MouseButton1Click:Connect(function()
    frame.Visible = true
    turtleBtn.Visible = false
end)

-- Fechar painel (X)
xBtn.MouseButton1Click:Connect(function()
    gui:Destroy()
end)

-- Fim do painel KreedxMD roxo, bonito, otimização real, remove árvores!
