##FLV format##
 
###tags normally present###

- audiodatarate: (double kbps)
- hasKeyframes: (bool)
- hasVideo: (bool)
- framerate: 30
- canSeekToEnd: (bool) true
- stereo: (bool) true
- lasttimestamp: (double)
- datasize: (double) bytes not incl. header size
- videocodecid: (double)
- audiosamplerate: (double) kHz
- audiosize: (double) bytes
- audiosamplesize: (double) bits
- videosize: (double) bytes
- audiodelay: (double) msec (0)
- hasAudio: (bool) 
- filesize: (double) bytes -entire file
- height: (double) pixels
- lastkeyframetimestamp: (double) seconds
- metadatacreator: (string)
- metadatadate: (date)
- duration: (double) seconds
- videodatarate: (double) kbits/sec
- audiocodecid: (double) 2
- keyframes: (mixed array)
- times: (array of double)
- filepositions: (array of double)
- hasMetadata: (bool) true
- width: (double) pixels
- hasCuePoints: (bool) false
- totalframes: (double) framecount




###FLV格式###

> All multibyte integer or fp-double data is big-endian。

所有的整数和浮点数都是大端的。

    header:
    
    uint24 magic = 'FLV'
    uint8 version = 0x01
    uint8 type flags {
      %00000000
            | |- has_audio (1)
            \--- has_video (4)
    uint32 header size: (9 + extra_data.length)
    string extra_data: default null
    uint32 unknown = 0x00 
    
    tag stream:
    
    foreach tag {
            uint8 tag_type {
                    audio = 8
                    video = 9
                    meta = 18
                    undef = 0
            }
            uint24 data_size (not incl. header size)
            uint24 timestamp (in ms since start of stream)
            uint8 timestampExtended (upper 8 bits of a 32 bit timestamp)
            uint24 streamID = always 0
            char[] data
    
            uint32 tag_size (incl. header size, == data_size + 11)
    }
    
    no footer
    
    ---
    
    video tag data format
    {
            uint8 codec_id_and_frame_type {
                    low 4 = codec_id {
                            2 = H.263 video
                            3 = SCREEN video
                            4 = ON.2 VP6 video
                    }
                    high 4 = frame_type {
                            1 = Keyframe
                            2 = IFrame
                            3 = Disposable IFrame
                    }
            }
            char[] video data
    }
    
    ---
    
    meta tag data format
    {
            AMFString event_name
            AMFData meta_data (any supported AMF type)
    }
    
    AMFDouble {
            uint8 type_id = 0
            double value (in big endian/network byte order)
    }
    
    AMFBoolean {
            uint8 type_id = 1
            uint8 value = (true ? 1 : 0)
    }
    
    AMFString {
            uint8 type_id = 2
            uint16 length
            char[] data
    }
    
    AMFDate {
            uint8 type_id = 11
            double milliseconds since the epoch (big-endian)
            int16 offset in minutes between current TZ and UTC
    }
    
    AMFArray {
            uint8 type_id = 10
            uint32 array_length
            foreach (value) {
                    AMFData value
            }
    }
    
    AMFMixedArray {
            uint8 type_id = 8
            uint32 nkeys
            foreach (array as key => value) {
                    uint16 key.length
                    char[] key
                    AMFData value
            }
            uint16 key array terminator = 0
            uint8 unknown = 9
    }
    
    AMFObject {
            uint8 type_id = 3
            foreach (object as key => value) {
                    uint16 key.length
                    char[] key
                    AMFData value
            }
            uint16 key array terminator = 0
            uint8 unknown = 9
    }