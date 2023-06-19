# On Init
```lua
aura_env.prefix,aura_env.icon,aura_env.showDura = "COZ_CD_ASSIGN",134300, 3
aura_env.regAddonMessagePrefix = C_ChatInfo.IsAddonMessagePrefixRegistered(aura_env.prefix)
if not aura_env.regAddonMessagePrefix then C_ChatInfo.RegisterAddonMessagePrefix(aura_env.prefix) end
aura_env.SplitMSG = function(msg, d)
  local split_msg = {} 
  for part in msg:gmatch("([^"..d.."]+)") do
    table.insert(split_msg, part)
  end
  return split_msg
end
```
[x] Play Sound
# Trigger 1
##### Event
`CHAT_MSG_ADDON`
```lua
function(event, pf, content, channel) 
  if pf ~= aura_env.prefix then
    return false
  else
    if channel == "RAID" or channel == "PARTY" then
      local s_msg = aura_env.SplitMSG(content, ";")
      if (UnitIsGroupAssistant(s_msg[1]) or UnitIsGroupLeader(s_msg[1])) then
        if s_msg[2] == UnitName("player") then
          aura_env.assignedPlayer = s_msg[2]
          aura_env.cdToUse = tonumber(s_msg[3])      
          local delay = tonumber(s_msg[4]) or 0
          aura_env.amIcon = tonumber(s_msg[5]) or 0
          aura_env.duration = aura_env.showDura + delay 
          return true
        end
      end
    end
  end
end
```
## Duration
```lua
function()
  local duration = aura_env.duration
  local expirationTime = GetTime() + aura_env.duration
  return duration, expirationTime
end
```
## Name
```lua
function()
  if WeakAuras.IsOptionsOpen() then
    return "Divine Guardian"
  else
    local cdName = (select(1,GetSpellInfo(aura_env.cdToUse)))
    if cdName == "Kick" then
      cdName = "Interrupt"
    end
    return cdName
  end  
end
```
## Icon
```lua
function()
  if WeakAuras.IsOptionsOpen() then return 253400 end
  if aura_env.cdToUse == 31821 and aura_env.amIcon ~= 0 then
    aura_env.icon = tonumber((select(3,GetSpellInfo(aura_env.amIcon))))
  else
    aura_env.icon = tonumber((select(3,GetSpellInfo(aura_env.cdToUse))))
  end
  return aura_env.icon
end
```