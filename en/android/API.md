
## P2P Configuration
A `P2pConfig` can be obtained via its builder, the parameters below is the default values:
```java
P2pConfig config = new P2pConfig.Builder()
    .logEnabled(false)                                // Enable or disable log
    .logLevel(LogLevel.WARN)                          // Print log level
    .announce("https://tracker.cdnbye.com/v1")        // The address of tracker server
    .wsSignalerAddr("wss://signal.cdnbye.com")        // The address of signal server
    .downloadTimeout(10_000, TimeUnit.MILLISECONDS)   // TS file download timeout by HTTP
    .dcDownloadTimeout(6_000, TimeUnit.MILLISECONDS)  // Max download timeout for WebRTC datachannel
    .localPort(52019)                                 // The port for local http server
    .diskCacheLimit(1024*1024*1024)                   // The max size of binary data that can be stored in the disk cache for VOD(Set to 0 will disable disk cache)
    .memoryCacheLimit(30*1024*1024)                   // The max size of binary data that can be stored in the memory cache
    .memoryCacheCountLimit(-1)                        // The max count of ts files that can be stored in the memory cache, regardless of memoryCacheLimit, parameter should be a integer greater than 0
    .p2pEnabled(true)                                 // Enable or disable p2p engine
    .withTag("unknown")                               // User defined tag which is presented in console
    .webRTCConfig(null)                               // Providing options to configure WebRTC connections
    .maxPeerConnections(20)                           // Max peer connections at the same time
    .useHttpRange(true)                               // Use HTTP ranges requests where it is possible. Allows to continue (and not start over) aborted P2P downloads over HTTP.
    .isSetTopBox(false)                               // If run on set-top box, please set it true for compatibility purpose.
    .build();  
P2pEngine.initEngine(getApplicationContext(), token, config);
```

## P2P Engine
Instantiate `P2pEngine`，which is a singleton：
```java
P2pEngine engine = P2pEngine.initEngine(Context context, String token, P2pConfig config);
```
Explanation:
<br>

| param | type | required | description |
| :-: | :-: | :-: | :-: |
| `context` | Context | Yes | The instance of Application Context is recommended.                                                                                
| `token` | String | Yes | Token assigned by CDNBye.
| `config` | P2pConfig | No | Custom configuration.

### P2pEngine API
#### `P2pEngine.Version`
Current SDK version.

#### `P2pEngine.getInstance()`
Get the singleton of `P2pEngine`.

#### `engine.parseStreamUrl(String url)`
Convert original playback address (m3u8) to the address of the local proxy server.

#### `engine.isConnected()`
Check if connected with CDNBye backend.

#### `engine.stopP2p()`
Disable engine to stop p2p and free used resources.

#### `engine.restartP2p()`
Resume P2P if it has been stopped.

#### `engine.getPeerId()`
Get the peer ID of this engine.

### P2P Statistics
Add a observer `P2pStatisticsListener` to observe downloading statistics:
```java
engine.addP2pStatisticsListener(new P2pStatisticsListener() {
            @Override
            public void onHttpDownloaded(long value) {
            }

            @Override
            public void onP2pDownloaded(long value) {
            }

            @Override
            public void onP2pUploaded(long value) {
            }

            @Override
            public void onPeers(List<String> peers) {
            }
        });
```
PS: The unit of download and upload is KB.

## Advanced Usage
### Switch Stream URL
When Switching to a new stream URL, before passing new stream url(m3u8) to the player, pass that URL through `P2pEngine` instance:
```java
String newParsedURL = P2pEngine.getInstance().parseStreamUrl(url);
```
### Use Your Own STUN or TURN Server
STUN (Session Traversal Utilities for NAT) allows clients to discover their public IP address and the type of NAT they are behind. This information is used to establish the media connection. Although there are default STUN servers in this SDK, you can replace them with your own via P2PConfig. TURN (Traversal Using Relays around NAT) server is used to relay traffic if direct connection fails. You can config your [TURN](https://github.com/coturn/coturn) server in the same way as STUN.
```java
import org.webrtc.PeerConnection;
import org.webrtc.PeerConnection.RTCConfiguration;

List<PeerConnection.IceServer> iceServers = new ArrayList<>();
iceServers.add(PeerConnection.IceServer.builder(YOUR_STUN_OR_TURN_SERVER).createIceServer());
RTCConfiguration rtcConfig = new RTCConfiguration(iceServers);
P2pConfig config = new P2pConfig.Builder()
    .webRTCConfig(rtcConfig)
    .build();
```
### Dynamic m3u8 Path Issue
Some m3u8 urls play the same live/vod but have different paths on them. For example, example.com/clientId1/file.m3u8 and example.com/clientId2/file.m3u8. In this case, you can format a common channelId for them.
```java
import com.cdnbye.sdk.ChannelIdCallback;

P2pConfig config = new P2pConfig.Builder()
    .channelId(new ChannelIdCallback() {
        @Override
        public String onChannelId(String urlString) {
            return formatChannelId(urlString);
        }
    }).build();
```
`It is strongly recommended to add a unique identifier to the channelid to prevent conflicts with other channels.`