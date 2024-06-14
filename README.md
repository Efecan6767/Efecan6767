--// ANTI-KICK
local mt = getrawmetatable(game)
local ncallsa = mt.__namecall
	setreadonly(mt, false)
	mt.__namecall = newcclosure(function(...)
		local args = {...}
		if not checkcaller() and getnamecallmethod() == "Kick" then
			return nil
		end
		return ncallsa(...)
	end)
	setreadonly(mt, true)
--//
	
--// ANTI-BAN
	local mmt = getrawmetatable(game)

local oldnamecall = mmt.__namecall

setreadonly(mmt, false)

mmt.__namecall = newcclosure(function(self, ...)
   local method = tostring(getnamecallmethod())
   local Args = {...}
   if not checkcaller() and method == "FireServer" and tostring(self) == "Banned" then
       return nil
   end
   
   return oldnamecall(self, ...)
end)

setreadonly(mmt, true)
	
	local gmt = getrawmetatable(game);
setreadonly(gmt, false);
local old_index = gmt.__index;
gmt.__index = function(a, b)
    if tostring(a) == "BannedA" or tostring(a) == "BannedB" or tostring(a) == "BannedC" or tostring(a) == "BannedD" then
        if tostring(b) == "Value" then
            return false;
        end
    end
    return old_index(a, b);
end

local bgmt = getrawmetatable(game);
setreadonly(bgmt, false);
local bold_index = bgmt.__index;
bgmt.__index = function(a, b)
    if tostring(a) == "BCount" then
        if tostring(b) == "Value" then
            return 0;
        end
    end
    return bold_index(a, b);
end

for i,BN in pairs(game:GetService("Workspace").FE.Settings:GetChildren()) do
    if BN.Name == "BName" then
    BN:Destroy()
end
end
--//

--// ANTI-WALKSPEED AND ANTI-JUMPPOWER
for i,b in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
    if b.Name == " " then
    b:Destroy()
end
end

for i,lc2 in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
    if lc2:IsA("LocalScript") and string.match(lc2.Name, "1") or string.match(lc2.Name, "2") or string.match(lc2.Name, "3") or string.match(lc2.Name, "4") or string.match(lc2.Name, "5") or string.match(lc2.Name, "6") or string.match(lc2.Name, "7") or string.match(lc2.Name, "8") or string.match(lc2.Name, "9") then
       lc2:Destroy()
    end
end

for i,lc in pairs(game.Players.LocalPlayer.PlayerGui.Start:GetChildren()) do
    if lc:IsA("LocalScript") and string.match(lc.Name, "1") or string.match(lc.Name, "2") or string.match(lc.Name, "3") or string.match(lc.Name, "4") or string.match(lc.Name, "5") or string.match(lc.Name, "6") or string.match(lc.Name, "7") or string.match(lc.Name, "8") or string.match(lc.Name, "9") then
       lc:Destroy()
    end
end

for i,c in pairs(game.Players.LocalPlayer.PlayerGui.Start:GetChildren()) do
    if c.Name == "CheckPlayerW" then
    c:Destroy()
end
end

for i,z in pairs(game.StarterGui.Start:GetChildren()) do
    if z.Name == "CheckPlayerW" then
    z:Destroy()
end
end

for _, v in pairs(game.StarterPlayer.StarterCharacterScripts:GetDescendants()) do
if v.Name == " " then
v:Destroy()
end
end

game.Players.LocalPlayer.CharacterAdded:Connect(function()
wait(0.5)
for i,char in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
    if char.Name == " " then
       char:Destroy()
    end
    end
end)
--//

--// ANTI-LAG (REMOVES LAG FROM GUI)
for i,nolag in pairs(game.StarterGui.Start:GetChildren()) do
if nolag.Name == "Gradient" then
nolag:Destroy()
end
end
for i,nolaglp in pairs(game.Players.LocalPlayer.PlayerGui.Start:GetChildren()) do
if nolaglp.Name == "Gradient" then
nolaglp:Destroy()
end
end
--//

--// FUNCTIONS, VARIABLES AND SCRIPTS //--
function GetPlayer(String)
	local Foundplr = {}
	local strl = String:lower()
	if strl == "all" then
		for i,v in pairs(game:GetService("Players"):GetPlayers()) do
			table.insert(Foundplr,v)
		end
	elseif strl == "others" then
		for i,v in pairs(game:GetService("Players"):GetPlayers()) do
			if v.Name ~= game.Players.LocalPlayer.Name then
				table.insert(Foundplr,v)
			end
		end
	elseif strl == "me" then
		for i,v in pairs(game:GetService("Players"):GetPlayers()) do
			if v.Name == game.Players.LocalPlayer.Name then
				table.insert(Foundplr,v)
			end
		end
	else
		for i,v in pairs(game:GetService("Players"):GetPlayers()) do
			if v.DisplayName:lower():sub(1, #String) == String:lower() or v.Name:lower():sub(1, #String) == String:lower() then
				table.insert(Foundplr,v)
			end
		end
	end
	return Foundplr
end

local RS
local LeftLeg
local RightLeg
local LeftFoot
local RightFoot
local Distance = 0
local DistanceTackle = 0
local DistanceReach = 0
local DistancePass = 0
local DistanceWalk = 0
local DistanceSide = 0
local DistanceJump = 0
local SaveDelay = 0
local Heartbeat
local HumanoidDied
local TouchedBallLoop
local RunStepped2
local RunStepBall
local AddBallA
local TouchedGKBallBox

local Player = game.Players.LocalPlayer
local RootPart = Player.Character.HumanoidRootPart


local Window = library:CreateWindow("TPS: Street Soccer", "Version: 1.48", 10044538000)

local Tab = Window:CreateTab("Scripts")

local GKPage = Tab:CreateFrame("Goalkeeper")
local SPage = Tab:CreateFrame("Striker")
local MPage = Tab:CreateFrame("Miscellaneous")
local LPPage = Tab:CreateFrame("LocalPlayer")
local PPage = Tab:CreateFrame("Players")
local KPage = Tab:CreateFrame("Kicks")
local PWRPage = Tab:CreateFrame("Powers")
local BPage = Tab:CreateFrame("Ball")
local MRPage = Tab:CreateFrame("Mobile Reach")
local TPPage = Tab:CreateFrame("Teleports")
local CPage = Tab:CreateFrame("Celebrations")
local VPage = Tab:CreateFrame("Visuals")
local CRPage = Tab:CreateFrame("Credits")

GKPage:CreateLabel("Miscellaneous")

GKPage:CreateToggle("Allow Save Everywhere", "Allows You Save On The Field", function(arg)
if arg then
for i,v in pairs(game.Workspace.GKSystem:GetChildren()) do
    if v.Name == "Fix" then
       v.CanTouch = false
    end
end
    else
        for i,v in pairs(game.Workspace.GKSystem:GetChildren()) do
    if v.Name == "Fix" then
       v.CanTouch = true
    end
end
end
end)

GKPage:CreateToggle("Auto Save [Touched Method]", "Auto Save The Ball [Touched Method]", function(arg)
if arg then
TouchedGKBallBox = game.Workspace.TPSSystem.TPS.Touched:Connect(function(HRP)
    if HRP == game.Players.LocalPlayer.Character.HumanoidRootPart then
        for i,v in pairs(game.Workspace:GetDescendants()) do
    if v.Name == "TPS" and v:IsA("Part") then
    if game.Players.LocalPlayer.Character.Humanoid.RigType == Enum.HumanoidRigType.R6 then
    AnimationId = "304581045"
local Anim = Instance.new("Animation")
Anim.AnimationId = "rbxassetid://"..AnimationId
local k = game.Players.LocalPlayer.Character.Humanoid:LoadAnimation(Anim)
k:Play()
wait(SaveDelay)

local A_1 = game:GetService("Workspace").TPSSystem.TPS
local A_2 = game.Players.LocalPlayer.Character["Right Leg"]
local Event = game:GetService("Workspace").FE.Actions.SaveRL
Event:FireServer(A_1, A_2)

local Events2 = game:GetService("Workspace").FE.Kick.RemoteEvent2
Events2:FireServer()
else
AnimationId = "3008336125"
local Anim = Instance.new("Animation")
Anim.AnimationId = "rbxassetid://"..AnimationId
local k = game.Players.LocalPlayer.Character.Humanoid:LoadAnimation(Anim)
k:Play()
wait(SaveDelay)

local A_1 = game:GetService("Workspace").TPSSystem.TPS
local A_2 = game.Players.LocalPlayer.Character["HumanoidRootPart"]
local Event = game:GetService("Workspace").FE.Actions.SaveT
Event:FireServer(A_1, A_2)

local Events3 = game:GetService("Workspace").FE.Kick.RemoteEvent2
Events3:FireServer()
end
end
end
end
end)
    else
TouchedGKBallBox:Disconnect()
end
end)

GKPage:CreateToggle("Auto Save [RemoteEvent Method]", "Auto Save The Ball [RemoteEvent Method]", function(arg)
if arg then
_G.GKS = true
    while _G.GKS do
    wait()
       for i,v in pairs(game.Workspace:GetDescendants()) do
    if v.Name == "TPS" and v:IsA("Part") then
    if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - v.Position).Magnitude <= Distance then
    if game.Players.LocalPlayer.Character.Humanoid.RigType == Enum.HumanoidRigType.R6 then
    AnimationId = "304581045"
local Anim = Instance.new("Animation")
Anim.AnimationId = "rbxassetid://"..AnimationId
local k = game.Players.LocalPlayer.Character.Humanoid:LoadAnimation(Anim)
k:Play()
wait(SaveDelay)

local A_1 = game:GetService("Workspace").TPSSystem.TPS
local A_2 = game.Players.LocalPlayer.Character["Right Leg"]
local Event = game:GetService("Workspace").FE.Actions.SaveRL
Event:FireServer(A_1, A_2)

local Events2 = game:GetService("Workspace").FE.Kick.RemoteEvent2
Events2:FireServer()
else
AnimationId = "3008336125"
local Anim = Instance.new("Animation")
Anim.AnimationId = "rbxassetid://"..AnimationId
local k = game.Players.LocalPlayer.Character.Humanoid:LoadAnimation(Anim)
k:Play()
wait(SaveDelay)

local A_1 = game:GetService("Workspace").TPSSystem.TPS
local A_2 = game.Players.LocalPlayer.Character["HumanoidRootPart"]
local Event = game:GetService("Workspace").FE.Actions.SaveT
Event:FireServer(A_1, A_2)

local Events3 = game:GetService("Workspace").FE.Kick.RemoteEvent2
Events3:FireServer()
end
end
end
end
end
    else
if _G.GKS == true then
_G.GKS = false
else
_G.GKS = true
end
end
end)

GKPage:CreateToggle("Auto Jump", "Auto Jump For The Ball", function(arg)
if arg then
_G.JUMP = true
    while _G.JUMP do
    wait()
    
for i,v in pairs(game.Workspace:GetDescendants()) do
    if v.Name == "TPS" and v:IsA("Part") then
    local a = Vector3.new(0, v.Position.Y, 0)
    local b = Vector3.new(0, game.Players.LocalPlayer.Character.Head.Position.Y, 0)
    if (a - b).Magnitude >= 5 then
    if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - v.Position).Magnitude <= DistanceJump then
    game.Players.LocalPlayer.Character.Humanoid.Jump = true
end
end
end
end
end
    else
if _G.JUMP == true then
_G.JUMP = false
else
_G.JUMP = true
end
end
end)

GKPage:CreateToggle("Auto Walk Sideways [WalkToPoint Method]", "Auto Walk Sideways In Net When The Ball Is Near", function(arg)
if arg then
_G.SIDEW = true
    while _G.SIDEW do
    wait(0.8)
       for i,v in pairs(game.Workspace:GetDescendants()) do
    if v.Name == "TPS" and v:IsA("Part") then
    if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - v.Position).Magnitude <= DistanceSide then
    if game.Players.LocalPlayer.TeamColor == BrickColor.new("Bright red") then
    game.Players.LocalPlayer.Character.Humanoid.WalkToPoint = Vector3.new(9.488, 13.3, -126.9)
    wait(0.8)
    game.Players.LocalPlayer.Character.Humanoid.WalkToPoint = Vector3.new(-9.697, 13.3, -126.49)
    else
    game.Players.LocalPlayer.Character.Humanoid.WalkToPoint = Vector3.new(-8.878, 13.3, 129.295)
    wait(0.8)
    game.Players.LocalPlayer.Character.Humanoid.WalkToPoint = Vector3.new(9.07, 13.3, 129.73)
end
end
end
end
end
    else
if _G.SIDEW == true then
_G.SIDEW = false
else
_G.SIDEW = true
end
end
end)

GKPage:CreateToggle("Auto Walk Sideways [MoveTo Method]", "Auto Walk Sideways In Net When The Ball Is Near", function(arg)
if arg then
_G.SIDEM = true
    while _G.SIDEM do
    wait(0.8)
       if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - game.Workspace.TPSSystem.TPS.Position).Magnitude <= DistanceSide then
game.Players.LocalPlayer.Character.Humanoid:MoveTo(game.Players.LocalPlayer.Character.HumanoidRootPart.Position + Vector3.new(game.Workspace.TPSSystem.TPS.Position.X, 0, 0))
wait(0.8)
game.Players.LocalPlayer.Character.Humanoid:MoveTo(game.Players.LocalPlayer.Character.HumanoidRootPart.Position + Vector3.new(-game.Workspace.TPSSystem.TPS.Position.X, 0, 0))
end
end
    else
if _G.SIDEM == true then
_G.SIDEM = false
else
_G.SIDEM = true
end
end
end)

local PartRedTouched
local PartBlueTouched

GKPage:CreateToggle("Auto Look At The Ball", "Auto Look At The Ball When In The Box. Switched Teams = Untoggle", function(arg)
if arg then
local PartB = game:GetService("Workspace").GKSystem.Fix2
local PartR = game:GetService("Workspace").GKSystem.Fix1

if game.Players.LocalPlayer.TeamColor == BrickColor.new("Bright blue") then
PartBlueTouched = PartB.Touched:Connect(function()
    local touching = PartB:GetTouchingParts()
	for i=1,#touching do
		if touching[i] == game.Players.LocalPlayer.Character.HumanoidRootPart then
			repeat wait()
			if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - game.Workspace.TPSSystem.TPS.Position).Magnitude > 6 then
			game.Players.LocalPlayer.PlayerGui.LockScript.SetLock.Value = true
game.Workspace.CurrentCamera.CFrame = CFrame.lookAt(game.Workspace.CurrentCamera.CFrame.Position,game.Workspace.TPSSystem.TPS.Position)
end

			until (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - game.Workspace.TPSSystem.TPS.Position).Magnitude <= 4.5
end
end
end)
else
PartRedTouched = PartR.Touched:Connect(function()
    local touching = PartR:GetTouchingParts()
	for i=1,#touching do
		if touching[i] == game.Players.LocalPlayer.Character.HumanoidRootPart then
			repeat wait()
			if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - game.Workspace.TPSSystem.TPS.Position).Magnitude > 6 then
			game.Players.LocalPlayer.PlayerGui.LockScript.SetLock.Value = true
game.Workspace.CurrentCamera.CFrame = CFrame.lookAt(game.Workspace.CurrentCamera.CFrame.Position,game.Workspace.TPSSystem.TPS.Position)
end

			until (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - game.Workspace.TPSSystem.TPS.Position).Magnitude <= 4.5
end
end
end)
end
    else
    PartRedTouched:Disconnect()
    PartBlueTouched:Disconnect()
    wait(1)
    game.Players.LocalPlayer.PlayerGui.LockScript.SetLock.Value = false
end
end)

GKPage:CreateToggle("Auto Return", "Auto Return To Team Goal When You Died.", function(arg)
if arg then
HumanoidDied = game.Players.LocalPlayer.CharacterAdded:Connect(function()
       wait(0.5)
          if game.Players.LocalPlayer.TeamColor == BrickColor.new("Bright red") then
          game.Players.LocalPlayer.Character.Humanoid.WalkToPoint = Vector3.new(-2.114, 13.3, -118.341)
    else
          game.Players.LocalPlayer.Character.Humanoid.WalkToPoint = Vector3.new(0.512, 13.3, 122.121)
       end
    end)
    else
    HumanoidDied:Disconnect()
end
end)

GKPage:CreateLabel("Configurations")

GKPage:CreateBox("Auto Save Delay", 10044538000, function(arg)
SaveDelay = tonumber(arg)
end)

GKPage:CreateSlider("Auto Save Distance", 0, 10,function(arg)
   Distance = arg
end)

GKPage:CreateSlider("Auto Jump Distance", 0, 50,function(arg)
   DistanceJump = arg
end)

GKPage:CreateSlider("Auto Walk Sideways Distance", 0, 300,function(arg)
   DistanceSide = arg
end)

SPage:CreateLabel("Miscellaneous")

SPage:CreateToggle("Auto Goal [Autofarm]", "Auto Goal [Autofarn]. Use At Your Own Risk", function(arg)
if arg then
_G.AUTOFARM = true
while _G.AUTOFARM do
wait()
local HRPRotation = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.Rotation
local GoalPST = game.Workspace.TPSSystem.TPS.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = HRPRotation + GoalPST.Position
    local A_1 = game:GetService("Workspace").TPSSystem.TPS
local A_2 = game:GetService("Players").LocalPlayer.Character.Head
local Event = game:GetService("Workspace").FE.Actions.Tackle
Event:FireServer(A_1, A_2)

local Events2 = game:GetService("Workspace").FE.Kick.RemoteEvent2
Events2:FireServer()
if game.Players.LocalPlayer.TeamColor == BrickColor.new("Bright red") then
game.Players.LocalPlayer.PlayerGui.LockScript.SetLock.Value = true
game.Workspace.CurrentCamera.CFrame = CFrame.lookAt(game.Workspace.CurrentCamera.CFrame.Position + Vector3.new(0, 45, 0),game.Workspace.BlueGoal.Part.Position)
end
if game.Players.LocalPlayer.TeamColor == BrickColor.new("Bright blue") then
game.Players.LocalPlayer.PlayerGui.LockScript.SetLock.Value = true
game.Workspace.CurrentCamera.CFrame = CFrame.lookAt(game.Workspace.CurrentCamera.CFrame.Position + Vector3.new(0, 45, 0),game.Workspace.RedGoal.Part.Position)
end
end
    else
_G.AUTOFARM = false
wait(1)
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Lines.Line12.CFrame
game.Players.LocalPlayer.PlayerGui.LockScript.SetLock.Value = false
end
end)

SPage:CreateToggle("Allow Kick GK Box", "Allows You Shoot From Goalkeeper's Goal Box", function(arg)
if arg then
game:GetService("Workspace").GKSystem.Fix1.CanTouch = false
        game:GetService("Workspace").GKSystem.Fix2.CanTouch = false
    else
        game:GetService("Workspace").GKSystem.Fix1.CanTouch = true
        game:GetService("Workspace").GKSystem.Fix2.CanTouch = true
end
end)

SPage:CreateToggle("Auto Shoot", "Auto Shoot The Ball When You Are Near", function(arg)
if arg then
_G.MOD = true
    while _G.MOD do
    wait()
    for i,v in pairs(game.Workspace:GetDescendants()) do
    if v.Name == "TPS" and v:IsA("Part") then
    if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - v.Position).Magnitude <= 6 then
       local ModuleKick = require(game:GetService("Players").LocalPlayer.Backpack.Module)
ModuleKick.Kick()
ModuleKick.Kick2()
end
end
end
end
    else
    _G.MOD = false
end
end)

SPage:CreateToggle("Auto Tackle", "Auto Tackle The Ball. Recommended 'Face At The Ball'", function(arg)
if arg then
_G.MODT = true
    while _G.MODT do
    wait()
    for i,v in pairs(game.Workspace:GetDescendants()) do
    if v.Name == "TPS" and v:IsA("Part") then
    if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - v.Position).Magnitude <= 6 then
       local ModuleKick = require(game:GetService("Players").LocalPlayer.Backpack.Module)
ModuleKick.Tackle()
end
end
end
end
    else
    _G.MODT = false
end
end)

SPage:CreateToggle("Auto Defence [BUGGY]", "Auto Defending Your Team Goal", function(arg)
if arg then
if game.Players.LocalPlayer.TeamColor == BrickColor.new("Bright blue") then
game.Players.LocalPlayer.Character.Humanoid.WalkToPoint = Vector3.new(0.6464786529541016, 13.299994468688965, 92.49656677246094)
else
game.Players.LocalPlayer.Character.Humanoid.WalkToPoint = Vector3.new(0.11751431971788406, 13.299994468688965, -91.30338287353516)
end
_G.AUTODEFENCE = true
while _G.AUTODEFENCE do
wait()
    if game.Players.LocalPlayer.TeamColor == BrickColor.new("Bright blue") then
        if (game.Workspace.TPSSystem.TPS.Position - game.Workspace.TPSSystem.Part2.Position).Magnitude <= 125 then
        game.Players.LocalPlayer.PlayerGui.LockScript.SetLock.Value = true
game.Workspace.CurrentCamera.CFrame = CFrame.lookAt(game.Workspace.CurrentCamera.CFrame.Position + Vector3.new(0, 45, 0),game.Workspace.RedGoal.Part.Position)
game.Players.LocalPlayer.Character.Humanoid:MoveTo(game.Workspace.TPSSystem.TPS.Position)
for i,v in pairs(game.Workspace:GetDescendants()) do
    if v.Name == "TPS" and v:IsA("Part") then
    if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - v.Position).Magnitude <= 6 then
       local ModuleKick = require(game:GetService("Players").LocalPlayer.Backpack.Module)
ModuleKick.Tackle()
local A_1 = game:GetService("Workspace").TPSSystem.TPS
local A_2 = game:GetService("Players").LocalPlayer.Character.Head
local Event = game:GetService("Workspace").FE.Actions.Tackle
Event:FireServer(A_1, A_2)
end
end
end
end
end
if game.Players.LocalPlayer.TeamColor == BrickColor.new("Bright red") then
        if (game.Workspace.TPSSystem.TPS.Position - game.Workspace.TPSSystem.Part1.Position).Magnitude <= 125 then
        game.Players.LocalPlayer.PlayerGui.LockScript.SetLock.Value = true
game.Workspace.CurrentCamera.CFrame = CFrame.lookAt(game.Workspace.CurrentCamera.CFrame.Position + Vector3.new(0, 45, 0),game.Workspace.BlueGoal.Part.Position)
game.Players.LocalPlayer.Character.Humanoid:MoveTo(game.Workspace.TPSSystem.TPS.Position)
for i,v in pairs(game.Workspace:GetDescendants()) do
    if v.Name == "TPS" and v:IsA("Part") then
    if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - v.Position).Magnitude <= 6 then
       local ModuleKick = require(game:GetService("Players").LocalPlayer.Backpack.Module)
ModuleKick.Tackle()
local A_1 = game:GetService("Workspace").TPSSystem.TPS
local A_2 = game:GetService
