function c()
    if
        not game.Workspace:FindFirstChild("Chest1") and not game.Workspace:FindFirstChild("Chest2") and
            not game.Workspace:FindFirstChild("Chest3")
     then
        return nil
    end
    min = math.huge
    chests = {}
    for r, v in pairs(game.Workspace:GetChildren()) do
        if string.find(v.Name, "Chest") then
            table.insert(chests, v.CFrame)
        end
    end
    for r, v in pairs(chests) do
        if (v.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < min then
            min = (v.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
        end
    end
    for r, v in pairs(chests) do
        if (v.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= min then
            return v
        end
    end
end
