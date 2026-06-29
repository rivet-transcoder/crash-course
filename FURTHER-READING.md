# Further Reading

You've finished the course — here's where to go deeper, organized by what you're trying to do. Every entry has a short note on *why* it's worth your time, because a link dump helps no one.

A word on honesty: the **specs** are authoritative but brutal to read cover-to-cover. The **explainers** are where you actually learn. The **tools** are where it clicks, because you can point them at a real file and watch the theory become bytes. Use them in that order when something confuses you.

---

## The specs (primary sources)

These are the documents implementers actually conform to. Treat them as references you *look things up in*, not tutorials you read front to back — they're precise, dense, and assume you already know the vocabulary (which, having read the [Glossary](GLOSSARY.md), you now do).

- **ITU-T H.264 (AVC)** — *Advanced Video Coding for generic audiovisual services* (itu.int/rec/T-REC-H.264). The definitive H.264 spec, including the [NAL unit](GLOSSARY.md#nal-unit) syntax, [SPS/PPS](GLOSSARY.md#spspps), and [Annex-B](GLOSSARY.md#annex-b) byte stream. Pair it with [Ch 04](chapters/04-how-codecs-work.md) and [Ch 07](chapters/07-bitstreams-and-nal-units.md).
- **ITU-T H.265 (HEVC)** — the HEVC text (itu.int/rec/T-REC-H.265). Adds [CTUs](GLOSSARY.md#ctu-coding-tree-unit), [VPS](GLOSSARY.md#spspps), [SAO](GLOSSARY.md#sao-sample-adaptive-offset), and the [tier/level](GLOSSARY.md#tier) tables. Worth a look to see how much more complex it got than H.264.
- **The AV1 Bitstream & Decoding Process Specification** — AOM's official AV1 spec (aomedia.org/av1/specification, also on aomediacodec.github.io/av1-spec). The source of truth for [OBUs](GLOSSARY.md#obu-open-bitstream-unit), [superblocks](GLOSSARY.md#superblock), and [CDEF](GLOSSARY.md#in-loop-filter). Free and openly published — fitting for a royalty-free codec.
- **ISO/IEC 14496-12 — ISO Base Media File Format ([ISOBMFF](GLOSSARY.md#isobmff-iso-base-media-file-format))** — the box/atom structure underneath MP4, [CMAF](GLOSSARY.md#cmaf-common-media-application-format), and fragmented MP4. Read this once and the entire MP4 family stops being mysterious. Pairs with [Ch 09](chapters/09-containers-and-muxing.md).
- **ISO/IEC 14496-14 — MP4 file format** — the thin layer that specializes ISOBMFF into the `.mp4` you know, including how codecs and [esds](GLOSSARY.md#aac-advanced-audio-coding) descriptors are carried.
- **HLS — Apple's documentation + RFC 8216** — the *HTTP Live Streaming* RFC (datatracker.ietf.org/doc/html/rfc8216) plus Apple's developer docs at developer.apple.com/streaming. Defines the `.m3u8` [playlist](GLOSSARY.md#manifest--playlist) format. Apple keeps evolving HLS past the RFC, so read both. Pairs with [Ch 11](chapters/11-adaptive-bitrate-streaming.md).
- **MPEG-DASH — ISO/IEC 23009-1** — the *Dynamic Adaptive Streaming over HTTP* standard, defining the `.mpd` [manifest](GLOSSARY.md#manifest--playlist). The codec-agnostic counterpart to HLS.
- **CMAF — ISO/IEC 23000-19** — the *Common Media Application Format*. The standard that lets one set of [fragmented-MP4](GLOSSARY.md#fragmented-mp4-fmp4) [segments](GLOSSARY.md#segment) serve both HLS and DASH. The reason you no longer package everything twice.
- **Opus — RFC 6716** — the *Definition of the Opus Audio Codec* (datatracker.ietf.org/doc/html/rfc6716). Notably readable for a codec spec, with reference code inline. See also RFC 7845 for Opus-in-Ogg encapsulation. Pairs with [Ch 08](chapters/08-audio.md).
- **NAL / Annex-B definitions** — there's no standalone "NAL spec"; the [NAL unit](GLOSSARY.md#nal-unit) and [Annex-B](GLOSSARY.md#annex-b) byte-stream formats live in **Annex B of H.264 and H.265** above. When someone says "the Annex-B spec," that's what they mean. ([Ch 07](chapters/07-bitstreams-and-nal-units.md) walks through it gently first.)

---

## Friendly explainers, books & sites

This is where you'll actually *learn* — start here, reach for the specs only when you need a precise detail.

- **leandromoreira / digital_video_introduction** (github.com/leandromoreira/digital_video_introduction) — the canonical free primer on how video compression works, with clear diagrams and runnable examples. If you read one external resource, read this. It's the perfect companion to chapters [03](chapters/03-why-compression.md)–[07](chapters/07-bitstreams-and-nal-units.md).
- **The FFmpeg documentation + wiki** (ffmpeg.org/documentation.html, trac.ffmpeg.org/wiki) — not just a tool manual; the wiki's encoding guides (H.264, H.265, AV1, [CRF](GLOSSARY.md#crf-constant-rate-factor) explanations) are genuinely educational and battle-tested. The H.264 and AV1 guides in particular teach [rate control](GLOSSARY.md#rate-control) by example.
- **Apple's HLS Authoring Specification** (developer.apple.com/documentation/http-live-streaming) — Apple's prescriptive "do exactly this" rules for [bitrate ladders](GLOSSARY.md#rendition), [keyframe](GLOSSARY.md#keyframe) alignment, and [segment](GLOSSARY.md#segment) durations. Even if you don't target Apple devices, it encodes hard-won best practices. Pairs with [Ch 11](chapters/11-adaptive-bitrate-streaming.md) and [Ch 12](chapters/12-web-delivery-and-compatibility.md).
- **The Netflix TechBlog** (netflixtechblog.com) — the source of [VMAF](GLOSSARY.md#vmaf) and *per-title / per-shot encoding*. Search their posts on "VMAF," "Dynamic Optimizer," and "per-title encoding" to understand how the industry thinks about quality-per-bit. Pairs with [Ch 06](chapters/06-encoders-and-rate-control.md).
- **Bitmovin's developer articles & blog** (bitmovin.com/blog) — practical, vendor-written deep dives on [ABR](GLOSSARY.md#abr-adaptive-bitrate-streaming), [CMAF](GLOSSARY.md#cmaf-common-media-application-format), low-latency streaming, and codec adoption. Good for connecting the standards to production reality.
- **MDN Web Docs — Media** (developer.mozilla.org) — the best plain-English reference for browser playback: the [`<video>` element], [Media Source Extensions (MSE)](GLOSSARY.md#mse-media-source-extensions), [MediaCapabilities](GLOSSARY.md#mediacapabilities), and especially the *"codecs" parameter* / [codec string](GLOSSARY.md#codec-string) guide that demystifies strings like `av01.0.05M.08`. Pairs with [Ch 12](chapters/12-web-delivery-and-compatibility.md).
- **Demuxed conference talks** (demuxed.com, and the Demuxed channel on YouTube) — the annual gathering of video engineers. Talks are practical, opinionated, and current; a great way to hear how real teams solve [transcoding](GLOSSARY.md#transcode), packaging, and player problems.

---

## Tools to inspect & experiment

Reading about boxes and timestamps is fine; *seeing* them in your own files is where it sticks. One line each on what it's for:

- **`ffmpeg` / `ffprobe`** (ffmpeg.org) — the Swiss Army knife. `ffmpeg` transcodes anything to anything; `ffprobe` reports streams, codecs, [pixel formats](GLOSSARY.md#pixel-format), and timestamps. The default starting point for almost any video question.
- **`mediainfo`** (mediaarea.net/MediaInfo) — a friendly, human-readable summary of a file's tracks, codecs, [bit depth](GLOSSARY.md#bit-depth), [color space](GLOSSARY.md#color-space), and bitrate. Great when `ffprobe`'s output feels like a firehose.
- **GPAC `MP4Box -info`** (gpac.io) — the go-to for inspecting and manipulating MP4/[ISOBMFF](GLOSSARY.md#isobmff-iso-base-media-file-format) structure, [fragmenting](GLOSSARY.md#fragmented-mp4-fmp4), and building [DASH](GLOSSARY.md#dash-mpeg-dash)/[CMAF](GLOSSARY.md#cmaf-common-media-application-format) packages. `-info` gives a quick track summary.
- **`mp4dump` / Bento4** (bento4.com) — `mp4dump` prints the full nested [box tree](GLOSSARY.md#isobmff-iso-base-media-file-format) of an MP4, atom by atom. The clearest way to *see* [faststart](GLOSSARY.md#faststart), `moov`/`mdat` ordering, and [avcC](GLOSSARY.md#avcc)/[hvcC](GLOSSARY.md#hvcc) config in the flesh.
- **A hex viewer** (e.g. `xxd`, `hexyl`, ImHex, or any editor's hex mode) — for walking [NAL units](GLOSSARY.md#nal-unit) and box headers byte by byte when you really want to understand the [bitstream](GLOSSARY.md#bitstream). Find the `00 00 00 01` start codes yourself once and Annex-B stops being abstract.
- **hls.js / dash.js / Shaka Player** (github.com/video-dev/hls.js, github.com/Dash-Industry-Forum/dash.js, github.com/shaka-project/shaka-player) — the open-source browser players built on [MSE](GLOSSARY.md#mse-media-source-extensions). Load your stream into one with its debug panel open to watch [ABR](GLOSSARY.md#abr-adaptive-bitrate-streaming) switching and buffer behavior live.
- **Bitmovin Stream Lab** (bitmovin.com/stream-lab) — a browser tool that validates and test-plays your HLS/DASH stream across configurations, flagging packaging problems you'd otherwise hit in production.
- **our own `rivet probe`** (github.com/rivet-transcoder/rivet) — the quickest structured read of any file using the same engine we built this course around. One command tells you codecs, resolution, [color metadata](GLOSSARY.md#color-space), and track layout, no flag-juggling required.

---

## Inspect a file yourself (5-minute mini-tutorial)

Theory lands when you run it. Grab any video file and try these — each reveals a different layer of everything the course covered.

```bash
# 1. The streams: codecs, resolution, pixel format, color, frame rate.
#    Your first question about any file, answered.
ffprobe -hide_banner -show_streams input.mp4

# 2. A human-readable summary — great for color space, bit depth, and bitrate
#    at a glance without parsing ffprobe's key=value output.
mediainfo input.mp4

# 3. The container's box tree: track structure, brands, and whether the
#    moov box is up front (faststart) or stuck at the end.
MP4Box -info input.mp4
#    ...or, for the full atom-by-atom dump:
mp4dump input.mp4

# 4. PTS vs DTS per packet — watch the timestamps reorder when B-frames
#    are present. This is decode order vs display order, made concrete.
ffprobe -hide_banner -show_packets -select_streams v input.mp4

# 5. Our transcoder's structured read — codecs, resolution, color, tracks —
#    the same engine the rest of this course is built on.
rivet probe input.mp4
```

What you'll notice: command **1** names the [codec](GLOSSARY.md#codec) and [resolution](GLOSSARY.md#resolution); **2** surfaces [color space](GLOSSARY.md#color-space) and [bit depth](GLOSSARY.md#bit-depth) mismatches that cause washed-out playback; **3** and the `mp4dump` variant expose the [ISOBMFF box tree](GLOSSARY.md#isobmff-iso-base-media-file-format) and [faststart](GLOSSARY.md#faststart) layout; **4** shows [PTS](GLOSSARY.md#pts)/[DTS](GLOSSARY.md#dts) reordering whenever [B-frames](GLOSSARY.md#b-frame-bi-directional-predicted-frame) are in play; and **5** ties it together through [our transcoder](https://github.com/rivet-transcoder/rivet). Run them on a few different files — an iPhone clip, a YouTube download, an HLS segment — and the differences will teach you more than any diagram.

---

That's the map. When you're ready to see all of it working together in real code, head to **[rivet](https://github.com/rivet-transcoder/rivet)** — the GPU-accelerated transcoder we built and the engine behind this whole course — and back to the **[course README](README.md)** to revisit any chapter.

*Back to the [course README](README.md) · See also the [Glossary](GLOSSARY.md)*
