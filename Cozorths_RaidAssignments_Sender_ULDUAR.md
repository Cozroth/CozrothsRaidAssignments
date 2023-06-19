# On Init
```lua
aura_env.sender = UnitName("player")
aura_env.prefix = "COZ_CD_ASSIGN"
aura_env.isRegistered = C_ChatInfo.IsAddonMessagePrefixRegistered(aura_env.prefix)
if not aura_env.isRegistered then C_ChatInfo.RegisterAddonMessagePrefix(aura_env.prefix) end
aura_env.channel = "RAID"
aura_env.pewpew = false
aura_env.counters = {}
aura_env.AoL = false
aura_env.encounterName = ""
aura_env.newAssigns = {}
aura_env.encounterIds = {
  ["Ignis the Furnace Master"] = 745,
  ["Razorscale"] = 746,
  ["XT-002 Deconstructor"] = 747,
  ["The Iron Council"] = 748,
  ["Kologarn"] = 749,
  ["Auriaya"] = 750,
  ["Hodir"] = 751,
  ["Thorim"] = 752,
  ["Freya"] = 753,
  ["Mimiron"] = 754,
  ["General Vezax"] = 755,
  ["Yogg-Saron"] = 756,
  ["Algalon the Observer"] = 757,
} 
aura_env.crsID = {
  [62437] = true, -- Ground Tremor         10m - Freya
  
  [62776] = true, -- Tantrum            10/25m - XT
  [62859] = true, -- Ground Tremor         25m - Freya
  [62661] = true, -- Searing Flames     10/25m - Vezax
  [62662] = true, -- Surge of Darkness     25m - Vezax
  [64189] = true, -- Deafening Roar        25m - Yogg
}
aura_env.boss_abilities = 
{
  ["Ignis the Furnace Master"] = 
  {
    slowSpellIds = 
    {
      [62680] = true,  -- Flame Jets 10 man
      [63472] = true,  -- Flame Jets 25 man
    },
    channeledSpellIds = nil,
    fastSpellIds = nil,
    buffDebuffSpellIds = nil,
  },
  ["Razorscale"] = 
  {
    slowSpellIds = 
    {
      [63317] = true,  -- Flame Breath 10 man - Razorscale
      [64021] = true,  -- Flame Breath 25 man - Razorscale
    },
    channeledSpellIds = nil,
    fastSpellIds = nil,
    buffDebuffSpellIds = nil,
  },
  ["XT-002 Deconstructor"] = 
  {
    slowSpellIds = 
    {
      [62776] = true,  -- Tantrum 10 / 25 man - XT
    },
    channeledSpellIds = nil,
    fastSpellIds = nil,
    buffDebuffSpellIds = 
    {
      [64193] = true,  -- Heartbreak 25 man - XT Hardmode
      [65737] = true,  -- Heardbreak 10 man - XT Hardmode
    },
  },
  ["The Iron Council"] = 
  {
    slowSpellIds = nil,
    channeledSpellIds = nil,
    fastSpellIds = 
    {
      [61888] = true,  -- Last phase 25 man - Council HM
      [64637] = true,  -- Last phase 10 man - Council HM
    },
    buffDebuffSpellIds = nil,
  },
  ["Kologarn"] = 
  {
    slowSpellIds = nil,
    channeledSpellIds = nil,
    fastSpellIds = nil,
    buffDebuffSpellIds = nil,
  },
  ["Auriaya"] = 
  {
    slowSpellIds = nil,
    channeledSpellIds = nil,
    fastSpellIds = nil,
    buffDebuffSpellIds = nil,
  },
  ["Hodir"] = 
  {
    slowSpellIds = nil,
    channeledSpellIds = nil,
    fastSpellIds = nil,
    buffDebuffSpellIds = 
    {
      [63512] = true,  -- Frozen Blows 25m - Hodir SPELL_AURA_APPLIED
      [62478] = true,  -- Frozen Blows 10m - Hodir SPELL_AURA_APPLIED
    },
  },
  ["Thorim"] = 
  {
    slowSpellIds = nil,
    channeledSpellIds = nil,
    fastSpellIds = 
    {
      [62466] = true,  -- Lightning Charge - start at 5 / 6 dura 14
      [64390] = true,  -- Chain Lightning - 25m
      [62131] = true,  -- Chain Lightning - 10m
    },
    buffDebuffSpellIds = 
    {
      [62130] = true,  -- Unbalancing Strikes - start at 4 dura 14
    },
  },
  ["Freya"] = 
  {
    slowSpellIds = 
    {
      [62437] = true,  -- Ground Tremor 10 man - Freya
      [62859] = true,  -- Ground Tremor 25 man - Freya
    },
    channeledSpellIds = nil,
    fastSpellIds = nil,
    buffDebuffSpellIds = nil,
  },
  ["Mimiron"] = 
  {
    slowSpellIds = 
    {
      [64529] = true,  -- Plasma Blast
    },
    channeledSpellIds = nil,
    fastSpellIds = nil,
    buffDebuffSpellIds = 
    {
      [63677] = true,  -- Heat Wave 10m
      [64533] = true,  -- Heat Wave 25m -- Mimiron -- SPELL_AURA_APPLIED -- C_TIMER ~5 sec
    },
  },
  ["General Vezax"] = 
  {
    slowSpellIds = 
    {
      [62662] = true,  -- Surge of Darkness
      [62661] = true,  -- Searing Flames - intterupt rotation
    },
    channeledSpellIds = nil,
    fastSpellIds = nil,
    buffDebuffSpellIds = nil,
  },
  ["Yogg-Saron"] = 
  {
    slowSpellIds = 
    {
      [64189] = true,-- Deafening Roar
    },
    channeledSpellIds = nil,
    fastSpellIds = nil,
    buffDebuffSpellIds = nil,
  },
  ["Algalon the Observer"] = 
  {
    slowSpellIds = nil,
    channeledSpellIds = nil,
    fastSpellIds = nil,
    buffDebuffSpellIds = nil,
  },
}
---------- COOLDOWN TABLE -------------
local cd_Table = {
  ["Ignis the Furnace Master"] = {
    [1] = 70940, -- "Divine Sacrifice"
    [2] = 31821, -- "Aura Mastery"
    [3] = 10278, -- "Hand of Protection"
    [4] = 1766, -- "Kick" > Change based on class in RECIEVER
    [5] = 64843, -- "Divine Hymn"
    [6] = 64843, -- "Pain Suppression"
    [7] = 6940,  -- "Hand of Sacrifice"
    [8] = 47788, -- "Guardian Spirit"
  },
  ["Razorscale"] = {
    [1] = 70940, -- "Divine Sacrifice"
    [2] = 31821, -- "Aura Mastery"
    [3] = 10278, -- "Hand of Protection"
    [4] = 1766, -- "Kick" > Change based on class in RECIEVER
    [5] = 64843, -- "Divine Hymn"
    [6] = 64843, -- "Pain Suppression"
    [7] = 6940,  -- "Hand of Sacrifice"
    [8] = 47788, -- "Guardian Spirit"
  },
  ["XT-002 Deconstructor"] = {
    [1] = 70940, -- "Divine Sacrifice"
    [2] = 31821, -- "Aura Mastery"
    [3] = 10278, -- "Hand of Protection"
    [4] = 1766, -- "Kick" > Change based on class in RECIEVER
    [5] = 64843, -- "Divine Hymn"
    [6] = 64843, -- "Pain Suppression"
    [7] = 6940,  -- "Hand of Sacrifice"
    [8] = 47788, -- "Guardian Spirit"
  },
  ["The Iron Council"] = {
    [1] = 70940, -- "Divine Sacrifice"
    [2] = 31821, -- "Aura Mastery"
    [3] = 10278, -- "Hand of Protection"
    [4] = 1766, -- "Kick" > Change based on class in RECIEVER
    [5] = 64843, -- "Divine Hymn"
    [6] = 64843, -- "Pain Suppression"
    [7] = 6940,  -- "Hand of Sacrifice"
    [8] = 47788, -- "Guardian Spirit"
  },
  ["Kologarn"] = {
    [1] = 70940, -- "Divine Sacrifice"
    [2] = 31821, -- "Aura Mastery"
    [3] = 10278, -- "Hand of Protection"
    [4] = 1766, -- "Kick" > Change based on class in RECIEVER
    [5] = 64843, -- "Divine Hymn"
    [6] = 64843, -- "Pain Suppression"
    [7] = 6940,  -- "Hand of Sacrifice"
    [8] = 47788, -- "Guardian Spirit"
  },
  ["Auriaya"] = {
    [1] = 70940, -- "Divine Sacrifice"
    [2] = 31821, -- "Aura Mastery"
    [3] = 10278, -- "Hand of Protection"
    [4] = 1766, -- "Kick" > Change based on class in RECIEVER
    [5] = 64843, -- "Divine Hymn"
    [6] = 64843, -- "Pain Suppression"
    [7] = 6940,  -- "Hand of Sacrifice"
    [8] = 47788, -- "Guardian Spirit"
  },
  ["Hodir"] = {
    [1] = 70940, -- "Divine Sacrifice"
    [2] = 31821, -- "Aura Mastery"
    [3] = 10278, -- "Hand of Protection"
    [4] = 1766, -- "Kick" > Change based on class in RECIEVER
    [5] = 64843, -- "Divine Hymn"
    [6] = 64843, -- "Pain Suppression"
    [7] = 6940,  -- "Hand of Sacrifice"
    [8] = 47788, -- "Guardian Spirit"
  },
  ["Thorim"] = {
    [1] = 70940, -- "Divine Sacrifice"
    [2] = 31821, -- "Aura Mastery"
    [3] = 10278, -- "Hand of Protection"
    [4] = 1766, -- "Kick" > Change based on class in RECIEVER
    [5] = 64843, -- "Divine Hymn"
    [6] = 64843, -- "Pain Suppression"
    [7] = 6940,  -- "Hand of Sacrifice"
    [8] = 47788, -- "Guardian Spirit"
  },
  ["Freya"] = {
    [1] = 70940, -- "Divine Sacrifice"
    [2] = 31821, -- "Aura Mastery"
    [3] = 10278, -- "Hand of Protection"
    [4] = 1766, -- "Kick" > Change based on class in RECIEVER
    [5] = 64843, -- "Divine Hymn"
    [6] = 64843, -- "Pain Suppression"
    [7] = 6940,  -- "Hand of Sacrifice"
    [8] = 47788, -- "Guardian Spirit"
  },
  ["Mimiron"] = {
    [1] = 70940, -- "Divine Sacrifice"
    [2] = 31821, -- "Aura Mastery"
    [3] = 10278, -- "Hand of Protection"
    [4] = 1766, -- "Kick" > Change based on class in RECIEVER
    [5] = 64843, -- "Divine Hymn"
    [6] = 64843, -- "Pain Suppression"
    [7] = 6940,  -- "Hand of Sacrifice"
    [8] = 47788, -- "Guardian Spirit"
  },
  ["General Vezax"] = {
    [1] = 70940, -- "Divine Sacrifice"
    [2] = 31821, -- "Aura Mastery"
    [3] = 10278, -- "Hand of Protection"
    [4] = 1766, -- "Kick" > Change based on class in RECIEVER
    [5] = 64843, -- "Divine Hymn"
    [6] = 64843, -- "Pain Suppression"
    [7] = 6940,  -- "Hand of Sacrifice"
    [8] = 47788, -- "Guardian Spirit"
  },
  ["Yogg-Saron"] = {
    [1] = 70940, -- "Divine Sacrifice"
    [2] = 31821, -- "Aura Mastery"
    [3] = 10278, -- "Hand of Protection"
    [4] = 1766, -- "Kick" > Change based on class in RECIEVER
    [5] = 64843, -- "Divine Hymn"
    [6] = 64843, -- "Pain Suppression"
    [7] = 6940,  -- "Hand of Sacrifice"
    [8] = 47788, -- "Guardian Spirit"
  },
  ["Algalon the Observer"] = {
    [1] = 70940, -- "Divine Sacrifice"
    [2] = 31821, -- "Aura Mastery"
    [3] = 10278, -- "Hand of Protection"
    [4] = 1766, -- "Kick" > Change based on class in RECIEVER
    [5] = 64843, -- "Divine Hymn"
    [6] = 64843, -- "Pain Suppression"
    [7] = 6940,  -- "Hand of Sacrifice"
    [8] = 47788, -- "Guardian Spirit"
  },
}
local cd_AM_variant =
{
  ["Ignis the Furnace Master"] = {
    [62680] = 48947, -- Fire Resistance Aura
    [63472] = 48947 -- Fire Resistance Aura
  },
  ["Razorscale"] = {
    [63317] = 48947, -- Fire Resistance Aura
    [64021] = 48947 -- Fire Resistance Aura
  },
  ["XT-002 Deconstructor"] = {
    [62776] = 48942 -- Armor Resistance Aura
  },
  ["Hodir"] = {
    [63512] = 48945, -- Frost Resistance Aura
    [62478] = 48945 -- Frost Resistance Aura
  },
  ["Thorim"] = {
    [62466] = 48945, -- Frost Resistance Aura
    [62130] = 48945 -- Frost Resistance Aura
  },
  ["Mimiron"] = {
    [63677] = 48947, -- Fire Resistance Aura
    [64533] = 48947 -- Fire Resistance Aura
  },
  ["Yogg-Saron"] = {
    [64189] = 19746 -- Conc Resistance Aura
  }
}

--~~~~~~~~~ GET ASSIGNMENTS ~~~~~~~~~--
aura_env.getAssignments = function()
  local newAssignments = {}
  for encounter, subT in pairs(aura_env.config) do
    if subT.useAssigns and cd_Table[encounter] then
      local bossAbilitiesForEncounter = aura_env.boss_abilities[encounter]
      if bossAbilitiesForEncounter then
        for _, hashTableType in pairs(bossAbilitiesForEncounter) do
          for bossSpellId, hashValue in pairs(hashTableType) do
            if type(subT) == "table" then
              newAssignments[bossSpellId] = {}
              for i = 1, 10 do
                local entry = subT[tostring(bossSpellId)]
                if entry then
                  local pName = entry["pName"..i]
                  local cd = entry["cd"..i]
                  local order = entry["order"..i]
                  local delay = entry["delay"..i]
                  local amVariant = ""
                  
                  if pName and pName ~= "" and cd and order and delay then
                    local cdSpellID = cd_Table[encounter][cd]
                    if cdSpellID == 31821 and cd_AM_variant[encounter] and cd_AM_variant[encounter][bossSpellId] then
                      amVariant = cd_AM_variant[encounter][bossSpellId]
                    end
                    
                    local assignment = {pName, cdSpellID, delay, amVariant}
                    if not newAssignments[bossSpellId][order] then
                      newAssignments[bossSpellId][order] = {}
                    end
                    table.insert(newAssignments[bossSpellId][order], assignment)
                  end
                end
              end
            end
          end
        end
      end
    end
  end
  local sortedAssignments = {}
  for spellID, orders in pairs(newAssignments) do
    sortedAssignments[spellID] = {}
    for order, data in pairs(orders) do
      table.sort(data, function(a, b)
          local delayA = tonumber(a[3]) or 0
          local delayB = tonumber(b[3]) or 0
          if (a[3] or "") == (b[3] or "") then
            return (a[3] or 0) < (b[3] or 0)
          else
            return delayA < delayB
          end
      end)
      sortedAssignments[spellID][order] = data
    end
  end
  return sortedAssignments
end
------ GENERATE THE ADDON MESSAGE --------
aura_env.generateAddonMessage = function(spellId,count)
  local addonMessages = {}      
  for bossSpellId, data in pairs(aura_env.newAssigns) do
    if bossSpellId == spellId then
      local order = data[count]
      if order then
        for _, assigns in ipairs(order) do
          local assignedPlayer = assigns[1]
          local spellId = assigns[2]
          local delay = assigns[3] or 0
          local amVariant = assigns[4] or 0         
          local msg = aura_env.sender .. ";" .. assignedPlayer .. ";" .. spellId .. ";" .. delay .. ";"..amVariant
          table.insert(addonMessages, msg)
        end
      end
    end
  end      
  return addonMessages
end
```

# Trigger 1
#### Event
`OPTIONS GROUP_ROSTER_UPDATE`
```lua
function()
  if (UnitIsGroupAssistant("player") or UnitIsGroupLeader("player")) then
    aura_env.AoL = true
  else
    aura_env.AoL = false
  end
  if aura_env.AoL and not aura_env.pewpew then    
    aura_env.newAssigns = aura_env.getAssignments()
    return true
  end
  if not aura_env.AoL and not aura_env.pewpew then
    aura_env.newAssigns = "NOPE"
    return false
  end
end
```
# Trigger 2
#### Event
`ENCOUNTER_START`
```lua
function(event, encounterID_Start, encounterName, difficultyID, groupSize, instanceID)
  if not aura_env.AoL then
    return false
  elseif type(aura_env.newAssigns) == "table" then
    if event == "ENCOUNTER_START" then      
      if encounterID_Start == aura_env.encounterIds[encounterName] then 
        aura_env.encounterName = encounterName
        aura_env.pewpew = true
        aura_env.encID = encounterID_Start
        aura_env.abl_tbl = aura_env.boss_abilities[encounterName]        
        local spellIds = {
          channeledSpellIds = aura_env.abl_tbl.channeledSpellIds,
          slowSpellIds = aura_env.abl_tbl.slowSpellIds,
          fastSpellIds = aura_env.abl_tbl.fastSpellIds,
          buffDebuffSpellIds = aura_env.abl_tbl.buffDebuffSpellIds
        }
        for spellType, spellIdTable in pairs(spellIds) do
          if spellIdTable then
            for bossSpellId in pairs(spellIdTable) do
              if not aura_env.counters[bossSpellId] then
                aura_env.counters[bossSpellId] = 0
              end
            end
          end
        end
        return true
      end
    end
  end
end
```
# Trigger 3
#### Event
`ENCOUNTER_END`
```lua
function(event, encounterID_end, encounterName, difficultyID, groupSize, success)
  if not aura_env.AoL then
    return false
  end
  if type(aura_env.newAssigns) ~= "table" then
    return false
  end
  if not aura_env.pewpew then
    return false
  end  
  if event == "ENCOUNTER_END" then
    if success == 1 then
    end
    if aura_env.encID == encounterID_end then
      aura_env.pewpew = false
      aura_env.counters = {}
      aura_env.encounterName = ""
      aura_env.failedNames = {}
      aura_env.failedNames2 = {}
    end
    return true
  end
end
```
# Trigger 4
#### Event
`CLEU:SPELL_CAST_START:SPELL_CAST_SUCCESS:SPELL_AURA_APPLIED:SPELL_AURA_APPLIED_DOSE:SPELL_AURA_REMOVED:UNIT_DIED`
```lua
function(event,_,subEvent,...) --,_,_, sourceGUID, sourceName, _, _, destGUID, destName, _, _,spellId
  if not aura_env.AoL then
    return false
  end
  if type(aura_env.newAssigns) ~= "table" then
    return false
  end
  if not aura_env.pewpew then
    return false
  end  
  if subEvent == "SPELL_CAST_START" then
    local  sourceName, _, _, destGUID, destName, _, _,spellId = select(3,...) --
    if (aura_env.abl_tbl.slowSpellIds and aura_env.abl_tbl.slowSpellIds[spellId]) or (aura_env.abl_tbl.channeledSpellIds and aura_env.abl_tbl.channeledSpellIds[spellId]) then
      if aura_env.crsID[spellId] then
        local cntReset = aura_env.config[aura_env.encounterName][tostring(spellId)].interruptReset
        if aura_env.counters[spellId] == cntReset then          
          aura_env.counters[spellId] = 0
        end
      end      
      aura_env.counters[spellId] = aura_env.counters[spellId] + 1
      local addonMessages = aura_env.generateAddonMessage(spellId, aura_env.counters[spellId])
      for _, msg in ipairs(addonMessages) do
        C_ChatInfo.SendAddonMessage(aura_env.prefix, msg, aura_env.channel)  
      end
      return true
    end    
  end
  if subEvent == "SPELL_CAST_SUCCESS" then
    local  sourceName, _, _, destGUID, destName, _, _,spellId = select(3,...) --
    if (aura_env.abl_tbl.fastSpellIds and aura_env.abl_tbl.fastSpellIds[spellId]) then
      if aura_env.crsID[spellId] then
        local cntReset = aura_env.config[aura_env.encounterName][tostring(spellId)].interruptReset
        if aura_env.counters[spellId] == cntReset then          
          aura_env.counters[spellId] = 0
        end
      end
      aura_env.counters[spellId] = aura_env.counters[spellId] + 1
      local addonMessages = aura_env.generateAddonMessage(spellId,aura_env.counters[spellId])
      for _, msg in ipairs(addonMessages) do
        C_ChatInfo.SendAddonMessage(aura_env.prefix, msg, aura_env.channel)  
      end
      return true
    end
  end
  if subEvent == "SPELL_AURA_APPLIED" or subEvent == "SPELL_AURA_APPLIED_DOSE" then
    local  sourceName, _, _, destGUID, destName, _, _,spellId = select(3,...) --
    if (aura_env.abl_tbl.buffDebuffSpellIds and aura_env.abl_tbl.buffDebuffSpellIds[spellId]) then
      if aura_env.crsID[spellId] then
        local cntReset = aura_env.config[aura_env.encounterName][tostring(spellId)].interruptReset
        if aura_env.counters[spellId] == cntReset then          
          aura_env.counters[spellId] = 0
        end
      end
      aura_env.counters[spellId] = aura_env.counters[spellId] + 1
      local addonMessages = aura_env.generateAddonMessage(spellId,aura_env.counters[spellId])
      for _, msg in ipairs(addonMessages) do
        C_ChatInfo.SendAddonMessage(aura_env.prefix, msg, aura_env.channel)  
      end
      return true
    end
  end
end
```
