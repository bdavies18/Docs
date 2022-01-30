Scripting (LUA)
===============

The client and world server used the LUA scripting language to implement
much of AI and special features, which are only used on some small amount
of objects. These scripts are attached via a :doc:`../components/005-script`
or the configuration in the :doc:`../file-structures/level` files.

Some considerable amount of the server side scripts have been removed from
the client files and only appear as :samp:`__removed` in the database.

As the scripting engine has access to some interface with the game engine,
documenting the relevant LUA-exposed functions can be of advantage in
understanding the game architeture as well as facilitate implementation
of a scripting engine in a server project, or even client modding.

Functions
---------

On every game message to an object, the scripting engine will call the
appropriate :file:`on{MessageName}` function in the scripts. When a lua
notfication is requested, the corresponding :file:`notify{Message}` will
be called.

Methods
-------

- Localize(key: string)

GameObject
----------

- obj:GetVar(key: string)
- obj:SetVar(key: string, value: any)
- obj:SetNetworkVar(key: string, value: any)
- obj:GetNetworkVar(key: string) -> any
- obj:SendLuaNotificationRequest{requestTarget: GameObject, messageName: string}
- obj:SendLuaNotificationCancel{requestTarget: GameObject, messageName: string}
- obj:GetRotation() -> Rotation
- obj:Exists() -> bool
- obj:GetFlag{iFlagID: int} -> Flag
- obj:GetLocationsVisited() -> Locations
- obj:SetRotation{x: float , y: float, z: float , w: float}
- obj:SetProximityRadius{iconID: int, radius: int, name: string}
- obj:UnsetProximityRadius{name: string}
- obj:CheckListOfPreconditionsFromLua{PreconditionsToCheck: ?, requestingID: GameObject}
- obj:RequestPickTypeUpdate()
- obj:GetID()
- obj:NotifyObject{ name: string, param1: int, ObjIDSender: ObjectID}

Game Messages
^^^^^^^^^^^^^

- SetStunned
- PlayAnimation
- PlayCinematic
- PlayNDAudioEmitter
- PlayFXEffect
- StopFXEffect
- TerminateInteraction
- PlayAnimation
- FireEventServerSide
- DisplayMessageBox

LEVEL
-----

- LEVEL:CLUTEffect(clut: string, fadeDuration: int, startIntensity: float, endIntensity: float, uiOverlay: bool)
- LEVEL:GetCinematicInfo(cinematicName: string)
- LEVEL:GetCurrentZoneID()
- LEVEL:SetLights(modifyAmbientColor: bool, ambientColor: int, modifyDirectionalColor: bool, directionalColor: int, modifySpecularColor: bool, specularColor: int, modifyUpperHemiColor: bool, upperHemiColor: int, modifyDirectionalDirection: bool, directionalDirection: {x: float, y: float, z: float}, modifyFogColor: bool, fogColor: int, modifyDrawDistance: bool, fogNearMin: float, fogNearMax: float, fogFarMin: float, fogFarMax: float, postFogSolidMin: float, postFogSolidMax: float, postFogFadeMin: float, postFogFadeMax: float, staticObjectCutoffMin: float, staticObjectCutoffMax: float, dynamicObjectCutoffMin: float, dynamicObjectCutoffMax: float, modifySkyDome: bool, skyDome: string, blendTime: float)
- LEVEL:SetSkyDome(skyDome: string)

GAMEOBJ
-------

- GAMEOBJ:GetControlledID() -> GameObject
- GAMEOBJ:GetZoneControlID()
- GAMEOBJ:GetTimer() -> Timer
- GAMEOBJ:GetObjectByID() -> GameObject
- GAMEOBJ:GetLocalCharID() -> ObjectID
- GAMEOBJ:DeleteObject(obj: GameObject)

RESMGR
------

- RESMGR:GetFilesInDir(string directory, string extension (blank for all extensions), bool check sub directories, string wildcard)
- RESMGR:LoadObject
  {
    objectTemplate = int object template,
    x = float x location,
    y = float y location,
    z = float z position,
    rw = float w rotation,
    rx = float x rotation,
    ry = float y rotation,
    rz = float z rotation,
    owner = GameObject game object,
    bIsSmashable = bool is the object smashable
  }
  


UI
--

- UI:SendMessage(msg: string, data: NDGfxValue)

Timer
-----

- timer:AddTimerWithCancel(delay: float, message: string, object: GameObject)
- timer:CancelAllTimers(object: GameObject)

Flag
----

- flag.bFlag -> bool

Locations
---------

- locations.locations -> list<ZoneID>
