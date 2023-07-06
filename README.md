local library = loadstring(game:HttpGet('https://raw.githubusercontent.com/cypherdh/VanisUILIB/main/.gitignore'))()

local Window = library:CreateWindow("Shadow Hub", "Version v2.1", 2.1)

local Tab = Window:CreateTab("Scripts")

local Page2 = Tab:CreateFrame("Humanoid")
local Page = Tab:CreateFrame("Main page")
Page2:CreateSlider("Walkspeed", 16, 500,function(arg)
   game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = arg
end)

Button = Page2:CreateButton("Fly = g", "Make your fly using g key", function()


local players = game:GetService("Players")
	local lp = players.LocalPlayer
	local Mouses = lp:GetMouse()
	mouse = Mouses
	local workspace = game.Workspace
	function sFLY(vfly)
		FLYING = false
		speedofthefly = 1.5
		speedofthevfly = 1
		while not lp or not lp.Character or not lp.Character:FindFirstChild('HumanoidRootPart') or not lp.Character:FindFirstChild('Humanoid') or not mouse do
			wait()
		end 
		local T = lp.Character.HumanoidRootPart
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
						lp.Character:FindFirstChild("Humanoid").PlatformStand = true
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
				lp.Character.Humanoid.PlatformStand = false
			end)
		end
		mouse.KeyDown:connect(function(KEY)
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
		mouse.KeyUp:connect(function(KEY)
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

	mouse.KeyDown:connect(function(KEY)
		if KEY:lower() == 'g' then
			if FLYING == false then
				sFLY()
			else
				FLYING = false
				lp.Character.Humanoid.PlatformStand = false
			end
		end
	end)
	end)



local InfiniteJumpEnabled;
local Player = game:GetService("Players").LocalPlayer
game:GetService("UserInputService").JumpRequest:Connect(function()
     if InfiniteJumpEnabled then
         Player.Character:WaitForChild("Humanoid"):ChangeState("Jumping")
     end
end)


Toggle = Page2:CreateToggle("Inf jump", "Make ur character jump infinite", function(arg)

  InfiniteJumpEnabled = arg
end)


Label = Page:CreateLabel("Items")

TextBox = Page:CreateBox("Enter Item name here", 10044538000, function(arg)
_G.customabuy = arg
local players = game:GetService("Players")
game:GetService("StarterGui"):SetCore("SendNotification", {
    Title = "SUCESS!";
    Text = "Item Selected , " .. _G.customabuy;
    Icon = "rbxassetid://11157772247";
    Duration = 5
    })
end)

Toggle = Page:CreateToggle("Auto buy", "Make your auto buy item", function(arg)

 if arg then
            _G.on = true
            
            while _G.on == true do
                wait()
            
            wait()
          
		game:GetService("ReplicatedStorage").RemoteEvents.BuyItemCash:FireServer(_G.customabuy)
            
            wait()
            
                end
                else
            _G.on = false
                    
                end
                
end)
Toggle = Page:CreateToggle("Auto sell", "Make your auto sell item", function(arg)

 if arg then
            _G.on = true
            
            while _G.on == true do
                wait()
            
            wait()
        
		game:GetService("ReplicatedStorage").RemoteEvents.Equip:FireServer(_G.customabuy)  
		wait()
		game:GetService("ReplicatedStorage").RemoteEvents.Sell:FireServer(_G.customabuy)

            
            wait()
            
                end
                else
            _G.on = false
                    
                end
            end)



Toggle = Page:CreateToggle("Auto drop", "Make your auto drop item", function(arg)
 if arg then
            _G.on = true
            
            while _G.on == true do
                wait()
            
            wait()
        
		game:GetService("ReplicatedStorage").RemoteEvents.Equip:FireServer(_G.customabuy)  
		wait()
		game:GetService("ReplicatedStorage").RemoteEvents.Drop:FireServer(_G.customabuy)

            
            wait()
            
                end
                else
            _G.on = false
                    
                end
            end)
            
Toggle = Page:CreateToggle("Auto equip", "Make your auto equip item", function(arg)

 if arg then
            _G.on = true
            
            while _G.on == true do
                wait()
            
            wait()
        
		game:GetService("ReplicatedStorage").RemoteEvents.Equip:FireServer(_G.customabuy)  
		

            
            wait()
            
                end
                else
            _G.on = false
                    
                end
            end)
            
            
            
TextBox = Page:CreateBox("Buy any item", 10044538000, function(arg)
_G.custombuy = arg
end)
TextBox = Page:CreateBox("put the number of items you want to buy", 10044538000, function(arg)
for i = 1,arg do
		wait()
		game:GetService("ReplicatedStorage").RemoteEvents.BuyItemCash:FireServer(_G.custombuy)

	end
end)
	
	
Label = Page:CreateLabel("Drop")


Button = Page:CreateButton("Fake drop in gui", "Make a fake drop gui show", function()


loadstring(game:HttpGet("https://raw.githubusercontent.com/Zykarius1/Pop-it-trading-fake-drop-script/main/Pop-it-trading-fake-drop-script"))()


end)




TextBox = Page:CreateBox("Drop Custom Item (x15)", 10044538000, function(arg)
_G.dropcustom = arg
	for i = 1,15 do
		game:GetService("ReplicatedStorage").RemoteEvents.Equip:FireServer(_G.dropcustom)
		wait(0.35)
		game:GetService("ReplicatedStorage").RemoteEvents.Drop:FireServer(_G.dropcustom)
		wait(0.35)
	end
	end)
	
Label = Page:CreateLabel("Fps")
TextBox = Page:CreateBox("Put your fps to cap here", 10044538000, function(arg)
 setfpscap(tonumber(arg))
 end)
 
 
Label = Page:CreateLabel("Others")
Button = Page:CreateButton("Night Mode", "Make your game Get night", function()
local Info = TweenInfo.new(3, Enum.EasingStyle.Exponential)
	if game:GetService("Players").LocalPlayer:GetAttribute("IsDay") then
		game:GetService("TweenService"):Create(game:GetService("Lighting"), Info, {ClockTime = 12}):Play()
		game:GetService("Players").LocalPlayer:SetAttribute("IsDay", false)
	else
		game:GetService("TweenService"):Create(game:GetService("Lighting"), Info, {ClockTime = 0}):Play()
		game:GetService("Players").LocalPlayer:SetAttribute("IsDay", true)
	end

end)
Button = Page:CreateButton("See inventory", "This make your see others inventory", function()
loadstring(game:HttpGet("https://raw.githubusercontent.com/cracked13/HAHAHSDWAHA/main/README.md"))()
end)

Button = Page:CreateButton("Xray", "Get xray gamepass for free", function()
game.Players.localPlayer.XRay.Value = true
end)


Toggle = Page:CreateToggle("Auto Jump", "it will jump automatically", function(arg)

 if arg then
            _G.on = true
            
            while _G.on == true do
                wait()
            
            wait()
        
game:GetService("ReplicatedStorage").RemoteEvents.Jumped:FireServer()		

            
            wait()
            
                end
                else
            _G.on = false
                    
                end
            end)




Button = Page:CreateButton("Nova anti reap", "If reap is back This script make your anti reap!", function()

loadstring(game:HttpGet("https://raw.githubusercontent.com/darckgames0103/ANTINOVA/main/README.md"))()

end)


Button = Page:CreateButton("Dupe", "Make your dupe Any item need 3 pianos or +!", function()



while true do
    wait(.00000000000000000000000000000000000000000000001)
game:GetService("ReplicatedStorage").RemoteEvents.Equip:FireServer("Piano")
end
  

end)





Label = Page:CreateLabel("Tp player")
 local PlayList = {}
for i,v in pairs(game:GetService("Players"):GetPlayers()) do 
    if v ~= game.Players.LocalPlayer then 
        table.insert(PlayList,v.Name)
    end
end



TextBox = Page:CreateBox("Enter player name here", 10044538000, function(arg)
_G.tpPlayer = arg
end)


Button = Page:CreateButton("Tp", "This make your tp to player", function()
local p1 = game.Players.LocalPlayer.Character.HumanoidRootPart
local p2 = _G.tpPlayer
local pos = p1.CFrame

p1.CFrame = game.Players[p2].Character.HumanoidRootPart.CFrame

end)
Label = Page:CreateLabel("Scam")

Button = Page:CreateButton("New Scam V5", "this try to make item secre example: equip a rainbow banana and click on this", function()

--//By Shield Scripts
--[[
What does this do? It makes some items look really weird.
How to use?
1- Equip a random item.
2- Execute.

If it didnt work, repeat with another item.
]]--
for _,c in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
	if c:IsA("Tool") then
		for _,c2 in pairs(c:GetDescendants()) do
			if c2.Name == "Mesh" then
				c2:Destroy()
			end
		end
	end
end
end)

TextBox = Page:CreateBox("Scam v5 custom: try to make your item a secret item", 10044538000, function(arg)
_G.Scamv5 = arg
end)

Button = Page:CreateButton("custom scam v5", "Click here to try to make a item secret", function()
game:GetService("ReplicatedStorage").RemoteEvents.Equip:FireServer(_G.Scamv5)
wait(1)
--//By Shield Scripts
--[[
What does this do? It makes some items look really weird.
How to use?
1- Equip a random item.
2- Execute.

If it didnt work, repeat with another item.
]]--
for _,c in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
	if c:IsA("Tool") then
		for _,c2 in pairs(c:GetDescendants()) do
			if c2.Name == "Mesh" then
				c2:Destroy()
			end
		end
	end
end
end)

Label = Page:CreateLabel("safe zone")
Button = Page:CreateButton("tp to safe zone", "Click here to tp to a safe zone", function()
local lplr = plr.LocalPlayer
                                                                                                                                                                                                                                                                                local lchar = lplr.Character
                                                                                                                                                                                                                                                                                local HRP = lchar.HumanoidRootPart
                                                                                                                                                                                                                                                                                 
                                                                                                                                                                                                                                                                                HRP.CFrame = CFrame.new(-100, 100, -10000)
                                                                                                                                                                                                                                                                                 
                                                                                                                                                                                                                                                                                local C = Instance.new("Part")
                                                                                                                                                                                                                                                                                C.Parent = workspace                                                                                                                                                                                                                                                  
                                                                                                                                                                                                                                                                                C.CFrame = CFrame.new(-101, 50, -10000)
                                                                                                                                                                                                                                                                                C.Size = Vector3.new(100000000, 100, 10000000)                                                                                                                                                                                                                                                                                C.Anchored = true
                                                                                                                                                                                                                                                                                end)
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                 game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
        
        for _, Player in ipairs(game:GetService("Players"):GetPlayers()) do
  if not Player:IsInGroup(14428241) then  -- replace 1 with your group id                  
      Player:Kick("Join on Group or no script acess, Copied to your Clipboard. Or group id is 14428241");
      setclipboard("https://web.roblox.com/groups/14428241/shadow-grupo#!/about")
   end
end
