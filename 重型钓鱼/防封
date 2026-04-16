getgenv().AntiAC = true
getgenv().ClearLogs = true

if rconsoleclear then rconsoleclear() end
if consoleclear then consoleclear() end

do
    local _print = print
    local _warn = warn
    local _error = error
    print = function(...) end
    warn = function(...) end
    error = function(...) end
    task.delay(1, function()
        print = _print
        warn = _warn
        error = _error
    end)
end

local function BlockDetect()
    local blocked = {
        "getrenv", "getgenv", "getproto", "getupvalues", "setupvalues",
        "getconstants", "getstack", "getinfo", "getmetatable", "setmetatable",
        "isexecutor", "isvm", "getexecutorname", "identifyexecutor",
        "checkclosure", "isclosure", "iscclosure", "islclosure",
        "getthreadidentity", "setthreadidentity", "getnamecallmethod",
        "getconnections", "getreg", "getgc", "getthread", "getsynapseproto"
    }
    for _, name in pairs(blocked) do
        if rawget(_G, name) then
            rawset(_G, name, function() end)
        end
        if rawget(getgenv(), name) then
            rawset(getgenv(), name, function() end)
        end
    end
end

local function CleanTraces()
    local allow = {
        "NWKZ_AutoCast", "NWKZ_Anchor", "NWKZ_AutoSell",
        "AutoZ", "AutoX", "AutoC", "AutoV", "AutoCalibrate",
        "AntiAC", "ClearLogs", "RandWait"
    }
    for k, v in pairs(getgenv()) do
        local ok = false
        for _, a in pairs(allow) do
            if k == a then ok = true break end
        end
        if not ok and type(v) == "function" then
            getgenv()[k] = nil
        end
    end
    for k in pairs(getgenv()) do
        local ok = false
        for _, a in pairs(allow) do
            if k == a then ok = true break end
        end
        if not ok and type(getgenv()[k]) == "nil" then
            getgenv()[k] = nil
        end
    end
end

getgenv().RandWait = function(min, max)
    return task.wait(min + math.random() * (max - min))
end

game.Players.LocalPlayer.Idled:Connect(function()
    task.wait(math.random(0.3, 1.5))
    local vu = game:GetService("VirtualUser")
    local p = Vector2.new(math.random(-30,30), math.random(-30,30))
    local cf = workspace.CurrentCamera.CFrame
    vu:Button2Down(p, cf)
    task.wait(0.08 + math.random() * 0.04)
    vu:Button2Up(p, cf)
end)

BlockDetect()
CleanTraces()

task.spawn(function()
    while task.wait(1) do
        BlockDetect()
        CleanTraces()
    end
end)
