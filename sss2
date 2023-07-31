local VisualizePosition = function(Position)
	local Part = Instance.new("Part")
	Part.Position = Position
	Part.CanCollide = false
	Part.Parent = workspace.Filter
	Part.Size = Vector3.new(0.1,0.1,0.1)
	Part.Anchored = true
end

local function GetDist(Model, Position)
	return (Model["Right Arm"].Position - Position).Magnitude
end

return function(Model, Enemy, EnemyTool)
	
	local Params = RaycastParams.new()
	Params.FilterType = Enum.RaycastFilterType.Blacklist
	Params.FilterDescendantsInstances = {Model, workspace.Filter, EnemyTool, table.unpack(Enemy.Humanoid:GetAccessories()), workspace.Map}
	
	local Raycasts = {}
	table.insert(Raycasts, {workspace:Raycast(Model["Right Arm"].Position, Model.PrimaryPart.CFrame.LookVector*10, Params), 0})
	table.insert(Raycasts, {workspace:Raycast(Model["Right Arm"].Position, (Model.PrimaryPart.CFrame * CFrame.Angles(0,-math.rad(1),0)).LookVector.Unit*10, Params), -1})
	table.insert(Raycasts, {workspace:Raycast(Model["Right Arm"].Position, (Model.PrimaryPart.CFrame * CFrame.Angles(0,math.rad(1),0)).LookVector.Unit*10, Params), 1})
	table.insert(Raycasts, {workspace:Raycast(Model["Right Arm"].Position, (Model.PrimaryPart.CFrame * CFrame.Angles(0,math.rad(2),0)).LookVector.Unit*10, Params), 2})
	table.insert(Raycasts, {workspace:Raycast(Model["Right Arm"].Position, (Model.PrimaryPart.CFrame * CFrame.Angles(0,-math.rad(2),0)).LookVector.Unit*10, Params), -2})
	workspace.Filter:ClearAllChildren()
	local ClosestDistance = math.huge
	local ClosestAngle = 0
	local ClosestPos = nil
	for i,v in pairs(Raycasts) do 
		if v[1] then
			local Dist = GetDist(Model, v[1].Position)
			
			if Dist < ClosestDistance then
				ClosestDistance = Dist
				ClosestAngle = v[2]
				ClosestPos = v.Position
			end
		end
	end
	
	

	return ClosestAngle
	
end
