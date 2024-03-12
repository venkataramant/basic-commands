# Creating unique keys
[Twitter-SnowFlake](https://blog.twitter.com/engineering/en_us/a/2010/announcing-snowflake)

[flick GUIDs] (https://code.flickr.net/2010/02/08/ticket-servers-distributed-unique-primary-keys-on-the-cheap/)


    Millisecond epoach -- 41 bits
    Node ID            -- 10 bits
    Local Counter      -- 12 bits
    Random             -- 01 bit
                        ------
                        64 bit
                        ----
