

folder = game.ReplicatedStorage:WaitForChild("FakeWindows")
cam = game.Workspace:WaitForChild("Camera")

game:GetService("RunService").RenderStepped:Connect(function()
    for _,ObjVal in pairs(folder:GetChildren()) do
        local Window = ObjVal.Value
        local RelativeCamCframe = Window.CFrame:ToObjectSpace(cam.CFrame)
        if -RelativeCamCframe.Position.Z > 0 then
            for _,texture in pairs(Window.FakeWindowTextures:GetChildren()) do
                local speed = (texture.Value.Distance.Value) / (-RelativeCamCframe.Position.Z + texture.Value.Distance.Value)
                local offset = (texture.Value.Size.Value - (texture.Value.Size.Value * (1-speed)))/2
                texture.Value.OffsetStudsU = (texture.Value.Offset.Value.X * (-(texture.Value.Size.Value * (1 - speed)))) - ((((Window.Size.X / texture.Value.Size.Value) - 1) / 2) * texture.Value.Size.Value) - offset + RelativeCamCframe.Position.X * speed
                texture.Value.OffsetStudsV = (texture.Value.Offset.Value.X * (-(texture.Value.Size.Value * (1 - speed)))) - ((((Window.Size.Y / texture.Value.Size.Value) - 1) / 2) * texture.Value.Size.Value) - offset + RelativeCamCframe.Position.Y * speed
                texture.Value.StudsPerTileU = texture.Value.Size.Value * (1-speed)--((Size / texture.Value.Size.Value) - texture.Value.Size.Value) -- Size
                texture.Value.StudsPerTileV = texture.Value.Size.Value * (1-speed)--((Size / texture.Value.Size.Value) - texture.Value.Size.Value) -- Size
            end 
        end
    end
end)
--(texture.Value.Offset.Value.Y)
