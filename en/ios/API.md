
## P2P Configuration
Create `CBP2pConfig` instance.
```
CBP2pConfig *config = [CBP2pConfig defaultConfiguration];
```

The default fields (shown below) can be overridden.

| Field | Type | Default | Description |
| :-: | :-: | :-: | :-: |
| `logLevel` | CBLogLevel | CBLogLevelWarn | Print log level(CBLogLevelNone, CBLogLevelDebug, CBLogLevelInfo, CBLogLevelWarn, CBLogLevelError).                                                                                       
| `webRTCConfig` | RTCConfiguration | - | Providing options to configure WebRTC connections.
| `wsSignalerAddr` | NSString | @"wss://signal.cdnbye.com/wss" | The address of signal server.
| `maxBufferSize` | NSUInteger | 1024 * 1024 * 1024 | The max size of binary data that can be stored in the cache for VOD.
| `p2pEnabled` | BOOL | YES | Enable or disable p2p engine.
| `packetSize` | NSUInteger | 64 * 1024 | The maximum package size sent by datachannel, 64KB should work with most of recent browsers.
| `downloadTimeout` | NSTimeInterval | 10 | TS file download timeout.
| `tag` | NSString | @"unknown" | User defined tag which is presented in console.

## P2P Engine
Initialize `CBP2pEngine` to an instance or static variable:
```
CBP2pEngine *engine = [[CBP2pEngine alloc] initWithToken:@"free" andP2pConfig:config];
```
Get parsed local stream url by passing the original stream url(m3u8) to `CBP2pEngine` instance:
```
NSURL *parsedURL = [engine parseStreamURL:ORIGINAL_URL];
```

## P2P Statistics
Add a observer to observe downloading statistics:
```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(didReceiveMsg:) name:kP2pEngineDidReceiveStatistics object:nil];
```
The get the downloading statistics, including totalP2PDownloaded, totalP2PUploaded and totalHTTPDownloaded from dictionary:
```
- (void)didReceiveMsg:(NSNotification *)note {
    NSDictionary *dict = (NSDictionary *)note.object;
    NSLog(@"didReceiveMsg %@", dict);
}
```

## Complete Example
```
#import "ViewController.h"
#import <AVFoundation/AVFoundation.h>
#import <AVKit/AVKit.h>
#import <CDNByeKit/CBP2pEngine.h>

@interface ViewController ()
@property (strong, nonatomic)AVPlayerViewController *player;
@end

@implementation ViewController
- (void)viewDidLoad
{
    [super viewDidLoad];
    
    self.player = [[AVPlayerViewController alloc] init];
    CBP2pConfig *config = [CBP2pConfig defaultConfiguration];
    config.logLevel =  CBLogLevelDebug;
    config.tag = @"avplayer";
    CBP2pEngine *engine = [[CBP2pEngine alloc] initWithToken:@"free" andP2pConfig:config];
    NSURL *url = [engine parseStreamURL:@"https://video-dev.github.io/streams/x36xhzz/url_2/193039199_mp4_h264_aac_ld_7.m3u8"];
    self.player.player = [[AVPlayer alloc] initWithURL:url];
    
    self.player.view.frame = CGRectMake(0, 100, 400, 400);
    [self.view addSubview:self.player.view];
    
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(didReceiveMsg:) name:kP2pEngineDidReceiveStatistics object:nil];
    
    [self.player.player play];
}
/*
 Get the downloading statistics, including totalP2PDownloaded, totalP2PUploaded and totalHTTPDownloaded.
 */
- (void)didReceiveMsg:(NSNotification *)note {
    NSDictionary *dict = (NSDictionary *)note.object;
    NSLog(@"didReceiveMsg %@", dict);
}
@end
```