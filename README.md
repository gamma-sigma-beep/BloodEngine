<picture>
 <img alt="Logo" src="https://devforum-uploads.s3.dualstack.us-east-2.amazonaws.com/uploads/optimized/5X/7/3/3/2/73326251a8afb11d5fc56cbdeae45a39dc22647c_2_690x176.png">
</picture>

## Usage

To use Blood Engine, you need to require the module in your script and create a new instance of it. You can pass some arguments to the constructor to change the default settings of the system. For example:

```lua
-- You can leave any of these values as nil or not assign them, it'll use the default values
local DripSettings = {
  IgnorePlayers = false, -- Ignores any player characters in the workspace.
  Decals = false, -- Use if you want to have your pools be decals instead of cylinders.
  RandomOffset = true, -- Whether to randomly offset the starting position of the droplets or not.
  DripVisible = false, -- Whether to show the droplets before they become a pool or not.
  DripDelay = 0.01, -- The delay between each droplet.
  DecayDelay = { 10, 15 }, -- Each pool will start to fade away randomly between min and max seconds after it’s created.
  Speed = 0.5, -- Determines the speed/velocity of the droplets.
  Limit = 500, -- The maximum number of droplets/pools.
  SplashAmount = 10, -- The amount of splash particles to emit, 0 to fully disable it.
  DefaultSize = { 0.4, 0.7 }, -- Minimum and Maximum. Both determine the default size of a pool.
  Filter = {}, -- An array that stores instances that don't interfere with the droplets raycast process.
}

-- MODULE
local BloodEngine = require(ReplicatedStorage.BloodEngine)
local BloodInstance = BloodEngine.new(DripSettings) -- customize to whatever you want
```

Then, you can use the Emit method to create blood drips from a base part in a given direction with a given amount. For example:

```lua
-- TARGET
local Part = workspace.Part

-- Emits drips from a part in the workspace, emits 10 blood drips only in the front direction
-- Leave the direction nil if you want it to go in a random direction `BloodInstance:Emit(Part, nil, 10)`
-- EXAMPLE: BloodInstance:Emit(Part, nil, 10)
BloodInstance:Emit(Part, Part.CFrame.LookVector, 10) -- also customize to whatever you want.
```

You can also change the settings of the system after creating an instance by accessing its properties. For example:

```lua
BloodInstance:UpdateSettings({
	Speed = 0
	DripDelay = 5
})
```

Now if you’d want to make a fully fledged system that makes blood appear in all clients, you can make a remote event, from server to client. When drips are needed, you can pass off the settings (BasePart, Direction, Amount) and the client will do the rest. Its recommended to have only one script manage the blood engine and let the server use its Emit method using the remote event.
