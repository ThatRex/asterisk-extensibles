# Asterisk Extensibles

> [!IMPORTANT]
> Basic terminal and PBX management skills are assumed.

Extensible apps for asterisk: [**Talk Bot**](/app-talk-bot/README.md) • [**Media Player**](/app-music-player/README.md)

## Conversion Script

This script will convert any **MP3**, **WAV** or **FLAC** files to **Mono 8kHz PCM WAV** files suitable for Asterisk. Converted files will be placed in a sub directory named `converted`.

1. Ensure [FFmpeg](https://ffmpeg.org/) is installed on your system.
2. Open your terminal, then navigate to the directory containing the audio files to be converted.
3. Copy and paste the appropriate script for your OS into your terminal.

<details>
<summary><h3>Windows (PowerShell)</h3></summary>

```powershell
$output = "converted"
New-Item -Path $output -ItemType Directory -Force
Get-ChildItem | where {$_.extension -in ".mp3",".wav",".flac"} | ForEach-Object {
   $name = "$output/$($_.BaseName).wav"
   & ffmpeg -i $_.Name -ar 8000 -ac 1 -acodec pcm_s16le -f wav $name
}

```

</details>

<details>
<summary><h3>Linux (Bash)</h3></summary>

```bash
output="converted"
mkdir -p $output
for file in *.mp3 *.wav *.flac; do
  name="$output/${file%.${file##*.}}.wav"
  ffmpeg -i "$file" -ar 8000 -ac 1 -acodec pcm_s16le -f wav "$name";
done

```

</details>
