# ✨ Wand UI (Redz Library V5 Remake)

## 📌 About
- **Wand UI** is a rebuilt and optimized version of **Redz Library V5**.
- It uses the same UI style as the original, with some improvements and refinements.
- The reason the UI is named **Wand** is that it should be the name of the next generation of **redz Hub** UIs

- 🔹 Made by **real_redz** and updated by **plock4444** 
- 🔹 Designed mainly for use in **Redz Hub** scripts  
- 🔹 Open-Source, Lightweight, and Optimized  

---

## 🚀 Getting Started
To load **Wand UI**, simply run:
```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/newredzv3/Library/refs/heads/main/Redz-V5-remake/main.luau"))()
```

### Creating a Window
```lua
local Window = Library:MakeWindow({
  Title = "Nice Hub : Cool Game",
  SubTitle = "by real_redz",
  ScriptFolder = "redz-library-V5"
})
```

- NewMinimizer: (self: Window, Config: { KeyCode: KeyCode }) -> Minimizer
  - IsMinimied: boolean
  - Cancel: (self: Minimizer) -> (nil)
  - Minimize: (self: Minimizer) -> (nil)
  - CreateMobileMinimizer: (self: Minimizer, ButtonProperties: { [string]: any? }) -> ImageButton
- MakeTab: (self: Window, Configs: { Title: string, Icon: string? }) -> Tab
  - IsEnabled: boolean
  - Title: string
  - Icon: string
  - Select: (self: Tab) -> (nil)
- Notify: (self: Window, Configs: { Title: string, Content: string, Duration: number?, Image: string? } ) -> Notification
  - Close: (self: Notification)
  - Closed: boolean
- NewNotifyGroup: (self: Window, Configs: { Title: string?, Content: string?, Duration: number?, Image: string? }) -> NotificationGroup
  - Notify: (self: Window, Configs: { Title: string?, Content: string?, Duration: number?, Image: string? }) -> Notification
- Dialog: (self: Window, Configs: { Title: string, Content: string, Options: { { Name: string, Callback: function? } }) -> Dialog
  - Close: (self: Dialog) -> (nil)
  - NewOption: (self: Dialog, Configs: { Name: string, Callback: function? }) -> (nil)
- SelectTab: (self: Window, Tab: Tab | number) -> (nil)
- SetUIScale: (self: Window | Library, Value: number) -> (nil)
- GetMaxScale: (self: Library) -> number
- GetMinScale: (self: Library) -> number
- SetTitle: (self: Window, Title: string) -> (nil)
- SetSubTitle: (self: Window, SubTitle: string) -> (nil)
- GetTitle: (self: Window) -> string
- GetSubTitle: (self: Window) -> string
- MinimizeButton: (self: Window) -> (nil)
- IsValidTheme: (self: Library, ThemeName: string) -> boolean
- SetTheme: (self: Library, ThemeName: string) -> (nil)
- GetTheme: (self: Library, ThemeName: string?) -> LibraryTheme
  - Name: string
- GetThemes: (self: Library) -> { string }
- GetIconByName: (self: Library, IconName: string) -> string?
- Destroy: (self: Library | Window) -> (nil)
- DeleteFlags: (self: Window) -> (Success: boolean)
- GetFlag: (self: Window, Flag: string, Value: any?) -> (nil)
- SetFlag: (self: Window, Flag: string) -> any

### Minimizer
```lua
local Minimizer = Window:NewMinimizer({
  KeyCode = Enum.KeyCode.LeftControl
})

local MobileButton = Minimizer:CreateMobileMinimizer({
    Image = "rbxassetid://15298567397",
    Size = UDim2.new(0,35,0,35),
    Corner = { CornerRadius = UDim.new(0,6) },
})
```

### Creating a Tab
Normal
```lua
local Tab = Window:MakeTab({
  Title = "Cool Tab",
  Icon = "Home"
})
```
Compact
```lua
local Tab = Window:MakeTab({ "Cool Tab", "Home" })
```

### Creating a Dialog
```lua
Window:Dialog({
  Title = "Hello!",
  Content = "do you like Coffee?",
  Options = {
    {
      Name = "No"
    },
    {
      Name = "Yes!",
      Callback = function(self)
        print("Yes, i like Coffee")
      end
    }
  })
})
```

### Creating a Notification
```lua
Window:Notify({
  Title = "Notification",
  Content = "this is a Notification",
  Image = "rbxassetid://10734953451",
  Duration = 5
})
```

### Options API
- Builder: { (Title|Name): string, (Desc|Description): string? }
> Options Properties & Functions
- SetTitle: (self: Option, Title: string) -> Option
- SetDescription: (self: Option, Description: string) -> Option
- SetVisible: (self: Option, Value: boolean) -> (nil)
- Destroy: (self: Option) -> (nil)
- AddCallback: (self: Option, Callback: function) -> Option
- Title: string
- Description: string
- Kind: string
> Create Options
- AddToggle: (self: Tab, Configs: Builder & { Default: boolean?, Callback: function?, Flag: string? }) -> Toggle
  - Value: boolean
  - SetValue: (self: Toggle, Value: boolean) -> (nil)
- AddSlider: (self: Tab, Configs: Builder & { Max: number, Min: number, Increment: number?, Callback: function?, Flag: string? }) -> Slider
  - Value: number
  - Min: number
  - Max: number
  - Increment: number
  - SetValue: (self: Slider, Value: number) -> Slider
- AddButton: (self: Tab, Configs: Builder & { Callback: function?, Debounce: number? }) -> Button
- AddSection: (self: Tab, Title: string?) -> Section
- AddDropdown: (self: Tab, Configs: Builder & { Options: { string? } | nil, Default: string | number | { string? | number? }, MultiSelect: boolean?, Callback: function?, Flag: string? }) -> Dropdown
  - Remove: (self: Dropdown, Option: string) -> (nil)
  - Add: (self: Dropdown, ...: string) -> (nil)
  - NewOptions: (self: Dropdown, { string? | number? }) -> (nil)
  - GetOptionsCount: (self: Dropdown) -> number
  - Clear: (self: Dropdown) -> (nil)
  - GetOptionsCount: (self: Dropdown) -> number
  - Opened: boolean
- AddTextBox: (self: Tab, Configs: Builder & { Placeholder: string?, ClearOnFocus: boolean?, Callback: function?, Flag: string? )) -> TextBox
  - CaptureFocus: (self: TextBox) -> TextBox
  - SetText: (self: TextBox, Text: string) -> TextBox
  - SetTextFilter: (self: TextBox, Filter: (text: string) -> string?) -> TextBox
  - SetPlaceholder: (self: TextBox, Text: string) -> TextBox
  - Clear: (self: TextBox) -> TextBox
- AddDiscordInvite: (self: Tab, Configs: Builder & { Banner: Image | Color3, Image: string, Invite: string, Members: number?, Online: number?) -> DiscordInvite

### Creating Options

#### Section
```lua
Tab:AddSection("Section")
```

#### Toggle
```lua
Tab:AddToggle({
  Name = "Toggle",
  Default = false,
  Callback = function(Value)
    
  end
})
```

#### Button
```lua
Tab:AddButton({
  Name = "My Button",
  Debounce = 0.5,
  Callback = function()
    
  end
})
```

#### Slider
```lua
Tab:AddSlider({
  Name = "Cool Title",
  Min = -5,
  Max = 5,
  Increment = 0.25,
  Default = 0,
  Callback = function(Value)
    
  end
})
```

#### Dropdown
```lua
Tab:AddDropdown({
  Name = "Dropdown",
  Options = {"one", "two", "three", "four", "five"},
  Default = "one",
  Callback = function(Value)
    
  end
})
```
```lua
Tab:AddDropdown({
  Name = "Dropdown",
  MultiSelect = true,
  Options = {"one", "two", "three", "four", "five"},
  Default = {"one", "four"},
  Callback = function(Value)
    
  end
})
```

#### TextBox
```lua
Tab:AddTextBox({
  Name = "My TextBox",
  Default "text",
  Placeholder = "input text...",
  ClearOnFocus = true,
  Callback = function(Value)
    
  end
})
```

#### Paragraph
```lua
Tab:AddParagraph("Paragraph", "This is a Paragraph\nSecond Line")
```

#### Discord Invite
```lua
MainTab:AddDiscordInvite({
	Title = "redz Hub | Community",
	Description = "Your Description",
	Banner = "rbxassetid://17382040552", -- You can put an RGB Color: Color3.fromRGB(233, 37, 69)
	Logo = "rbxassetid://17382040552",
	Invite = "https://discord.gg/Mkj6W5Rz8E",
	Members = 470000, -- Optional
	Online = 20000, -- Optional
})
```

### UI Scale
- Min Scale: ``0.6``
- Max Scale: ``1.6``
- Default Scale: ``1.0``
```lua
Library:SetUIScale(1.0)
```
```lua
print(`UI Max Scale is: {Library:GetMinScale()} and the minimum is: {Library:GetMaxScale()}`)
```

### Flags
```lua
Tab:AddToggle({
  Name = "Cool Toggle",
  Flag = "toggle_flag"
})
```
```lua
local ToggleValue = Window:GetFlag("toggle_flag") or false

Tab:AddToggle({
  Name = "Cool Toggle",
  Default = ToggleValue,
  Callback = function(Value)
    Window:SetFlag("toggle_flag", Value)
  end
})
```

### example of use 
```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/newredzv3/Library/refs/heads/main/Redz-V5-remake/main.luau"))()

local Window = Library:MakeWindow({
  Title = "redz hub : Game",
  SubTitle = "Wand UI Demo",
  ScriptFolder = "wand-ui"
})

local Minimizer = Window:NewMinimizer({
  KeyCode = Enum.KeyCode.LeftControl
})

local MobileButton = Minimizer:CreateMobileMinimizer({
    Image = "rbxassetid://15298567397",
    Size = UDim2.new(0,35,0,35),
    Corner = { CornerRadius = UDim.new(0,6) },
})

local MainTab = Window:MakeTab({
  Title = "Main",
  Icon = "Home"
})

local ConfigTab = Window:MakeTab({
  Title = "Config",
  Icon = "Settings"
})

MainTab:AddSection("Button")
MainTab:AddButton({
  Name = "Test Button",
  Callback = function()
    Window:Notify({
      Title = "Clicked",
      Content = "You pressed the button",
      Duration = 3
    })
  end
})

MainTab:AddSection("Toggle")
MainTab:AddToggle({
  Name = "Auto Farm",
  Default = false,
  Flag = "auto_farm",
  Callback = function(v)
    Window:Notify({
      Title = "Toggle",
      Content = tostring(v),
      Duration = 3
    })
  end
})

MainTab:AddSection("Slider")
MainTab:AddSlider({
  Name = "Speed",
  Min = 0,
  Max = 100,
  Increment = 5,
  Default = 50,
  Callback = function(v)
    print(v)
  end
})

MainTab:AddSection("Dropdown")
MainTab:AddDropdown({
  Name = "Select Fruit",
  Options = {"Light","Dough","Leopard"},
  Default = "Light",
  Callback = function(v)
    print(v)
  end
})

MainTab:AddSection("Dropdown Multi")
MainTab:AddDropdown({
  Name = "Multi Select",
  MultiSelect = true,
  Options = {"A","B","C","D","E","F","G","H","I"},
  Default = {"A"},
  Callback = function(v)
    print(v)
  end
})

MainTab:AddSection("Textbox")
MainTab:AddTextBox({
  Name = "Enter Text",
  Placeholder = "type...",
  ClearOnFocus = true,
  Callback = function(v)
    print(v)
  end
})

MainTab:AddSection("Paragraph")
MainTab:AddParagraph("Info","Line 1\nLine 2")

MainTab:AddSection("Discord")
MainTab:AddDiscordInvite({
  Title = "redz hub : Community",
  Description = "",
  Banner = "rbxassetid://17382040552",
  Logo = "rbxassetid://17382040552",
  Invite = "https://discord.gg/Mkj6W5Rz8E"
})

ConfigTab:AddSection("UI Scale")
ConfigTab:AddSlider({
  Name = "Scale",
  Min = 0.6,
  Max = 1.6,
  Increment = 0.1,
  Default = 1,
  Callback = function(v)
    Library:SetUIScale(v)
  end
})

ConfigTab:AddSection("Theme")
ConfigTab:AddDropdown({
  Name = "Theme",
  Options = Library:GetThemes(),
  Default = Library:GetTheme().Name,
  Callback = function(v)
    Library:SetTheme(v)
  end
})

ConfigTab:AddSection("Flags")
local val = Window:GetFlag("auto_farm") or false
ConfigTab:AddToggle({
  Name = "Auto Farm Sync",
  Default = false,
  Callback = function(v)
    Window:SetFlag("auto_farm", v)
  end
})
Window:Notify({
  Title = 'Script Loaded',
  Content = 'redz hub loaded successfully! Press "LeftControl" to Minimize',
  Image = 'rbxassetid://112146984347920',
  Duration = 5
})
Window:SelectTab(1)
