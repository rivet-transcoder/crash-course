# Glossary

Every important term in **The Video Crash Course**, in plain English. Terms are grouped alphabetically. Where a concept has a home chapter, you'll find a "→ see" link to it.

New to all this? Skim the chapters first ([start at the README](README.md)); come back here whenever a word trips you up.

---

## Numbers & Symbols

**4:2:0** — The most common [chroma subsampling](#chroma-subsampling) scheme: full-resolution brightness (luma), but color (chroma) sampled at half width *and* half height — one color sample per 2×2 block of pixels. Cuts data ~50% versus 4:4:4 and is nearly invisible to the eye. The default for almost all web and broadcast video. (→ see [Ch 02](chapters/02-color-and-pixels.md))

**4:2:2** — Chroma sampled at half horizontal resolution but full vertical. More color detail than 4:2:0; common in professional capture and editing formats. (→ see [Ch 02](chapters/02-color-and-pixels.md))

**4:4:4** — No chroma subsampling — every pixel carries full luma *and* full color. Used in high-end production, screen recording, and where color fidelity matters (e.g., chroma keying). Largest of the three. (→ see [Ch 02](chapters/02-color-and-pixels.md))

---

## A

**AAC (Advanced Audio Coding)** — The dominant lossy audio codec for video files; successor to MP3, better quality at the same bitrate. The default audio track in most MP4s. (→ see [Ch 08](chapters/08-audio.md))

**ABR (Adaptive Bitrate Streaming)** — Delivering several quality versions ("renditions") of the same video so the player can switch up or down based on network speed and screen size. The foundation of HLS and DASH. (→ see [Ch 11](chapters/11-adaptive-bitrate-streaming.md))

**Access unit** — All the coded data for a single decoded picture (one frame's worth of [NAL units](#nal-unit) plus any associated metadata). The unit a decoder turns into one output frame. (→ see [Ch 07](chapters/07-bitstreams-and-nal-units.md))

**AMF (Advanced Media Framework)** — AMD's SDK for hardware-accelerated encoding and decoding on Radeon GPUs. One of the hardware backends our transcoder can use. (→ see [Ch 14](chapters/14-gpu-acceleration.md))

**Annex-B** — A byte-stream format for H.264/H.265 where NAL units are separated by start codes (`00 00 01`). Used in MPEG-TS and raw `.h264`/`.h265` streams, as opposed to the length-prefixed [avcC](#avcc)/[hvcC](#hvcc) form inside MP4. (→ see [Ch 07](chapters/07-bitstreams-and-nal-units.md))

**AOM (Alliance for Open Media)** — The industry consortium (Google, Netflix, Amazon, Microsoft, Mozilla, Apple, and others) that created AV1 as a royalty-free alternative to HEVC. (→ see [Ch 05](chapters/05-the-codec-zoo.md), [Ch 16](chapters/16-patents-and-royalties.md))

**Aspect ratio** — The shape of the picture, width-to-height. Three related flavors: **DAR** (Display Aspect Ratio, e.g. 16:9 — how it should look on screen), **SAR** (Storage/Sample Aspect Ratio — the shape of an individual pixel), and **PAR** (Pixel Aspect Ratio, a synonym for SAR). When pixels aren't square, `DAR = SAR × (width/height)`. (→ see [Ch 01](chapters/01-what-is-video.md))

**AV1** — A modern, royalty-free video codec from the [Alliance for Open Media](#aom-alliance-for-open-media). Compresses better than H.264 and HEVC at the cost of heavier encoding. The default output codec of our transcoder. (→ see [Ch 05](chapters/05-the-codec-zoo.md))

**AVC (H.264)** — See [H.264](#h264-avc). "AVC" (Advanced Video Coding) and "H.264" are two names for the same codec.

**avcC** — The configuration box inside an MP4 that holds an H.264 decoder's setup data ([SPS/PPS](#spspps)) and tells the demuxer how many bytes prefix each NAL unit. The MP4 counterpart to [Annex-B](#annex-b). (→ see [Ch 09](chapters/09-containers-and-muxing.md))

---

## B

**B-frame (Bi-directional predicted frame)** — A frame predicted from frames both *before* and *after* it in display order. The most compressible frame type, but it forces the decoder to reorder output (which is why [PTS](#pts) and [DTS](#dts) can differ). (→ see [Ch 04](chapters/04-how-codecs-work.md))

**Bit depth** — Bits per color component per pixel. 8-bit (256 levels) is standard; 10-bit (1024 levels) reduces banding and is required for most HDR. More bits = smoother gradients, larger data. (→ see [Ch 02](chapters/02-color-and-pixels.md))

**Bitrate** — How many bits the video (or audio) spends per second, e.g. 5 Mbps. The single biggest lever on file size and quality. Can be constant ([CBR](#cbr)) or variable ([VBR](#vbr)). (→ see [Ch 06](chapters/06-encoders-and-rate-control.md))

**Bitstream** — The actual encoded sequence of bits a codec produces — the compressed video itself, before it's wrapped in a container. (→ see [Ch 07](chapters/07-bitstreams-and-nal-units.md))

**BT.601 / BT.709 / BT.2020** — ITU-R standards defining [color spaces](#color-space). **BT.601** is standard-definition; **BT.709** is HD (the web default); **BT.2020** is the ultra-wide gamut used for 4K/HDR. Mislabeling one as another causes washed-out or oversaturated color. (→ see [Ch 02](chapters/02-color-and-pixels.md), [Ch 15](chapters/15-filters-scaling-tonemapping.md))

---

## C

**CABAC / CAVLC** — The two [entropy coding](#entropy-coding) methods in H.264. **CABAC** (Context-Adaptive Binary Arithmetic Coding) compresses better but is heavier; **CAVLC** (Context-Adaptive Variable-Length Coding) is simpler and faster. (→ see [Ch 04](chapters/04-how-codecs-work.md))

**Capped CRF** — A rate-control mode that targets a constant quality ([CRF](#crf)) but won't exceed a bitrate ceiling. Best of both worlds for streaming: efficient on easy content, bounded on hard content. (→ see [Ch 06](chapters/06-encoders-and-rate-control.md))

**CBR (Constant Bitrate)** — Rate control that holds a steady bitrate throughout, regardless of scene difficulty. Predictable bandwidth, but spends bits inefficiently. Common in broadcast and live streaming. (→ see [Ch 06](chapters/06-encoders-and-rate-control.md))

**CDN (Content Delivery Network)** — A geographically distributed network of caching servers that deliver video segments to viewers from a nearby edge, reducing latency and origin load. The delivery backbone of streaming. (→ see [Ch 12](chapters/12-web-delivery-and-compatibility.md))

**Chroma** — The color part of a video signal, carried as two difference channels (Cb and Cr) separate from brightness. Human eyes are less sensitive to it, which is why it can be [subsampled](#chroma-subsampling). (→ see [Ch 02](chapters/02-color-and-pixels.md))

**Chroma subsampling** — Storing color at lower resolution than brightness to save data. Expressed as ratios like [4:2:0](#420), [4:2:2](#422), [4:4:4](#444). (→ see [Ch 02](chapters/02-color-and-pixels.md))

**Closed / open GOP** — A **closed** [GOP](#gop) can be decoded fully on its own — no frame references outside it. An **open** GOP lets some frames reference the previous GOP, gaining a little compression but complicating seeking and stream-switching. (→ see [Ch 04](chapters/04-how-codecs-work.md))

**CMAF (Common Media Application Format)** — A standardized fragmented-MP4 segment format that lets a single set of media files serve *both* HLS and DASH, ending the era of packaging everything twice. (→ see [Ch 11](chapters/11-adaptive-bitrate-streaming.md))

**Codec** — Short for **co**der-**dec**oder: the algorithm/standard that compresses (encodes) and decompresses (decodes) video or audio. H.264, AV1, AAC, and Opus are codecs. Not the same as a [container](#container). (→ see [Ch 04](chapters/04-how-codecs-work.md), [Ch 05](chapters/05-the-codec-zoo.md))

**Codec string** — A short identifier (like `avc1.640028` or `av01.0.05M.08`) that tells a browser exactly which codec [profile](#profile), [level](#level), and settings a stream uses, so it can answer "can I play this?" before downloading. Used in HLS/DASH manifests and the [MediaCapabilities](#mediacapabilities) API. (→ see [Ch 12](chapters/12-web-delivery-and-compatibility.md))

**Color primaries** — The exact red, green, and blue reference colors that define the corners of a [color space's](#color-space) [gamut](#gamut). One of three independent tags (with [transfer function](#transfer-function-eotf--oetf) and matrix) that fully describe how to interpret pixel values. (→ see [Ch 02](chapters/02-color-and-pixels.md))

**Color space** — The full definition of how stored numbers map to visible color: which [primaries](#color-primaries), [transfer function](#transfer-function-eotf--oetf), and matrix. BT.709 and BT.2020 are color spaces. (→ see [Ch 02](chapters/02-color-and-pixels.md))

**Container** — The file format that wraps coded video, audio, subtitles, and metadata together with timing — e.g. MP4, MKV, MPEG-TS, WebM. It holds the streams; it is *not* the codec inside. (→ see [Ch 09](chapters/09-containers-and-muxing.md))

**CQP (Constant QP)** — A rate-control mode that uses the same [quantization](#quantization-qp) value for every frame. Simple and predictable, but ignores the fact that different frames need different precision; rarely ideal for quality-per-bit. (→ see [Ch 06](chapters/06-encoders-and-rate-control.md))

**CRF (Constant Rate Factor)** — A rate-control mode that targets a consistent *perceived quality* rather than a fixed bitrate, letting the bitrate rise and fall with scene complexity. The go-to for file-based encoding; lower CRF = higher quality + bigger files. (→ see [Ch 06](chapters/06-encoders-and-rate-control.md))

**CTU (Coding Tree Unit)** — HEVC's basic coding block, up to 64×64 pixels, recursively split into smaller blocks. The HEVC successor to H.264's 16×16 [macroblock](#macroblock); larger blocks are a big reason HEVC beats H.264. (→ see [Ch 04](chapters/04-how-codecs-work.md))

---

## D

**DASH (MPEG-DASH)** — Dynamic Adaptive Streaming over HTTP: an open, codec-agnostic [ABR](#abr-adaptive-bitrate-streaming) standard (ISO/IEC 23009-1) using an XML manifest (the `.mpd`). The main alternative to [HLS](#hls). (→ see [Ch 11](chapters/11-adaptive-bitrate-streaming.md))

**DCT (Discrete Cosine Transform)** — The math that converts a block of pixels into frequency coefficients, concentrating energy into a few values so the high-frequency detail can be cheaply discarded. The heart of [transform](#transform) coding in most codecs. (→ see [Ch 04](chapters/04-how-codecs-work.md))

**Decoder** — The component that turns a compressed [bitstream](#bitstream) back into displayable frames (or playable audio). The reverse of an [encoder](#encoder). (→ see [Ch 04](chapters/04-how-codecs-work.md))

**Deinterlacing** — Converting [interlaced](#interlacing) video (alternating half-frames) into progressive full frames, needed for modern displays. Quality varies a lot by algorithm. (→ see [Ch 15](chapters/15-filters-scaling-tonemapping.md))

**Demux (demultiplex)** — Pulling the separate streams (video, audio, subtitles) back out of a [container](#container) so each can be decoded. The inverse of [mux](#mux). (→ see [Ch 10](chapters/10-demuxing.md))

**DRM (Digital Rights Management)** — Encryption-plus-licensing systems (Widevine, PlayReady, FairPlay) that restrict playback to authorized users/devices. Delivered to browsers through [EME](#eme). (→ see [Ch 12](chapters/12-web-delivery-and-compatibility.md))

**DTS (Decode Time Stamp)** — When a frame should be *decoded*, which can differ from when it's *displayed* ([PTS](#pts)) because of [B-frame](#b-frame-bi-directional-predicted-frame) reordering. (→ see [Ch 10](chapters/10-demuxing.md)) *(Not to be confused with DTS the audio codec.)*

---

## E

**EBML (Extensible Binary Meta Language)** — The binary, tag-based structure underlying the [Matroska](#mkv-matroska) (MKV) and WebM containers — conceptually like a binary XML. (→ see [Ch 09](chapters/09-containers-and-muxing.md))

**EME (Encrypted Media Extensions)** — The browser API that lets web players hand encrypted streams to a [DRM](#drm) system (Content Decryption Module) for licensed playback. (→ see [Ch 12](chapters/12-web-delivery-and-compatibility.md))

**Encoder** — The component that compresses raw frames into a coded [bitstream](#bitstream). Where most of the engineering effort (and CPU/GPU time) goes. (→ see [Ch 06](chapters/06-encoders-and-rate-control.md))

**Entropy coding** — The final, lossless compression stage that squeezes redundancy out of the symbol stream, using methods like [CABAC](#cabac--cavlc), [CAVLC](#cabac--cavlc), or [range/arithmetic coding](#range-coding). (→ see [Ch 04](chapters/04-how-codecs-work.md))

**EOTF / OETF** — See [transfer function](#transfer-function-eotf--oetf).

---

## F

**Faststart** — An MP4 optimization that moves the `moov` index box to the *front* of the file (before the media data) so playback can begin before the whole file downloads. Essential for web video. (→ see [Ch 09](chapters/09-containers-and-muxing.md))

**Field** — One half of an [interlaced](#interlacing) frame, containing either the odd or the even scan lines. Two fields make a full frame. (→ see [Ch 01](chapters/01-what-is-video.md))

**FLAC (Free Lossless Audio Codec)** — A royalty-free *lossless* audio codec — perfect reconstruction, smaller than raw [PCM](#pcm). Used where audio fidelity must be bit-exact. (→ see [Ch 08](chapters/08-audio.md))

**fps / frame rate** — Frames per second — how many images play each second (24, 30, 60…). Higher is smoother but more data. (→ see [Ch 01](chapters/01-what-is-video.md))

**Fragmented MP4 (fMP4)** — An MP4 split into many small, independently downloadable fragments (`moof`+`mdat` pairs) instead of one monolithic block. The basis of [CMAF](#cmaf-common-media-application-format) and modern streaming. (→ see [Ch 11](chapters/11-adaptive-bitrate-streaming.md))

**Frame** — One still image in the sequence that makes up video. Plays in rapid succession to create motion. (→ see [Ch 01](chapters/01-what-is-video.md))

---

## G

**Gamut** — The full range of colors a [color space](#color-space) can represent, bounded by its [primaries](#color-primaries). BT.2020 has a much wider gamut than BT.709. (→ see [Ch 02](chapters/02-color-and-pixels.md))

**GOP (Group of Pictures)** — A sequence of frames starting with a [keyframe](#keyframe) ([I-frame](#i-frame-intra-coded-frame)) followed by predicted ([P-](#p-frame-predicted-frame)/[B-](#b-frame-bi-directional-predicted-frame)) frames, before the next keyframe. GOP length governs seek granularity and stream-switch points. (→ see [Ch 04](chapters/04-how-codecs-work.md))

---

## H

**H.264 (AVC)** — The most widely supported video codec in the world (2003). Plays virtually everywhere; the safe compatibility baseline, though newer codecs compress better. (→ see [Ch 05](chapters/05-the-codec-zoo.md))

**H.265 (HEVC)** — See [HEVC](#hevc-h265).

**H.266 (VVC)** — See [VVC](#vvc-h266).

**HDR (High Dynamic Range)** — Video carrying a much wider range of brightness (deep blacks to brilliant highlights) and usually wider color, signaled by [PQ](#pq-st-2084) or [HLG](#hlg-hybrid-log-gamma) transfer functions and 10-bit depth. The opposite is SDR. (→ see [Ch 02](chapters/02-color-and-pixels.md), [Ch 15](chapters/15-filters-scaling-tonemapping.md))

**HEVC (H.265)** — High Efficiency Video Coding (2013), roughly 50% better compression than H.264, but burdened by a tangled [patent](#royalty--patent-pool) landscape that slowed adoption. (→ see [Ch 05](chapters/05-the-codec-zoo.md), [Ch 16](chapters/16-patents-and-royalties.md))

**HLG (Hybrid Log-Gamma)** — An [HDR](#hdr-high-dynamic-range) [transfer function](#transfer-function-eotf--oetf) (BBC/NHK) designed for backward compatibility — it looks reasonable on SDR screens too. Common in broadcast and phone cameras. (→ see [Ch 02](chapters/02-color-and-pixels.md))

**HLS (HTTP Live Streaming)** — Apple's [ABR](#abr-adaptive-bitrate-streaming) protocol, using `.m3u8` [playlists](#manifest--playlist) and media segments. The most widely deployed streaming format, mandatory on iOS. (→ see [Ch 11](chapters/11-adaptive-bitrate-streaming.md))

**hvcC** — The HEVC equivalent of [avcC](#avcc): the MP4 configuration box holding HEVC's [VPS/SPS/PPS](#spspps) and NAL length info. (→ see [Ch 09](chapters/09-containers-and-muxing.md))

---

## I

**I-frame (Intra-coded frame)** — A frame compressed using only its own data, no references to other frames — like a standalone JPEG. Larger than predicted frames but a valid starting point for decoding. (→ see [Ch 04](chapters/04-how-codecs-work.md))

**IDR (Instantaneous Decoder Refresh)** — A special [I-frame](#i-frame-intra-coded-frame) that also clears the decoder's reference buffers, guaranteeing nothing after it can reference anything before it. The clean seek/switch point streaming relies on. (→ see [Ch 04](chapters/04-how-codecs-work.md), [Ch 11](chapters/11-adaptive-bitrate-streaming.md))

**In-loop filter** — Filtering applied *inside* the encode/decode loop to clean up compression artifacts before a frame is used as a reference. Includes **deblocking** (smooths block edges), **SAO** (Sample Adaptive Offset, HEVC), and **CDEF** (Constrained Directional Enhancement Filter, AV1). (→ see [Ch 04](chapters/04-how-codecs-work.md))

**Init segment** — The header-only first piece of a streaming [rendition](#rendition) (an MP4 `init.mp4` / `ftyp`+`moov`) that sets up the decoder; the [media segments](#segment) that follow carry only frames. (→ see [Ch 11](chapters/11-adaptive-bitrate-streaming.md))

**Inter prediction** — Compressing a frame by describing how it differs from *other* frames (via [motion compensation](#motion-compensation)), rather than from scratch. The reason video compresses far better than a pile of JPEGs. (→ see [Ch 04](chapters/04-how-codecs-work.md))

**Interlacing** — A legacy technique that splits each frame into two [fields](#field) (odd/even lines) shown in alternation to fake a higher frame rate on old TVs. Modern video is [progressive](#progressive); interlaced sources need [deinterlacing](#deinterlacing). (→ see [Ch 01](chapters/01-what-is-video.md))

**Intra prediction** — Compressing a block using only *already-decoded neighboring blocks in the same frame* as a starting guess. The within-frame counterpart to [inter prediction](#inter-prediction). (→ see [Ch 04](chapters/04-how-codecs-work.md))

**ISOBMFF (ISO Base Media File Format)** — The box-based file structure (ISO/IEC 14496-12) that MP4, [CMAF](#cmaf-common-media-application-format), and many others are built on. Everything is a nested "box" (atom) with a size and a four-character type. (→ see [Ch 09](chapters/09-containers-and-muxing.md))

---

## K

**Keyframe** — A frame that can be decoded with no reference to any other frame — in practice an [I-frame](#i-frame-intra-coded-frame), and for clean seeking an [IDR](#idr-instantaneous-decoder-refresh). The anchor points for seeking and stream switching. (→ see [Ch 04](chapters/04-how-codecs-work.md))

---

## L

**Lanczos / bilinear / bicubic** — Algorithms for [scaling](#resolution) (resizing) images. **Bilinear** is fast and soft; **bicubic** is sharper; **Lanczos** is sharpest (best for downscaling) but slowest. Choosing well matters for quality. (→ see [Ch 15](chapters/15-filters-scaling-tonemapping.md))

**Latency** — The delay between something happening and a viewer seeing it. Critical for live/interactive streaming; usually traded against efficiency and robustness (longer segments = more latency but smoother delivery). (→ see [Ch 11](chapters/11-adaptive-bitrate-streaming.md))

**Level** — A codec constraint set bounding decoder workload — max resolution, frame rate, and bitrate (e.g. H.264 Level 4.0). Paired with a [profile](#profile) in the [codec string](#codec-string). (→ see [Ch 06](chapters/06-encoders-and-rate-control.md), [Ch 12](chapters/12-web-delivery-and-compatibility.md))

**Limited / full range** — Whether luma uses the full 0–255 (8-bit) value range ("full"/PC) or the broadcast-legacy 16–235 ("limited"/TV). Mismatching them on playback produces crushed blacks or gray, washed-out images. (→ see [Ch 02](chapters/02-color-and-pixels.md))

**Lossless / lossy** — **Lossy** compression discards information you (mostly) won't notice for big size savings (H.264, AAC); **lossless** reconstructs the original bit-for-bit (FLAC, PNG). Most video is lossy. (→ see [Ch 03](chapters/03-why-compression.md))

**Luma** — The brightness component of a video signal (the Y in [Y′CbCr](#yuv--ycbcr)). Eyes are most sensitive to it, so codecs protect it more carefully than [chroma](#chroma). (→ see [Ch 02](chapters/02-color-and-pixels.md))

---

## M

**Macroblock** — H.264's basic 16×16-pixel coding unit, subdividable for prediction and [transform](#transform). HEVC replaces it with the larger, flexible [CTU](#ctu-coding-tree-unit). (→ see [Ch 04](chapters/04-how-codecs-work.md))

**Manifest / playlist** — The text index a streaming player reads first, listing the available [renditions](#rendition) and where to fetch their [segments](#segment). Called a *playlist* (`.m3u8`) in [HLS](#hls) and a *manifest* (`.mpd`) in [DASH](#dash-mpeg-dash). (→ see [Ch 11](chapters/11-adaptive-bitrate-streaming.md))

**MediaCapabilities** — A browser API that asks "can this device play (and play *smoothly*) this codec/profile/resolution?" before you commit to a stream — smarter than the older `canPlayType`. (→ see [Ch 12](chapters/12-web-delivery-and-compatibility.md))

**MKV (Matroska)** — A flexible, open [container](#container) built on [EBML](#ebml-extensible-binary-meta-language) that can hold almost any codec and many tracks. [WebM](#vp8--vp9) is a web-focused subset. (→ see [Ch 09](chapters/09-containers-and-muxing.md))

**Motion compensation** — Reconstructing a block of the current frame by copying a (possibly shifted) block from a [reference frame](#reference-frame) and adding a small [residual](#residual). The payoff of [motion estimation](#motion-estimation). (→ see [Ch 04](chapters/04-how-codecs-work.md))

**Motion estimation** — The encoder's search for where a block "moved" from in a reference frame, producing a motion vector. Typically the most expensive part of encoding. (→ see [Ch 04](chapters/04-how-codecs-work.md), [Ch 06](chapters/06-encoders-and-rate-control.md))

**MP4** — The ubiquitous [container](#container) (ISO/IEC 14496-14), built on [ISOBMFF](#isobmff-iso-base-media-file-format), that holds video, audio, and metadata in nested boxes. The default for web download and a building block for streaming. (→ see [Ch 09](chapters/09-containers-and-muxing.md))

**MPEG-2** — An older codec (and transport format) from the DVD/broadcast era. Still encountered in TV, MPEG-TS, and legacy files. (→ see [Ch 05](chapters/05-the-codec-zoo.md))

**MPEG-DASH** — See [DASH](#dash-mpeg-dash).

**MPEG-LA / Via LA** — Patent-pool administrators that license bundles of patents for codecs like H.264 and HEVC. MPEG-LA merged into **Via LA** (Via Licensing Alliance). The reason "free to use" is more complicated than it sounds. (→ see [Ch 16](chapters/16-patents-and-royalties.md))

**MPEG-TS (MPEG Transport Stream)** — A [container](#container) of fixed 188-byte packets designed for broadcast and unreliable links, with stream maps ([PAT/PMT](#pat--pmt)). Long used by [HLS](#hls) segments. (→ see [Ch 09](chapters/09-containers-and-muxing.md))

**MSE (Media Source Extensions)** — The browser API that lets JavaScript feed media [segments](#segment) directly to a `<video>` element, enabling custom [ABR](#abr-adaptive-bitrate-streaming) players like hls.js and dash.js. (→ see [Ch 12](chapters/12-web-delivery-and-compatibility.md))

**Mux (multiplex)** — Combining coded video, audio, and other streams into a single [container](#container) with synchronized timing. The inverse of [demux](#demux-demultiplex). (→ see [Ch 09](chapters/09-containers-and-muxing.md))

---

## N

**NAL unit (Network Abstraction Layer unit)** — The packet structure of an H.264/H.265 [bitstream](#bitstream): each NAL unit carries a piece of coded data ([SPS](#spspps), [PPS](#spspps), a slice, [SEI](#sei), etc.) with a type tag. (→ see [Ch 07](chapters/07-bitstreams-and-nal-units.md))

**NV12** — A common semi-planar [pixel format](#pixel-format): a full plane of Y followed by one plane of interleaved U/V at quarter resolution ([4:2:0](#420)). The native layout many GPU decoders output. (→ see [Ch 14](chapters/14-gpu-acceleration.md))

**Nyquist (theorem)** — The principle that to capture a signal without aliasing you must sample at more than twice its highest frequency. The math reason [chroma subsampling](#chroma-subsampling) and downscaling need pre-filtering. (→ see [Ch 02](chapters/02-color-and-pixels.md), [Ch 15](chapters/15-filters-scaling-tonemapping.md))

---

## O

**OBU (Open Bitstream Unit)** — AV1's packet structure, its answer to the [NAL unit](#nal-unit): each OBU carries a typed chunk (sequence header, frame header, tile group, metadata…). (→ see [Ch 07](chapters/07-bitstreams-and-nal-units.md))

**Opus** — A modern, royalty-free, low-latency audio codec that beats AAC and MP3 across most bitrates, from voice to music. The default audio codec of our transcoder. (→ see [Ch 08](chapters/08-audio.md))

---

## P

**P-frame (Predicted frame)** — A frame predicted from *earlier* frames only. More compressible than an [I-frame](#i-frame-intra-coded-frame), less than a [B-frame](#b-frame-bi-directional-predicted-frame). (→ see [Ch 04](chapters/04-how-codecs-work.md))

**P010** — The 10-bit cousin of [NV12](#nv12): a semi-planar [4:2:0](#420) format storing each sample in 16 bits (10 significant). The common GPU output format for 10-bit/HDR. (→ see [Ch 14](chapters/14-gpu-acceleration.md))

**PAT / PMT** — The Program Association Table and Program Map Table inside [MPEG-TS](#mpeg-ts-mpeg-transport-stream): the directory that tells a demuxer which packet IDs carry which streams. (→ see [Ch 10](chapters/10-demuxing.md))

**PCM (Pulse-Code Modulation)** — Raw, uncompressed digital audio — straight amplitude samples. The baseline everything else compresses from; large but lossless. (→ see [Ch 08](chapters/08-audio.md))

**Pixel** — The smallest element of an image, a single colored dot. A frame is a grid of pixels; resolution counts them. (→ see [Ch 01](chapters/01-what-is-video.md))

**Pixel format** — How a pixel's components are laid out in memory — which channels, what [bit depth](#bit-depth), [subsampling](#chroma-subsampling), and ordering (e.g. `yuv420p`, [`nv12`](#nv12), [`p010`](#p010)). (→ see [Ch 02](chapters/02-color-and-pixels.md), [Ch 14](chapters/14-gpu-acceleration.md))

**PQ (ST 2084)** — Perceptual Quantizer, the [HDR](#hdr-high-dynamic-range) [transfer function](#transfer-function-eotf--oetf) (SMPTE ST 2084) behind HDR10 and Dolby Vision, mapping code values to absolute brightness up to 10,000 nits. (→ see [Ch 02](chapters/02-color-and-pixels.md))

**Preset** — An encoder speed/efficiency knob (e.g. `slow`, `medium`, `fast`) that trades encoding time for compression quality at a given bitrate. Slower presets pack more quality per bit. (→ see [Ch 06](chapters/06-encoders-and-rate-control.md))

**Profile** — A defined subset of a codec's tools (e.g. H.264 Baseline/Main/High) that a decoder must support. Paired with a [level](#level) in the [codec string](#codec-string) to express compatibility. (→ see [Ch 06](chapters/06-encoders-and-rate-control.md), [Ch 12](chapters/12-web-delivery-and-compatibility.md))

**Progressive** — Video where each frame is a complete image, drawn top to bottom in one pass. The opposite of [interlaced](#interlacing); standard for all modern video. (→ see [Ch 01](chapters/01-what-is-video.md))

**PSNR (Peak Signal-to-Noise Ratio)** — A simple objective quality metric comparing encoded output to the source, in decibels. Easy to compute but only loosely tracks what the eye perceives; see [SSIM](#ssim) and [VMAF](#vmaf). (→ see [Ch 06](chapters/06-encoders-and-rate-control.md))

**PTS (Presentation Time Stamp)** — When a decoded frame should be *displayed*. With [B-frames](#b-frame-bi-directional-predicted-frame), display order ([PTS](#pts)) differs from decode order ([DTS](#dts)). (→ see [Ch 10](chapters/10-demuxing.md))

---

## Q

**Quantization (QP)** — The lossy step that rounds [transform](#transform) coefficients to coarser values, throwing away detail to save bits. The **QP** (Quantization Parameter) sets how aggressive it is — the main quality/size dial inside a codec. (→ see [Ch 04](chapters/04-how-codecs-work.md), [Ch 06](chapters/06-encoders-and-rate-control.md))

---

## R

**Range coding** — A form of arithmetic [entropy coding](#entropy-coding) used by VP9, AV1, and others to pack symbols into fractional bits with high efficiency. (→ see [Ch 04](chapters/04-how-codecs-work.md))

**Rate control** — The encoder logic that decides how many bits to spend where to hit a target ([CBR](#cbr), [VBR](#vbr), [CRF](#crf), [capped CRF](#capped-crf), [CQP](#cqp-constant-qp)). The bridge between "quality I want" and "bitrate I get." (→ see [Ch 06](chapters/06-encoders-and-rate-control.md))

**Reference frame** — A previously decoded frame that later frames use as a prediction source via [motion compensation](#motion-compensation). (→ see [Ch 04](chapters/04-how-codecs-work.md))

**Rendition** — One specific quality/resolution version of a video in an [ABR](#abr-adaptive-bitrate-streaming) ladder (e.g. 1080p@5Mbps, 720p@3Mbps). The player switches among renditions. (→ see [Ch 11](chapters/11-adaptive-bitrate-streaming.md))

**Residual** — The difference between a predicted block and the real block — the small "error" the encoder still has to transmit after [prediction](#inter-prediction). Smaller residuals = better compression. (→ see [Ch 04](chapters/04-how-codecs-work.md))

**Resolution** — The pixel dimensions of the frame (e.g. 1920×1080). More pixels = more detail and more data. (→ see [Ch 01](chapters/01-what-is-video.md))

**Royalty / patent pool** — A licensing arrangement where many patent holders bundle their rights and charge fees for using a codec (notably HEVC). Avoiding these fees is the whole point of royalty-free codecs like [AV1](#av1) and [Opus](#opus). (→ see [Ch 16](chapters/16-patents-and-royalties.md))

---

## S

**Sample** — Two distinct meanings: **(audio)** one amplitude measurement at one instant (44,100 of them per second at 44.1 kHz); **(video/container)** one coded unit in a track — typically one frame — as indexed by the container's sample tables. Context tells you which. (→ see [Ch 08](chapters/08-audio.md), [Ch 09](chapters/09-containers-and-muxing.md))

**SAO (Sample Adaptive Offset)** — An HEVC [in-loop filter](#in-loop-filter) that nudges sample values to reduce banding and ringing artifacts after deblocking. (→ see [Ch 04](chapters/04-how-codecs-work.md))

**Segment** — A short, independently downloadable chunk of a streaming [rendition](#rendition) (typically 2–10 seconds), each starting at a [keyframe](#keyframe) so players can switch between renditions at segment boundaries. (→ see [Ch 11](chapters/11-adaptive-bitrate-streaming.md))

**SEI (Supplemental Enhancement Information)** — Optional metadata [NAL units](#nal-unit) in H.264/H.265 carrying things like HDR mastering info, timecodes, or closed captions — not needed to decode pixels, but useful to players. (→ see [Ch 07](chapters/07-bitstreams-and-nal-units.md))

**Sisvel** — A patent-pool administrator that licenses, among other things, patents some parties claim read on [AV1](#av1) and VP9 — a reminder that even "royalty-free" codecs face legal challenges. (→ see [Ch 16](chapters/16-patents-and-royalties.md))

**SPS / PPS / VPS** — The parameter sets that configure an H.264/H.265 decoder: **SPS** (Sequence Parameter Set — resolution, profile, frame structure), **PPS** (Picture Parameter Set — per-picture coding options), and HEVC's **VPS** (Video Parameter Set — layer/sub-layer info). Stored in [avcC](#avcc)/[hvcC](#hvcc) or inline as [NAL units](#nal-unit). (→ see [Ch 07](chapters/07-bitstreams-and-nal-units.md))

**SSIM (Structural Similarity Index)** — An objective quality metric that compares structural detail rather than raw pixel error, correlating with perception better than [PSNR](#psnr-peak-signal-to-noise-ratio). (→ see [Ch 06](chapters/06-encoders-and-rate-control.md))

**Streaming** — Delivering video so it plays as it arrives, rather than downloading the whole file first — typically via [ABR](#abr-adaptive-bitrate-streaming) over HTTP ([HLS](#hls)/[DASH](#dash-mpeg-dash)). (→ see [Ch 11](chapters/11-adaptive-bitrate-streaming.md))

**Subsampling** — See [chroma subsampling](#chroma-subsampling).

**Superblock** — AV1's top-level coding block (up to 128×128 pixels), recursively partitioned — AV1's counterpart to HEVC's [CTU](#ctu-coding-tree-unit). (→ see [Ch 04](chapters/04-how-codecs-work.md))

---

## T

**Tier** — In HEVC, a flag (Main vs High tier) within a [level](#level) that raises the bitrate ceiling for demanding professional content. (→ see [Ch 06](chapters/06-encoders-and-rate-control.md))

**Timescale / timebase** — The clock resolution a container uses to express timestamps — e.g. a timescale of 90,000 means time is counted in 1/90,000-second ticks. [PTS](#pts)/[DTS](#dts) are measured in these units. (→ see [Ch 09](chapters/09-containers-and-muxing.md))

**Tonemapping** — Converting [HDR](#hdr-high-dynamic-range) content to SDR (or between HDR formats), compressing the brightness range so highlights and colors survive on a narrower display. Easy to do badly; quality hinges on the curve used. (→ see [Ch 15](chapters/15-filters-scaling-tonemapping.md))

**Transcode** — Decoding media in one format and re-encoding it into another (different codec, bitrate, resolution, or container). The core job of our transcoder. (→ see [Ch 13](chapters/13-the-transcoding-pipeline.md))

**Transform** — The step that converts a block of pixels (or [residuals](#residual)) into frequency-domain coefficients — usually a [DCT](#dct-discrete-cosine-transform) variant — so detail can be compactly [quantized](#quantization-qp). (→ see [Ch 04](chapters/04-how-codecs-work.md))

**Transfer function (EOTF / OETF)** — The curve mapping between light and stored code values. The **OETF** (Opto-Electronic Transfer Function) is applied at capture (light → signal); the **EOTF** (Electro-Optical) at display (signal → light). [PQ](#pq-st-2084) and [HLG](#hlg-hybrid-log-gamma) are HDR transfer functions; gamma 2.4 / BT.709 is the SDR norm. (→ see [Ch 02](chapters/02-color-and-pixels.md))

---

## V

**VBR (Variable Bitrate)** — Rate control that lets bitrate rise on complex scenes and fall on simple ones to hold quality steady. More efficient than [CBR](#cbr) for file-based use. (→ see [Ch 06](chapters/06-encoders-and-rate-control.md))

**VMAF (Video Multimethod Assessment Fusion)** — Netflix's machine-learned perceptual quality metric that fuses several measures to predict human opinion scores. Widely used to compare encoders and drive per-title encoding. (→ see [Ch 06](chapters/06-encoders-and-rate-control.md))

**VP8 / VP9** — Google's royalty-free codecs predating [AV1](#av1). **VP8** rivaled H.264; **VP9** rivaled HEVC and powered much of YouTube. Both ride in [WebM](#mkv-matroska). (→ see [Ch 05](chapters/05-the-codec-zoo.md))

**VVC (H.266)** — Versatile Video Coding (2020), the successor to HEVC with another ~50% efficiency gain — but very heavy and, like HEVC, facing patent uncertainty that has slowed adoption. (→ see [Ch 05](chapters/05-the-codec-zoo.md))

---

## Y

**YUV / Y′CbCr** — The color model video actually uses: one brightness channel (Y′, [luma](#luma)) plus two color-difference channels (Cb, Cr, [chroma](#chroma)), instead of RGB. Separating brightness from color enables [chroma subsampling](#chroma-subsampling). "YUV" is the loose everyday name; **Y′CbCr** is the precise digital term. (→ see [Ch 02](chapters/02-color-and-pixels.md))

---

*Back to the [course README](README.md) · See also [Further Reading](FURTHER-READING.md)*
