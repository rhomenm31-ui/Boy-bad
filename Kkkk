local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "EquinozHub"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

local toggleButton = Instance.new("TextButton")
toggleButton.Size = UDim2.new(0,50,0,50)
toggleButton.Position = UDim2.new(0,20,0.5,-25)
toggleButton.BackgroundColor3 = Color3.fromRGB(220, 0, 0)
toggleButton.BackgroundTransparency = 0.1
toggleButton.Text = "🎄EQUINOZ🎄"
toggleButton.Font = Enum.Font.Arcade
toggleButton.TextSize = 10
toggleButton.TextColor3 = Color3.fromRGB(255,255,255)
toggleButton.Active = true
toggleButton.Draggable = true
toggleButton.Parent = screenGui

local uiCorner = Instance.new("UICorner")
uiCorner.CornerRadius = UDim.new(0,8)
uiCorner.Parent = toggleButton

local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0,110,0,215)
mainFrame.Position = UDim2.new(1, 10, 0.5, -107)
mainFrame.BackgroundColor3 = Color3.fromRGB(0, 30, 0)
mainFrame.BackgroundTransparency = 0.1
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Visible = true
mainFrame.Parent = screenGui

local frameCorner = Instance.new("UICorner")
frameCorner.CornerRadius = UDim.new(0,8)
frameCorner.Parent = mainFrame

local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(1,0,0,20)
titleLabel.Position = UDim2.new(0,0,0,5)
titleLabel.BackgroundTransparency = 1
titleLabel.Text = "🎅 EQUINOZ HUB🎅"
titleLabel.Font = Enum.Font.Arcade
titleLabel.TextSize = 11
titleLabel.TextColor3 = Color3.fromRGB(255, 215, 0)
titleLabel.Parent = mainFrame

local function createButton(name, position)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0,100,0,20)
    button.Position = position
    button.Text = name
    button.Font = Enum.Font.Arcade
    button.TextSize = 11
    button.TextColor3 = Color3.fromRGB(255,255,255)
    button.BackgroundColor3 = Color3.fromRGB(220, 0, 0)
    button.AutoButtonColor = false
    
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0,6)
    corner.Parent = button
    
    button.Parent = mainFrame
    return button
end

local fpsButton = createButton("🎄 Fly", UDim2.new(0.05,0,0.15,0))
local speedButton = createButton("🎁 Speed", UDim2.new(0.05,0,0.25,0))
local floatButton = createButton("❄️ Float", UDim2.new(0.05,0,0.35,0))
local desyncButton = createButton("🦌 Desync", UDim2.new(0.05,0,0.45,0))
local tweenSetButton = createButton("⭐ Set Tween", UDim2.new(0.05,0,0.55,0))
local tweenButton = createButton("✨ Tween", UDim2.new(0.05,0,0.65,0))
local tpHitButton = createButton("🎯 TP Hit", UDim2.new(0.05,0,0.75,0))
local infJumpButton = createButton("🪂 Inf Jump", UDim2.new(0.05,0,0.85,0))

local uiVisible = false
local slideIn = TweenService:Create(mainFrame, TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {Position = UDim2.new(1, -120, 0.5, -107)})
local slideOut = TweenService:Create(mainFrame, TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {Position = UDim2.new(1, 10, 0.5, -107)})

toggleButton.MouseButton1Click:Connect(function()
    uiVisible = not uiVisible
    if uiVisible then
        slideIn:Play()
    else
        slideOut:Play()
    end
end)

local infiniteJumpEnabled = false
local jumpConnection = nil
local lastJumpTime = 0
local JUMP_COOLDOWN = 0.3

local function makeCharacterJump()
    local character = player.Character
    if not character then return end
    
    local humanoid = character:FindFirstChildOfClass("Humanoid")
    local rootPart = character:FindFirstChild("HumanoidRootPart")
    
    if not humanoid or not rootPart then return end
    
    humanoid:ChangeState(Enum.HumanoidStateType.Running)
    wait(0.01)
    
    humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
    
    local currentVelocity = rootPart.AssemblyLinearVelocity
    rootPart.AssemblyLinearVelocity = Vector3.new(
        currentVelocity.X,
        35,
        currentVelocity.Z
    )
    
    rootPart.CFrame = rootPart.CFrame + Vector3.new(0, 2, 0)
end

infJumpButton.MouseButton1Click:Connect(function()
    infiniteJumpEnabled = not infiniteJumpEnabled
    
    if infiniteJumpEnabled then
        infJumpButton.Text = "Activated Inf Jump!"
        infJumpButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
        
        if jumpConnection then
            jumpConnection:Disconnect()
        end
        
        jumpConnection = RunService.Heartbeat:Connect(function()
            if not infiniteJumpEnabled then return end
            
            local character = player.Character
            if not character then return end
            
            local humanoid = character:FindFirstChildOfClass("Humanoid")
            if not humanoid then return end
            
            local isJumping = false
            
            if humanoid:GetState() == Enum.HumanoidStateType.Jumping then
                isJumping = true
            end
            
            if humanoid.Jump then
                isJumping = true
            end
            
            if UserInputService:IsKeyDown(Enum.KeyCode.Space) then
                isJumping = true
            end
            
            if isJumping then
                local currentTime = tick()
                if currentTime - lastJumpTime >= JUMP_COOLDOWN then
                    lastJumpTime = currentTime
                    makeCharacterJump()
                end
            end
        end)
        
        player.CharacterAdded:Connect(function(newChar)
            task.wait(2)
            if infiniteJumpEnabled then
                if jumpConnection then
                    jumpConnection:Disconnect()
                end
                jumpConnection = RunService.Heartbeat:Connect(function()
                    if not infiniteJumpEnabled then return end
                    
                    local character = player.Character
                    if not character then return end
                    
                    local humanoid = character:FindFirstChildOfClass("Humanoid")
                    if not humanoid then return end
                    
                    local isJumping = false
                    
                    if humanoid:GetState() == Enum.HumanoidStateType.Jumping then
                        isJumping = true
                    end
                    
                    if humanoid.Jump then
                        isJumping = true
                    end
                    
                    if UserInputService:IsKeyDown(Enum.KeyCode.Space) then
                        isJumping = true
                    end
                    
                    if isJumping then
                        local currentTime = tick()
                        if currentTime - lastJumpTime >= JUMP_COOLDOWN then
                            lastJumpTime = currentTime
                            makeCharacterJump()
                        end
                    end
                end)
            end
        end)
        
    else
        infJumpButton.Text = "🪂 Inf Jump"
        infJumpButton.BackgroundColor3 = Color3.fromRGB(220, 0, 0)
        
        if jumpConnection then
            jumpConnection:Disconnect()
            jumpConnection = nil
        end
    end
end)

local FFLAGS = {
    SAFE_OFFSET = 3,
    HEIGHT_OFFSET = 0,
    TELEPORT_DURATION = 1.5
}

local function performTeleport(targetPlayer)
    if not targetPlayer or not targetPlayer.Character then
        return false
    end
    
    local targetHRP = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
    if not targetHRP then
        return false
    end
    
    local character = player.Character
    if not character then
        return false
    end
    
    local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")
    if not humanoidRootPart then
        return false
    end
    
    local originalCFrame = humanoidRootPart.CFrame
    local targetCFrame = targetHRP.CFrame
    local teleportPosition = targetCFrame.Position - targetCFrame.LookVector * FFLAGS.SAFE_OFFSET
    teleportPosition = teleportPosition + Vector3.new(0, FFLAGS.HEIGHT_OFFSET, 0)
    
    humanoidRootPart.CFrame = CFrame.new(teleportPosition)
    
    local timeLeft = FFLAGS.TELEPORT_DURATION
    while timeLeft > 0 do
        tpHitButton.Text = "Active: " .. string.format("%.1f", timeLeft) .. "s"
        wait(0.1)
        timeLeft = timeLeft - 0.1
        
        if targetPlayer.Character and targetHRP and targetHRP.Parent then
            local newTargetCFrame = targetHRP.CFrame
            local newTeleportPosition = newTargetCFrame.Position - newTargetCFrame.LookVector * FFLAGS.SAFE_OFFSET
            newTeleportPosition = newTeleportPosition + Vector3.new(0, FFLAGS.HEIGHT_OFFSET, 0)
            humanoidRootPart.CFrame = CFrame.new(newTeleportPosition)
        else
            break
        end
    end
    
    if humanoidRootPart and humanoidRootPart.Parent then
        humanoidRootPart.CFrame = originalCFrame
    end
    
    tpHitButton.Text = "🎯 TP Hit"
    return true
end

tpHitButton.MouseButton1Click:Connect(function()
    local nearestPlayer = nil
    local shortestDistance = math.huge
    
    local character = player.Character
    if not character then return end
    
    local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")
    if not humanoidRootPart then return end
    
    for _, otherPlayer in pairs(Players:GetPlayers()) do
        if otherPlayer ~= player and otherPlayer.Character then
            local targetHRP = otherPlayer.Character:FindFirstChild("HumanoidRootPart")
            if targetHRP then
                local distance = (humanoidRootPart.Position - targetHRP.Position).Magnitude
                if distance < shortestDistance then
                    shortestDistance = distance
                    nearestPlayer = otherPlayer
                end
            end
        end
    end
    
    if nearestPlayer then
        tpHitButton.Text = "Activated TP Hit!"
        tpHitButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
        performTeleport(nearestPlayer)
        task.wait(0.5)
        tpHitButton.BackgroundColor3 = Color3.fromRGB(220, 0, 0)
    else
        tpHitButton.Text = "No Target Found!"
        task.wait(1)
        tpHitButton.Text = "🎯 TP Hit"
    end
end)

local FFlags = {
    ["DisableDPIScale"] = "true",
    ["S2PhysicsSenderRate"] = "15000",
    ["AngularVelociryLimit"] = "360",
    ["StreamJobNOUVolumeCap"] = "2147483647",
    ["GameNetDontSendRedundantDeltaPositionMillionth"] = "1",
    ["TimestepArbiterOmegaThou"] = "1073741823",
    ["MaxMissedWorldStepsRemembered"] = "-2147483648",
    ["GameNetPVHeaderRotationalVelocityZeroCutoffExponent"] = "-5000",
    ["PhysicsSenderMaxBandwidthBps"] = "20000",
    ["LargeReplicatorSerializeWrite4"] = "true",
    ["MaxAcceptableUpdateDelay"] = "1",
    ["ServerMaxBandwith"] = "52",
    ["InterpolationFrameRotVelocityThresholdMillionth"] = "5",
    ["GameNetDontSendRedundantNumTimes"] = "1",
    ["StreamJobNOUVolumeLengthCap"] = "2147483647",
    ["CheckPVLinearVelocityIntegrateVsDeltaPositionThresholdPercent"] = "1",
    ["TimestepArbiterHumanoidTurningVelThreshold"] = "1",
    ["MaxTimestepMultiplierAcceleration"] = "2147483647",
    ["SimOwnedNOUCountThresholdMillionth"] = "2147483647",
    ["SimExplicitlyCappedTimestepMultiplier"] = "2147483646",
    ["TimestepArbiterVelocityCriteriaThresholdTwoDt"] = "2147483646",
    ["CheckPVCachedVelThresholdPercent"] = "10",
    ["ReplicationFocusNouExtentsSizeCutoffForPauseStuds"] = "2147483647",
    ["InterpolationFramePositionThresholdMillionth"] = "5",
    ["DebugSendDistInSteps"] = "-2147483648",
    ["LargeReplicatorEnabled9"] = "true",
    ["CheckPVDifferencesForInterpolationMinRotVelThresholdRadsPerSecHundredth"] = "1",
    ["LargeReplicatorWrite5"] = "true",
    ["NextGenReplicatorEnabledWrite4"] = "true",
    ["MaxTimestepMultiplierContstraint"] = "2147483647",
    ["MaxTimestepMultiplierBuoyancy"] = "2147483647",
    ["MaxDataPacketPerSend"] = "2147483647",
    ["LargeReplicatorRead5"] = "true",
    ["CheckPVDifferencesForInterpolationMinVelThresholdStudsPerSecHundredth"] = "1",
    ["TimestepArbiterHumanoidLinearVelThreshold"] = "1",
    ["WorldStepMax"] = "30",
    ["InterpolationFrameVelocityThresholdMillionth"] = "5",
    ["LargeReplicatorSerializeRead3"] = "true",
    ["GameNetPVHeaderLinearVelocityZeroCutoffExponent"] = "-5000",
    ["CheckPVCachedRotVelThresholdPercent"] = "10",
}

local function respawn(plr)
    for name, value in pairs(FFlags) do
        pcall(function()
            setfflag(tostring(name), tostring(value))
        end)
    end
end

desyncButton.MouseButton1Click:Connect(function()
    local char = player.Character
    local root = char and char:FindFirstChild("HumanoidRootPart")

    if root then
        local backCFrame = root.CFrame * CFrame.new(0, 0, 50)
        root.CFrame = backCFrame
    end

    task.wait(0.2)
    respawn(player)
    desyncButton.Text = "Activated Desync!"
    task.wait(1)
    desyncButton.Text = "🦌 Desync"
end)

local tweenTarget = nil
local tweenActive = false
local tweenConn = nil

tweenSetButton.MouseButton1Click:Connect(function()
    local char = player.Character
    local root = char and char:FindFirstChild("HumanoidRootPart")
    
    if root then
        tweenTarget = root.Position
        tweenSetButton.Text = "Activated Set Tween!"
        tweenSetButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
        task.wait(1)
        tweenSetButton.Text = "⭐ Set Tween"
        tweenSetButton.BackgroundColor3 = Color3.fromRGB(220, 0, 0)
    end
end)

tweenButton.MouseButton1Click:Connect(function()
    local char = player.Character
    local root = char and char:FindFirstChild("HumanoidRootPart")
    
    if not root or not tweenTarget then return end
    
    tweenActive = not tweenActive
    
    if tweenActive then
        tweenButton.Text = "Activated Tween!"
        tweenButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
        
        tweenConn = RunService.Heartbeat:Connect(function()
            if tweenActive and root then
                local direction = (tweenTarget - root.Position).Unit
                root.AssemblyLinearVelocity = direction * 29.5
            end
        end)
    else
        tweenButton.Text = "✨ Tween"
        tweenButton.BackgroundColor3 = Color3.fromRGB(220, 0, 0)
        if tweenConn then 
            tweenConn:Disconnect() 
            tweenConn = nil 
        end
        if root then
            root.AssemblyLinearVelocity = Vector3.new(0, root.AssemblyLinearVelocity.Y, 0)
        end
    end
end)

do
    local speedConn
    local baseSpeed = 27.5
    local active = false
    local function GetCharacter()
        local Char = player.Character or player.CharacterAdded:Wait()
        local HRP = Char:WaitForChild("HumanoidRootPart")
        local Hum = Char:FindFirstChildOfClass("Humanoid")
        return Char, HRP, Hum
    end

    local function getMovementInput()
        local Char, HRP, Hum = GetCharacter()
        if not Char or not HRP or not Hum then return Vector3.new(0,0,0) end
        local moveVector = Hum.MoveDirection
        if moveVector.Magnitude > 0.1 then
            return Vector3.new(moveVector.X,0,moveVector.Z).Unit
        end
        return Vector3.new(0,0,0)
    end

    local function startSpeedControl()
        if speedConn then return end
        speedConn = RunService.Heartbeat:Connect(function()
            local Char, HRP, Hum = GetCharacter()
            if not Char or not HRP or not Hum then return end
            local inputDirection = getMovementInput()
            if inputDirection.Magnitude > 0 then
                HRP.AssemblyLinearVelocity = Vector3.new(inputDirection.X*baseSpeed, HRP.AssemblyLinearVelocity.Y, inputDirection.Z*baseSpeed)
            else
                HRP.AssemblyLinearVelocity = Vector3.new(0, HRP.AssemblyLinearVelocity.Y, 0)
            end
        end)
    end

    local function stopSpeedControl()
        if speedConn then speedConn:Disconnect() speedConn=nil end
        local Char, HRP = GetCharacter()
        if HRP then HRP.AssemblyLinearVelocity = Vector3.new(0,HRP.AssemblyLinearVelocity.Y,0) end
    end

    speedButton.MouseButton1Click:Connect(function()
        active = not active
        if active then
            startSpeedControl()
            speedButton.Text = "Activated Speed!"
            speedButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
        else
            stopSpeedControl()
            speedButton.Text = "🎁 Speed"
            speedButton.BackgroundColor3 = Color3.fromRGB(220, 0, 0)
        end
    end)
end

do
    local guidedOn=false
    local guidedConn
    fpsButton.MouseButton1Click:Connect(function()
        local char = player.Character or player.CharacterAdded:Wait()
        local hum = char:FindFirstChildOfClass("Humanoid")
        guidedOn = not guidedOn
        if guidedOn then
            fpsButton.Text = "Activated Fly!"
            fpsButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
            local hrp = char:FindFirstChild("HumanoidRootPart")
            if hrp then
                guidedConn = RunService.RenderStepped:Connect(function()
                    if guidedOn and hrp then
                        hrp.Velocity = workspace.CurrentCamera.CFrame.LookVector * 28.5
                    end
                end)
            end
        else
            fpsButton.Text = "🎄 Fly"
            fpsButton.BackgroundColor3 = Color3.fromRGB(220, 0, 0)
            if guidedConn then guidedConn:Disconnect() guidedConn=nil end
            if hum then hum:ChangeState(Enum.HumanoidStateType.GettingUp) end
        end
    end)
end

do
    local platform, connection
    local active=false
    local function destroyPlatform()
        if platform then platform:Destroy() platform=nil end
        active=false
        if connection then connection:Disconnect() connection=nil end
        floatButton.Text = "❄️ Float"
        floatButton.BackgroundColor3 = Color3.fromRGB(220, 0, 0)
    end

    local function setupFloat(character)
        local root = character:WaitForChild("HumanoidRootPart")
        floatButton.MouseButton1Click:Connect(function()
            active = not active
            if active then
                floatButton.Text = "Activated Float!"
                platform = Instance.new("Part")
                platform.Size = Vector3.new(6,0.5,6)
                platform.Anchored=true
                platform.CanCollide=true
                platform.Color = Color3.fromRGB(220, 0, 0)
                platform.Material = Enum.Material.Neon
                platform.Position = root.Position - Vector3.new(0, root.Size.Y/2 + platform.Size.Y/2, 0)
                platform.Parent = workspace

                connection = RunService.Heartbeat:Connect(function()
                    if platform and active then
                        local cur = platform.Position
                        local newXZ = Vector3.new(root.Position.X, cur.Y, root.Position.Z)
                        platform.Position = newXZ
                    end
                end)
                floatButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
            else
                destroyPlatform()
            end
        end)
        character:WaitForChild("Humanoid").Died:Connect(destroyPlatform)
    end
    if player.Character then setupFloat(player.Character) end
    player.CharacterAdded:Connect(setupFloat)
end
