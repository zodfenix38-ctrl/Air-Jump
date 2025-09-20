local P=game:GetService("Players")
local U=game:GetService("UserInputService")
local L=P.LocalPlayer
local C=L.Character or L.CharacterAdded:Wait()
local H=C:WaitForChild("Humanoid")
local A=false
local B=false
H.StateChanged:Connect(function(_,S)
	if S==Enum.HumanoidStateType.Running or S==Enum.HumanoidStateType.Landed then
		A=true
		B=false
	end
end)
U.JumpRequest:Connect(function()
	if not H or not H.Parent then return end
	if H.FloorMaterial~=Enum.Material.Air then
		A=true
	else
		if A and not B then
			H:ChangeState(Enum.HumanoidStateType.Jumping)
			B=true
		end
	end
end)
