# PluginGuide
The guide to creating a custom BackSeatGamer Reverse Proxy plugin

Note that calls to `print` are automatically routed to the ReverseProxy's console, and not STDOUT

## Events
TODO

## Functions
Note that if you are using an IDE such as PyCharm, it will not recognize function calls and will flag them as errors. We are working on a solution.

- `speak(text: str)` - Adds `text` to the text to speech queue
- `get_rewards()` - Returns a list of rewards availbile. See the **Rewards** section for the structure of a reward. 
- `clear_tts_queue()` - Clears the text to speech queue
- `set_tts_state(state: bool)` - If `state` is `True`, then text to speech will be enabled. `False` will disable it.
- `disable_tts()` - Disables text to speech
- `enable_tts()` - Enables text to speech
- `get_tts_state()` - Returns `True` if text to speech is enabled. Otherwise it will return `False`.
- `toggle_tts_state()` - Toggles if text to speech is enabled or disabled
- `clear_console()` - Clears the console
- `stop_session()` - Ends the proxy session and returns the user to the main menu
- `update_rewards()` - Pulls the latest version of the rewards from the server
- `background_task(target: callable, *args, **kwargs)` - Runs the function passed into `target` (with `args` and `kwargs`) as a background process (thread)
- `play_sound(path: str)` - Plays the sound file at the given path. The path MUST be relative to the plugin folder! Supported formats: .wavv, .flv, .ogg, .mp3 (.ogg is recomended)
- `read(path: str)` - Returns the contents of the specified file as a string. The path MUST be relative to the plugin folder!
- `read_raw(path: str)` - Returns the contents of the specified file as bytes (recomended for binary files). The path MUST be relative to the plugin folder!
- `write(path: str, content: str, encoding: str = "utf-8")` - Writes `content` to the specified path. The path MUST be relative to the plugin folder!
- `write_raw(path: str, content: bytes)` - Writes `content` to the specified path (recomended for binary files). The path MUST be relative to the plugin folder!
- `remove_file(path: str)` - Removes the file at the specified path. The path MUST be relative to the plugin folder!

## Objects
- `keyboard` - Provides an interface to the keyboard for simulating keystrokes. Use the funcitons `keyboard.press_key(key: str)` and `keyboard.release_key(key: str)` to simulate the keys. The key names are based on the DIK codes.
- `info` - contains all of the information provided in `info.json` as an object. For example, to reference the version of the mod, simply run `info.version`

## Rewards
A reward is a dictionary with the following format. Note that dict values are used to describe the real value which could be found.
```json
{
	"available_in": "the datetime when the reward will become availible again (or None if it has not been used)",
	"command": "the command to execute",
	"cooldown": "the cooldown between uses of the command",
	"enabled": "1 if it is enabled, or 0 if it is disabled",
	"id": "the reward ID",
	"last_guest": "The ID of the guest who last used the reward, or None if it has never been used",
	"last_used": "The datetime the reward was last used, or 0001-01-01T01:01:01 if it has never been used",
	"min_cooldown": "the smallest cooldown allowed to be set for the reward",
	"name": "the display name of the reward",
	"price": "the cost of using the reward",
	"single_use": "if the reward can only be used once per user"
}
```
