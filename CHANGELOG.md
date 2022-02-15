# v0.3 (2022-01-27)

- add lua navmesh lib
- replace json lib with yyjson, decode speed 2x of rapidjson
- add json.decode option:null_as_userdata
- bugfix: http client connection pool reset
- improve redisd service:print redis request(base64) when error
- improve moon.log avoid memory copy

# v0.2 (2021-12-20)
- add mongodb driver
- improve message dispatch

 ```lua
    ---old style
    local function docmd(sender,sessionid, CMD,...)

    end

    moon.dispatch('lua',function(msg,unpack)
        local sender, sz, len = moon.decode(msg, "SC")
        docmd(sender, unpack(sz, len))
    end)


    ---new style
    moon.dispatch('lua',function(sender,session, cmd, ...)
        -- body
        local f = command[cmd]
        if f then
            f(sender,...)
        else
            error(string.format("Unknown command %s", tostring(cmd)))
        end
    end)
 ```

# v0.1 (2021-11-17)
- remove socket.readline. use: socket.read
- bugfix: buffer's move assignment operator
- message object passed by right value in cpp code
- use isocalendar calculate datetime
- improve code