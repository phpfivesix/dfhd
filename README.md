# Delta Force 1 (1998) HD

A patched executable (`dfhd.exe`) for Delta Force v1.00.03.03P that runs at higher resolutions, up to your desktop resolution, without extra tools like dgVoodoo2.

Download `dfhd.zip` from the [releases page](https://github.com/phpfivesix/dfhd/releases).

See [readme.txt](readme.txt) for installation, changes and commands.

## Troubleshooting

Remove any wrappers or modified files from the game directory:

- `dgVoodoo*` files
- `DDraw.dll`, `D3D8.dll`, `D3D9.dll`, `D3DImm.dll`
- a modified `netsock.dll`: restore the original from the game CD/installer instead of deleting it

## Roadmap

```mermaid
flowchart TD
    A["✅ Higher resolutions<br/>(software renderer)"] --> B["Modernize toolchain"]
    B --> C["Hardware rendering"]
    C --> D["???"]
```

## Screenshots

![Delta Force HD screenshot](images/df1_005.png)
![Delta Force HD screenshot](images/df1_004.png)
![Delta Force HD screenshot](images/df1_006.png)
![Delta Force HD screenshot](images/df1_007.png)
![Delta Force HD screenshot](images/df1_001.png)
![Delta Force HD screenshot](images/df1_002.png)
![Delta Force HD screenshot](images/df1_003.png)
