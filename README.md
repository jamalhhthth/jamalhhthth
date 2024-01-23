--[[
╭━╮╱╭╮╱╱╱╱╱╱╱╱╭╮╱╱╱╱╱╱╱╱╱╱╭━━━╮╱╭╮            |
┃┃╰╮┃┃╱╱╱╱╱╱╱╱┃┃╱╱╱╱╱╱╱╱╱╱┃╭━╮┃╱┃┃            |
┃╭╮╰╯┣━━┳╮╭┳━━┫┃╭━━┳━━┳━━╮┃┃╱┃┣━╯┣╮╭┳┳━╮     | Welcome to the Nameless Admin source, feel free to take a look around.
┃┃╰╮┃┃╭╮┃╰╯┃┃━┫┃┃┃━┫━━┫━━┫┃╰━╯┃╭╮┃╰╯┣┫╭╮╮    | Enjoy.
┃┃╱┃┃┃╭╮┃┃┃┃┃━┫╰┫┃━╋━━┣━━┃┃╭━╮┃╰╯┃┃┃┃┃┃┃┃    |
╰╯╱╰━┻╯╰┻┻┻┻━━┻━┻━━┻━━┻━━╯╰╯╱╰┻━━┻┻┻┻┻╯╰╯    |
--]]

 -- Waits until game is loaded
 local game = game
 local GetService = game.GetService
 if (not game.IsLoaded(game)) then
	 local Loaded = game.Loaded
	 Loaded.Wait(Loaded);
	 wait(1.5)
 end
 
 -- Notification library
 local Notification = loadstring(game:HttpGet("https://raw.githubusercontent.com/FilteringEnabled/FE/main/notificationtest"))();
 local Notify = Notification.Notify;

 Notify({
		 Description = "Happy New Years!";
		 Title = "NA";
		 Duration = 5;
		 
});
 
 -- Custom file functions checker checker
 local CustomFunctionSupport = isfile and isfolder and writefile and readfile and listfiles
 local FileSupport = isfile and isfolder and writefile and readfile
 
 -- Creates folder & files for Prefix & Plugins
 if FileSupport then
 if not isfolder('Nameless-Admin') then
 makefolder('Nameless-Admin')
 end
 
 if not isfolder('Nameless-Admin/Plugins') then
	 makefolder('Nameless-Admin/Plugins')
 end
 
 if not isfile("Nameless-Admin/Prefix.txt") then
 writefile("Nameless-Admin/Prefix.txt", ';')
 else
 end
 end
 
 -- [[ PREFIX AND OTHER STUFF. ]] -- 
 local opt = {
	 prefix = readfile("Nameless-Admin/Prefix.txt", ';'), -- If player's executor has the custom file function support it reads the prefix file to get prefix
	 tupleSeparator = ',',	-- ;ff me,others,all | ;ff me/others/all
	 ui = {					-- never did anything with this
		 
	 },
	 keybinds = {			-- never did anything with this
		 
	 },
 }
 
 -- [[ Version ]] -- 
 currentversion = 1.13
 
 --[[ VARIABLES ]]--
 PlaceId, JobId = game.PlaceId, game.JobId
 local Players = game:GetService("Players")
 local UserInputService = game:GetService("UserInputService")
 local TweenService = game:GetService("TweenService")
 local RunService = game:GetService("RunService")
 local TeleportService = game:GetService("TeleportService")
 local RunService2 = game:FindService("RunService")
 local StarterGui = game:GetService("StarterGui")
 local SoundService = game:GetService("SoundService")
 sethidden = sethiddenproperty or set_hidden_property or set_hidden_prop
 local Player = game.Players.LocalPlayer
 local IYLOADED = false -- This is used for the ;iy command that executes infinite yield commands using this admin command script (BTW)
 local Humanoid = Character and Character:FindFirstChildWhichIsA("Humanoid") or false
 local Character = game.Players.LocalPlayer.Character
 local Clicked = true
 _G.Spam = false
 --[[ FOR LOOP COMMANDS ]]--
 view = false
 anniblockspam = false
 control = false
 FakeLag = false
 Loopvoid = false
 Loopkill = false
 Loopbring = false
 Loopbanish = false
 Loopvoid = false
 Loopcuff = false
 loopgrab = false
 Loopstand = false
 Looptornado = false
 Loopmute = false
 Loopglitch = false
 Watch = false
 local Admin = {}
 
 -- [[ HAT ORBIT (PATCHED IN MOST GAMES) ]]
 local Offset = 10
 local Rotation = 0
 local Speed = 1
 local Height = 2
 
 local EditingPos = false
 
 local Power = 50000
 local Damping = 500
 
 local Mode = 1
 
 local NormalSpin = true
 
 
 --[[ Some more variables ]]--
 
 local localPlayer = Players.LocalPlayer
 local LocalPlayer = Players.LocalPlayer
 local character = localPlayer.Character
 local mouse = localPlayer:GetMouse()
 local camera = workspace.CurrentCamera
 local camtype = camera.CameraType
 local Commands, Aliases = {}, {}
 player, plr, lp = localPlayer, localPlayer, localPlayer, localPlayer
 
 localPlayer.CharacterAdded:Connect(function(c)
	 character = c
 end)
 
 local bringc = {}
 
 --[[ COMMAND FUNCTIONS ]]--
 commandcount = 0
 cmd = {}
 cmd.add = function(...)
	 local vars = {...}
	 local aliases, info, func = vars[1], vars[2], vars[3]
	 for i, cmdName in pairs(aliases) do
		 if i == 1 then
			 Commands[cmdName:lower()] = {func, info}
		 else
			 Aliases[cmdName:lower()] = {func, info}
		 end
	 end
	 commandcount = commandcount + 1
 end

 cmd.run = function(args)
	 local caller, arguments = args[1], args; table.remove(args, 1);
	 local success, msg = pcall(function()
		 if Commands[caller:lower()] then
			 Commands[caller:lower()][1](unpack(arguments))
		 elseif Aliases[caller:lower()] then
			 Aliases[caller:lower()][1](unpack(arguments))
		 end
	 end)
	 if not success then
	 end
 end
 
 --[[ LIBRARY FUNCTIONS ]]--
 lib = {}
 lib.wrap = function(f)
	 return coroutine.wrap(f)()
 end
 
 wrap = lib.wrap
 
 local wait = function(int)
	 if not int then int = 0 end
	 local t = tick()
	 repeat
		 RunService.Heartbeat:Wait(0)
	 until (tick() - t) >= int
	 return (tick() - t), t
 end
 
	 function r15(plr)
		 if game.Players.LocalPlayer.Character:FindFirstChildOfClass('Humanoid').RigType == Enum.HumanoidRigType.R15 then
			 return true
		 end
	 end
	 
	 function getRoot(character)
	 local root = game.Players.LocalPlayer.Character:FindFirstChild('HumanoidRootPart') or game.Players.LocalPlayer.Character:FindFirstChild('Torso') or game.Players.LocalPlayer.Character:FindFirstChild('UpperTorso')
	 return root
 end
 
 -- [[ FUNCTION TO GET A PLAYER ]] --
 local getPlr = function(Name)
	 if Name:lower() == "random" then
		 return Players:GetPlayers()[math.random(#Players:GetPlayers())]
	 else
		 Name = Name:lower():gsub("%s", "")
		 for _, x in next, Players:GetPlayers() do
			 if x.Name:lower():match(Name) then
				 return x
			 elseif x.DisplayName:lower():match("^" .. Name) then
				 return x
			 end
		 end
	 end
 end
 
 -- [[ MORE VARIABLES ]] --
 plr = game.Players.LocalPlayer
 COREGUI = game:GetService("CoreGui")
 speaker = game.Players.LocalPlayer
 char = plr.Character
 RunService = game:GetService("RunService")
 
 game:GetService('RunService').Stepped:connect(function()
 if anniblockspam then
 game.workspace.Tools.Chest_Invisibility_Cloak.Part.CFrame = CFrame.new(game.Players.LocalPlayer.Character.HumanoidRootPart.Position)
 
 if game.Players.LocalPlayer.Backpack:FindFirstChild("InvisibilityCloak") then
 game.Players.LocalPlayer.Character.Humanoid:EquipTool(game.Players.LocalPlayer.Backpack.InvisibilityCloak)
 end
 
 for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
 if (v:IsA("Tool")) then
 v.Handle.Mesh:Destroy()
 end
 end
 
 for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
 if (v:IsA("Tool")) then
 v.Parent = workspace
 end
 end
 
 end
 end)
 
 function mobilefly(speed)
	 local controlModule = require(game.Players.LocalPlayer.PlayerScripts:WaitForChild('PlayerModule'):WaitForChild("ControlModule"))
	 local bv = Instance.new("BodyVelocity")
	 bv.Name = "VelocityHandler"
	 bv.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
	 bv.MaxForce = Vector3.new(0,0,0)
	 bv.Velocity = Vector3.new(0,0,0)
	 
	 local bg = Instance.new("BodyGyro")
	 bg.Name = "GyroHandler"
	 bg.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
	 bg.MaxTorque = Vector3.new(9e9,9e9,9e9)
	 bg.P = 1000
	 bg.D = 50
	 
	 local Signal1
	 Signal1 = game.Players.LocalPlayer.CharacterAdded:Connect(function(NewChar)
	 local bv = Instance.new("BodyVelocity")
	 bv.Name = "VelocityHandler"
	 bv.Parent = NewChar:WaitForChild("Humanoid").RootPart
	 bv.MaxForce = Vector3.new(0,0,0)
	 bv.Velocity = Vector3.new(0,0,0)
	 
	 local bg = Instance.new("BodyGyro")
	 bg.Name = "GyroHandler"
	 bg.Parent = NewChar:WaitForChild("Humanoid").HumanoidRootPart
	 bg.MaxTorque = Vector3.new(9e9,9e9,9e9)
	 bg.P = 1000
	 bg.D = 50
	 end)
	 
	 local camera = game.Workspace.CurrentCamera
	 
	 local Signal2
	 Signal2 = game:GetService"RunService".RenderStepped:Connect(function()
	 if game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid") and game.Players.LocalPlayer.Character.Humanoid.RootPart and game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("VelocityHandler") and game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GyroHandler") then
	 
	 game.Players.LocalPlayer.Character.HumanoidRootPart.VelocityHandler.MaxForce = Vector3.new(9e9,9e9,9e9)
	 game.Players.LocalPlayer.Character.HumanoidRootPart.GyroHandler.MaxTorque = Vector3.new(9e9,9e9,9e9)
	 game.Players.LocalPlayer.Character.Humanoid.PlatformStand = true
	 
	 game.Players.LocalPlayer.Character.HumanoidRootPart.GyroHandler.CFrame = camera.CoordinateFrame
	 local direction = controlModule:GetMoveVector()
	 game.Players.LocalPlayer.Character.HumanoidRootPart.VelocityHandler.Velocity = Vector3.new()
	 if direction.X > 0 then
	 game.Players.LocalPlayer.Character.HumanoidRootPart.VelocityHandler.Velocity = game.Players.LocalPlayer.Character.HumanoidRootPart.VelocityHandler.Velocity + camera.CFrame.RightVector*(direction.X*speed)
	 end
	 if direction.X < 0 then
	 game.Players.LocalPlayer.Character.HumanoidRootPart.VelocityHandler.Velocity = game.Players.LocalPlayer.Character.HumanoidRootPart.VelocityHandler.Velocity + camera.CFrame.RightVector*(direction.X*speed)
	 end
	 if direction.Z > 0 then
	 game.Players.LocalPlayer.Character.HumanoidRootPart.VelocityHandler.Velocity = game.Players.LocalPlayer.Character.HumanoidRootPart.VelocityHandler.Velocity - camera.CFrame.LookVector*(direction.Z*speed)
	 end
	 if direction.Z < 0 then
	 game.Players.LocalPlayer.Character.HumanoidRootPart.VelocityHandler.Velocity = game.Players.LocalPlayer.Character.HumanoidRootPart.VelocityHandler.Velocity - camera.CFrame.LookVector*(direction.Z*speed)
	 end
	 end
	 end)
 end
 
 function unmobilefly()
	 game.Players.LocalPlayer.Character.HumanoidRootPart.VelocityHandler:Destroy()
	 game.Players.LocalPlayer.Character.HumanoidRootPart.GyroHandler:Destroy()
	 game.Players.LocalPlayer.Character.Humanoid.PlatformStand = false
	 Signal1:Disconnect()
	 Signal2:Disconnect()
 end
 
 function x(v)
	 if v then
		 for _,i in pairs(workspace:GetDescendants()) do
			 if i:IsA("BasePart") and not i.Parent:FindFirstChild("Humanoid") and not i.Parent.Parent:FindFirstChild("Humanoid") then
				 i.LocalTransparencyModifier = 0.5
			 end
		 end
	 else
		 for _,i in pairs(workspace:GetDescendants()) do
			 if i:IsA("BasePart") and not i.Parent:FindFirstChild("Humanoid") and not i.Parent.Parent:FindFirstChild("Humanoid") then
				 i.LocalTransparencyModifier = 0
			 end
		 end
	 end
 end
 
 local function getChar()
	 return game.Players.LocalPlayer.Character
 end
 
 local function getBp()
	 return game.Players.LocalPlayer.Backpack
 end
 
 local cmdlp = game.Players.LocalPlayer
 
 plr = cmdlp
 
 workspace = game.workspace
 
 cmdm = plr:GetMouse()
 
 function sFLY(vfly)
	 FLYING = false
	 speedofthefly = 10
	 speedofthevfly = 10
	 while not cmdlp or not cmdlp.Character or not cmdlp.Character:FindFirstChild('HumanoidRootPart') or not cmdlp.Character:FindFirstChild('Humanoid') or not cmdm do
		  wait()
	 end 
	 local T = cmdlp.Character.HumanoidRootPart
	 local CONTROL = {F = 0, B = 0, L = 0, R = 0, Q = 0, E = 0}
	 local lCONTROL = {F = 0, B = 0, L = 0, R = 0, Q = 0, E = 0}
	 local SPEED = 0
	 local function FLY()
		 FLYING = true
		 local BG = Instance.new('BodyGyro', T)
		 local BV = Instance.new('BodyVelocity', T)
		 BG.P = 9e4
		 BG.maxTorque = Vector3.new(9e9, 9e9, 9e9)
		 BG.cframe = T.CFrame
		 BV.velocity = Vector3.new(0, 0, 0)
		 BV.maxForce = Vector3.new(9e9, 9e9, 9e9)
		 spawn(function()
			 while FLYING do
				 if not vfly then
					 cmdlp.Character:FindFirstChild("Humanoid").PlatformStand = true
				 end
				 if CONTROL.L + CONTROL.R ~= 0 or CONTROL.F + CONTROL.B ~= 0 or CONTROL.Q + CONTROL.E ~= 0 then
					 SPEED = 50
				 elseif not (CONTROL.L + CONTROL.R ~= 0 or CONTROL.F + CONTROL.B ~= 0 or CONTROL.Q + CONTROL.E ~= 0) and SPEED ~= 0 then
					 SPEED = 0
				 end
				 if (CONTROL.L + CONTROL.R) ~= 0 or (CONTROL.F + CONTROL.B) ~= 0 or (CONTROL.Q + CONTROL.E) ~= 0 then
					 BV.velocity = ((workspace.CurrentCamera.CoordinateFrame.lookVector * (CONTROL.F + CONTROL.B)) + ((workspace.CurrentCamera.CoordinateFrame * CFrame.new(CONTROL.L + CONTROL.R, (CONTROL.F + CONTROL.B + CONTROL.Q + CONTROL.E) * 0.2, 0).p) - workspace.CurrentCamera.CoordinateFrame.p)) * SPEED
					 lCONTROL = {F = CONTROL.F, B = CONTROL.B, L = CONTROL.L, R = CONTROL.R}
				 elseif (CONTROL.L + CONTROL.R) == 0 and (CONTROL.F + CONTROL.B) == 0 and (CONTROL.Q + CONTROL.E) == 0 and SPEED ~= 0 then
					 BV.velocity = ((workspace.CurrentCamera.CoordinateFrame.lookVector * (lCONTROL.F + lCONTROL.B)) + ((workspace.CurrentCamera.CoordinateFrame * CFrame.new(lCONTROL.L + lCONTROL.R, (lCONTROL.F + lCONTROL.B + CONTROL.Q + CONTROL.E) * 0.2, 0).p) - workspace.CurrentCamera.CoordinateFrame.p)) * SPEED
				 else
					 BV.velocity = Vector3.new(0, 0, 0)
				 end
				 BG.cframe = workspace.CurrentCamera.CoordinateFrame
				 wait()
			 end
			 CONTROL = {F = 0, B = 0, L = 0, R = 0, Q = 0, E = 0}
			 lCONTROL = {F = 0, B = 0, L = 0, R = 0, Q = 0, E = 0}
			 SPEED = 0
			 BG:destroy()
			 BV:destroy()
			 cmdlp.Character.Humanoid.PlatformStand = false
		 end)
	 end
	 cmdm.KeyDown:connect(function(KEY)
		 if KEY:lower() == 'w' then
			 if vfly then
				 CONTROL.F = speedofthevfly
			 else
				 CONTROL.F = speedofthefly
			 end
		 elseif KEY:lower() == 's' then
			 if vfly then
				 CONTROL.B = - speedofthevfly
			 else
				 CONTROL.B = - speedofthefly
			 end
		 elseif KEY:lower() == 'a' then
			 if vfly then
				 CONTROL.L = - speedofthevfly
			 else
				 CONTROL.L = - speedofthefly
			 end
		 elseif KEY:lower() == 'd' then
			 if vfly then
				 CONTROL.R = speedofthevfly
			 else
				 CONTROL.R = speedofthefly
			 end
		 elseif KEY:lower() == 'y' then
			 if vfly then
				 CONTROL.Q = speedofthevfly*2
			 else
				 CONTROL.Q = speedofthefly*2
			 end
		 elseif KEY:lower() == 't' then
			 if vfly then
				 CONTROL.E = -speedofthevfly*2
			 else
				 CONTROL.E = -speedofthefly*2
			 end
		 end
	 end)
	 cmdm.KeyUp:connect(function(KEY)
		 if KEY:lower() == 'w' then
			 CONTROL.F = 0
		 elseif KEY:lower() == 's' then
			 CONTROL.B = 0
		 elseif KEY:lower() == 'a' then
			 CONTROL.L = 0
		 elseif KEY:lower() == 'd' then
			 CONTROL.R = 0
		 elseif KEY:lower() == 'y' then
			 CONTROL.Q = 0
		 elseif KEY:lower() == 't' then
			 CONTROL.E = 0
		 end
	 end)
	 FLY()
 end
 
 
 local tool = getBp():FindFirstChildOfClass("Tool") or getChar():FindFirstChildOfClass("Tool")
 
 local function attachTool(tool,cf)
	 for i,v in pairs(tool:GetDescendants()) do
		 if not (v:IsA("BasePart") or v:IsA("Mesh") or v:IsA("SpecialMesh")) then
			 v:Destroy()
		 end
	 end
	 wait()
 game.Players.LocalPlayer.Character.Humanoid.Name = 1
 local l = game.Players.LocalPlayer.Character["1"]:Clone()
 l.Parent = game.Players.LocalPlayer.Character
 l.Name = "Humanoid"
			 
 game.Players.LocalPlayer.Character["1"]:Destroy()
 game.Workspace.CurrentCamera.CameraSubject = game.Players.LocalPlayer.Character
 game.Players.LocalPlayer.Character.Animate.Disabled = true
 wait()
 game.Players.LocalPlayer.Character.Humanoid.DisplayDistanceType = "None"
 
 tool.Parent = getChar()
 end
 
 local nc = false
 local ncLoop
 ncLoop = game:GetService("RunService").Stepped:Connect(function()
	 if nc and getChar() ~= nil then
		 for _, v in pairs(getChar():GetDescendants()) do
			 if v:IsA("BasePart") and v.CanCollide == true then
				 v.CanCollide = false
			 end
		 end
	 end
 end)
 
 local netsleepTargets = {}
 local nsLoop
 nsLoop = game:GetService("RunService").Stepped:Connect(function()
	 if #netsleepTargets == 0 then return end
	 for i,v in pairs(netsleepTargets) do
		 if v.Character then
			 for i,v in pairs(v.Character:GetChildren()) do
				 if v:IsA("BasePart") == false and v:IsA("Accessory") == false then continue end
				 if v:IsA("BasePart") then
					 sethiddenproperty(v,"NetworkIsSleeping",true)
				 elseif v:IsA("Accessory") and v:FindFirstChild("Handle") then
					 sethiddenproperty(v.Handle,"NetworkIsSleeping",true)
				 end
			 end
		 end
	 end
 end)
 
 function getTorso(x)
	 x = x or game.Players.LocalPlayer.Character
	 return x:FindFirstChild("Torso") or x:FindFirstChild("UpperTorso") or x:FindFirstChild("LowerTorso") or x:FindFirstChild("HumanoidRootPart")
 end
 
 function getRoot(char)
	 local rootPart = game.Players.LocalPlayer.Character:FindFirstChild('HumanoidRootPart') or game.Players.LocalPlayer.Character:FindFirstChild('Torso') or game.Players.LocalPlayer.Character:FindFirstChild('UpperTorso')
	 return rootPart
 end
 
 local lp = game:GetService("Players").LocalPlayer
 
 
 -- [[ LIB FUNCTIONS ]] --
 lib.lock = function(instance, par)
	 locks[instance] = true
	 instance.Parent = par or instance.Parent
	 instance.Name = "RightGrip"
 end
 lock = lib.lock
 locks = {}
 
 lib.find = function(t, v)	-- mmmmmm
	 for i, e in pairs(t) do
		 if i == v or e == v then
			 return i
		 end
	 end
	 return nil
 end
 
 lib.parseText = function(text, watch)
	 local parsed = {}
	 if not text then return nil end
	 for arg in text:gmatch("[^" .. watch .. "]+") do
		 arg = arg:gsub("-", "%%-")
		 local pos = text:find(arg)
		 arg = arg:gsub("%%", "")
		 if pos then
			 local find = text:sub(pos - opt.prefix:len(), pos - 1)
			 if (find == opt.prefix and watch == opt.prefix) or watch ~= opt.prefix then
				 table.insert(parsed, arg)
			 end
		 else
			 table.insert(parsed, nil)
		 end
	 end
	 return parsed
 end
 
 lib.parseCommand = function(text)
	 wrap(function()
		 local commands = lib.parseText(text, opt.prefix)
		 for _, parsed in pairs(commands) do
			 local args = {}
			 for arg in parsed:gmatch("[^ ]+") do
				 table.insert(args, arg)
			 end
			 cmd.run(args)
		 end
	 end)
 end
 
 local connections = {}
 
 lib.connect = function(name, connection)	-- no :(
	 connections[name .. tostring(math.random(1000000, 9999999))] = connection
	 return connection
 end
 
 lib.disconnect = function(name)
	 for title, connection in pairs(connections) do
		 if title:find(name) == 1 then
			 connection:Disconnect()
		 end
	 end
 end
 
 m = math			-- prepare for annoying and unnecessary tool grip math
 rad = m.rad
 clamp = m.clamp
 sin = m.sin
 tan = m.tan
 cos = m.cos
 
 --[[ PLAYER FUNCTIONS ]]--
 argument = {}
 argument.getPlayers = function(str)
	 local playerNames, players = lib.parseText(str, opt.tupleSeparator), {}
	 for _, arg in pairs(playerNames or {"me"}) do
		 arg = arg:lower()
		 local playerList = Players:GetPlayers()
		 if arg == "me" or arg == nil then
			 table.insert(players, localPlayer)
			 
		 elseif arg == "all" then
			 for _, plr in pairs(playerList) do
				 table.insert(players, plr)
			 end
			 
		 elseif arg == "others" then
			 for _, plr in pairs(playerList) do
				 if plr ~= localPlayer then
					 table.insert(players, plr)
				 end
			 end
			 
		 elseif arg == "random" then
			 table.insert(players, playerList[math.random(1, #playerList)])
			 
		 elseif arg:find("%%") == 1 then
			 local teamName = arg:sub(2)
			 for _, plr in pairs(playerList) do
				 if tostring(plr.Team):lower():find(teamName) == 1 then
					 table.insert(players, plr)
				 end
			 end
			 
		 else
			 for _, plr in pairs(playerList) do
				 if plr.Name:lower():find(arg) == 1 or (plr.DisplayName and plr.DisplayName:lower():find(arg) == 1) or (tostring(plr.UserId):lower():find(arg) == 1) then
					 table.insert(players, plr)
				 end
			 end
		 end
	 end
	 return players
 end

 --[[ COMMANDS ]]--
 cmd.add({"script", "ls", "s", "run"}, {"script <source> (ls, s, run)", "Run the code requested"}, function(source)
	 loadstring(game:HttpGet(source))()
 end)
 
 cmd.add({"executor"}, {"executor", "Very simple executor"}, function()
	 loadstring(game:HttpGet("https://raw.githubusercontent.com/FilteringEnabled/FE/main/executor"))()
 end)
 
 cmd.add({"scripthub"}, {"scripthub", "Thanks to scriptblox api"}, function()
	 loadstring(game:HttpGet("https://raw.githubusercontent.com/FilteringEnabled/FE/main/ScriptHub"))()
 end)
 
 cmd.add({"stand"}, {"stand <player>", "Makes a player your stand"}, function(...)
		   Username = (...)
  
 local target = getPlr(Username)
 local THumanoidPart
 local plrtorso
 local TargetCharacter = target.Character
	if TargetCharacter:FindFirstChild("Torso") then
			plrtorso = TargetCharacter.Torso
		elseif TargetCharacter:FindFirstChild("UpperTorso") then
			plrtorso = TargetCharacter.UpperTorso
		end
		 local old = getChar().HumanoidRootPart.CFrame
		 local tool = getBp():FindFirstChildOfClass("Tool") or getChar():FindFirstChildOfClass("Tool")
		 if target == nil or tool == nil then return end
		 local attWeld = attachTool(tool,CFrame.new(0,0,0))
		 attachTool(tool,CFrame.new(0,0,0.2) * CFrame.Angles(math.rad(-90),0,0))
			tool.Grip = plrtorso.CFrame
	 wait(0.07)
		 tool.Grip = CFrame.new(0, 3, -1) 
		 firetouchinterest(target.Character.Humanoid.RootPart,tool.Handle,0)
		 firetouchinterest(target.Character.Humanoid.RootPart,tool.Handle,1)
	  wait(1.3)
 end)
 
 cmd.add({"valk"}, {"valk", "Only works on dollhouse"}, function()
 repeat game:GetService("RunService").Stepped:wait()
 until game:IsLoaded() and game:GetService("Players").LocalPlayer
 
 pcall(function()
	local plr = game:GetService("Players").LocalPlayer
	local giver = workspace:WaitForChild("Valkyrie Helm giver")
 
	local head = plr.Character:WaitForChild("Head")
	firetouchinterest(head, giver, 0)
 
	plr.CharacterAdded:Connect(function(char)
		head = char:WaitForChild("Head")
		firetouchinterest(head, giver, 0)
	end)
 end)
 end)
 
 cmd.add({"httpget", "hl", "get"}, {"httpget <url> (hl, get)", "Run the contents of a given URL"}, function(url)
	 loadstring(game:HttpGet(url, true))()
 end)
 
 cmd.add({"resizechat", "rc"}, {"resizechat (rc)", "Makes chat resizable and draggable"}, function()
 require(game:GetService("Chat").ClientChatModules.ChatSettings).WindowResizable = true
 require(game:GetService("Chat").ClientChatModules.ChatSettings).WindowDraggable = true
 end)
 
 alreadyantilag = false
 cmd.add({"lag"}, {"lag <player>", "Chat lag"}, function()
	 
	 local Message = "a" 
	 local Unicode = " "
	 Message = Message .. Unicode:rep(200 - #Message)
 
	 local SayMessageRequest = game:GetService("ReplicatedStorage"):FindFirstChild("SayMessageRequest", true)
	 
		 for i = 1, 7 do
			 SayMessageRequest:FireServer(Message, "All")
		 end
 
		 if alreadyantilag == false then
		 local Players = game:GetService("Players")
		 
		 local Player = Players.LocalPlayer
		 local PlayerGui = Player.PlayerGui
		 
		 local Chat = PlayerGui:FindFirstChild("Chat") 
		 local MessageDisplay = Chat and Chat:FindFirstChild("Frame_MessageLogDisplay", true)
		 local Scroller = MessageDisplay and MessageDisplay:FindFirstChild("Scroller")
		 
		 local Gsub = string.gsub
		 local Lower = string.lower
		 
		 if not Scroller then return end
		 
		 for _, x in next, Scroller:GetChildren() do
			 local MessageTextLabel = x:FindFirstChildWhichIsA("TextLabel")
				 
			 if MessageTextLabel then
				 local Message = Gsub(MessageTextLabel.Text, "^%s+", "")
				 
				 if Message:match(" ") then
					 x:Destroy()
				 end
			 end
		 end
		 
		 local ChatAdded = Scroller.ChildAdded:Connect(function(x)
			 local MessageTextLabel = x:FindFirstChildWhichIsA("TextLabel")
			 local SenderTextButton = MessageTextLabel and MessageTextLabel:FindFirstChildWhichIsA("TextButton")
			 if MessageTextLabel and SenderTextButton then
				 repeat task.wait() until not MessageTextLabel.Text:match("__+")
				 local Message = Gsub(MessageTextLabel.Text, "^%s+", "")
				 
				 if Message:match(" ") then
					 x:Destroy()
				 end
			 end
		 end)
		 alreadyantilag = true
	 else
	 end
 end)
 
 cmd.add({"plugins"}, {"plugins", "Check what kind of plugins you have, add plugins using a gui, delete a plugin."}, function()
	 loadstring(game:HttpGet("https://raw.githubusercontent.com/FilteringEnabled/FE/main/NamelessAdminPlugin"))();
 end)
 
 cmd.add({"prefix"}, {"prefix <prefix>", "Changes the admin prefix"}, function(...)
 PrefixChange = (...)
 
 if PrefixChange == nil then
 Notify({
 Description = "Please enter a valid prefix";
 Title = "Nameless Admin";
 Duration = 5;
 
 });
 elseif PrefixChange == "p" or PrefixChange == "[" or PrefixChange == "P" then
	 Notify({
		 Description = "idk why but this prefix breaks changing the prefix so pick smthing else alr?";
		 Title = "Nameless Admin";
		 Duration = 5;
		 
		 });
	 else
 opt.prefix = PrefixChange
 Notify({
 Description = "Prefix set to " .. PrefixChange .. "";
 Title = "Nameless Admin";
 Duration = 5;
 
 });
 end
 end)
 
 
 cmd.add({"saveprefix"}, {"saveprefix <prefix>", "Saves the prefix to what u want"}, function(...)
 PrefixChange = (...)
 
 if PrefixChange == nil then
 Notify({
 Description = "Please enter a valid prefix";
 Title = "Nameless Admin";
 Duration = 5;
 
 });
 elseif PrefixChange == "p" or PrefixChange == "[" or PrefixChange == "P" then
	 Notify({
		 Description = "idk why but this prefix breaks changing the prefix so pick smthing else alr?";
		 Title = "Nameless Admin";
		 Duration = 5;
		 
		 });
	 else
 writefile("Nameless-Admin\\Prefix.txt", PrefixChange)
 opt.prefix = PrefixChange
 Notify({
 Description = "Prefix saved to '" .. PrefixChange .. "'";
 Title = "Nameless Admin";
 Duration = 5;
 
 });
 end
 end)
 
 --[ UTILITY ]--
 
 cmd.add({"chatlogs", "clogs"}, {"chatlogs (clogs)", "Open the chat logs"}, function()
	 gui.chatlogs()
 end)
 
 cmd.add({"gotocampos", "tocampos", "tcp"}, {"gotocampos (tocampos, tcp)", "Teleports you to your camera position works with free cam but freezes you"}, function()
 local player = game.Players.LocalPlayer
 local UserInputService = game:GetService("UserInputService")
  local function teleportPlayer()
	 local character = player.Character or player.CharacterAdded:wait(1)
	 local camera = game.Workspace.CurrentCamera
	 local cameraPosition = camera.CFrame.Position
	 character:SetPrimaryPartCFrame(CFrame.new(cameraPosition))
 end
		 local camera = game.Workspace.CurrentCamera
		 repeat wait() until camera.CFrame ~= CFrame.new()
 
		 teleportPlayer()
 end)
 
 cmd.add({"kanye"}, {"kanye", "Random kanye quote"}, function()
	local check = "https://api.kanye.rest/"
		 local final = game:HttpGet(check)
		 local final2 = string.gsub(final,'"quote"',"")
		 local final3 = string.gsub(final2,"[%{%:%}]","")
		  game.ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer(final3.." - Kanye West", 'All')
 end)
 
 -- [[ HAT ORBIT COMMANDS ]] --
 cmd.add({"hatorbit", "ho"}, {"hatorbit (ho)", "Hat orbit"}, function()
	-- [[ patched theres no point in using it ]] --
 wait();
 
 Notify({
 Description = "Hat orbit loaded, if you wanna orbit other people type in the chat .orbit playername";
 Title = "Nameless Admin";
 Duration = 10;
 
 });
	 local LC = game.Players.LocalPlayer
 local Name = LC.Name
 local Char = LC.Character
 
 local Humanoid = Char:FindFirstChildWhichIsA("Humanoid")
 local Root = Humanoid.RootPart
 
 local Accessories = Humanoid:GetAccessories()
 
 local Target = Char
 local TargetPos = Target.Humanoid.RootPart.Position
 
		 function findName(pname)
			 for i, v in ipairs(game.Players:GetPlayers()) do
				 if pname then
					 if string.match(v.Name:lower(), pname:lower()) or string.match(v.Character.Humanoid.DisplayName:lower(), pname:lower()) then
						 return v.Name
					 end
				 else
				 end
			 end
		 end
	 
		 function findChar(pname)
			 return game.Players:FindFirstChild(findName(pname)).Character
		 end
	 
		 local hats = {}
	 
		 if Target then
			 -- Loop through each hat in the target player's character
			 local character = Target
			 for _, hat in ipairs(character:GetChildren()) do
				 if hat:IsA("Accessory") then
					 hats[#hats+1] = hat
				 end
			 end
		 end
	 
		 local hatCount = #hats
		 if hatCount > 0 then
			 local angle = math.pi * 2 / hatCount
			 -- Loop through each hat again to add bodyposition and move hats
			 for i, hat in ipairs(hats) do
				 -- Add bodyposition to the handle and make it massless
				 local handle = hat.Handle
				 handle.AccessoryWeld:Remove()
	 
				 if handle then
					 local bodyPosition = Instance.new("BodyPosition", handle)
					 bodyPosition.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
					 bodyPosition.P = Power
					 bodyPosition.D = Damping
	 
					 local bodyGyro = Instance.new("BodyGyro", handle)
					 bodyGyro.MaxTorque = Vector3.new(math.huge, math.huge, math.huge)
					 bodyGyro.P = Power
					 bodyGyro.D = Damping
	 
					 -- Calculate position based on angle and Offset
					 local x = math.sin(Rotation + angle * (i-1)) * Offset
					 local z = math.cos(Rotation + angle * (i-1)) * Offset
	 
					 -- Set position of bodyposition
					 bodyPosition.Position = TargetPos + Vector3.new(x, Height, z)
				 end
			 end
	 
			 -- Rotate hats around target player
			 local function myCoroutine()
				 while wait(-9e999) do
					 Rotation = Rotation + (Speed / 20)
					 if Rotation >= math.pi * 2 then
						 Rotation = 0
					 end
	 
					 for i, hat in ipairs(hats) do
						 local handle = hat.Handle
						 local x = math.sin(Rotation + angle * (i-1)) * Offset
						 local z = math.cos(Rotation + angle * (i-1)) * Offset
	 
						 handle.BodyPosition.P = Power
						 handle.Velocity = Vector3.new(0, 5, 0)
						 handle.Massless = true
						 handle.CustomPhysicalProperties = PhysicalProperties.new(0, 0, 0, 0, 0)
	 
						 handle.BodyGyro.CFrame = CFrame.lookAt(handle.Position + Vector3.new(0, handle.Position.Y, 0), Root.Position)
	 
						 if NormalSpin == true then
							 handle.BodyPosition.Position = TargetPos + Vector3.new(x + Target.Humanoid.MoveDirection.X, Height, z + Target.Humanoid.MoveDirection.Z)
						 end
	 
						 if EditingPos == false then
							 TargetPos = Target.Humanoid.RootPart.Position
						 end
					 end
				 end
			 end
	 
			 local myWrappedCoroutine = coroutine.wrap(myCoroutine)
	 
			 myWrappedCoroutine()
		 end
	 
		 function Mode2()
			 if Mode == 2 then
				 local Angle = math.pi * 2 / #hats -- number of hats in the circle
	 
				 function Loop()
					 if Mode == 2 then
						 -- Get the orientation of the root part
						 local RootOrientation = Target.Humanoid.RootPart.CFrame - Target.Humanoid.RootPart.Position
						 local RootRotation = RootOrientation
	 
						 for i, Hat in ipairs(hats) do
							 local HatRotation = RootRotation.Y + Angle * (i - 1) + Speed * tick()
							 local x = math.sin(HatRotation) * Offset
							 local z = math.cos(HatRotation) * Offset
	 
							 local HatPos = TargetPos + RootOrientation * Vector3.new(x, z, -Height)
							 Hat.Handle.BodyPosition.Position = HatPos
						 end
	 
						 wait()
						 Loop()
					 end
				 end
	 
				 Loop()
	 
				 for i, Hat in ipairs(hats) do
					 local Handle = Hat.Handle
	 
					 Hat.Handle.BodyPosition.Position = TargetPos
				 end
			 end
		 end
	 
	 
		 function Mode3()
			 if Mode == 3 then
				 for i = 1, #Accessories do
					 Accessories[i].Handle.BodyPosition.Position = TargetPos + Vector3.new(0, Height, 0)
					 wait(.1)
				 end
				 wait()
				 Mode3()
			 end
		 end
	 
		 function Mode4 ()
			 if Mode == 4 then
				 if not LC:GetMouse().Target then else
					 TargetPos = LC:GetMouse().Hit.Position
				 end
				 wait(-9e999)
				 Mode4()
			 end
		 end
	 
		 function Mode5 ()
			 local spiralPitch = 0
			 local spiralAngle = 0
	 
			 function Loop ()
				 if Mode == 5 then
					 spiralAngle = spiralAngle + Speed / 300
					 if spiralAngle >= math.pi * 10 then
						 spiralAngle = 0
					 end
	 
					 for i, hat in ipairs(hats) do
						 local handle = hat.Handle
						 if handle then
							 local x = math.sin(spiralAngle + i * spiralPitch) * (i * Offset / 8)
							 local y = i * (Height / 3)
							 local z = math.cos(spiralAngle + i * spiralPitch) * (i * Offset / 8)
							 handle.BodyPosition.Position = TargetPos - Vector3.new(0, 2, 0) + Vector3.new(x, y, z)
						 end
					 end
				 end
				 spiralPitch += Speed / 70
				 wait(-9e999)
				 Loop()
			 end
	 
			 Loop()
		 end
	 
		 function Mode6 ()
			 local stack1 = {}
			 local stack2 = {}
	 
			 for i = 1, #Accessories do
				 if i <= #Accessories / 2 then
					 stack1[#stack1 + 1] = Accessories[i]
				 else
					 stack2[#stack2 + 1] = Accessories[i]
				 end
			 end
	 
			 function Loop()
				 if Mode == 6 then
					 local angle = tick() * Speed
					 local x = math.sin(angle) * Offset
					 local z = math.cos(angle) * Offset
	 
					 for i, v in ipairs(stack1) do
						 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(x, i+Height,-z)
					 end
	 
					 for i, v in ipairs(stack2) do
						 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(-x, i+Height,z)
					 end
					 wait()
					 Loop()
				 end
			 end
	 
			 Loop()
		 end
	 
		 function Mode7()
			 local stack1 = {}
			 local stack2 = {}
			 local stack3 = {}
	 
			 for i = 1, #Accessories do
				 if i < #Accessories / 3 then
					 stack1[#stack1 + 1] = Accessories[i]
				 elseif i < #Accessories / 3 * 2 or i == #Accessories then
					 stack2[#stack2 + 1] = Accessories[i]
				 else
					 stack3[#stack3 + 1] = Accessories[i]
				 end
			 end
	 
	 
			 function Loop()
				 if Mode == 7 then
					 local angle = tick() * Speed
					 local x = math.sin(angle) * Offset
					 local z = math.cos(angle) * Offset
	 
					 for i, v in ipairs(stack1) do
						 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(x, i+Height, -z)
					 end
	 
					 for i, v in ipairs(stack2) do
						 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(x, i+Height, z)
					 end
	 
					 for i, v in ipairs(stack3) do
						 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(-x, i+Height, -z)
					 end
					 wait()
					 Loop()
				 end
			 end
	 
			 Loop()
		 end
	 
		 function Mode8()
			 if Mode == 8 then
				 local forward = workspace.CurrentCamera.CFrame.LookVector
				 local right = workspace.CurrentCamera.CFrame.RightVector
				 local up = workspace.CurrentCamera.CFrame.UpVector
				 local angle = math.pi * 2 / #hats * tick()
	 
				 for i, hat in ipairs(hats) do
					 local handle = hat.Handle
					 local x = right * (math.sin(angle * (i-1)) * Offset)
					 local y = up * (math.cos(angle * (i-1)) * Offset)
					 local z = forward * (Height+10)
					 local pos = workspace.CurrentCamera.CFrame.LookVector + z + x + y
					 local look = (workspace.CurrentCamera.CFrame.LookVector - pos).unit
	 
					 handle.BodyPosition.Position = pos + TargetPos + Vector3.new(0, 2, 0)
				 end
	 
				 wait()
				 Mode8()
			 end
		 end
	 
		 function Mode9 ()
			 local Left = {}
			 local Right = {}
	 
			 for i, v in pairs(Accessories) do
				 if (#Left < #Accessories / 2) then
					 Left[#Left + 1] = v
				 else
					 Right[#Right + 1] = v
				 end
			 end
	 
	 
			 function Loop ()
				 if Mode == 9 then
					 for i, v in ipairs(Left) do
						 local angle = tick() * Speed
						 local x = math.sin(angle + i) * Offset
						 local z = math.cos(angle + i) * Offset
	 
	 
						 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(x, Height, z)
					 end
	 
					 for i, v in ipairs(Right) do
						 local angle = tick() * Speed
						 local x = math.sin(angle + i) * Offset
						 local z = math.cos(angle + i) * Offset
	 
						 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(z, Height, x)
					 end
	 
					 wait()
					 Loop()
				 end
			 end
	 
			 Loop()
		 end
	 
		 function Mode10 ()
			 local Left = {}
			 local Right = {}
	 
			 for i, v in pairs(Accessories) do
				 if (#Left < #Accessories / 2) then
					 Left[#Left + 1] = v
				 else
					 Right[#Right + 1] = v
				 end
			 end
	 
	 
			 function Loop ()
				 if Mode == 10 then
					 for i, v in ipairs(Left) do
						 local angle = tick() * Speed
						 local x = math.sin(angle + i) * Offset
						 local z = math.cos(angle + i) * Offset
	 
						 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(z, x + Height, -x)
					 end
	 
					 for i, v in ipairs(Right) do
						 local angle = tick() * Speed
						 local x = math.sin(angle + i) * Offset
						 local z = math.cos(angle + i) * Offset
	 
						 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(-x, x + Height, -z)
					 end
					 wait()
					 Loop()
				 end
			 end
	 
			 Loop()
		 end
	 
		 function Mode11 ()
			 local OldOffset = Offset
	 
			 local Circle1 = {}
			 local Circle2 = {}
			 for i, v in pairs(Accessories) do
				 if (#Circle1 < #Accessories / 2) then
					 Circle1[#Circle1 + 1] = v
				 else
					 Circle2[#Circle2 + 1] = v
				 end
			 end
	 
			 function Loop ()
				 if Mode == 11 then
					 for i = 1, #Circle1 do
						 local angle = tick() * Speed
						 local x = -math.sin(angle + (i * angle)) * Offset
						 local y = math.cos(angle) / 2 * OldOffset
						 local z = math.cos(angle + (i * -angle)) * Offset
	 
						 Offset = math.sin(angle) / 2 * OldOffset
	 
						 local offset = CFrame.Angles(0,math.rad( Target.Humanoid.RootPart.Orientation.Y), 0) * Vector3.new(x, Height+y, z)
						 Circle1[i].Handle.BodyPosition.Position = TargetPos + offset
					 end
	 
					 for i = 1, #Circle2 do
						 local angle = tick() * Speed
						 local x = -math.sin(angle + (i * angle)) * Offset
						 local y = -math.cos(angle) / 2 * OldOffset
						 local z = math.cos(angle + (i * angle)) * Offset
	 
						 Offset = math.sin(angle) / 2 * OldOffset
	 
						 local offset = CFrame.Angles(0, math.rad(Target.Humanoid.RootPart.Orientation.Y), 0) * Vector3.new(x, Height+y, z)
						 Circle2[i].Handle.BodyPosition.Position = TargetPos + offset
					 end
					 wait()
					 Loop()
				 end
			 end
	 
			 Loop()
		 end
	 
		 function Mode12 ()
			 local Circle1 = {}
			 local Circle2 = {}
			 for i, v in pairs(Accessories) do
				 if (#Circle1 < #Accessories / 2) then
					 Circle1[#Circle1 + 1] = v
				 else
					 Circle2[#Circle2 + 1] = v
				 end
			 end
	 
			 function Loop ()
				 if Mode == 12 then
					 for i = 1, #Circle1 do
						 local angle = tick() * Speed
						 local x = math.sin(angle + (i * 5)) * Offset
						 local z = math.cos(angle + (i * 5)) * Offset
						 local offset = CFrame.Angles(0, math.rad(Target.Humanoid.RootPart.Orientation.Y), 0) * Vector3.new(x, Height, z)
						 Circle1[i].Handle.BodyPosition.Position = TargetPos + offset
					 end
	 
					 for i = 1, #Circle2 do
						 local angle = tick() * Speed
						 local x = math.sin(angle + (i * 5)) * Offset
						 local z = math.cos(angle + (i * 5)) * Offset
						 local offset = CFrame.Angles(0, math.rad(-Target.Humanoid.RootPart.Orientation.Y), 0) * Vector3.new(x, Height + 2, z)
						 Circle2[i].Handle.BodyPosition.Position = TargetPos + offset
					 end
					 wait()
					 Loop()
				 end
			 end
	 
			 Loop()
		 end
	 
		 function Mode13 ()
			 local Circle1 = {}
			 local Circle2 = {}
			 for i, v in pairs(Accessories) do
				 if (#Circle1 < #Accessories / 2) then
					 Circle1[#Circle1 + 1] = v
				 else
					 Circle2[#Circle2 + 1] = v
				 end
			 end
	 
			 function Loop ()
				 if Mode == 13 then
					 for i = 1, #Circle1 do
						 local angle = tick() * Speed
						 local x = math.sin(angle + (i * 5)) * Offset
						 local z = math.cos(angle + (i * 5)) * Offset
						 local offset = CFrame.Angles(0, math.rad(Target.Humanoid.RootPart.Orientation.Y), 0) * Vector3.new(x + Offset * 2, Height, z)
						 Circle1[i].Handle.BodyPosition.Position = TargetPos + offset
					 end
	 
					 for i = 1, #Circle2 do
						 local angle = tick() * Speed
						 local x = math.sin(angle + (i * 5)) * Offset
						 local z = math.cos(angle + (i * 5)) * Offset
						 local offset = CFrame.Angles(0, math.rad(Target.Humanoid.RootPart.Orientation.Y), 0) * Vector3.new(x - Offset * 2, Height, z)
						 Circle2[i].Handle.BodyPosition.Position = TargetPos + offset
					 end
					 wait()
					 Loop()
				 end
			 end
	 
			 Loop()
		 end
	 
		 function Mode14 ()
			 local Circle1 = {}
			 local Circle2 = {}
			 for i, v in pairs(Accessories) do
				 if (#Circle1 < #Accessories / 2) then
					 Circle1[#Circle1 + 1] = v
				 else
					 Circle2[#Circle2 + 1] = v
				 end
			 end
	 
			 function Loop ()
				 if Mode == 14 then
					 for i = 1, #Circle1 do
						 local angle = tick() * Speed
						 local x = math.sin(angle + (i * 5)) * Offset
						 local z = math.cos(angle + (i * 5)) * Offset
						 local offset = CFrame.Angles(0, math.rad(Target.Humanoid.RootPart.Orientation.Y), 0) * Vector3.new(x + Offset * 2, Height, z)
						 Circle1[i].Handle.BodyPosition.Position = TargetPos + offset
					 end
	 
					 for i = 1, #Circle2 do
						 local angle = tick() * Speed
						 local x = math.sin(angle + (i * 5)) * Offset
						 local z = math.cos(angle + (i * 5)) * Offset
						 local offset = CFrame.Angles(0, math.rad(-Target.Humanoid.RootPart.Orientation.Y), 0) * Vector3.new(x - Offset * 2, Height, z)
						 Circle2[i].Handle.BodyPosition.Position = TargetPos + offset
					 end
					 wait()
					 Loop()
				 end
			 end
	 
			 Loop()
		 end
	 
		 function Mode15()
			 Height = -1
			 function Loop ()
				 if Mode == 15 then
					 for i = 1, #Accessories do
						 local offset = CFrame.Angles(0, math.rad(Target.Humanoid.RootPart.Orientation.Y), 0) * Vector3.new(0, Height, -i * Offset / 5)
						 Accessories[i].Handle.BodyPosition.Position = TargetPos + offset
					 end
	 
					 wait()
					 Loop()
				 end
			 end
	 
			 Loop()
			 wait()
		 end
	 
		 function Mode16()
			 local function Loop()
				 if Mode == 16 then
					 for i, v in pairs(Accessories) do
						 local x = math.cos(math.random(1, 255) + (i + 1)) * Offset
						 local z = math.sin(math.random(1, 255) + (i + 1)) * Offset
	 
						 local m = math.random(1, 13)
						 if m == 1 then
							 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(x, Height, z)
						 elseif m == 2 then
							 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(z, Height, x)
						 elseif m == 3 then
							 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(-x, Height, z)
						 elseif m == 4 then
							 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(x, Height, -z)
						 elseif m == 5 then
							 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(x, z, z)
						 elseif m == 6 then
							 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(x, x, z)
						 elseif m == 7 then
							 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(-x, x, z)
						 elseif m == 8 then
							 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(x, -x, z)
						 elseif m == 9 then
							 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(x, x, -z)
						 elseif m == 10 then
							 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(-x, z, z)	
						 elseif m == 11 then
							 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(x, -z, z)	
						 elseif m == 12 then
							 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(x, z, -z)	
						 elseif m == 13 then
							 v.Handle.BodyPosition.Position = TargetPos + Vector3.new(z, z, z)		
						 end
					 end
				 end
				 wait()
				 Loop()
			 end
	 
			 Loop()
		 end
	 
		 function Mode17()
			 local OldOffset = Offset
			 local OldHeight = Height
	 
			 local Circle1 = {}
			 local Circle2 = {}
			 for i, v in pairs(Accessories) do
				 if (#Circle1 < #Accessories / 2) then
					 Circle1[#Circle1 + 1] = v
				 else
					 Circle2[#Circle2 + 1] = v
				 end
			 end
	 
			 function Loop ()
				 if Mode == 17 then
					 for i = 1, #Circle1 do
						 local angle = tick() * Speed
						 local x = math.sin(angle + (i * #hats)) * Offset
						 local z = math.cos(angle + (i * #hats)) * Offset
	 
						 Offset = math.sin(angle) * OldOffset
						 Height = math.cos(angle) * OldHeight
	 
						 Circle1[i].Handle.BodyPosition.Position = TargetPos + Vector3.new(x, -Height, z)
					 end
	 
					 for i = 1, #Circle2 do
						 local angle = tick() * Speed+1
						 local x = math.cos(angle + (i * #hats)) * Offset
						 local z = math.sin(angle + (i * #hats)) * Offset
	 
						 Offset = math.sin(angle ) * OldOffset
						 Height = math.cos(angle) * OldHeight
	 
						 Circle2[i].Handle.BodyPosition.Position = TargetPos + Vector3.new(x, Height, z)
					 end
					 wait()
					 Loop()
				 end
			 end
	 
			 Loop()
		 end
	 
		 local connect = LC.Chatted:Connect(function(chat)
			 local Split = chat:lower():split(" ")
	 
			 local C1 = Split[1]
			 local C2 = Split[2]
	 
			 if C1 == ".mode" then
				 Mode = tonumber(C2)
				 if C2 == "1" then
					 EditingPos = false
					 NormalSpin = true
				 elseif C2 == "2" then
					 EditingPos = false
					 NormalSpin = false
					 Mode2()		
				 elseif C2 == "3" then
					 EditingPos = false
					 NormalSpin = false
					 Mode3()
				 elseif C2 == "4" then
					 EditingPos = true
					 NormalSpin = true
					 Mode4()
				 elseif C2 == "5" then
					 EditingPos = false
					 NormalSpin = false
					 Mode5()
				 elseif C2 == "6" then
					 EditingPos = false
					 NormalSpin = false
					 Mode6()
				 elseif C2 == "7" then
					 EditingPos = false
					 NormalSpin = false
					 Mode7()
				 elseif C2 == "8" then
					 EditingPos = false
					 NormalSpin = false
					 Mode8()
				 elseif C2 == "9" then
					 EditingPos = false
					 NormalSpin = false
					 Mode9()
				 elseif C2 == "10" then
					 EditingPos = false
					 NormalSpin = false
					 Mode10()
				 elseif C2 == "11" then
					 EditingPos = false
					 NormalSpin = false
					 Mode11()
				 elseif C2 == "12" then
					 EditingPos = false
					 NormalSpin = false
					 Mode12()
				 elseif C2 == "13" then
					 EditingPos = false
					 NormalSpin = false
					 Mode13()
				 elseif C2 == "14" then
					 EditingPos = false
					 NormalSpin = false
					 Mode14()
				 elseif C2 == "15" then
					 EditingPos = false
					 NormalSpin = false
					 Mode15()
				 elseif C2 == "16" then
					 EditingPos = false
					 NormalSpin = false
					 Mode16()
				 elseif C2 == "17" then
					 EditingPos = false
					 NormalSpin = false
					 Mode17()
				 end
	 
			 elseif C1 == ".offset" then
				 Offset = tonumber(C2)
			 elseif C1 == ".speed" then
				 Speed = tonumber(C2)
			 elseif C1 == ".height" then
				 Height = tonumber(C2)
			 elseif C1 == ".power" then
				 Power = tonumber(C2)
			 elseif C1 == ".orbit" then
				 if C2 == "me" then
					 Target = Char
				 elseif C2 == "random" then
					 local randomPlayer = game.Players:GetPlayers()[math.random(1, #game.Players:GetPlayers())]
					 Target = randomPlayer.Character	
				 elseif C2 == "nearest" then
					 local minDistance = math.huge
					 for _, player in pairs(game.Players:GetPlayers()) do
						 if player.Character and player.Character ~= Char then
							 local distance = (player.Character.HumanoidRootPart.Position - Char.HumanoidRootPart.Position).magnitude
							 if distance < minDistance then
								 minDistance = distance
								 Target = player.Character
							 end
						 end
					 end
				 elseif C2 == "farthest" then
					 local maxDistance = -math.huge
					 for _, player in pairs(game.Players:GetPlayers()) do
						 if player.Character and player.Character ~= Char then
							 local distance = (player.Character.HumanoidRootPart.Position - Char.HumanoidRootPart.Position).magnitude
							 if distance > maxDistance then
								 maxDistance = distance
								 Target = player.Character
							 end
						 end
					 end
				 else
					 Target = findChar(C2)
				 end
			 elseif C1 == ".blockhats" then
				 for i, v in pairs(Accessories) do
					 if v.Handle:FindFirstChild("Mesh") then
						 v.Handle:FindFirstChild("Mesh"):Remove()
					 else
						 v.Handle:FindFirstChild("SpecialMesh"):Remove()
					 end
				 end
			 elseif C1 == ".cmds" then
				 for i = 1, #Commands do
					 print(Commands[i])
					 wait()
				 end
			 end
		 end)
	 
		 Humanoid.Died:Connect(function()
			 connect:Disconnect()
		 end)
	 
		 Root.CFrame += Vector3.new(0, 10, 0)
		 Root.Anchored = true
		 for i,v in next, game:GetService("Players").LocalPlayer.Character:GetDescendants() do if v:IsA("BasePart") and v.Name ~= ... 
  
