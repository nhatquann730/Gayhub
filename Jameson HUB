--📦 Tải Rayfield
local Rayfield = loadstring(game:HttpGet("https://sirius.menu/rayfield"))()

--🧠 Tạo cửa sổ GUI chính dùng Config
local Window = Rayfield:CreateWindow({
    Name = (Config.namescript or "Jameson HUB") .. " | by " .. (Config.tacgia or "Unknown"),
    LoadingTitle = Config.namescript or "Jameson HUB",
    LoadingSubtitle = "By " .. (Config.tacgia or "Unknown"),
    ConfigurationSaving = {
        Enabled = true,
        FolderName = "JamesonHUB",
        FileName = "Settings"
    },
    KeySystem = false,
    Discord = {Enabled = false}
})

--🌊 Tab chính
local Tab = Window:CreateTab("🌊 Auto Farm", tonumber(Config.logoscript) or 4483362458)
Tab:CreateSection("Tính năng tự động")

--⚙️ Biến điều khiển
getgenv().AutoFarm = false
getgenv().AutoQuest = false
getgenv().KillAura = false
getgenv().AutoPickup = false
getgenv().AutoSea = false

--🧩 Các Toggle
Tab:CreateToggle({
    Name = "Auto Farm Level",
    CurrentValue = false,
    Callback = function(Value)
        getgenv().AutoFarm = Value
    end,
})

Tab:CreateToggle({
    Name = "Auto Quest",
    CurrentValue = false,
    Callback = function(Value)
        getgenv().AutoQuest = Value
    end,
})

Tab:CreateToggle({
    Name = "Kill Aura (Auto Attack)",
    CurrentValue = false,
    Callback = function(Value)
        getgenv().KillAura = Value
    end,
})

Tab:CreateToggle({
    Name = "Auto Pickup Items",
    CurrentValue = false,
    Callback = function(Value)
        getgenv().AutoPickup = Value
    end,
})

Tab:CreateToggle({
    Name = "Auto Sea Transfer",
    CurrentValue = false,
    Callback = function(Value)
        getgenv().AutoSea = Value
    end,
})

--⚔️ Logic xử lý
local plr = game.Players.LocalPlayer
local ws = game.Workspace
local rs = game:GetService("ReplicatedStorage")

spawn(function()
    while task.wait(1) do
        pcall(function()
            if getgenv().AutoQuest then
                for _, npc in pairs(ws.NPCs:GetChildren()) do
                    if npc:FindFirstChild("QuestLevel") and plr.Data.Level.Value >= npc.QuestLevel.Value then
                        plr.Character.HumanoidRootPart.CFrame = npc.HumanoidRootPart.CFrame + Vector3.new(0,2,0)
                        fireclickdetector(npc:FindFirstChildOfClass("ClickDetector"))
                        wait(1)
                        rs.RemoteEvent:FireServer("AcceptQuest")
                        break
                    end
                end
            end

            if getgenv().KillAura or getgenv().AutoFarm then
                for _, mob in pairs(ws.Enemies:GetChildren()) do
                    if mob:FindFirstChild("Humanoid") and mob.Humanoid.Health > 0 then
                        repeat
                            plr.Character.HumanoidRootPart.CFrame = mob.HumanoidRootPart.CFrame + Vector3.new(0,2,0)
                            for _, tool in pairs(plr.Backpack:GetChildren()) do
                                if tool:IsA("Tool") then
                                    tool.Parent = plr.Character
                                    tool:Activate()
                                end
                            end
                            wait(0.2)
                        until mob.Humanoid.Health <= 0 or not (getgenv().KillAura or getgenv().AutoFarm)
                    end
                end
            end

            if getgenv().AutoPickup then
                for _, item in pairs(ws:GetDescendants()) do
                    if item:IsA("TouchTransmitter") and item.Parent:IsA("Part") then
                        firetouchinterest(plr.Character.HumanoidRootPart, item.Parent, 0)
                        wait()
                        firetouchinterest(plr.Character.HumanoidRootPart, item.Parent, 1)
                    end
                end
            end

            if getgenv().AutoSea then
                local level = plr.Data.Level.Value
                if level >= 700 and game.PlaceId == 2753915549 then
                    rs.Remotes.CommF_:InvokeServer("TravelDressrosa")
                elseif level >= 1500 and game.PlaceId == 4442272183 then
                    rs.Remotes.CommF_:InvokeServer("TravelZou")
                end
            end
        end)
    end
end)
