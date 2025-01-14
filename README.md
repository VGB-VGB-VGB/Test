

if not game.CoreGui:FindFirstChild("XScreen") then

    local XScreen = Instance.new("ScreenGui")

    local XToggle = Instance.new("TextButton")

    local ThunderCornerUI = Instance.new("UICorner")

    local ThunderImageUI = Instance.new("ImageLabel")

    local TestLabelEN = Instance.new("TextLabel")

    local TestLabelVN = Instance.new("TextLabel")



    XScreen.Name = "Copy Discord Link (New Link)"

    XScreen.Parent = game.CoreGui

    XScreen.ZIndexBehavior = Enum.ZIndexBehavior.Sibling



    XToggle.Name = "XToggle"

    XToggle.Parent = XScreen

    XToggle.BackgroundColor3 = Color3.fromRGB(244, 244, 0)

    XToggle.Position = UDim2.new(0.5, -75, 0.0952890813, 0)
    XToggle.Size = UDim2.new(0, 150, 0, 30)

    XToggle.Font = Enum.Font.SourceSansSemibold

    XToggle.Text = "Copy Discord Link"

    XToggle.TextColor3 = Color3.fromRGB(0, 0, 0)

    XToggle.TextSize = 19

    XToggle.Draggable = true



    TestLabelEN.Name = "TestLabelEN"

    TestLabelEN.Parent = XScreen

    TestLabelEN.BackgroundTransparency = 1

    TestLabelEN.Size = UDim2.new(0, 200, 0, 50)

    TestLabelEN.Position = UDim2.new(0.5, -100, 0.4, -25)

    TestLabelEN.Font = Enum.Font.SourceSansBold

    TestLabelEN.Text = "English: Script update"

    TestLabelEN.TextColor3 = Color3.fromRGB(255, 255, 255)

    TestLabelEN.TextSize = 30



    TestLabelVN.Name = "TestLabelVN"

    TestLabelVN.Parent = XScreen

    TestLabelVN.BackgroundTransparency = 1

    TestLabelVN.Size = UDim2.new(0, 200, 0, 50)

    TestLabelVN.Position = UDim2.new(0.5, -100, 0.5, -25)

    TestLabelVN.Font = Enum.Font.SourceSansBold

    TestLabelVN.Text = "VN : Script đang cập nhập"

    TestLabelVN.TextColor3 = Color3.fromRGB(255, 255, 255)

    TestLabelVN.TextSize = 30



    XToggle.MouseButton1Click:Connect(function()

        setclipboard("https://discord.gg/98ww9CJ5fQ")

    end)

end
repeat wait() until game:IsLoaded()

wait()



for _, v in next, getconnections(game:GetService("Players").LocalPlayer.Idled) do

    v:Disable()

end


local ScreenGui = Instance.new("ScreenGui")
local LinkLabel = Instance.new("TextLabel")
local PingLabel = Instance.new("TextLabel")
local FPSLabel = Instance.new("TextLabel")

ScreenGui.Name = "PingFPSDisplay"
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

LinkLabel.Name = "LinkLabel"
LinkLabel.Parent = ScreenGui
LinkLabel.BackgroundTransparency = 1 -- Loại bỏ khung nền
LinkLabel.Position = UDim2.new(0.1, 0, 0, 0) -- Di chuyển vị trí sang bên trái (0.1, 0 là 10% từ bên trái màn hình)
LinkLabel.Size = UDim2.new(0, 250, 0, 20) -- Điều chỉnh chiều rộng (250 pixel)
LinkLabel.Font = Enum.Font.SourceSans
LinkLabel.TextColor3 = Color3.new(1, 1, 1)
LinkLabel.TextSize = 14
LinkLabel.Text = "https://discord.gg/98ww9CJ5fQ"
LinkLabel.TextWrapped = true
LinkLabel.TextScaled = false
PingLabel.Name = "PingLabel"
PingLabel.Parent = ScreenGui
PingLabel.BackgroundTransparency = 1 -- Loại bỏ khung nền
PingLabel.Position = UDim2.new(0.1, 0, 0.05, 0) -- Vị trí dưới LinkLabel, bên trái
PingLabel.Size = UDim2.new(0, 250, 0, 20) -- Đặt chiều rộng giống như LinkLabel
PingLabel.Font = Enum.Font.SourceSans -- Đặt font giống LinkLabel
PingLabel.TextColor3 = Color3.new(1, 1, 1)
PingLabel.TextSize = 14 -- Đặt kích thước chữ giống LinkLabel
PingLabel.Text = "Ping: 0 ms" -- Hiển thị "Ping: 0 ms" mặc định

FPSLabel.Name = "FPSLabel"
FPSLabel.Parent = ScreenGui
FPSLabel.BackgroundTransparency = 1 -- Loại bỏ khung nền
FPSLabel.Position = UDim2.new(0.1, 0, 0.1, 0) -- Vị trí dưới PingLabel, bên trái
FPSLabel.Size = UDim2.new(0, 250, 0, 20) -- Đặt chiều rộng giống như PingLabel
FPSLabel.Font = Enum.Font.SourceSans
FPSLabel.TextColor3 = Color3.new(1, 1, 1)
FPSLabel.TextSize = 14
FPSLabel.Text = "FPS: Calculating..."

-- Hàm cập nhật Ping
local RunService = game:GetService("RunService")
local function UpdatePing()
    while true do
        local pingValue = game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValueString()
        local pingNumber = tonumber(pingValue:match("([0-9]+)")) -- Lấy số từ chuỗi (loại bỏ phần "ms")
        PingLabel.Text = "Ping: " .. tostring(pingNumber) .. " ms" -- Hiển thị "Ping: giá trị ms"
        wait(1) -- Cập nhật mỗi giây
    end
end

-- Hàm cập nhật FPS
local function UpdateFPS()
    local lastTime = tick()
    local frameCount = 0
    while true do
        frameCount = frameCount + 1
        if tick() - lastTime >= 1 then
            FPSLabel.Text = "FPS: " .. tostring(math.min(frameCount, 120)) -- Giới hạn tối đa 120 FPS
            frameCount = 0
            lastTime = tick()
        end
        RunService.RenderStepped:Wait() -- Cập nhật mỗi frame
    end
end

-- Chạy các hàm cập nhật
spawn(UpdatePing)
spawn(UpdateFPS)
