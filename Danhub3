--// DAN HUB DELTA FINAL OTIMIZADO

repeat task.wait() until game:IsLoaded()

local player = game.Players.LocalPlayer
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

--------------------------------------------------
-- GUI SAFE
--------------------------------------------------

local gui = Instance.new("ScreenGui")
pcall(function()
	gui.Parent = game.CoreGui
end)
if not gui.Parent then
	gui.Parent = player:WaitForChild("PlayerGui")
end

--------------------------------------------------
-- VARS
--------------------------------------------------

local speedValue = 16
local jumpValue = 50

local speedOn = false
local jumpOn = false
local infiniteJump = false
local noclip = false
local fly = false

--------------------------------------------------
-- FLY VARS
--------------------------------------------------

local bv, bg
local control = {f=0,b=0,l=0,r=0,u=0,d=0}
local flySpeed = 70

--------------------------------------------------
-- LOOP ÚNICO (ANTI BUG DELTA)
--------------------------------------------------

RunService.Heartbeat:Connect(function()

	local char = player.Character
	if not char then return end

	local hum = char:FindFirstChildOfClass("Humanoid")
	local hrp = char:FindFirstChild("HumanoidRootPart")

	if not hum or not hrp then return end

	-- SPEED
	if speedOn then
		hum.WalkSpeed = speedValue
	end

	-- SUPER JUMP
	if jumpOn then
		hum.JumpPower = jumpValue
		if hum.FloorMaterial ~= Enum.Material.Air then
			hrp.Velocity = Vector3.new(0, jumpValue * 1.5, 0)
		end
	end

	-- NOCLIP
	if noclip then
		for _,v in pairs(char:GetDescendants()) do
			if v:IsA("BasePart") then
				v.CanCollide = false
			end
		end
	end

	-- FLY
	if fly and bv and bg then
		local cam = workspace.CurrentCamera

		local dir =
			(cam.CFrame.LookVector * (control.f - control.b)) +
			(cam.CFrame.RightVector * (control.r - control.l)) +
			Vector3.new(0, control.u - control.d, 0)

		if dir.Magnitude > 0 then
			bv.Velocity = dir.Unit * flySpeed
		else
			bv.Velocity = Vector3.zero
		end

		bg.CFrame = cam.CFrame
	end

end)

--------------------------------------------------
-- INFINITE JUMP
--------------------------------------------------

UIS.JumpRequest:Connect(function()
	if infiniteJump and player.Character then
		local hrp = player.Character:FindFirstChild("HumanoidRootPart")
		if hrp then
			hrp.Velocity = Vector3.new(hrp.Velocity.X, 80, hrp.Velocity.Z)
		end
	end
end)

--------------------------------------------------
-- FLY FUNÇÕES
--------------------------------------------------

local function startFly()
	local char = player.Character or player.CharacterAdded:Wait()
	local hrp = char:WaitForChild("HumanoidRootPart")

	bv = Instance.new("BodyVelocity")
	bv.MaxForce = Vector3.new(1e5,1e5,1e5)
	bv.Velocity = Vector3.zero
	bv.Parent = hrp

	bg = Instance.new("BodyGyro")
	bg.MaxTorque = Vector3.new(1e5,1e5,1e5)
	bg.CFrame = hrp.CFrame
	bg.Parent = hrp
end

local function stopFly()
	if bv then bv:Destroy() end
	if bg then bg:Destroy() end
end

--------------------------------------------------
-- CONTROLES
--------------------------------------------------

UIS.InputBegan:Connect(function(i,g)
	if g then return end

	if i.KeyCode == Enum.KeyCode.W then control.f = 1 end
	if i.KeyCode == Enum.KeyCode.S then control.b = 1 end
	if i.KeyCode == Enum.KeyCode.A then control.l = 1 end
	if i.KeyCode == Enum.KeyCode.D then control.r = 1 end
	if i.KeyCode == Enum.KeyCode.Space then control.u = 1 end
	if i.KeyCode == Enum.KeyCode.LeftShift then control.d = 1 end
end)

UIS.InputEnded:Connect(function(i)
	if i.KeyCode == Enum.KeyCode.W then control.f = 0 end
	if i.KeyCode == Enum.KeyCode.S then control.b = 0 end
	if i.KeyCode == Enum.KeyCode.A then control.l = 0 end
	if i.KeyCode == Enum.KeyCode.D then control.r = 0 end
	if i.KeyCode == Enum.KeyCode.Space then control.u = 0 end
	if i.KeyCode == Enum.KeyCode.LeftShift then control.d = 0 end
end)

--------------------------------------------------
-- FUNÇÕES (PAINEL USA)
--------------------------------------------------

function setSpeed(v)
	speedValue = v
	speedOn = true
end

function stopSpeed()
	speedOn = false
	if player.Character then
		local hum = player.Character:FindFirstChildOfClass("Humanoid")
		if hum then hum.WalkSpeed = 16 end
	end
end

function setJump(v)
	jumpValue = v
	jumpOn = true
end

function stopJump()
	jumpOn = false
	if player.Character then
		local hum = player.Character:FindFirstChildOfClass("Humanoid")
		if hum then hum.JumpPower = 50 end
	end
end

function toggleInfinite()
	infiniteJump = not infiniteJump
end

function toggleNoclip()
	noclip = not noclip
end

function toggleFly()
	fly = not fly
	if fly then
		startFly()
	else
		stopFly()
	end
end

--------------------------------------------------
-- DEBUG
--------------------------------------------------

print("DAN HUB DELTA FINAL OK 🔥")
