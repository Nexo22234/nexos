-- Кирилл negr Hub v1.0
-- Loadstring: loadstring(game:HttpGet("https://raw.githubusercontent.com/ВАШ_АККАУНТ/РЕПОЗИТОРИЙ/main/kirill_negr_hub.lua"))()

return function()
    --===[ НАСТРОЙКИ ]===--
    local Settings = {
        ClickTP = {Keybind = Enum.UserInputType.MouseButton1}, -- ЛКМ
        AimLock = {
            Keybind = Enum.UserInputType.MouseButton2, -- ПКМ
            Smoothness = 0.15,
            TargetPart = "Head" -- Head/HumanoidRootPart
        },
        Fly = {Speed = 50, UpKey = Enum.KeyCode.W, DownKey = Enum.KeyCode.S},
        SpeedHack = {Default = 16, Min = 16, Max = 100},
        ESP = {
            BoxColor = Color3.fromRGB(255, 50, 50),
            TextColor = Color3.fromRGB(255, 255, 255),
            BoxSize = Vector3.new(3, 5, 1),
            BoxTransparency = 0.7
        }
    }

    --===[ СЕРВИСЫ ]===--
    local Players = game:GetService("Players")
    local RunService = game:GetService("RunService")
    local UserInputService = game:GetService("UserInputService")
    local Lighting = game:GetService("Lighting")
    local LocalPlayer = Players.LocalPlayer
    local Camera = workspace.CurrentCamera

    --===[ GUI ]===--
    local KirillNegrHub = Instance.new("ScreenGui")
    KirillNegrHub.Name = "KirillNegrHub"
    KirillNegrHub.Parent = game:GetService("CoreGui")

    -- Главное окно
    local MainFrame = Instance.new("Frame")
    MainFrame.Size = UDim2.new(0.25, 0, 0.5, 0)
    MainFrame.Position = UDim2.new(0.05, 0, 0.25, 0)
    MainFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 30)
    MainFrame.BackgroundTransparency = 0.15
    MainFrame.BorderSizePixel = 0
    MainFrame.Active = true
    MainFrame.Draggable = true
    MainFrame.Parent = KirillNegrHub

    -- Заголовок
    local Title = Instance.new("TextLabel")
    Title.Size = UDim2.new(1, 0, 0.08, 0)
    Title.Position = UDim2.new(0, 0, 0, 0)
    Title.Text = "Кирилл negr Hub"
    Title.TextColor3 = Color3.fromRGB(255, 50, 50)
    Title.BackgroundTransparency = 1
    Title.Font = Enum.Font.SourceSansBold
    Title.TextSize = 22
    Title.Parent = MainFrame

    -- Разделитель
    local Divider = Instance.new("Frame")
    Divider.Size = UDim2.new(1, 0, 0, 1)
    Divider.Position = UDim2.new(0, 0, 0.08, 0)
    Divider.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
    Divider.BorderSizePixel = 0
    Divider.Parent = MainFrame

    -- Контейнер кнопок
    local ButtonsFrame = Instance.new("Frame")
    ButtonsFrame.Size = UDim2.new(1, -10, 0.9, -10)
    ButtonsFrame.Position = UDim2.new(0, 5, 0.1, 5)
    ButtonsFrame.BackgroundTransparency = 1
    ButtonsFrame.Parent = MainFrame

    -- Click Teleport
    local ClickTPToggle = Instance.new("TextButton")
    ClickTPToggle.Size = UDim2.new(1, 0, 0.1, 0)
    ClickTPToggle.Position = UDim2.new(0, 0, 0, 0)
    ClickTPToggle.Text = "Click TP: OFF"
    ClickTPToggle.TextColor3 = Color3.fromRGB(255, 255, 255)
    ClickTPToggle.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
    ClickTPToggle.BorderSizePixel = 0
    ClickTPToggle.Font = Enum.Font.SourceSansBold
    ClickTPToggle.TextSize = 16
    ClickTPToggle.Parent = ButtonsFrame

    -- ESP Player
    local ESPToggle = Instance.new("TextButton")
    ESPToggle.Size = UDim2.new(1, 0, 0.1, 0)
    ESPToggle.Position = UDim2.new(0, 0, 0.12, 0)
    ESPToggle.Text = "ESP: OFF"
    ESPToggle.TextColor3 = Color3.fromRGB(255, 255, 255)
    ESPToggle.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
    ESPToggle.BorderSizePixel = 0
    ESPToggle.Font = Enum.Font.SourceSansBold
    ESPToggle.TextSize = 16
    ESPToggle.Parent = ButtonsFrame

    -- AimLock (RMB)
    local AimLockToggle = Instance.new("TextButton")
    AimLockToggle.Size = UDim2.new(1, 0, 0.1, 0)
    AimLockToggle.Position = UDim2.new(0, 0, 0.24, 0)
    AimLockToggle.Text = "AimLock (RMB): OFF"
    AimLockToggle.TextColor3 = Color3.fromRGB(255, 255, 255)
    AimLockToggle.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
    AimLockToggle.BorderSizePixel = 0
    AimLockToggle.Font = Enum.Font.SourceSansBold
    AimLockToggle.TextSize = 16
    AimLockToggle.Parent = ButtonsFrame

    -- FullBright
    local FullBrightToggle = Instance.new("TextButton")
    FullBrightToggle.Size = UDim2.new(1, 0, 0.1, 0)
    FullBrightToggle.Position = UDim2.new(0, 0, 0.36, 0)
    FullBrightToggle.Text = "FullBright: OFF"
    FullBrightToggle.TextColor3 = Color3.fromRGB(255, 255, 255)
    FullBrightToggle.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
    FullBrightToggle.BorderSizePixel = 0
    FullBrightToggle.Font = Enum.Font.SourceSansBold
    FullBrightToggle.TextSize = 16
    FullBrightToggle.Parent = ButtonsFrame

    -- Noclip
    local NoclipToggle = Instance.new("TextButton")
    NoclipToggle.Size = UDim2.new(1, 0, 0.1, 0)
    NoclipToggle.Position = UDim2.new(0, 0, 0.48, 0)
    NoclipToggle.Text = "Noclip: OFF"
    NoclipToggle.TextColor3 = Color3.fromRGB(255, 255, 255)
    NoclipToggle.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
    NoclipToggle.BorderSizePixel = 0
    NoclipToggle.Font = Enum.Font.SourceSansBold
    NoclipToggle.TextSize = 16
    NoclipToggle.Parent = ButtonsFrame

    -- SpeedHack
    local SpeedToggle = Instance.new("TextButton")
    SpeedToggle.Size = UDim2.new(1, 0, 0.1, 0)
    SpeedToggle.Position = UDim2.new(0, 0, 0.6, 0)
    SpeedToggle.Text = "SpeedHack (16): OFF"
    SpeedToggle.TextColor3 = Color3.fromRGB(255, 255, 255)
    SpeedToggle.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
    SpeedToggle.BorderSizePixel = 0
    SpeedToggle.Font = Enum.Font.SourceSansBold
    SpeedToggle.TextSize = 16
    SpeedToggle.Parent = ButtonsFrame

    -- Fly (W/S)
    local FlyToggle = Instance.new("TextButton")
    FlyToggle.Size = UDim2.new(1, 0, 0.1, 0)
    FlyToggle.Position = UDim2.new(0, 0, 0.72, 0)
    FlyToggle.Text = "Fly (W/S): OFF"
    FlyToggle.TextColor3 = Color3.fromRGB(255, 255, 255)
    FlyToggle.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
    FlyToggle.BorderSizePixel = 0
    FlyToggle.Font = Enum.Font.SourceSansBold
    FlyToggle.TextSize = 16
    FlyToggle.Parent = ButtonsFrame

    -- Кредиты
    local Credits = Instance.new("TextLabel")
    Credits.Size = UDim2.new(1, 0, 0.05, 0)
    Credits.Position = UDim2.new(0, 0, 0.95, 0)
    Credits.Text = "by Кирилл negr | v1.0"
    Credits.TextColor3 = Color3.fromRGB(150, 150, 150)
    Credits.BackgroundTransparency = 1
    Credits.Font = Enum.Font.SourceSans
    Credits.TextSize = 14
    Credits.Parent = MainFrame

    --===[ ФУНКЦИОНАЛ ]===--
    local function ToggleButton(button, value)
        button.Text = button.Name .. ": " .. (value and "ON" or "OFF")
        button.BackgroundColor3 = value and Color3.fromRGB(0, 170, 0) or Color3.fromRGB(60, 60, 70)
        return value
    end

    -- Click Teleport
    local ClickTPEnabled = false
    local ClickTPConnection

    ClickTPToggle.Name = "Click TP"
    ClickTPToggle.MouseButton1Click:Connect(function()
        ClickTPEnabled = ToggleButton(ClickTPToggle, not ClickTPEnabled)
        
        if ClickTPEnabled then
            ClickTPConnection = UserInputService.InputBegan:Connect(function(input, gameProcessed)
                if input.UserInputType == Settings.ClickTP.Keybind and not gameProcessed then
                    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
                        local ray = Camera:ScreenPointToRay(UserInputService:GetMouseLocation().X, UserInputService:GetMouseLocation().Y)
                        local part, position = workspace:FindPartOnRay(ray, LocalPlayer.Character)
                        if part then LocalPlayer.Character:MoveTo(position) end
                    end
                end
            end)
        elseif ClickTPConnection then
            ClickTPConnection:Disconnect()
        end
    end)

    -- ESP Player
    local ESPEnabled = false
    local ESPObjects = {}

    local function CreateESP(player)
        if player == LocalPlayer then return end
        
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
        
        local billboard = Instance.new("BillboardGui")
        billboard.Name = "ESP_" .. player.Name
        billboard.AlwaysOnTop = true
        billboard.Size = UDim2.new(4, 0, 2, 0)
        billboard.Adornee = humanoidRootPart
        billboard.StudsOffset = Vector3.new(0, 3.5, 0)
        billboard.Parent = character
        
        local textLabel = Instance.new("TextLabel")
        textLabel.Size = UDim2.new(1, 0, 1, 0)
        textLabel.BackgroundTransparency = 1
        textLabel.TextColor3 = Settings.ESP.TextColor
        textLabel.Text = player.Name
        textLabel.TextStrokeTransparency = 0.5
        textLabel.TextStrokeColor3 = Color3.new(0, 0, 0)
        textLabel.Font = Enum.Font.SourceSansBold
        textLabel.TextSize = 14
        textLabel.Parent = billboard
        
        local box = Instance.new("BoxHandleAdornment")
        box.Name = "ESPBox_" .. player.Name
        box.Adornee = humanoidRootPart
        box.AlwaysOnTop = true
        box.Size = Settings.ESP.BoxSize
        box.Transparency = Settings.ESP.BoxTransparency
        box.Color3 = Settings.ESP.BoxColor
        box.Parent = humanoidRootPart
        
        ESPObjects[player] = {
            Billboard = billboard,
            Box = box,
            Character = character
        }
    end

    ESPToggle.Name = "ESP"
    ESPToggle.MouseButton1Click:Connect(function()
        ESPEnabled = ToggleButton(ESPToggle, not ESPEnabled)
        
        if ESPEnabled then
            for _, player in ipairs(Players:GetPlayers()) do
                if player ~= LocalPlayer then
                    if player.Character then CreateESP(player) end
                    player.CharacterAdded:Connect(function() CreateESP(player) end)
                end
            end
            Players.PlayerAdded:Connect(function(player)
                player.CharacterAdded:Connect(function() CreateESP(player) end)
            end)
        else
            for player, esp in pairs(ESPObjects) do
                if esp.Billboard then esp.Billboard:Destroy() end
                if esp.Box then esp.Box:Destroy() end
            end
            ESPObjects = {}
        end
    end)

    -- AimLock (RMB)
    local AimLockEnabled = false
    local AimLockTarget = nil
    local AimLockConnection

    local function GetClosestPlayer()
        local closestPlayer, shortestDistance = nil, math.huge
        local cameraPos = Camera.CFrame.Position

        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and player.Character then
                local character = player.Character
                local humanoid = character:FindFirstChild("Humanoid")
                local targetPart = character:FindFirstChild(Settings.AimLock.TargetPart)

                if humanoid and humanoid.Health > 0 and targetPart then
                    local screenPoint, onScreen = Camera:WorldToViewportPoint(targetPart.Position)
                    if onScreen then
                        local mousePos = UserInputService:GetMouseLocation()
                        local distance = (Vector2.new(screenPoint.X, screenPoint.Y) - Vector2.new(mousePos.X, mousePos.Y)).Magnitude
                        if distance < shortestDistance then
                            shortestDistance = distance
                            closestPlayer = player
                        end
                    end
                end
            end
        end
        return closestPlayer
    end

    AimLockToggle.Name = "AimLock (RMB)"
    AimLockToggle.MouseButton1Click:Connect(function()
        AimLockEnabled = ToggleButton(AimLockToggle, not AimLockEnabled)
        
        if AimLockEnabled then
            AimLockConnection = RunService.Heartbeat:Connect(function()
                if UserInputService:IsMouseButtonPressed(Settings.AimLock.Keybind) then
                    if not AimLockTarget then AimLockTarget = GetClosestPlayer() end
                    if AimLockTarget and AimLockTarget.Character then
                        local targetPart = AimLockTarget.Character:FindFirstChild(Settings.AimLock.TargetPart)
                        if targetPart then
                            local cameraPos = Camera.CFrame.Position
                            Camera.CFrame = CFrame.new(cameraPos, targetPart.Position):Lerp(
                                Camera.CFrame, Settings.AimLock.Smoothness
                            )
                        end
                    end
                else
                    AimLockTarget = nil
                end
            end)
        elseif AimLockConnection then
            AimLockConnection:Disconnect()
            AimLockTarget = nil
        end
    end)

    -- FullBright
    local FullBrightEnabled = false
    local OriginalBrightness = Lighting.Brightness
    local OriginalAmbient = Lighting.Ambient

    FullBrightToggle.Name = "FullBright"
    FullBrightToggle.MouseButton1Click:Connect(function()
        FullBrightEnabled = ToggleButton(FullBrightToggle, not FullBrightEnabled)
        
        if FullBrightEnabled then
            Lighting.Brightness = 2
            Lighting.Ambient = Color3.new(1, 1, 1)
            Lighting.OutdoorAmbient = Color3.new(1, 1, 1)
            Lighting.GlobalShadows = false
        else
            Lighting.Brightness = OriginalBrightness
            Lighting.Ambient = OriginalAmbient
            Lighting.OutdoorAmbient = Color3.new(0.5, 0.5, 0.5)
            Lighting.GlobalShadows = true
        end
    end)

    -- Noclip
    local NoclipEnabled = false
    local NoclipConnection

    NoclipToggle.Name = "Noclip"
    NoclipToggle.MouseButton1Click:Connect(function()
        NoclipEnabled = ToggleButton(NoclipToggle, not NoclipEnabled)
        
        if NoclipEnabled then
            NoclipConnection = RunService.Stepped:Connect(function()
                if LocalPlayer.Character then
                    for _, part in ipairs(LocalPlayer.Character:GetDescendants()) do
                        if part:IsA("BasePart") then part.CanCollide = false end
                    end
                end
            end)
        elseif NoclipConnection then
            NoclipConnection:Disconnect()
        end
    end)

    -- SpeedHack
    local SpeedEnabled = false
    local DefaultWalkspeed = Settings.SpeedHack.Default
    local CurrentSpeed = DefaultWalkspeed

    local function UpdateSpeed(value)
        CurrentSpeed = math.clamp(value, Settings.SpeedHack.Min, Settings.SpeedHack.Max)
        SpeedToggle.Text = "SpeedHack ("..CurrentSpeed.."): "..(SpeedEnabled and "ON" or "OFF")
        if SpeedEnabled and LocalPlayer.Character then
            local humanoid = LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
            if humanoid then humanoid.WalkSpeed = CurrentSpeed end
        end
    end

    SpeedToggle.Name = "SpeedHack"
    SpeedToggle.MouseButton1Click:Connect(function()
        SpeedEnabled = ToggleButton(SpeedToggle, not SpeedEnabled)
        if SpeedEnabled then
            if LocalPlayer.Character then
                local humanoid = LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
                if humanoid then
                    DefaultWalkspeed = humanoid.WalkSpeed
                    humanoid.WalkSpeed = CurrentSpeed
                end
            end
        elseif LocalPlayer.Character then
            local humanoid = LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
            if humanoid then humanoid.WalkSpeed = DefaultWalkspeed end
        end
    end)

    -- Управление скоростью
    local SpeedPlus = Instance.new("TextButton")
    SpeedPlus.Size = UDim2.new(0.1, 0, 0.1, 0)
    SpeedPlus.Position = UDim2.new(0.85, 0, 0.6, 0)
    SpeedPlus.Text = "+"
    SpeedPlus.TextColor3 = Color3.fromRGB(255, 255, 255)
    SpeedPlus.BackgroundColor3 = Color3.fromRGB(80, 80, 90)
    SpeedPlus.BorderSizePixel = 0
    SpeedPlus.Font = Enum.Font.SourceSansBold
    SpeedPlus.TextSize = 16
    SpeedPlus.Parent = ButtonsFrame

    local SpeedMinus = Instance.new("TextButton")
    SpeedMinus.Size = UDim2.new(0.1, 0, 0.1, 0)
    SpeedMinus.Position = UDim2.new(0.7, 0, 0.6, 0)
    SpeedMinus.Text = "-"
    SpeedMinus.TextColor3 = Color3.fromRGB(255, 255, 255)
    SpeedMinus.BackgroundColor3 = Color3.fromRGB(80, 80, 90)
    SpeedMinus.BorderSizePixel = 0
    SpeedMinus.Font = Enum.Font.SourceSansBold
    SpeedMinus.TextSize = 16
    SpeedMinus.Parent = ButtonsFrame

    SpeedPlus.MouseButton1Click:Connect(function() UpdateSpeed(CurrentSpeed + 5) end)
    SpeedMinus.MouseButton1Click:Connect(function() UpdateSpeed(CurrentSpeed - 5) end)

    -- Fly (W/S)
    local FlyEnabled = false
    local FlyConnection

    FlyToggle.Name = "Fly (W/S)"
    FlyToggle.MouseButton1Click:Connect(function()
        FlyEnabled = ToggleButton(FlyToggle, not FlyEnabled)
        
        if FlyEnabled then
            local bodyVelocity = Instance.new("BodyVelocity")
            bodyVelocity.Velocity = Vector3.new(0, 0, 0)
            bodyVelocity.MaxForce = Vector3.new(0, math.huge, 0)
            bodyVelocity.Parent = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
            
            FlyConnection = RunService.Heartbeat:Connect(function()
                if not LocalPlayer.Character then return end
                local root = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                if not root then return end
                
                local velocity = root.Velocity
                root.Velocity = Vector3.new(velocity.X, 0, velocity.Z)
                
                if UserInputService:IsKeyDown(Settings.Fly.UpKey) then
                    root.Velocity = root.Velocity + Vector3.new(0, Settings.Fly.Speed, 0)
                elseif UserInputService:IsKeyDown(Settings.Fly.DownKey) then
                    root.Velocity = root.Velocity + Vector3.new(0, -Settings.Fly.Speed, 0)
                end
            end)
        elseif FlyConnection then
            FlyConnection:Disconnect()
            if LocalPlayer.Character then
                local root = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                if root then
                    for _, v in ipairs(root:GetChildren()) do
                        if v:IsA("BodyVelocity") then v:Destroy() end
                    end
                end
            end
        end
    end)

    -- Автоочистка при выходе
    LocalPlayer.CharacterRemoving:Connect(function()
        if ClickTPConnection then ClickTPConnection:Disconnect() end
        if AimLockConnection then AimLockConnection:Disconnect() end
        if NoclipConnection then NoclipConnection:Disconnect() end
        if FlyConnection then FlyConnection:Disconnect() end
    end)

    print("Кирилл negr Hub успешно загружен!")
end
