function OnTick()
DoSpells(OnProcessSpell)
UpdateMessage()
--Util__OnTick()
if autoCrit then DrawText("AutoCrit active!",100,0,0xFFFF0000) end
if spellTarget ~= nil and spellTarget.visible == false then forceAttack = false end
if forceAttack == true and spellTarget ~= nil then AttackTarget(spellTarget) end
end
function OnProcessSpell(object,spell)
if autoCrit then
if object ~= nil and spell ~= nil and object.charName == GetSelf().charName and string.find(spell.name,"BasicAttack") then
spellTarget = spell.target
if spellTarget ~= nil then
if critHeroesOnly == true then
for i=1, objManager:GetMaxHeroes(), 1 do
local object = objManager:GetHero(i)
if object ~= nil and heroTarget == nil then heroTarget = true end
end
if heroTarget == true then
MoveToXYZ(GetSelf().x,GetSelf().y,GetSelf().z)
forceAttack = true
end
heroTarget = false
else
MoveToXYZ(GetSelf().x,GetSelf().y,GetSelf().z)
forceAttack = true
end
end
end
end
end
function OnWndMsg(msg,key)
if key == critToggle and msg == KEY_UP thenif autoCrit == true then autoCrit = false
elseif autoCrit == false then autoCrit = true end
end
if msg == WM_RBUTTONDOWN then forceAttack = false end
end
function GetDistance(o1,o2)
if o1 and o2 and o1 ~= nil and o2 ~= nil then return math.sqrt(math.pow(o1.x - o2.x, 2) + math.pow(o1.z - o2.z, 2)) end
end
--OnProcessSpellStuff
HookSpell()
function DoSpells(spellCallback)
local a={GetCastSpell()}
local g=0
while (a[1] ~= nil and g<200) do
local spell={}
local startPos={}
local endPos={}
spell.name=a[2]
startPos.x=a[3]
startPos.y=a[4]
startPos.z=a[5]
endPos.x=a[6]
endPos.y=a[7]
endPos.z=a[8]
spell.target=a[12];
spell.startPos=startPos
spell.endPos=endPos
spellCallback(a[1],spell)
a={GetCastSpell()}
g=g+1
end
end
function DoSpellCallback()
DoSpells(OnProcessSpell)
end
--OnWndMsgStuff
KEY_DOWN = 256
KEY_UP = 257
WM_LBUTTONDOWN = 513
WM_LBUTTONUP = 514
WM_RBUTTONDOWN = 516
WM_RBUTTONUP = 517
HookWnd()
function UpdateMessage()
msg,key,param=GetMessage()
while msg ~= nil do
if OnWndMsg ~= nil then  OnWndMsg(msg, key) end
msg,key,param=GetMessage()
end
end
