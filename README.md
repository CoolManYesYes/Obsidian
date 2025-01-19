Linoria with different front-end and optimizations

Format Changes:
- Toggles are Switches (You can change that using AddCheckbox or Library.ForceCheckbox)

Breaking Changes:
- Dropdown with SpecialType returns Instance instead of strings

This Lua script is creating a user interface (UI) library for a Roblox script using `LinoriaLib` and its various features. It provides a comprehensive example of how to create and manipulate UI elements like buttons, toggles, sliders, textboxes, and more, along with managing themes and saving configurations. Here's a breakdown of what each section does:

1. **Library Initialization**:
   - The script fetches external Lua files (`Library.lua`, `ThemeManager.lua`, `SaveManager.lua`) from a GitHub repository and loads them into the script.
 ```lua
local repo = "https://raw.githubusercontent.com/CoolManYesYes/Obsidian/main/"
local Library = loadstring(game:HttpGet(repo .. "Library.lua"))()
local ThemeManager = loadstring(game:HttpGet(repo .. "addons/ThemeManager.lua"))()
local SaveManager = loadstring(game:HttpGet(repo .. "addons/SaveManager.lua"))()
```


2. **Window Creation**:
   - A window titled "Example menu" is created with the UI centered and set to show automatically when initialized.

   ```lua
   local Window = Library:CreateWindow({
       Title = 'Example menu',
       Center = true,
       AutoShow = true,
       TabPadding = 8,
       MenuFadeTime = 0.2
   })
   ```

3. **Tab Creation**:
   - Two tabs, "Main" and "UI Settings", are added to the window.

   ```lua
   local Tabs = {
       Main = Window:AddTab('Main'),
       ['UI Settings'] = Window:AddTab('UI Settings'),
   }
   ```

4. **Groupboxes**:
   - A groupbox is added to the "Main" tab, which can contain UI elements like toggles, sliders, buttons, etc.

   ```lua
   local LeftGroupBox = Tabs.Main:AddLeftGroupbox('Groupbox')
   ```

5. **Toggle Creation**:
   - A toggle named "MyToggle" is added to the groupbox, which has a callback that prints the toggle state when changed.

   ```lua
   LeftGroupBox:AddToggle('MyToggle', {
       Text = 'This is a toggle',
       Default = true,
       Tooltip = 'This is a tooltip',
       Callback = function(Value)
           print('[cb] MyToggle changed to:', Value)
       end
   })
   ```

6. **Button Creation**:
   - A button named "Button" is added, and clicking it triggers a print statement.

   ```lua
   local MyButton = LeftGroupBox:AddButton({
       Text = 'Button',
       Func = function()
           print('You clicked a button!')
       end,
       Tooltip = 'This is the main button'
   })
   ```

7. **Slider Creation**:
   - A slider is created with customizable options like default value, minimum, maximum, and callback function when the value changes.

   ```lua
   LeftGroupBox:AddSlider('MySlider', {
       Text = 'This is my slider!',
       Default = 0,
       Min = 0,
       Max = 5,
       Rounding = 1,
       Callback = function(Value)
           print('[cb] MySlider was changed! New value:', Value)
       end
   })
   ```

8. **Textbox Input**:
   - A textbox is created with a callback that triggers when the text is updated.

   ```lua
   LeftGroupBox:AddInput('MyTextbox', {
       Default = 'My textbox!',
       Numeric = false,
       Callback = function(Value)
           print('[cb] Text updated. New text:', Value)
       end
   })
   ```

9. **Dropdown Creation**:
   - A dropdown menu is created with predefined options and a callback when the selection changes.

   ```lua
   LeftGroupBox:AddDropdown('MyDropdown', {
       Values = { 'This', 'is', 'a', 'dropdown' },
       Default = 1,
       Callback = function(Value)
           print('[cb] Dropdown got changed. New value:', Value)
       end
   })
   ```

10. **Color Picker**:
    - A color picker is added with the ability to change and track colors.

    ```lua
    LeftGroupBox:AddLabel('Color'):AddColorPicker('ColorPicker', {
        Default = Color3.new(0, 1, 0),
        Callback = function(Value)
            print('[cb] Color changed!', Value)
        end
    })
    ```

11. **Keybind Picker**:
    - A keybind picker allows users to select a key to trigger specific actions.

    ```lua
    LeftGroupBox:AddLabel('Keybind'):AddKeyPicker('KeyPicker', {
        Default = 'MB2',
        Callback = function(Value)
            print('[cb] Keybind clicked!', Value)
        end
    })
    ```

12. **Watermark**:
    - The watermark is updated dynamically to show FPS and ping information.

    ```lua
    local WatermarkConnection = game:GetService('RunService').RenderStepped:Connect(function()
        -- FPS and ping calculations
        Library:SetWatermark(('LinoriaLib demo | %s fps | %s ms'):format(math.floor(FPS), math.floor(game:GetService('Stats').Network.ServerStatsItem['Data Ping']:GetValue())))
    end)
    ```

13. **SaveManager and ThemeManager**:
    - These are used for saving configurations and managing themes.

    ```lua
    ThemeManager:SetLibrary(Library)
    SaveManager:SetLibrary(Library)
    ```

    The configuration is handled by `SaveManager`, and themes are applied via `ThemeManager`.

14. **Unload Function**:
    - The library has an unload function, which disconnects the watermark update and sets `Library.Unloaded` to true.

    ```lua
    Library:OnUnload(function()
        WatermarkConnection:Disconnect()
        print('Unloaded!')
        Library.Unloaded = true
    end)
    ```

This script demonstrates how to use the `LinoriaLib` to create a complex and interactive UI in Roblox, with support for toggles, buttons, sliders, keybinds, dropdowns, themes, and configurations.
