local function killOtherPlayersOnce()
    for i, player in ipairs(game:GetService("Players"):GetPlayers()) do
        pcall(function()
            if player ~= game:GetService("Players").LocalPlayer and not player.Character:FindFirstChildOfClass("ForceField") and player.Character.Humanoid.Health > 0 then
                while player.Character:WaitForChild("Humanoid").Health > 0 do
                    wait()
                    game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
                    for _, otherPlayer in ipairs(game:GetService("Players"):GetPlayers()) do
                        if otherPlayer ~= game:GetService("Players").LocalPlayer then
                            game.ReplicatedStorage.meleeEvent:FireServer(otherPlayer)
                        end
                    end
                end
            end
        end)
    end
end

killOtherPlayersOnce()
