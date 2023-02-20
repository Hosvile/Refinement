local CoreGui = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")

local ranstart = os.clock()

local Lib = {}
Lib.connections = {}

local ClickInput = (Enum.UserInputType.MouseButton1)
local TouchInput = (Enum.UserInputType.Touch)

local services = setmetatable({}, {
	__index = function(_, k)
	k = (k == "InputService" and "UserInputService") or k
	return game:GetService(k)
	end
})

local client = services.Players.LocalPlayer

local Utility = {}

function Utility.connect(signal, callback)
local connection = signal:Connect(callback)
table.insert(Lib.connections, connection)

return connection
end

function Utility.disconnect(connection)
local index = table.find(Lib.connections, connection)
connection:Disconnect()

if index then
table.remove(Lib.connections, index)
end
end

local touchpoints = {}
local conducting = 0

local hasdragged = false
function Utility.dragify(import,object, dragoutline, stroke, multi)
local start, objectposition, dragging, currentpos

UserInputService.InputBegan:Connect(function(input)
	if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then
	conducting = conducting + 1
	touchpoints[conducting] = input
	end
	if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) and not hasdragged and dragoutline and dragoutline.Visible == true then
	dragoutline.Visible = false; hasdragged = true
	end
	end)

local dragtouch

import.InputBegan:Connect(function(input)
	if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then
	dragging = true
	dragtouch = input
	start = input.Position
	if dragoutline then
	dragoutline.Visible = true
	end
	objectposition = object.Position
	end
	end)

Utility.connect(services.InputService.InputChanged, function(input)
	if (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) and dragging then
	local input = input
	if multi then
	input = dragtouch
	end
	currentpos = UDim2.new(objectposition.X.Scale, objectposition.X.Offset + (input.Position - start).X, objectposition.Y.Scale, objectposition.Y.Offset + (input.Position - start).Y)
	if dragoutline then
	dragoutline.Position = currentpos
	end
	end
	end)

Utility.connect(services.InputService.InputEnded, function(input)
	if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) and dragging then
	dragging = false
	dragtouch = nil
	if dragoutline then
	dragoutline.Visible = false
	end
	object.Position = currentpos
	end
	end)

local Signal
Signal = UserInputService.InputEnded:Connect(function(input)
	if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then
	touchpoints[conducting] = nil
	conducting = conducting - 1
	end
	end)

end

function Utility.getcenter(sizeX, sizeY)
return UDim2.new(0.5, -(sizeX / 2), 0.5, -(sizeY / 2))
end

if getgenv and getgenv().ScreenGui_ then
ScreenGui_:Destroy()
end

if getgenv and getgenv().DC_ then
for i, v in pairs(DC_) do
v:Disconnect()
DC_[i] = nil
end
end

getgenv().DC_ = {}

local CProvider = game:GetService("ContentProvider")

local creations = 0

--Window
local BarIn = "rbxassetid://12002282362"
--Bar
local SearchIn = "rbxassetid://12112852615"
local MenuIn = "rbxassetid://11949054349"
local OutIn = "rbxassetid://11949055629"
--Minimized
local IconIn = "rbxassetid://12213561084"
--Scroll
local MoreIn = "rbxassetid://11949185875"
--Features
local TogOn = "rbxassetid://12007342639"
local TogOff = "rbxassetid://12007348679"
local PointerIn = "rbxassetid://12080467938"
local DropIn = "rbxassetid://12080300828"

CProvider:PreloadAsync({
	BarIn,SearchIn,MenuIn,OutIn,IconIn,MoreIn,TogOn,TogOff,DropIn
})

function Lib:Randomized()
local length = math.random(15,30)
local array = {}
local forstart = os.clock()
for i = 1, length do
local ranstart = ranstart-os.clock()
local forstart = forstart-os.clock()
local start = os.clock()
array[i] = string.char(math.random(32, 126))
local calc = (start-os.clock()+ranstart+forstart)*math.random(1871,37129)+os.time()
math.randomseed(calc)
end
return table.concat(array)
end

function Lib:UICorner(instance,num)
local UIC = Instance.new("UICorner")
local num = num or 8
UIC.CornerRadius = UDim.new(0, num)
UIC.Parent = instance
return UIC
end

function Lib:UIPad(instance,num,a,b,c)
local UIP = Instance.new("UIPadding")
UIP.Parent = instance
return UIP
end

function Lib:UIList(instance,num,num2,align)
local UIL = Instance.new("UIListLayout")
local align = align or "Center"
UIL.Padding = UDim.new(num,num2)
UIL.HorizontalAlignment = align
UIL.SortOrder = "LayoutOrder"
UIL.Parent = instance
return UIL
end

local guiInset = game:GetService("GuiService"):GetGuiInset()
function Lib:InScreen(gui)
local pos = gui.AbsolutePosition + guiInset
return pos.X + gui.AbsoluteSize.X <= game.Workspace.CurrentCamera.ViewportSize.X and pos.X >= 0, pos.Y + gui.AbsoluteSize.Y <= game.Workspace.CurrentCamera.ViewportSize.Y and pos.Y >= 0
end

function Lib:Scale(gui,parent)
local parent = parent or gui.Parent
return (gui.AbsoluteSize.X/parent.AbsoluteSize.X), (gui.AbsoluteSize.Y/parent.AbsoluteSize.Y)
end

function Lib:CreateWindow(name,tabnum,winsize)
local name = tostring(name) or "InfiniX"
local func = func or function() end

local hiddenUI = get_hidden_gui or gethui
local protect_gui = protect_gui or (syn and syn.protect_gui) or function() end

local ScreenGui = Instance.new("ScreenGui")

protect_gui(ScreenGui)

if getgenv and getgenv().ScreenGui_ then
ScreenGui_:Destroy()
end
getgenv().ScreenGui_ = ScreenGui
ScreenGui.Name = Lib:Randomized()

if hiddenUI then
ScreenGui.Parent = hiddenUI()
else
	ScreenGui.Parent = CoreGui
end

local iconsize = 0.15
local Icon = Instance.new("ImageButton")
Icon.Visible = false
Icon.Name = "Icon"
Icon.BorderSizePixel = 0
Icon.Image = IconIn
Icon.ImageTransparency = 0
Icon.Active = true
Icon.BackgroundColor3 = Color3.fromRGB(255,255,255)
Icon.Position = UDim2.new(0.105, 0, 0.05, 0)
Icon.AnchorPoint = Vector2.new(0.5,0.5)
Icon.Size = UDim2.new(iconsize, 0, iconsize, 0)
Icon.Transparency = 0
Icon.BackgroundTransparency = 1
Icon.BorderSizePixel = 0
Icon.ZIndex = 10
Icon.SizeConstraint = "RelativeYY"
Icon.Parent = ScreenGui

local winsize = winsize or 0.49994444444444
local windowsize = UDim2.new(0.41005555555556+winsize, 0, winsize,0)
local windowpos = nil
local Window = Instance.new("Frame")
local WindowBox = Instance.new("Frame")

local ui_minimized = false

local closefunc = function(...) return end
local openfunc = func or closefunc

function OpenRS(time)
local Timer = time or 0.05
local Info = TweenInfo.new(Timer)
local Goal = {}
Goal.Size = windowsize
Goal.Position = windowpos
Tween = TweenService:Create(Window,Info,Goal)
Icon.Visible = false
openfunc()
Tween:Play()
Window.Visible = true
task.wait(Timer)
if not hasdragged then
WindowBox.Visible = true
end
ui_minimized = false
return ui_minimized
end

DC_[#DC_+1] = Icon.MouseButton1Click:Connect(OpenRS)

WindowBox.Active = false
WindowBox.Name = "WindowBox"
WindowBox.BackgroundColor3 = Color3.fromRGB(39,39,39)
WindowBox.Position = UDim2.new(0.5,0,0.5, 0)
WindowBox.AnchorPoint = Vector2.new(0.5,0.5)
WindowBox.Transparency = 0.5
WindowBox.BackgroundTransparency = 0.75
WindowBox.ClipsDescendants = false
WindowBox.BorderColor3 = Color3.fromRGB(100,255,100)
WindowBox.BorderSizePixel = 3.25
WindowBox.BorderMode = "Outline"
WindowBox.SizeConstraint = "RelativeYY"
WindowBox.Size = windowsize
WindowBox.Parent = ScreenGui

local BoxStroke = Instance.new("UIStroke")
BoxStroke.ApplyStrokeMode = "Border"
BoxStroke.LineJoinMode = "Bevel"
BoxStroke.Color = Color3.fromRGB(100,255,100)
BoxStroke.Thickness = 2.5
BoxStroke.Transparency = 0.5
BoxStroke.Enabled = true
BoxStroke.Parent = WindowBox

--Original Size
--Window.Size = UDim2.new(0.38976422764228, 0, 0.49994444444444,0)
Window.Name = "Window"
Window.BackgroundColor3 = Color3.fromRGB(39,39,39)
Window.Position = UDim2.new(0.5,0,0.5, 0)
Window.AnchorPoint = Vector2.new(0.5,0.5)
Window.Size = UDim2.new(0.41005555555556+winsize, 0, winsize,0)
Window.Transparency = 0.5
Window.BorderSizePixel = 0
Window.Draggable = false
Window.ClipsDescendants = false
Window.SizeConstraint = "RelativeYY"
--Window.Size = UDim2.new(0.38976422764228, 0, 0.215,0)
--Window.SizeConstraint = "RelativeXX"
Window.Parent = ScreenGui
Lib:UICorner(Window,10)

local Bar = Instance.new("ImageButton")
Bar.Active = true
Bar.Name = "Bar"
Bar.Image = BarIn
Bar.ImageColor3 = Color3.fromRGB(20,20,20)
Bar.ScaleType = "Crop"
Bar.BackgroundColor3 = Color3.fromRGB(0,0,0)
Bar.Position = UDim2.new(-0,0,-0,0)
Bar.Size = UDim2.new(1, 0, 0.0825, 0)
Bar.Transparency = 0
Bar.BorderSizePixel = 0
Bar.AutoButtonColor = false
Bar.BackgroundTransparency = 1
Bar.Parent = Window
Lib:UICorner(Bar,5)

print (Bar.Size)
warn (Lib:Scale(Bar,Bar.Parent))

local Padding = Instance.new("Frame")
Padding.Visible = SearchUp or false
Padding.Name = "TextBoxPadding"
Padding.BorderSizePixel = 0
Padding.Active = true
Padding.BackgroundColor3 = Color3.fromRGB(50,50,50)
Padding.Position = UDim2.new(0.556, 0, 0.505, 0)
Padding.AnchorPoint = Vector2.new(0.5,0.5)
Padding.Size = UDim2.new(0.54, 0, 0.6, 0)
Padding.Transparency = 0
Padding.BackgroundTransparency = 0
Padding.BorderSizePixel = 0
Padding.ZIndex = 4
Padding.SizeConstraint = "RelativeXY"
Padding.Parent = Bar
Lib:UICorner(Padding,4)

local Textbox = Instance.new("TextBox")
Textbox.Visible = SearchUp or false
Textbox.Name = "TextBox"
Textbox.BorderSizePixel = 0
Textbox.Active = true
Textbox.BackgroundColor3 = Color3.fromRGB(39,39,39)
Textbox.TextColor3 = Color3.fromRGB(255,255,255)
Textbox.Position = UDim2.new(0.564, 0, 0.505, 0)
Textbox.AnchorPoint = Vector2.new(0.5,0.5)
Textbox.Size = UDim2.new(0.54, 0, 0.6, 0)
Textbox.Transparency = 0
Textbox.BackgroundTransparency = 0
Textbox.BorderSizePixel = 0
Textbox.RichText = true
Textbox.Font = "Nunito"
Textbox.TextSize = 10
Textbox.Text = ""
Textbox.PlaceholderText = "Search"
Textbox.ZIndex = 4
Textbox.TextXAlignment = "Left"
Textbox.SizeConstraint = "RelativeXY"
Textbox.Parent = Bar
Lib:UICorner(Textbox,4)

local Base = {}
local Canvas = {}
function MatchSearch()
local matched = false
for i, t in pairs(Base) do
local v = t[1]
local Tab = t[2]
local Container = v.Parent.Parent
local Scroll = v.Parent
local Insert = {
	Scroll.CanvasPosition,Scroll
}
local Found = false
local Position
local Index
for i, v in pairs(Canvas) do
if v[2] == Scroll then
Index = i
Found = true
Position = v[1]
end
end
if string.lower(v.Name):match(Textbox.Text:lower()) and not v.ClassName:match("UI") then
matched = true
v.Visible = true
if not Found then
table.insert(Canvas,Insert)
Scroll.CanvasPosition = Vector2.new(0,0)
elseif Found and Position and Index then
if string.len(Textbox.Text) <= 0 then
Scroll.CanvasPosition = Position
table.remove(Canvas,Index)
if Canvas[Index] then Canvas[Index] = nil end
end
end
elseif Textbox.Text == "" or Textbox.Text == " " and not v.ClassName:match("UI") then
matched = false
Tab.Visible = true
v.Visible = true
if Found and Position then
Scroll.CanvasPosition = Position
table.remove(Canvas,Index)
end
elseif not v.ClassName:match("UI") then
v.Visible = false
end
if matched == false then
Tab.Visible = false
elseif matched == true then
Tab.Visible = true
end
end
end

DC_[#DC_+1] = Textbox:GetPropertyChangedSignal("Text"):Connect(MatchSearch)

local Search = Instance.new("ImageButton")
Search.Visible = true
Search.Name = "Search"
Search.BorderSizePixel = 0
Search.Image = SearchIn
Search.ImageTransparency = 0
Search.Active = true
Search.BackgroundColor3 = Color3.fromRGB(255,255,255)
Search.Position = UDim2.new(0.855, 0, 0.505, 0)
Search.AnchorPoint = Vector2.new(0.5,0.5)
Search.Size = UDim2.new(0.0375, 0, 0.7, 0)
Search.Transparency = 0
Search.BackgroundTransparency = 1
Search.BorderSizePixel = 0
Search.ZIndex = 4
Search.SizeConstraint = "RelativeXY"
Search.Parent = Bar

local Googling = false
DC_[#DC_+1] = Search.MouseButton1Down:Connect(function()
	Googling = true
	end)

DC_[#DC_+1] = Search.MouseButton1Up:Connect(function()
	if Googling == true then
	Padding.Visible = not Padding.Visible
	Textbox.Visible = not Textbox.Visible
	Textbox.Text = ""
--MatchSearch()
	Googling = false
	end
	end)

local Menu = Instance.new("ImageButton")
Menu.Visible = true
Menu.Name = "Menu"
Menu.BorderSizePixel = 0
Menu.Image = MenuIn
Menu.ImageTransparency = 0
Menu.Active = true
Menu.BackgroundColor3 = Color3.fromRGB(255,255,255)
Menu.Position = UDim2.new(0.9025, 0, 0.505, 0)
Menu.AnchorPoint = Vector2.new(0.5,0.5)
Menu.Size = UDim2.new(0.0375, 0, 0.925, 0)
Menu.Transparency = 0
Menu.BackgroundTransparency = 1
Menu.BorderSizePixel = 0
Menu.ZIndex = 4
Menu.SizeConstraint = "RelativeXY"
Menu.Parent = Bar

local Close = Instance.new("ImageButton")
Close.Visible = true
Close.Name = "Close"
Close.BorderSizePixel = 0
Close.Image = OutIn
Close.ImageTransparency = 0
Close.Active = true
Close.BackgroundColor3 = Color3.fromRGB(255,255,255)
Close.Position = UDim2.new(0.95, 0, 0.4925, 0)
Close.AnchorPoint = Vector2.new(0.5,0.5)
Close.Size = UDim2.new(0.0425, 0, 0.9, 0)
Close.Transparency = 0
Close.BackgroundTransparency = 1
Close.BorderSizePixel = 0
Close.ZIndex = 4
Close.SizeConstraint = "RelativeXY"
Close.Parent = Bar

function CloseRS(time)
local Timer = time or 0.05
local Info = TweenInfo.new(Timer)
local Goal = {}
local guiInset = game:GetService("GuiService"):GetGuiInset()
local ISX,ISY = Icon.AbsoluteSize.X, Icon.AbsoluteSize.Y
local DSX,DSY = ISX*0.575,ISY*0.575
local GSX,GSY = ISX+guiInset.X,ISY+guiInset.Y
Goal.Size = UDim2.new(0,ISX*0.75,0,ISY*0.75)
Goal.Position = UDim2.new(0,Icon.AbsolutePosition.X+DSX,0,Icon.AbsolutePosition.Y+DSY)
Tween = TweenService:Create(Window,Info,Goal)
windowpos = Window.Position
closefunc()
WindowBox.Visible = false
Tween:Play()
task.wait(Timer)
Icon.Visible = true
Window.Visible = false
ui_minimized = true
return ui_minimized
end

DC_[#DC_+1] = Close.MouseButton1Click:Connect(CloseRS)

Utility.dragify(Bar,Window,WindowBox,BoxStroke,true)
--[[
local UserInputService = game:GetService("UserInputService")

local gui = Window

local dragging
local dragInput
local dragStart
local startPos

local function update(input)
local delta = input.Position - dragStart
gui.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
end

Bar.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
	dragging = true
	dragStart = input.Position
	startPos = gui.Position

	input.Changed:Connect(function()
		if input.UserInputState == Enum.UserInputState.End then
		dragging = false
		end
		end)
	end
	end)

Bar.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
	dragInput = input
	end
	end)

UserInputService.InputChanged:Connect(function(input)
	if input == dragInput and dragging then
	update(input)
	end
	end)
]]

local Scroll = Instance.new("Frame")
Scroll.Name = "ScrollTab"
Scroll.BackgroundColor3 = Color3.fromRGB(52,52,52)
Scroll.Position = UDim2.new(0.025,0,0.125, 0)
Scroll.Size = UDim2.new(0.21, 0, 0.825,0)
Scroll.Transparency = 0
Scroll.BorderSizePixel = 0
Scroll.Parent = Window

local Categories = Instance.new("ScrollingFrame")
Categories.Active = true
Categories.Name = "Categories"
Categories.BackgroundColor3 = Color3.fromRGB(52,52,52)
Categories.Size = UDim2.new(1, 0, 1, 0)
Categories.Transparency = 1
Categories.BorderSizePixel = 0
Categories.ElasticBehavior = "Never"
Categories.CanvasSize = UDim2.new(0,0,0,0)
Categories.ScrollBarThickness = 2
Categories.ScrollingDirection = "Y"
Categories.ScrollBarImageTransparency = 1
Categories.Parent = Scroll
Lib:UICorner(Scroll,7.5)

local UIPad = Lib:UIPad(Categories)
UIPad.PaddingTop = UDim.new(0,Categories.AbsoluteSize.Y*0.05)
local UIList = Lib:UIList(Categories,0,Categories.AbsoluteSize.Y*0.05)

local Tab_ = {}

local TabTable = {}
local PreviousTab
local ExistingTabs = {}

function Tab_:Minimize(bool,time,yield)
local time = time or 0.2
local function Yield()
repeat task.wait() until ui_minimized == bool
end
if bool then
CloseRS(time)
else
	OpenRS(time)
end;if yield then Yield() end
end

function Tab_:Closing(func)
if type (func) == "function" then else return end
closefunc = func
end

function Tab_:Opening(func)
if type(func) == "function" then else return end
openfunc = func
end

function Tab_:CreateTab(name,func)
local name = tostring(name) or "InfiniX"
local func = func or function() end
local tabnum = tabnum or 1
local tabVis = true

if #ExistingTabs >= tabnum then
tabVis = false
elseif #ExistingTabs < tabnum and PreviousTab then
PreviousTab.Visible = false
end

local TabColor = Color3.fromRGB(65,65,65)
local Tab = Instance.new("TextButton")
Tab.Active = true
Tab.Name = name
Tab.BackgroundColor3 = Color3.fromRGB(65,65,65)
Tab.Position = UDim2.new(0, 0, 0, 0)
Tab.Size = UDim2.new(0.875, 0, 0.145,0)
Tab.Transparency = 0
Tab.Text = ""
Tab.AutoButtonColor = false
Tab.BorderSizePixel = 0
Tab.SizeConstraint = "RelativeXX"
Tab.ZIndex = 2
Tab.Parent = Categories
Lib:UICorner(Tab,5)

if #ExistingTabs < tabnum then
Tab.BackgroundColor3 = Color3.fromRGB(100,100,100)
for i, v in pairs(TabTable) do
if v ~= Tab then
v.BackgroundColor3 = TabColor
end
end
end

table.insert(TabTable,Tab)

local Center = Instance.new("Frame")
Center.Active = false
Center.Name = "Center"
Center.BackgroundColor3 = Color3.fromRGB(255,255,255)
Center.Position = UDim2.new(0.5, 0, 0.1, 0)
Center.AnchorPoint = Vector2.new(0.5,0,0.5,0)
Center.Size = UDim2.new(0.925,0,0.75,0)
Center.Transparency = 0.975
Center.BorderSizePixel = 0
Center.SizeConstraint = "RelativeXY"
Center.ZIndex = 2
Center.Parent = Tab
Lib:UICorner(Center,5)

local Shade = Instance.new("Frame")
Shade.Active = true
Shade.Name = "Shade"
Shade.BackgroundColor3 = Color3.fromRGB(0,0,0)
Shade.Position = UDim2.new(-0.01, 0, 0.075, 0)
Shade.Size = UDim2.new(1, 0, 1,0)
Shade.Transparency = 0.75
Shade.BorderSizePixel = 0
Shade.SizeConstraint = "RelativeXY"
Shade.ZIndex = 1
Shade.Parent = Tab
Lib:UICorner(Shade,5)

local Light = Instance.new("Frame")
Light.Active = true
Light.Name = "Light"
Light.BackgroundColor3 = Color3.fromRGB(255,255,255)
Light.Position = UDim2.new(0, 0, -0.05, 0)
Light.Size = UDim2.new(1, 0, 1,0)
Light.Transparency = 0.9
Light.BorderSizePixel = 0
Light.SizeConstraint = "RelativeXY"
Light.ZIndex = 1
Light.Parent = Tab
Lib:UICorner(Light,5)

Categories.CanvasSize = UDim2.new(0,0,0,UIList.AbsoluteContentSize.Y+UIList.Padding.Offset+Tab.AbsoluteSize.Y*0.75)

local Text = Instance.new("TextLabel")
Text.Name = "Text"
Text.BackgroundColor3 = Color3.fromRGB(0,0,0)
Text.Position = UDim2.new(0.05, 0, 0.2, 0)
Text.Size = UDim2.new(0.9, 0, 0.115,0)
Text.TextScaled = true
Text.Transparency = 0
Text.BackgroundTransparency = 1
Text.TextColor3 = Color3.new(255,255,255)
Text.BorderSizePixel = 0
Text.SizeConstraint = "RelativeXX"
Text.TextSize = 0
Text.RichText = true
Text.Text = name
Text.Font = "Nunito"
Text.ZIndex = 3
Text.Parent = Tab

local Inside = Instance.new("Frame")
Inside.Active = false
Inside.Name = "ScrollFrame"
Inside.BackgroundColor3 = Color3.fromRGB(30,30,30)
Inside.Position = UDim2.new(1.125, 0, 0, 0)
Inside.Size = UDim2.new(3.4, 0, 1,0)
Inside.Transparency = 0
Inside.Visible = tabVis
Inside.BorderSizePixel = 0
Inside.SizeConstraint = "RelativeXY"
Inside.Parent = Scroll
Lib:UICorner(Inside,5)

PreviousTab = Inside
if #ExistingTabs == tabnum-1 then
for i, v in pairs(ExistingTabs) do
Inside.Visible = true
if v ~= Inside then
v.Visible = false
end
end
end

table.insert(ExistingTabs,Inside)

local InScroll = Instance.new("ScrollingFrame")
InScroll.Active = true
InScroll.Name = "InScroll"
InScroll.BackgroundColor3 = Color3.fromRGB(30,30,30)
InScroll.Position = UDim2.new(0, 0, 0, 0)
InScroll.Size = UDim2.new(1, 0, 1,0)
InScroll.Transparency = 1
InScroll.BorderSizePixel = 0
InScroll.SizeConstraint = "RelativeXY"
InScroll.ElasticBehavior = "Never"
InScroll.CanvasSize = UDim2.new(0,0,0,0)
InScroll.ScrollBarThickness = 2
InScroll.ScrollingDirection = "Y"
InScroll.ScrollBarImageTransparency = 1
InScroll.Parent = Inside
Lib:UICorner(Scroll,5)
local UIPad = Lib:UIPad(InScroll)
UIPad.PaddingTop = UDim.new(0,InScroll.AbsoluteSize.Y*0.03)
local UIList = Lib:UIList(InScroll,0,InScroll.AbsoluteSize.Y*0.015)
local ScrollList = UIList

local Clicked = function()
for i, v in pairs(TabTable) do
Tab.BackgroundColor3 = Color3.fromRGB(100,100,100)
if v ~= Tab then
v.BackgroundColor3 = TabColor
end
end
for i, v in pairs(ExistingTabs) do
Inside.Visible = true
if v ~= Inside then
v.Visible = false
end
end;func(Tab,Text,Inside,InScroll)
end

local TabDown = false
DC_[#DC_+1] = Tab.MouseButton1Down:Connect(function()
	TabDown = true
	end)

DC_[#DC_+1] = Tab.MouseButton1Up:Connect(function()
	if TabDown == true then
	Clicked()
	TabDown = false
	end
	end)

DC_[#DC_+1] = Tab.InputBegan:Connect(function(input)
	if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then
	input.Changed:Connect(function()
		if input.UserInputState == Enum.UserInputState.End then
--TabDown = false
		end
		end)
	end
	end)

local Feat = {}

local More = Instance.new("ImageLabel")
local MoreVis = More
More.Visible = false
More.Name = "Cat_More2nd"
More.BorderSizePixel = 0
More.Image = MoreIn
More.ImageTransparency = 0.5
More.Active = false
More.BackgroundColor3 = Color3.fromRGB(255,255,255)
More.Position = UDim2.new(0.46, 0, 0.845, 0)
More.Size = UDim2.new(0.04, 0, 0.06,0)
More.Transparency = 0
More.BackgroundTransparency = 1
More.BorderSizePixel = 0
More.ZIndex = 1000
More.SizeConstraint = "RelativeXY"
More.Parent = Inside

local More = Instance.new("ImageLabel")
More.Visible = true
More.Name = "Cat_More1st"
More.BorderSizePixel = 0
More.Image = MoreIn
More.ImageTransparency = 0.75
More.Active = false
More.BackgroundColor3 = Color3.fromRGB(255,255,255)
More.Position = UDim2.new(0.5, 0, 0.75, 0)
More.AnchorPoint = Vector2.new(0.5,0.5)
More.Size = UDim2.new(1.5, 0, 2, 0)
More.Transparency = 0
More.BackgroundTransparency = 1
More.BorderSizePixel = 0
More.ZIndex = 1000
More.SizeConstraint = "RelativeXY"
More.Parent = MoreVis

function CheckGap()
if InScroll.CanvasSize.Y.Offset > InScroll.AbsoluteSize.Y and InScroll.CanvasPosition.Y >= (InScroll.AbsoluteCanvasSize.Y-InScroll.AbsoluteSize.Y)*0.99 then
MoreVis.Visible = false
elseif InScroll.CanvasSize.Y.Offset then
MoreVis.Visible = true
end
end

function Gap(scroll,more)
local scroll = scroll or InScroll
local more = more or MoreVis
if scroll.CanvasSize.Y.Offset > scroll.AbsoluteSize.Y and scroll.CanvasPosition.Y >= (scroll.AbsoluteCanvasSize.Y-scroll.AbsoluteSize.Y)*0.99 then
more.Visible = false
more.Active = false
elseif scroll.CanvasSize.Y.Offset > scroll.AbsoluteSize.Y and scroll.CanvasPosition.Y <= (scroll.AbsoluteCanvasSize.Y-scroll.AbsoluteSize.Y)*0.99 then
more.Visible = true
more.Active = false
end
end

DC_[#DC_+1] = InScroll:GetPropertyChangedSignal("CanvasPosition"):Connect(CheckGap)

function Button(name,func)
local Inner = Instance.new("TextButton")
Inner.Active = false
Inner.Name = name
Inner.BackgroundColor3 = Color3.fromRGB(47,47,47)
Inner.Position = UDim2.new(0.0375, 0, 0, 0)
Inner.Size = UDim2.new(0.935, 0, 0.07,0)
Inner.Transparency = 0
Inner.BorderSizePixel = 0
Inner.AutoButtonColor = true
Inner.Text = ""
Inner.SizeConstraint = "RelativeXX"
Inner.ZIndex = 2
Inner.Parent = InScroll
Lib:UICorner(Inner,5)

local InnerBase = {
	Inner,Tab
}
table.insert(Base,InnerBase)

local Shade = Instance.new("Frame")
Shade.Active = false
Shade.Name = name
Shade.BackgroundColor3 = Color3.fromRGB(0,0,0)
Shade.Position = UDim2.new(0.0075, 0, 0.075, 0)
Shade.Size = UDim2.new(1, 0, 1,0)
Shade.Transparency = 0.25
Shade.BorderSizePixel = 0
Shade.SizeConstraint = "RelativeXY"
Shade.Parent = Inner
Lib:UICorner(Shade,5)

local Text = Instance.new("TextLabel")
Text.Name = "Text"
Text.Active = false
Text.BackgroundColor3 = Color3.fromRGB(0,0,0)
Text.Position = UDim2.new(0.015, 0, 0.1, 0)
Text.Size = UDim2.new(0.75, 0, 0.5,0)
Text.TextScaled = true
Text.Transparency = 0
Text.BackgroundTransparency = 1
Text.TextColor3 = Color3.new(255,255,255)
Text.BorderSizePixel = 0
Text.SizeConstraint = "RelativeXY"
Text.TextSize = 0
Text.RichText = true
Text.TextXAlignment = "Left"
Text.Text = name
Text.Font = "Nunito"
Text.ZIndex = 3
Text.Parent = Inner

InScroll.CanvasSize = UDim2.new(0,0,0,UIList.AbsoluteContentSize.Y+UIList.Padding.Offset+Tab.AbsoluteSize.Y*0.75)

Gap(InScroll,MoreVis)

return Inner,Shade,Text
end

function Feat:CreateButton(name,func)
local name = tostring(name) or "InfiniX"
local func = func or function() end

local Inner,Shade,Text = Button(name,func)

local InnerDown = false
DC_[#DC_+1] = Inner.MouseButton1Down:Connect(function()
	InnerDown = true
	end)

DC_[#DC_+1] = Inner.MouseButton1Up:Connect(function()
	if InnerDown == true then
	func()
	InnerDown = false
	end
	end)

return name,Inner,Shade,Text
end

local Processdelay = 0
function Feat:CreateToggle(name,bool,func)
local name = tostring(name) or "InfiniX"
local bool = bool or false
local func = func or function() end
local defimage = nil

function Define(bool)
if bool == true then defimage = TogOn elseif bool == false then defimage = TogOff end
return defimage
end

Define(bool)

local Inner,Shade,Text = Button(name,func)

local Container = Instance.new("Frame")
Container.Active = false
Container.Name = "Container_Status_"..tostring(bool)
Container.BackgroundColor3 = Color3.fromRGB(38,38,38)
Container.Position = UDim2.new(0.885, 0, 0.11, 0)
Container.Size = UDim2.new(0.1, 0, 0.8,0)
Container.Transparency = 0
Container.BorderSizePixel = 0
Container.SizeConstraint = "RelativeXY"
Container.ZIndex = 4
Container.Parent = Inner
Lib:UICorner(Container,5)

local OnShade = Instance.new("Frame")
OnShade.Active = false
OnShade.Name = "OnShade"
OnShade.BackgroundColor3 = Color3.fromRGB(0,0,0)
OnShade.Position = UDim2.new(0.8875, 0, 0.14, 0)
OnShade.Size = UDim2.new(0.1, 0, 0.8,0)
OnShade.Transparency = 0.25
OnShade.BorderSizePixel = 0
OnShade.SizeConstraint = "RelativeXY"
OnShade.ZIndex = 3
OnShade.Visible = false
OnShade.Parent = Inner
Lib:UICorner(OnShade,5)

local Status = Instance.new("ImageLabel")
Status.Visible = true
Status.Name = "Status_"..tostring(bool)
Status.BorderSizePixel = 0
Status.Image = defimage
Status.ImageTransparency = 0
Status.Active = false
Status.BackgroundColor3 = Color3.fromRGB(255,255,255)
Status.Position = UDim2.new(0.5225, 0, 0.5, 0)
Status.AnchorPoint = Vector2.new(0.5,0.5)
Status.Size = UDim2.new(0.55, 0, 0.55, 0)
Status.Transparency = 0
Status.BackgroundTransparency = 1
Status.BorderSizePixel = 0
Status.ZIndex = 5
Status.SizeConstraint = "RelativeXY"
Status.Parent = Container

local InnerDown = false
DC_[#DC_+1] = Inner.MouseButton1Down:Connect(function()
	InnerDown = true
	end)

DC_[#DC_+1] = Inner.MouseButton1Up:Connect(function()
	if InnerDown == true then
	bool = not bool
	Status.Image = Define(bool)
	func(bool)
	InnerDown = false
	end
	end)

local Activated = false
local Timer = 0.75
local Tween
local Info = TweenInfo.new(Timer,Enum.EasingStyle.Elastic,Enum.EasingDirection.In)
local Goal = {}

task.spawn(function()
	task.wait(Processdelay)
	Processdelay = Processdelay + 0.1
	while Status do
	if bool == true and Inside.Visible == true then
	if Activated == true then Activated = false
	Goal.ImageTransparency = 0.75
	Goal.Position = UDim2.new(0.5, 0, 0.5, 0)
	Info = TweenInfo.new(Timer,Enum.EasingStyle.Bounce,Enum.EasingDirection.In)
	Tween = TweenService:Create(Status,Info,Goal)
	elseif Activated == false then Activated = true
	Goal.ImageTransparency = 0
	Goal.Position = UDim2.new(0.55, 0, 0.5, 0)
	Info = TweenInfo.new(Timer,Enum.EasingStyle.Elastic,Enum.EasingDirection.Out)
	Tween = TweenService:Create(Status,Info,Goal)
	end
	Tween:Play()
	local start = os.clock()
	repeat
	if not bool and Tween or Inside.Visible == false then
	Tween:Pause()
	Activated = false
	Status.ImageTransparency = 0
	end
	task.wait()
	until (os.clock()-start) >= Timer
	end
	task.wait()
	end
	end)

local Add = {}

function Add:State()
return bool
end

return Add,name,Inner,Shade,Text
end

function Feat:CreateSlider(name,min,max,def,func)
local name = tostring(name) or "InfiniX"
local min = min or def
local max = max or 255
local val = val or def or min
local func = func or function() end

local Inner,Shade,Text = Button(name,func)

local Slipper = Instance.new("Frame")
Slipper.Active = false
Slipper.Name = "Slipper"
Slipper.BackgroundColor3 = Color3.fromRGB(87,87,87)
Slipper.Position = UDim2.new(0.0325, 0, 0.7, 0)
Slipper.Size = UDim2.new(0.935, 0, 0.05,0)
Slipper.Transparency = 0
Slipper.BorderSizePixel = 0
Slipper.SizeConstraint = "RelativeXY"
Slipper.ZIndex = 3
Slipper.Parent = Inner
Lib:UICorner(Slipper,10)

local SlipperSize = Slipper.AbsoluteSize.X

local Slider = Instance.new("TextButton")
Slider.Active = false
Slider.Name = "Slider"
Slider.BackgroundColor3 = Color3.fromRGB(255,255,255)
Slider.Position = UDim2.new(0.0325, 0, 0.7, 0)
--Size 0.935, 0.05
Slider.Size = UDim2.new(0, 0, 0.05,0)
if val > min then
--targget val/1.7155
local calc = val/(max/Slipper.AbsoluteSize.X)
Slider.Size = UDim2.new(0, calc, 0.05,0)
end
Slider.Transparency = 0
Slider.BorderSizePixel = 0
Slider.AutoButtonColor = false
Slider.Text = ""
Slider.SizeConstraint = "RelativeXY"
Slider.ZIndex = 3
Slider.Parent = Inner
Lib:UICorner(Slider,10)

local Formed = Instance.new("TextLabel")
Formed.Name = "Formed"
Formed.BackgroundColor3 = Color3.fromRGB(255,255,255)
Formed.Position = UDim2.new(0.7, 0, 0.15, 0)
Formed.Size = UDim2.new(3.5, 0, 0.4,0)
Formed.TextColor3 = Color3.fromRGB(255,255,255)
Formed.TextScaled = true
Formed.TextWrapped = true
Formed.Transparency = 0.45
Formed.BorderSizePixel = 0
Formed.BackgroundTransparency = 1
Formed.TextSize = 11
Formed.Text = string.format("%d / %d", val, max)
Formed.RichText = true
Formed.Font = "Nunito"
Formed.TextXAlignment = "Right"
Formed.SizeConstraint = "RelativeYY"
Formed.ZIndex = 4
Formed.Parent = Inner

local Pointer = Instance.new("ImageLabel")
Pointer.Visible = false
Pointer.Name = "Pointer"
Pointer.BorderSizePixel = 0
Pointer.Image = PointerIn
Pointer.ImageTransparency = 0
Pointer.Active = false
Pointer.BackgroundColor3 = Color3.fromRGB(255,255,255)
--Pointer.Position = UDim2.new(0.5, 0, 0.275, 0)
Pointer.Position = UDim2.new(1,0,-8,0)
Pointer.AnchorPoint = Vector2.new(0.5,0.5)
Pointer.Size = UDim2.new(20, 0, 20, 0)
Pointer.Transparency = 0
Pointer.BackgroundTransparency = 1
Pointer.BorderSizePixel = 0
Pointer.ZIndex = 5
Pointer.SizeConstraint = "RelativeYY"
Pointer.Parent = Slider

local Digit = Instance.new("TextLabel")
Digit.Name = "Digit"
Digit.BackgroundColor3 = Color3.fromRGB(255,255,255)
Digit.Position = UDim2.new(0.125, 0, 0.15, 0)
Digit.Size = UDim2.new(0.725, 0, 0.5,0)
Digit.TextColor3 = Color3.fromRGB(255,255,255)
Digit.TextScaled = true
Digit.TextWrapped = false
Digit.Transparency = 0
Digit.BorderSizePixel = 0
Digit.TextSize = 11
Digit.BackgroundTransparency = 1
Digit.Text = val
Digit.RichText = true
Digit.Font = "Nunito"
Digit.SizeConstraint = "RelativeXY"
Digit.ZIndex = 6
Digit.Parent = Pointer

local mouse = game:GetService("Players").LocalPlayer:GetMouse()
local uis = game:GetService("UserInputService")
local x = mouse.X
local down = false --if MouseButton1 is down or not

function clamped()
local ap = Vector2.new(Slipper.AbsolutePosition.X, Slipper.AbsolutePosition.Y)
local as = Vector2.new(Slipper.AbsoluteSize.X, Slipper.AbsoluteSize.Y)
local clamped = math.clamp((mouse.X-ap.X),0,ap.X)
clamped = math.clamp(clamped,0,SlipperSize)
return clamped
end

DC_[#DC_+1] = Inner.MouseButton1Click:Connect(function()
	Slider.Size = UDim2.new(0, clamped(), 0.05, 0)
	down = true
	end)

DC_[#DC_+1] = Inner.MouseButton1Down:Connect(function()
	Slider.Size = UDim2.new(0, clamped(), 0.05, 0)
	down = true
	Pointer.Visible = true
	while down do
	Slider.Size = UDim2.new(0, clamped(), 0.05, 0)
	percentage = math.clamp(((mouse.X - Slipper.AbsolutePosition.X) / Slipper.AbsoluteSize.X), 0, 1)
	val = (percentage * (max - min)) + min
	Formed.Text = string.format("%d / %d", val, max)
	Digit.Text = math.floor(val)
	task.wait()
	end
	end)

DC_[#DC_+1] = mouse.Move:Connect(function()
	local ap = Vector2.new(Slipper.AbsolutePosition.X, Slipper.AbsolutePosition.Y)
	local as = Vector2.new(Slipper.AbsoluteSize.X, Slipper.AbsoluteSize.Y)
	if down == true then --if true, then this represents the mouse being dragged
	InScroll.ScrollingEnabled = false
	if mouse.X < ap.X then --out of bounds (to the left)
	Slider.Size = UDim2.new(0, 0, 0.05, 0)
	elseif mouse.X > (ap.X + as.X) then --out of bounds (to the right)
	Slider.Size = UDim2.new(0, as.X, 0.05, 0)
	else --within bounds
		Slider.Size = UDim2.new(0, clamped(), 0.05, 0)
	end
--Pointer.Position = UDim2.new(0, clamped(), 0.275, 0)
	end
	end)

DC_[#DC_+1] = UserInputService.InputBegan:Connect(function(input)
	input.Changed:Connect(function()
		if input.UserInputState == Enum.UserInputState.End then
		if down == true then
		InScroll.ScrollingEnabled = true
		func(val)
		Pointer.Visible = false
		down = false
		end
		end
		end)
	end)

local Add = {}

function Add:State()
return val
end

return Add,name,Inner,Shade,Text
end

local ScaledList = false
function Feat:CreateDropdown(name,options,visible,func)
local name = tostring(name) or "InfiniX"
local func = func or function() end
local options = options or {
	"nil"
}
local visible = visible or false
local current = "nil"

local Inner,Shade,Text = Button(name,func)

local Arrow = Instance.new("ImageLabel")
Arrow.Visible = true
Arrow.Name = "Arrow"
Arrow.BorderSizePixel = 0
Arrow.Image = DropIn
Arrow.ImageTransparency = 0
Arrow.Active = false
Arrow.BackgroundColor3 = Color3.fromRGB(255,255,255)
Arrow.Position = UDim2.new(0.925,0,0.5,0)
Arrow.AnchorPoint = Vector2.new(0,0.5)
Arrow.Size = UDim2.new(0.5, 0, 0.5, 0)
Arrow.Transparency = 0
Arrow.BackgroundTransparency = 1
Arrow.BorderSizePixel = 0
Arrow.ZIndex = 5
Arrow.SizeConstraint = "RelativeYY"
Arrow.Rotation = 180
Arrow.Parent = Inner

local Container = Instance.new("ScrollingFrame")
Container.Visible = visible
Container.Active = false
Container.Name = "Container"
Container.BackgroundColor3 = Color3.fromRGB(39,39,39)
Container.Position = UDim2.new(0.2, 0, 1.15, 0)
Container.Size = UDim2.new(0.675, 0, 4,0)
Container.Transparency = 0.25
Container.BorderSizePixel = 0
Container.SizeConstraint = "RelativeXY"
Container.ZIndex = 7
Container.ElasticBehavior = "Never"
Container.CanvasSize = UDim2.new(0,0,0,0)
Container.ScrollBarThickness = 2
Container.ScrollingDirection = "Y"
Container.ScrollBarImageTransparency = 1
Container.Parent = Inner
local UIPad = Lib:UIPad(Container)
UIPad.PaddingTop = UDim.new(0,Container.AbsoluteSize.Y*0.03)
local UIList = Lib:UIList(Container,0,Container.AbsoluteSize.Y*0.025)

local InnerDown = false
DC_[#DC_+1] = Inner.MouseButton1Down:Connect(function()
	InnerDown = true
	end)

local ContainerSize = math.round(math.floor(Container.AbsoluteSize.Y*1.02))

local ScrollPos
DC_[#DC_+1] = Inner.MouseButton1Click:Connect(function()
	if InnerDown == true then
	visible = not visible
	if visible == true then
	Arrow.Rotation = 0
	Container.Visible = true
	InScroll.CanvasSize = UDim2.new(0,0,0,InScroll.AbsoluteCanvasSize.Y+ContainerSize)
	if ScrollPos then
	InScroll.CanvasPosition = Vector2.new(0,ScrollPos.Y)
	end
	elseif visible == false then
	Arrow.Rotation = 180
	Container.Visible = false
	ScrollPos = InScroll.CanvasPosition
	InScroll.CanvasSize = UDim2.new(0,0,0,InScroll.AbsoluteCanvasSize.Y-ContainerSize)
	end
	InnerDown = false
	end
	end)

local Add = {}

for i, v in pairs(options) do
local defined
if type(v) == "table" and v["Name"] then
defined = v["Name"]
elseif type(v) == "table" and not v["Name"] then
defined = v[1]
else
	defined = tostring (v)
end
local Option = Instance.new("TextButton")
Option.Active = true
Option.Name = name
Option.BackgroundColor3 = Color3.fromRGB(47,47,47)
Option.Position = UDim2.new(0.0375, 0, 0, 0)
Option.Size = UDim2.new(0.935, 0, 0.07,0)
Option.Transparency = 0
Option.BorderSizePixel = 0
Option.AutoButtonColor = true
Option.TextColor3 = Color3.fromRGB(255,255,255)
Option.Text = defined
Option.TextScaled = true
Option.RichText = true
Option.Font = "Nunito"
Option.TextSize = 11
Option.SizeConstraint = "RelativeXX"
Option.ZIndex = 8
Option.Parent = Container
Lib:UICorner(Option,5)

Container.CanvasSize = UDim2.new(0,0,0,UIList.AbsoluteContentSize.Y+UIList.Padding.Offset+Option.AbsoluteSize.Y*0.2)

local Down = false
DC_[#DC_+1] = Option.MouseButton1Down:Connect(function()
	Down = true
	end)

DC_[#DC_+1] = Option.MouseButton1Up:Connect(function()
	if Down == true then
	current = v
	if type(v) == "table" and v["Name"] and v["Option"] then
	func(v["Name"],v["Option"])
	elseif type(v) == "table" and not v["Name"] and not v["Option"] then
	func(v[1],v[2])
	else
		func(v)
	end
	Down = false
	end
	end)
end

function Add:State()
return current
end

function Add:Decrease()
Container.CanvasSize = UDim2.new(0,0,0,-(UIList.AbsoluteContentSize.Y+UIList.Padding.Offset+Option.AbsoluteSize.Y*0.2))
end

function Add:Increase()
Container.CanvasSize = UDim2.new(0,0,0,UIList.AbsoluteContentSize.Y+UIList.Padding.Offset+Option.AbsoluteSize.Y*0.2)
end

return Add,name,Inner,Shade,Text
end

function Feat:CreateTextbox(name,text,func)
local name = tostring(name) or "InfiniX"
local text = text or "TextBox"
local func = func or function() end

local Inner,Shade,Text = Button(name,func)
Text:Destroy()

local Padding = Instance.new("Frame")
Padding.Visible = false
Padding.Name = "TextBoxPadding"
Padding.BorderSizePixel = 0
Padding.Active = true
Padding.BackgroundColor3 = Color3.fromRGB(75,75,75)
Padding.Position = UDim2.new(0,0,0,0)
Padding.Size = UDim2.new(1,0,1,0)
Padding.Transparency = 0
Padding.BackgroundTransparency = 0
Padding.BorderSizePixel = 0
Padding.ZIndex = 4
Padding.SizeConstraint = "RelativeXY"
Padding.Parent = Inner
Lib:UICorner(Padding,4)

local Textbox = Instance.new("TextBox")
Textbox.Visible = true
Textbox.Name = "TextBox"
Textbox.Active = true
Textbox.BackgroundColor3 = Color3.fromRGB(39,39,39)
Textbox.TextColor3 = Color3.fromRGB(255,255,255)
Textbox.BorderColor3 = Color3.fromRGB(255,255,255)
Textbox.Position = UDim2.new(0.0175,0,0.53,0)
Textbox.AnchorPoint = Vector2.new(0,0.5)
Textbox.Size = UDim2.new(0.965,0,0.75,0)
Textbox.Transparency = 0
Textbox.BackgroundTransparency = 0
Textbox.BorderSizePixel = 10
Textbox.RichText = true
Textbox.Font = "Nunito"
Textbox.Text = text
Textbox.PlaceholderText = name
Textbox.ZIndex = 5
Textbox.TextXAlignment = "Left"
Textbox.SizeConstraint = "RelativeXY"
Textbox.Parent = Inner
Textbox.TextSize = Textbox.AbsoluteSize.Y * 0.6
Textbox:GetPropertyChangedSignal("AbsoluteSize"):Connect(function()
	Textbox.TextSize = Textbox.AbsoluteSize.Y * 0.6
	end)
Lib:UICorner(Textbox,1)

local Shade = Instance.new("Frame")
Shade.Visible = true
Shade.Name = "Shade"
Shade.Active = true
Shade.BackgroundColor3 = Color3.fromRGB(0,0,0)
Shade.BorderColor3 = Color3.fromRGB(255,255,255)
Shade.Position = UDim2.new(0.01475,0,0.5,0)
Shade.AnchorPoint = Vector2.new(0,0.5)
Shade.Size = UDim2.new(0.9675,0,0.8,0)
Shade.Transparency = 0
Shade.BackgroundTransparency = 0
Shade.BorderSizePixel = 10
Shade.ZIndex = 4
Shade.SizeConstraint = "RelativeXY"
Shade.Parent = Inner
Lib:UICorner(Shade,1)

return Textbox,name,Inner,Shade
end

return Feat,name,Tab,Text,Inside
end

local More = Instance.new("ImageLabel")
local MoreVis = More
More.Visible = false
More.Name = "Cat_More2nd"
More.BorderSizePixel = 0
More.Image = MoreIn
More.ImageTransparency = 0.25
More.Active = false
More.BackgroundColor3 = Color3.fromRGB(255,255,255)
More.Position = UDim2.new(0.115, 0, 0.845, 0)
More.Size = UDim2.new(0.025, 0, 0.05,0)
More.Transparency = 0
More.BackgroundTransparency = 1
More.BorderSizePixel = 0
More.ZIndex = 1000
More.SizeConstraint = "RelativeXY"
More.Parent = Window

local More = Instance.new("ImageLabel")
More.Visible = true
More.Name = "Cat_More1st"
More.BorderSizePixel = 0
More.Image = MoreIn
More.ImageTransparency = 0.5
More.Active = false
More.BackgroundColor3 = Color3.fromRGB(255,255,255)
More.Position = UDim2.new(0.5, 0, 0.75, 0)
More.AnchorPoint = Vector2.new(0.5,0.5)
More.Size = UDim2.new(1.5, 0, 2, 0)
More.Transparency = 0
More.BackgroundTransparency = 1
More.BorderSizePixel = 0
More.ZIndex = 1000
More.SizeConstraint = "RelativeXY"
More.Parent = MoreVis

function CheckGap()
if Categories.CanvasSize.Y.Offset > Categories.AbsoluteSize.Y and Categories.CanvasPosition.Y >= (Categories.AbsoluteCanvasSize.Y-Categories.AbsoluteSize.Y)*0.99 then
MoreVis.Visible = false
else
	MoreVis.Visible = true
end
end

CheckGap()

DC_[#DC_+1] = Categories:GetPropertyChangedSignal("CanvasPosition"):Connect(CheckGap)

return Tab_,name,Window
end

return Lib, Utility
