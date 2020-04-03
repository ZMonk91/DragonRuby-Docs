## MP3's to Wav converstion script:#
---

```ruby
`ls .`.each_line.to_a.map do |l|
  l = l.strip
  if l.end_with? "mp3"
    `ffmpeg -i #{l} -acodec pcm_s16le -ar 44100 prep-#{l.split(".")[0]}.wav`
    `ffmpeg -y -i prep-#{l.split(".")[0]}.wav -f wav -bitexact -acodec pcm_s16le -ar 44100 -ac 1 #{l.split(".")[0]}.wav`
  end
end
```
