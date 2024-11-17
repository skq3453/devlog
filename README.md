## Get Stuff
```lua
--themes
local Halloween = Color3.fromRGB(255, 60, 1) --october
local Christmas = Color3.fromRGB(250, 0, 0) --chrtismas
local July = Color3.fromRGB(0, 85, 255) --july
local Regular = Color3.fromRGB(49, 0, 148)

local Library = {}

function Library:CreateWindow(title)
	local UI = Instance.new("ScreenGui")
	local Main = Instance.new("Frame")
	local UICorner = Instance.new("UICorner")
	local TopBar = Instance.new("Frame")
	local Title = Instance.new("TextLabel")
	local Line = Instance.new("Frame")
	local Navigation = Instance.new("ScrollingFrame")
	local UIListLayout = Instance.new("UIListLayout")
	local UIPadding = Instance.new("UIPadding")
	local Line_2 = Instance.new("Frame")
	local Content = Instance.new("Frame")
	
	UI.Name = "UI"
	UI.Parent = game:GetService("Players").LocalPlayer.PlayerGui or game:GetService("CoreGui")
	UI.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
	UI.ResetOnSpawn = false

	Main.Name = "Main"
	Main.Parent = UI
	Main.BackgroundColor3 = Color3.fromRGB(11, 11, 11)
	Main.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Main.BorderSizePixel = 0
	Main.Position = UDim2.new(0, 389, 0, 150)
	Main.Size = UDim2.new(0, 511, 0, 352)

	UICorner.CornerRadius = UDim.new(0, 4)
	UICorner.Parent = Main

	TopBar.Name = "TopBar"
	TopBar.Parent = Main
	TopBar.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	TopBar.BackgroundTransparency = 1.000
	TopBar.BorderColor3 = Color3.fromRGB(0, 0, 0)
	TopBar.BorderSizePixel = 0
	TopBar.Size = UDim2.new(0, 511, 0, 50)

	Title.Name = "Title"
	Title.Parent = TopBar
	Title.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Title.BackgroundTransparency = 1.000
	Title.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Title.BorderSizePixel = 0
	Title.Position = UDim2.new(0.0587084144, 0, 0, 5)
	Title.Size = UDim2.new(0, 200, 0, 50)
	Title.Font = Enum.Font.IndieFlower
	Title.Text = title
	Title.TextColor3 = Color3.fromRGB(222, 222, 222)
	Title.TextSize = 47.000
	Title.TextXAlignment = Enum.TextXAlignment.Left
	
	local currentMonth = os.date("*t").month

	if currentMonth == 12 then
		Title.Text = title .. " 🎁"  -- December: Gift emoji
	elseif currentMonth == 10 or 11 then
		Title.Text = title .. " 🎃"  -- October: Pumpkin emoji
	elseif currentMonth == 7 or 8 then
		Title.Text = title .. " 🎇"  -- July: Fireworks emoji
	else
		Title.Text = title  -- Default title for other months
	end

	Line.Name = "Line"
	Line.Parent = Main
	Line.BackgroundColor3 = Color3.fromRGB(51, 51, 51)
	Line.BackgroundTransparency = 0.500
	Line.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Line.BorderSizePixel = 0
	Line.Position = UDim2.new(0, 0, 0.142045453, 0)
	Line.Size = UDim2.new(0, 511, 0, 1)

	Navigation.Name = "Navigation"
	Navigation.Parent = Main
	Navigation.Active = true
	Navigation.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Navigation.BackgroundTransparency = 1.000
	Navigation.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Navigation.BorderSizePixel = 0
	Navigation.Position = UDim2.new(0, 0, 0.14488636, 0)
	Navigation.Size = UDim2.new(0, 140, 0, 301)
	Navigation.ScrollBarImageColor3 = Color3.fromRGB(0, 0, 0)
	Navigation.ScrollBarThickness = 0

	UIListLayout.Parent = Navigation
	UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
	UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
	UIListLayout.Padding = UDim.new(0, 4)

	UIPadding.Parent = Navigation
	UIPadding.PaddingTop = UDim.new(0, 6)
	
	Line_2.Name = "Line"
	Line_2.Parent = Main
	Line_2.BackgroundColor3 = Color3.fromRGB(51, 51, 51)
	Line_2.BackgroundTransparency = 0.500
	Line_2.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Line_2.BorderSizePixel = 0
	Line_2.Position = UDim2.new(0.273972601, 0, 0.14488636, 0)
	Line_2.Size = UDim2.new(0, 1, 0, 301)

	Content.Name = "Content"
	Content.Parent = Main
	Content.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Content.BackgroundTransparency = 1.000
	Content.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Content.BorderSizePixel = 0
	Content.Position = UDim2.new(0.27592954, 0, 0.14488636, 0)
	Content.Size = UDim2.new(0, 370, 0, 301)
	
	local function ZPBE_script() -- Main.dragWindow 
		local script = Instance.new('LocalScript', Main)

		local TweenService = game:GetService("TweenService")
		local UserInputService = game:GetService("UserInputService")

		local gui = script.Parent

		local dragging
		local dragInput
		local dragStart
		local startPos

		local tweenInfo = TweenInfo.new(0.16, Enum.EasingStyle.Linear, Enum.EasingDirection.Out)

		local function update(input)
			local delta = input.Position - dragStart
			local targetPos = UDim2.new(
				startPos.X.Scale, 
				startPos.X.Offset + delta.X, 
				startPos.Y.Scale, 
				startPos.Y.Offset + delta.Y
			)

			local tween = TweenService:Create(gui, tweenInfo, {Position = targetPos})
			tween:Play()
		end

		gui.InputBegan:Connect(function(input)
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

		gui.InputChanged:Connect(function(input)
			if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
				dragInput = input
			end
		end)

		UserInputService.InputChanged:Connect(function(input)
			if input == dragInput and dragging then
				update(input)
			end
		end)

	end
	coroutine.wrap(ZPBE_script)()
	
	local SelectedTab = nil

	function Library:CreateTab(title)
		local Tab = {}

		local TabButton = Instance.new("TextButton")
		local UICorner_3 = Instance.new("UICorner")
		local Items = Instance.new("ScrollingFrame")
		local UIListLayout_2 = Instance.new("UIListLayout")
		local UIPadding_2 = Instance.new("UIPadding")

		TabButton.Name = "Tab"
		TabButton.Parent = Navigation
		TabButton.BackgroundColor3 = Halloween
		TabButton.BackgroundTransparency = 1.000
		TabButton.BorderColor3 = Color3.fromRGB(0, 0, 0)
		TabButton.BorderSizePixel = 0
		TabButton.Position = UDim2.new(0.0357142873, 0, 0, 0)
		TabButton.Size = UDim2.new(0, 130, 0, 35)
		TabButton.AutoButtonColor = false
		TabButton.Font = Enum.Font.SourceSans
		TabButton.Text = title
		TabButton.TextColor3 = Color3.fromRGB(212, 212, 212)
		TabButton.TextSize = 18.000
		TabButton.TextTransparency = 0.600

		UICorner_3.CornerRadius = UDim.new(0, 6)
		UICorner_3.Parent = TabButton

		Items.Name = title
		Items.Parent = Content
		Items.Active = true
		Items.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Items.BackgroundTransparency = 1.000
		Items.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Items.BorderSizePixel = 0
		Items.Size = UDim2.new(0, 370, 0, 301)
		Items.ScrollBarImageColor3 = Color3.fromRGB(0, 0, 0)
		Items.ScrollBarThickness = 0
		Items.Visible = false

		UIListLayout_2.Parent = Items
		UIListLayout_2.HorizontalAlignment = Enum.HorizontalAlignment.Center
		UIListLayout_2.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout_2.Padding = UDim.new(0, 6)

		UIPadding_2.Parent = Items
		UIPadding_2.PaddingTop = UDim.new(0, 6)

		if not SelectedTab then
			Items.Visible = true
			TabButton.BackgroundTransparency = 0
			TabButton.TextTransparency = 0
			SelectedTab = TabButton
		end

		TabButton.MouseButton1Click:Connect(function()
			if SelectedTab then
				local prevTabContent = Content:FindFirstChild(SelectedTab.Text)
				if prevTabContent then
					prevTabContent.Visible = false
				end
				SelectedTab.BackgroundTransparency = 1
				SelectedTab.TextTransparency = 0.6
			end

			Items.Visible = true
			TabButton.BackgroundTransparency = 0
			TabButton.TextTransparency = 0
			SelectedTab = TabButton
		end)
		
		return TabButton, Items
	end
	
	local TweenService = game:GetService("TweenService")

	function Library:CreateToggle(title, TabParent, callback)
		local Toggle = Instance.new("ImageButton")
		local UICorner_6 = Instance.new("UICorner")
		local UIStroke_3 = Instance.new("UIStroke")
		local Title_3 = Instance.new("TextLabel")
		local Checkbox_2 = Instance.new("Frame")
		local UICorner_7 = Instance.new("UICorner")
		local Checkmark_2 = Instance.new("ImageLabel")
		local UIAspectRatioConstraint_2 = Instance.new("UIAspectRatioConstraint")
		local UIStroke_4 = Instance.new("UIStroke")

		-- Setup the Toggle
		Toggle.Name = "Toggle"
		Toggle.Parent = TabParent
		Toggle.BackgroundColor3 = Color3.fromRGB(7, 7, 7)
		Toggle.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Toggle.BorderSizePixel = 0
		Toggle.Position = UDim2.new(0.0229729731, 0, 0, 0)
		Toggle.Size = UDim2.new(0, 353, 0, 39)
		Toggle.AutoButtonColor = false

		UICorner_6.CornerRadius = UDim.new(0, 6)
		UICorner_6.Parent = Toggle

		UIStroke_3.Parent = Toggle
		UIStroke_3.Color = Color3.fromRGB(51, 51, 51)
		UIStroke_3.Transparency = 0.500
		UIStroke_3.Thickness = 1.500

		Title_3.Name = "Title"
		Title_3.Parent = Toggle
		Title_3.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Title_3.BackgroundTransparency = 1.000
		Title_3.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Title_3.BorderSizePixel = 0
		Title_3.Position = UDim2.new(0.118198469, 0, 0.179487184, 0)
		Title_3.Size = UDim2.new(0, 200, 0, 24)
		Title_3.Font = Enum.Font.SourceSans
		Title_3.Text = title
		Title_3.TextColor3 = Color3.fromRGB(222, 222, 222)
		Title_3.TextSize = 18.000
		Title_3.TextTransparency = 0
		Title_3.TextXAlignment = Enum.TextXAlignment.Left

		Checkbox_2.Name = "Checkbox"
		Checkbox_2.Parent = Toggle
		Checkbox_2.BackgroundColor3 = Color3.fromRGB(11, 11, 11)
		Checkbox_2.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Checkbox_2.BorderSizePixel = 0
		Checkbox_2.Position = UDim2.new(0, 5, 0.15384616, 0)
		Checkbox_2.Size = UDim2.new(0, 28, 0, 26)

		UICorner_7.CornerRadius = UDim.new(0, 4)
		UICorner_7.Parent = Checkbox_2

		Checkmark_2.Name = "Checkmark"
		Checkmark_2.Parent = Checkbox_2
		Checkmark_2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Checkmark_2.BackgroundTransparency = 1.000
		Checkmark_2.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Checkmark_2.BorderSizePixel = 0
		Checkmark_2.Position = UDim2.new(0.107142858, 0, 0.0769230798, 0)
		Checkmark_2.Size = UDim2.new(0, 22, 0, 25)
		Checkmark_2.Image = "rbxassetid://10709790644"
		Checkmark_2.ImageTransparency = 1.000

		UIAspectRatioConstraint_2.Parent = Checkmark_2

		UIStroke_4.Parent = Checkbox_2
		UIStroke_4.Thickness = 1.500

		local function tweenCheckboxBackgroundColor(targetColor)
			local tweenInfo = TweenInfo.new(0.1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
			local tween = TweenService:Create(Checkbox_2, tweenInfo, {BackgroundColor3 = targetColor})
			tween:Play()
		end

		Toggle.MouseButton1Click:Connect(function()
			local state = Checkmark_2.ImageTransparency == 1
			Checkmark_2.ImageTransparency = state and 0 or 1
			callback(state)

			if state then
				tweenCheckboxBackgroundColor(Halloween)
			else
				tweenCheckboxBackgroundColor(Color3.fromRGB(11, 11, 11))
			end
		end)
	end
	
	local UIS = game:GetService("UserInputService")

	function Library:CreateSlider(title, TabParent, min, max, callback) 
		local Slider = Instance.new("ImageButton")
		local UICorner_8 = Instance.new("UICorner")
		local UIStroke_5 = Instance.new("UIStroke")
		local Title_4 = Instance.new("TextLabel")
		local SliderBack = Instance.new("Frame")
		local UICorner_9 = Instance.new("UICorner")
		local Draggable = Instance.new("Frame")
		local UICorner_10 = Instance.new("UICorner")
		local Value = Instance.new("TextLabel")

		Slider.Name = "Slider"
		Slider.Parent = TabParent
		Slider.BackgroundColor3 = Color3.fromRGB(7, 7, 7)
		Slider.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Slider.BorderSizePixel = 0
		Slider.Position = UDim2.new(0.0229729731, 0, 0.305084735, 0)
		Slider.Size = UDim2.new(0, 353, 0, 47)
		Slider.AutoButtonColor = false

		UICorner_8.CornerRadius = UDim.new(0, 6)
		UICorner_8.Parent = Slider

		UIStroke_5.Parent = Slider
		UIStroke_5.Color = Color3.fromRGB(51, 51, 51)
		UIStroke_5.Transparency = 0.500
		UIStroke_5.Thickness = 1.500

		Title_4.Name = "Title"
		Title_4.Parent = Slider
		Title_4.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Title_4.BackgroundTransparency = 1.000
		Title_4.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Title_4.BorderSizePixel = 0
		Title_4.Position = UDim2.new(0.0218811892, 0, 0.101362228, 0)
		Title_4.Size = UDim2.new(0, 200, 0, 24)
		Title_4.Font = Enum.Font.SourceSans
		Title_4.Text = title
		Title_4.TextColor3 = Color3.fromRGB(222, 222, 222)
		Title_4.TextSize = 18.000
		Title_4.TextXAlignment = Enum.TextXAlignment.Left

		SliderBack.Name = "SliderBack"
		SliderBack.Parent = Slider
		SliderBack.BackgroundColor3 = Color3.fromRGB(21, 21, 21)
		SliderBack.BorderColor3 = Color3.fromRGB(0, 0, 0)
		SliderBack.BorderSizePixel = 0
		SliderBack.Position = UDim2.new(0.0226628892, 0, 0.750383735, 0)
		SliderBack.Size = UDim2.new(0, 338, 0, 5)

		UICorner_9.Parent = SliderBack

		Draggable.Name = "Draggable"
		Draggable.Parent = SliderBack
		Draggable.BackgroundColor3 = Halloween
		Draggable.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Draggable.BorderSizePixel = 0
		Draggable.Size = UDim2.new(0, 233, 0, 5)

		UICorner_10.Parent = Draggable

		Value.Name = "Value"
		Value.Parent = Slider
		Value.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Value.BackgroundTransparency = 1.000
		Value.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Value.BorderSizePixel = 0
		Value.Position = UDim2.new(0.395818859, 0, 0.101362512, 0)
		Value.Size = UDim2.new(0, 200, 0, 24)
		Value.Font = Enum.Font.SourceSans
		Value.Text = "0.1"
		Value.TextColor3 = Color3.fromRGB(222, 222, 222)
		Value.TextSize = 18.000
		Value.TextXAlignment = Enum.TextXAlignment.Right

		local currentValue = min
		local isDragging = false
		local touchID = nil

		local function UpdateSliderPosition()
			local percentage = math.clamp((currentValue - min) / (max - min), 0, 1)
			Value.Text = string.format("%.1f", currentValue)
			Draggable.Size = UDim2.new(percentage, 0, 1, 0)
			callback(currentValue)
		end

		local function StartDragging(input)
			isDragging = true
			if input.UserInputType == Enum.UserInputType.Touch then
				touchID = input.UserInputIndex
			end
		end

		local function UpdateDragging(input)
			local inputPosition
			if input.UserInputType == Enum.UserInputType.MouseMovement then
				inputPosition = input.Position.X
			elseif input.UserInputType == Enum.UserInputType.Touch then
				inputPosition = input.Position.X
			end

			if isDragging then
				local sliderX = SliderBack.AbsolutePosition.X
				local sliderWidth = SliderBack.AbsoluteSize.X
				local newPercentage = math.clamp((inputPosition - sliderX) / sliderWidth, 0, 1)
				currentValue = min + (newPercentage * (max - min))
				currentValue = math.round(currentValue * 10) / 10
				UpdateSliderPosition()
			end
		end

		local function StopDragging(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
				isDragging = false
				touchID = nil
			end
		end

		Slider.MouseButton1Down:Connect(StartDragging)
		UIS.InputChanged:Connect(UpdateDragging)
		UIS.InputEnded:Connect(StopDragging)

		UpdateSliderPosition()
	end
	
	function Library:CreateDropdown(title, TabParent, options, callback)
		local Dropdown = Instance.new("ImageButton")
		local UICorner = Instance.new("UICorner")
		local UIStroke = Instance.new("UIStroke")
		local TitleLabel = Instance.new("TextLabel")
		local SelectedText = Instance.new("TextLabel")
		local DropdownList = Instance.new("Frame")
		local UICorner_9 = Instance.new("UICorner")
		local UIStroke_9 = Instance.new("UIStroke")
		local UIListLayout = Instance.new("UIListLayout")

		Dropdown.Name = "Dropdown"
		Dropdown.Parent = TabParent
		Dropdown.BackgroundColor3 = Color3.fromRGB(7, 7, 7)
		Dropdown.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Dropdown.BorderSizePixel = 0
		Dropdown.Position = UDim2.new(0.0229729731, 0, 0, 0)
		Dropdown.Size = UDim2.new(0, 353, 0, 39)
		Dropdown.AutoButtonColor = false

		UICorner.CornerRadius = UDim.new(0, 6)
		UICorner.Parent = Dropdown

		UIStroke.Parent = Dropdown
		UIStroke.Color = Color3.fromRGB(51, 51, 51)
		UIStroke.Transparency = 0.500
		UIStroke.Thickness = 1.500

		TitleLabel.Name = "Title"
		TitleLabel.Parent = Dropdown
		TitleLabel.BackgroundTransparency = 1
		TitleLabel.Position = UDim2.new(0.214515746, 0, 0.179487184, 0)
		TitleLabel.Size = UDim2.new(0, 200, 0, 24)
		TitleLabel.Font = Enum.Font.SourceSans
		TitleLabel.Text = title
		TitleLabel.TextColor3 = Color3.fromRGB(222, 222, 222)
		TitleLabel.TextSize = 18.000

		SelectedText.Name = "SelectedText"
		SelectedText.Parent = Dropdown
		SelectedText.BackgroundTransparency = 1
		SelectedText.Position = UDim2.new(0.630946338, 0, 0.179487184, 0)
		SelectedText.Size = UDim2.new(0, 116, 0, 24)
		SelectedText.Font = Enum.Font.SourceSans
		SelectedText.Text = options[1] or "Select an Option"
		SelectedText.TextColor3 = Color3.fromRGB(222, 222, 222)
		SelectedText.TextSize = 18.000
		SelectedText.TextXAlignment = Enum.TextXAlignment.Right

		DropdownList.Name = "DropdownList"
		DropdownList.Parent = Dropdown
		DropdownList.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
		DropdownList.BackgroundTransparency = 0.7
		DropdownList.Position = UDim2.new(0, 0, 1, 0)
		DropdownList.Size = UDim2.new(0, 353, 0, #options * 40)
		DropdownList.Visible = false

		UIListLayout.Parent = DropdownList
		UIListLayout.FillDirection = Enum.FillDirection.Vertical
		UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout.Padding = UDim.new(0, 2)

		for i, option in ipairs(options) do
			local OptionButton = Instance.new("TextButton")
			OptionButton.Name = "Option" .. i
			OptionButton.Parent = DropdownList
			OptionButton.BackgroundColor3 = Color3.fromRGB(7, 7, 7)
			OptionButton.Size = UDim2.new(1, 0, 0, 40)
			OptionButton.Position = UDim2.new(0, 0, (i-1) * 0.1, 0)
			OptionButton.Font = Enum.Font.SourceSans
			OptionButton.Text = option
			OptionButton.TextColor3 = Color3.fromRGB(222, 222, 222)
			OptionButton.TextSize = 18
			OptionButton.AutoButtonColor = false

			UICorner_9.CornerRadius = UDim.new(0, 6)
			UICorner_9.Parent = OptionButton

			UIStroke_9.Parent = OptionButton
			UIStroke_9.Color = Color3.fromRGB(51, 51, 51)
			UIStroke_9.Transparency = 0.500
			UIStroke_9.Thickness = 1.500

			OptionButton.MouseButton1Click:Connect(function()
				SelectedText.Text = option
				DropdownList.Visible = false
				if callback then
					callback(option)
				end
			end)
		end

		Dropdown.MouseButton1Click:Connect(function()
			DropdownList.Visible = not DropdownList.Visible
		end)
	end

	return Library
end
```
## Create Window
```lua
Library:CreateWindow("SHADOW")
```
## Create Tab
```lua
local tab1, tab1 = Library:CreateTab("band4band")
```
## Create Toggle
```lua
Library:CreateToggle("Example Toggle 1", tab1, function(state)
	print(state)
end)
```
## Create Slider
```lua
Library:CreateSlider("Magnet Range", tab1, 0, 10, function(value)
	print("Slider Value: ", value)
end)
```
## Create Dropdown
```lua
Library:CreateDropdown("Select a color", tab1, {"Red", "Green", "Blue"}, function(selectedOption)
	print("Selected option:", selectedOption)
end)
```
