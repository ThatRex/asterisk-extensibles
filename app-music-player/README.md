# [Asterisk Extensible] Music Player

AEMP makes it easy to add music to your PBX.

```thrift
EXT,TRK ─ Select Track

/// Controls (Available Once Track Playing)
# ┬ Track Next
* ┴ Track Previous
0 ─ Pause Play

3 ┬ Fast Forward
2 ┴ Rewind
1 ─ Restart

6 ┬ Volume Up
5 ┴ Volume Down
4 ─ Volume Reset

9 ┬ Toggle Repeat╶──╮   
8 ┴ Toggle Playlist╶┴─ Repeat List
7 ─ Menu
```

A playlist is a group of consecutively numbered tracks. Example: [1,2,3,4] [6,7,8,9]

# Initial Setup

This section instructs you on preparing your PBX to add music. You will only need to follow this once.

<details _open>
<summary><h3>Instructions: FreePBX</h3></summary>

1. FTP into your PBX.
2. Under `/var/lib/asterisk/sounds/` create a directory named `music`.
3. In your PBX admin navigate to **Admin > Config Edit**, then copy the contents of `main.conf` into `extensions_custom.conf`. Remember to save.
   ![Config Edit](../screenshots/m_freepbx_config_edit.png)
4. Create a custom destination with the target set to `music,menu,1`. Alternatively you can put a track number instead of `menu`.
   ![Custom Destination](../screenshots/m_freepbx_custom_destination.png)
5. Create a virtual extension.
   ![Create Extension](../screenshots/freepbx_create_virtual_extension.png)
6. Under **Advanced > Optional Destinations** set **Not Reachable** to the custom destination you created.
   ![Set Optional Destination](../screenshots/m_freepbx_set_optional_destination.png)
7. Save & Apply Config. Then [add your music tracks](#adding-music-tracks).

</details>

<details _open>
<summary><h3>Instructions: VitalPBX</h3></summary>

1. FTP into your PBX.
2. Copy `main.conf` into `/etc/asterisk/vitalpbx/` then rename it to `extensions__90-music.conf`.
3. Under `/var/lib/asterisk/sounds/` create a directory named `music`.
4. Create a Custom Context with the destination set to hangup. Alternatively you can put a track number instead of `menu`.
   ![Custom Context](../screenshots/m_vitalpbx_custom_contexts.png)
5. Create a Custom Application with the destination set to your Custom Context.
   ![Custom Application](../screenshots/m_vitalpbx_custom_applications.png)
6. Save & Apply Config. Then [add your music tracks](#adding-music-tracks).

</details>

# Adding Music Tracks

This section instructs you on adding music tracks. You will need to repeat these steps every time you add a new music to your PBX.

<details _open>
<summary><h3>Instructions</h3></summary>

1. Convert your music using the provided [conversion script](../#conversion-script).
2. Prepend the track names with a unique track number like followed by a period. Example:
    > Track names **MUST NOT** contain commas.
    ```
    1. Track A.wav
    2. Track B.wav
    3. Track C.wav
    ```
3. FTP into your PBX, then copy your named and converted tracks into `/var/lib/asterisk/sounds/music/`.
4. You can now dial the music app extension then enter a track number.

</details>

# Enabling Connected Line

For the best experience you will want to enable connected line. This will allow the track name will show up (assuming your softphone supports such functionality.)

<details _open>
<summary><h3>Instructions: FreePBX</h3></summary>

Under an extensions advanced settings, enable **Send Connected Line**.
![advanced extension settings](../screenshots/freepbx_connected_line.png)

</details>

<details _open>
<summary><h3>Instructions: VitalPBX</h3></summary>

Under **Settings > Technology Settings > Device Profiles** enable **Send Connected Line** for the Default **PJSIP** and **WebRTC** profiles.
![device profile settings](../screenshots/vitalpbx_connected_line.png)

</details>
